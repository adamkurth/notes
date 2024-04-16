### Notes on SOL

- [ASU Research Computing](https://researchcomputing.asu.edu/)
- [SOL User Guide](https://confluence.cc.asu.edu/display/RC/SOL+User+Guide)
- [SOL User Guide - Getting Started](https://confluence.cc.asu.edu/display/RC/SOL+User+Guide+-+Getting+Started)

### Remote Desktop via SSH:
To get a **VSCode window** on the remote machine:

- Open the command palette (Ctrl+Shift+P)
- Type `Remote-SSH: Connect to Host...`
- Select "Host `sol`" from the list, if this does not show up then use the Command Palette to Open SSH Configuration File and add the following entry:****
    ```bash
    Host sol
    HostName sol.asu.edu
    User amkurth
    ForwardX11 yes  
    ```
- Enter the password when prompted
- Then open a folder in the remote machine, by clicking on the "Open Folder" button.


### Normal workflow:

To open a Remote Desktop on SOL using the web interface, go to [ASU Research Computing](https://ood06.sol.rc.asu.edu/pun/sys/dashboard/batch_connect/sessions).

- Ensure that you are not on a login node, by typing,
```bash
interactive
# or
interactive -p <partition_name> -q <QOS>
```
Partition names are `general`, 

- To login to SOL supercomputer, 
```bash
ssh -Y <ASURITE>@sol.asu.edu
```

- To check the status of the nodes, 
```bash
sinfo 
# or
sinfo -p <partition_name>
```

- To check the status of your jobs,
```bash 
squeue -u <ASURITE>
```

- Check the available modules, 
```bash
# To list all available modules
module avail
# To search for a specific module
module avail <module_name>
```

- To load a module, 
```bash
# To load a module
module load <module_name>
```

#### `mamba` Package Manager:

- To install a package using `mamba`, 
```bash
mamba install <package_name>
# or
mamba install -c conda-forge <package_name>
```