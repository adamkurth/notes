## How to run Reborn

0. Make sure environment is set up correctly.
   - Also make sure that you're in the root directory or `reborn` directory on `master` branch.
  
    ```bash
    conda env update --file environment.yml
    ```

    and to swtich branches
    
    ```bash
    git checkout master
    ```

1. Update the `PATH` variable to the `reborn` directory in the root directory. 

export PYTHONPATH="/Users/adamkurth/Documents/vscode/CXFEL/reborn_dev/developer/rkirian/projects/cxls:$PYTHONPATH"   

    ```bash

    export PYTHONPATH="/Users/adamkurth/Documents/vscode/CXFEL/reborn_dev:$PYTHONPATH"
    python developer/rkirian/projects/cxls/water_background.py
    ```

2. Change directories into this directory.

    ```bash
    /Users/adamkurth/Documents/vscode/CXFEL_Image_Analysis/CXFEL/reborn/developer/rkirian/projects/cxls
    ```

3. Type this command to run the program.

    ```bash
    python water_background.py
    ```

    or

- Run this file from the root directory. Where the `reborn` module is visible in the root directory.

    ```bash
    python developer/rkirian/projects/cxls/water_background.py
    ```

### Troubleshooting

1. Ensure that `check_fortran.sh` script gets ran with no errors.
    
    ``` bash
    # from root directory
    cd developer
    ./check_fortran.sh
    ```

and, if you have pytest installed, run the tests.

    ```bash
    # from root directory
    cd tests 
    pytest
    ```

- This was the bottleneck for my mac. I had to install `meson` to get the fortran to work.

- Ensure that `meson` and `ninja` are installed, run the following command:

    ```bash
    conda install -c conda-forge meson
    ```

