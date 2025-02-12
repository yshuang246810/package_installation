# Building VASP 5.4.4 on NERSC

This guide provides step-by-step instructions for compiling and installing VASP 5.4.4 on NERSC systems.

## 1. Copy VASP Source Code

First, create a working directory and copy the VASP source code into it:

```bash
mkdir ~/vasp_build
cd ~/vasp_build
cp -r /path/to/vasp.5.4.4 vasp_5.4.4_cpu
cd vasp_5.4.4_cpu
```

## 2. Load Required Modules

Set up the environment by loading the necessary modules:

```bash
module reset
module load vasp/5.4.4-cpu
module load cpu
module load PrgEnv-nvidia
module load cray-hdf5 cray-fftw
module load intel-mixed
```

## 3. Prepare Makefiles

Ensure that you have a properly configured `makefile` and `makefile.include` in the `vasp_5.4.4_cpu` directory. Modify `makefile.include` for optimal performance on NERSC:

Example modifications:

- Set `FC = mpiifort`
- Enable `-fopenmp`
- Use `-march=native -xHost` for optimization

This installation is based on the official NERSC VASP guide: [NERSC VASP Documentation](https://docs.nersc.gov/applications/vasp/).

## 4. Compile VASP

Navigate to the `vasp.5.4.4` directory and compile:

```bash
make clean
make all
```

Compilation should generate the required VASP binaries in the `bin/` directory.

## Reference

For more details on memory optimization in VASP, refer to:
[Not Enough Memory - VASP Wiki](https://www.vasp.at/wiki/index.php/Not_enough_memory).
