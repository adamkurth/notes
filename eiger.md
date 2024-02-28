# Dectris-Eiger4M
################################
#    SETUP EIGER DETECTOR
################################
# On any browser, open this site on localhost http://10.139.1.5 for Dectris menu options for the detector. http://10.139.1.5/data/ will be where the data images will be stored. setup.sh has a function which downloads these images onto computer. (will specify later in README)
# Step 1: Activate zmq listener
## activate zmq listener:
# in order to see what the detector is doing at any given moment, this is helpful to have running simultaneously with capturing images. 
#    cd to correct directory:  
    cd /home/labuser/Projects/Dectris/reborn/developer/rkirian/projects/cxls/dectris/fromzach/DEigerStream
#    activate reborn:
    conda activate reborn
#    set log file
    python DEigerStream.py -i 10.139.1.5 -f junk.log

# STEP 2: Initalization and arming
## initalize/arm/trigger detector: 
# set source file to setup (pervided in the repository) to give simplified commands such as initalize, arm, disarm, etc. 
    source setup.sh
    initalize
# set parameters enable: 
# call functions enable_monitor, etc, from setup.sh for desired output.  
    enable_monitor
    enable_stream
    enable_filewriter
# specify quantities for desired output.
    nimages <x>         # type int
    frame_time <x>      # seconds, type int or double
    count_time <x>      # seconds, type int or double
    nimages_per_file <x>  # type int
# capture images:
    arm                 #arms detector
    disarm              #disarms detector
    trigger             #triggers detector

# STEP 3: Further instruction
# Problems fetching images from http://10.139.1.5/data/? 
# On the Eiger Detector menu, go to Admin on the lefthand side, click the 'REBOOT DCU' option. http://10.139.1.5/#/admin/system

# Downloading and overwriting images: 
source setup.sh
# call download function to start downloading of images on http://10.139.1.5/data/
download_images_from_IP
# For CXLS, this is stored in /home/labuser/Projects/Dectris/test/temp_data 

################################
VIEW HDF5 IMAGES THROUGH REBORN
################################
# go to working directory:
    cd /home/labuser/Projects/Dectris/test/temp_data 
# Export python path:
    export PYTHONPATH=$PYTHONPATH:/home/labuser/Projects/Dectris/reborn
# Run test_h5_reading.py (or any other python file)
    python test_h5_reading
 
# Troubleshooting: "error occurs module '' not found" 
# View the modules available in reborn by
    conda list
# if not installed in conda list 
    conda install <modulename>

###############################
#            AGAVE
################################
# upon startup in AGAVE (https://asurc.atlassian.net/wiki/spaces/RC/overview?homepageId=45711712), remember to get off interactive node before doing computationally intensive tasks, by typing 
    interactive 
# link to AGAVE:

# AGAVE activate conda either enviornment:
    anaconda3: source /home/amkurth/anaconda3/bin/activate
  
# loading modules: 
# check available modules: 
    module -l avail 
# to load a module: 
    module load <module name/version number>
# to check which modules that are loaded: 
    module list
# unload all loaded modules: 
    module purge 

# Notes on using ./index-turbo-slurm 
# finding partitions: 
    sinfo
# selecting output of only partition names: 
    sinfo -h --format="%P" 
# detailed information of specific 'partition_name': 
    sinfo -p <partition_name>
# watch tasks: 
    watch 'squeue -u <username>



# Running pattern_sim data
    # first load crystfel, find partition, make sure run_pattern_sim_1vds.sh has the right settings
    ./run_pattern_sim_1vds.sh sim_0_3e8keV Eiger4M.geom 1vds.pdb 1vds.pdb.hkl 10 gpu wildfire 7 

## INTEXING PATTERN SIMULATION IMAGES   
# Taking all h5 images and putting them in a list (for example)
    ls /home/amkurth/Development/pattern_simulations/9_18_23_high_intensity/*.h5 > high_intensity.list
# check
    less high_intensity.list
# make sure and load this or else there will be mosflm error 
    module load ccp4/7.0
# actually indexing 
    indexamajig -i low_intensity.list -o index_test_low/test_low.stream -g Eiger4M.geom --peaks=peakfinder8 --threshold=200 --min-snr=8.0 --min-pix-count=1 --min-peaks=8 --min-res=50 --int-rad=2,4,6 --indexing=mosflm  --pdb=1vds.pdb --multi --check-peaks 
# Note: commented out parts of Eiger4M.geom file
