# VASP 5.4.4 CPU Compilation on NERSC

This guide provides step-by-step instructions for compiling VASP on **NERSC CPU nodes**.

## 1. Copy the VASP Directory

Before compiling, create a new directory for your VASP build:

```bash
cp -r /path/to/original/vasp vasp_5.4.4_cpu
cd vasp_5.4.4_cpu
```

## 2. Load Required Modules

Ensure the necessary modules are loaded for compilation on NERSC:

```bash
module reset
module load cpu
module load PrgEnv-nvidia
module load cray-hdf5 cray-fftw
module load intel-mixed
module load vasp/5.4.4-cpu
```

## 3. Prepare Makefiles
Ensure that you have a properly configured `makefile` and `makefile.include` in the `vasp_5.4.4_cpu` directory. Use the `makefile` and `makefile.include` from this repository.

## 4. Compile VASP

Navigate to the `vasp_5.4.4_cpu`.
To clean previous builds before recompiling:

```bash
rm -rf build/ bin/* src/*.o src/*.mod
make clean
```

Manually create the build directory:

```bash
mkdir -p build/std
mkdir -p build/ncl
```

Then re-run the compilation:

```bash
make std ncl
```
## 5. References

For more details, refer to the official NERSC documentation:

- [NERSC VASP Compilation Guide](https://docs.nersc.gov/applications/vasp/)
- [VASP Memory Optimization](https://www.vasp.at/wiki/index.php/Not_enough_memory)
