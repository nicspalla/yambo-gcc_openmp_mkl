# yambo-gcc_openmp_mkl

Docker container for Yambo code v4.5.3 compiled with GCC v9.3 (OpenMP enabled) and MKL from Ubuntu 20.04 repository

In this Docker container the OS Ubuntu v20.04 is used as starting point for the installation of the Yambo code compiled with gcc@9.3. 
As parallelization strategies OpenMP threading system is enabled, the MPI parallelization is disabled.
The library used are: 
- IOTK
- HDF5
- NetCFD
- Intel MKL
- FFTW
- LibXC

## How to use it in a x86_64 personal computer

In order to run the container in a personal computer first pull the container:

```
docker pull nicspalla/yambo-gcc_openmp_mkl
```

To run Yambo into the container:

```
docker run -ti --user $(id -u):$(id -g) \
   --mount type=bind,source="$(pwd)",target=/tmpdir \
   -e OMP_NUM_THREADS=4  \
   nicspalla/yambo-gcc_openmp_mkl \
   yambo -F yambo.in -J yambo.out
```

Otherwise (suggested!), copy and paste the code below in a file, i.e called drun.sh:

```
#!/bin/bash 
docker run -ti --user $(id -u):$(id -g) \
   --mount type=bind,source="$(pwd)",target=/tmpdir \
   -e OMP_NUM_THREADS=4  \
   nicspalla/yambo-gcc_openmp_mkl $@
```

then give the file execute privileges:

```
chmod +x drun.sh
```

Move (or copy) this file in the directory where you want to use Yambo and use it as prefix of your Yambo calculation:

```
./drun.sh yambo -F yambo.in -J yambo.out
```

If the yambo container is working correctly you should obtain:

```
./drun.sh yambo
yambo: cannot access CORE database (SAVE/*db1 and/or SAVE/*wf)
```

```
./drun.sh yambo -h
```

should provide in output the help for yambo usage.
