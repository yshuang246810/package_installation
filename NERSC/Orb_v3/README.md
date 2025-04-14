# nersc-orb-v3-build
Build mamba(a faster Conda) environment for orb_v3 @ NERSC.

Execute the instructions in order. 
https://github.com/orbital-materials/orb-models/tree/main 

Be sure to upload ckpts for orb to NERSC manually when running orb jobs!

## Install environmental kernel for interactive jobs
`module load conda`  

`mamba create --prefix <your_path> python=3.11`

`pip install orb-models`

`pip install --extra-index-url=https://pypi.nvidia.com "cuml-cu11==25.2.*" ` # For cuda versions >=11.4, <11.8

`pip install --extra-index-url=https://pypi.nvidia.com "cuml-cu12==25.2.*" ` # For cuda versions >=12.0, <13.0 (Use this one.)

`mamba install ase e3nn pymatgen numba orjson jupyter seaborn pyyaml tqdm submitit tensorboard wandb ipython ipykernel torch-dftd`

`mamba install -c conda-forge python-lmdb` 

## Setup environmental kernel for interactive jobs
`python -m ipykernel install --user --name orb-v3 --display-name orb-v3`
