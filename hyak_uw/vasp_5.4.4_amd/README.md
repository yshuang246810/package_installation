# Compiling and Running VASP on UW Hyak (AMD ckpt-g2)

This guide provides step-by-step instructions for compiling and running VASP on **UW Hyak (AMD ckpt-g2)**.

## 1. Copy the VASP Directory

Before compiling, create a new directory for your VASP build:

```bash
cp -r /path/to/original/vasp /your/target/directory/vasp_amd
cd /your/target/directory/vasp_amd
```

## 2. Load Required Modules

Load the necessary modules for Intel oneAPI:

```bash
module load intel/oneAPI/2021.1.1
export MKL_CBWR=AVX2
```

## 3. Prepare Makefiles
Ensure that you have a properly configured `makefile` and `makefile.include` in the `vasp_amd` directory. Use the `makefile` and `makefile.include` from this repository.

## 4. Compile VASP

Navigate to the `vasp_amd`.
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

## 5. Submitting a Job on Hyak

Create a job script (e.g., `vasp_job.sh`) with the following configuration:

```bash
#!/bin/bash
#SBATCH --job-name=vasp_sliding
#SBATCH --output=job.out
#SBATCH --error=job.err
#SBATCH --partition=ckpt-g2
#SBATCH --account=memc
#SBATCH --nodes=1
#SBATCH --ntasks=192
#SBATCH --time=24:00:00
#SBATCH --mem=1500G
#SBATCH --export=all

module load intel/oneAPI/2021.1.1
export MKL_CBWR=AVX2

mpirun -n 192 /your/target/directory/vasp_amd/bin/vasp_std
```

## 6. Submit the Job

Run the following command to submit the job:

```bash
sbatch vasp_job.sh
```

To check job status:

```bash
squeue -u $USER
```

## 7. Optimize `KPAR` and `NPAR` for Performance

### Current Settings:
- `KPAR = 3`
- `NPAR = 64`

### Optimization Guidelines:
- `KPAR` should match the number of **k-points** for best efficiency.
- If memory usage is too high, increase `NPAR` and test different values to balance efficiency.

### Checking Memory Usage
Inspect the VASP output to check memory per MPI rank:

```bash
grep 'total amount of memory used by VASP MPI-rank0' OUTCAR
```

Adjust `NPAR` and `KPAR` accordingly if memory is insufficient.

For more details on memory optimization, refer to the [VASP Wiki](https://www.vasp.at/wiki/index.php/Not_enough_memory).

## References

- [VASP Wiki: Not Enough Memory](https://www.vasp.at/wiki/index.php/Not_enough_memory)
