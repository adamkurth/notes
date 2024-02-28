## *Running sfall on Mac (locally)*

1. Go to CCP4 directory.
   `/Applications/ccp4-8.0`
  
2. Start CCP4 with:
   `./start` 

    - Note: this will open a new bash terminal with CCP4 environment variables set.

3. `cd` to directory where the script `run_sfall.sh` is located. 
    
    - For purposes for this repo, it is located in:
      `~/Documents/vscode/CXFEL_Image_Analysis/CXFEL/peak_gaussian_filter/sim`

4. Run the script with:
    `./run_sfall.sh <PDB file> <space group> [<resolution>] [<point group>]`
    
    - Note: ensure that the `.pdb` file is located in the same directory as the script.
    
    - Example:
      `./run_sfall.sh 1IC6.pdb P43212 1.0 4/mmm`

5. The `.hkl` file will be in the `sfall_output/data_P43212/` directory.