# nersc-fair-chem-build
Build mamba(a faster Conda) environment for orb_v3 @ NERSC.

Execute the instructions in order. 
https://github.com/orbital-materials/orb-models/tree/main 

Be sure to upload ckpts for orb to NERSC manually!

## Install environmental kernel for interactive jobs
`module load conda`  
`amba create --prefix <your_path> python=3.11`
`pip install orb-models`
`pip install --extra-index-url=https://pypi.nvidia.com "cuml-cu11==25.2.*"  # For cuda versions >=11.4, <11.8`
`pip install --extra-index-url=https://pypi.nvidia.com "cuml-cu12==25.2.*"  # For cuda versions >=12.0, <13.0`


`chgrp -R <your_project> <your_path>`  
`conda activate <your_path>`  
`mamba install numpy==1.26.4 scipy==1.15.1 ase e3nn pymatgen numba orjson jupyter seaborn pyyaml tqdm submitit tensorboard wandb==0.17.2 ipython ipykernel -y`  
`mamba install -c conda-forge python-lmdb`  
`pip install torch==2.4.0 torchvision==0.19.0 torchaudio==2.4.0 -f https://download.pytorch.org/whl/cu121/torch_stable.html`  
`pip install torch_scatter torch_sparse torch_cluster torch_spline_conv -f https://data.pyg.org/whl/torch-2.4.0+cu121.html`  
`pip install torch-geometric==2.5.3`  
`pip install fairchem-core`  
`pip install orb-models torch-dftd`  
`pip install "pynanoflann@git+https://github.com/dwastberg/pynanoflann#egg=af434039ae14bedcbb838a7808924d6689274168",`  

## Setup environmental kernel for interactive jobs
`python -m ipykernel install --user --name fair-chem --display-name fair-chem`

