## Agave Notes:

Using `conda` in `agave`:

- Loading common modules:
``` bash
module load crystel/0.9.0
module load python/3.7.1
```

- Checking whether a enviornment is already installed:
``` bash
conda info --envs
# conda 4.7.11
source activate [env_name]
```

- Using the `pytorch-1.20` environment:
``` bash
source activate pytorch-1.20
```

- Any module which are not already installed can be installed using `pip`:
``` bash
pip install [module_name]
```
