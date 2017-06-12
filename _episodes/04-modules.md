---
title: "Using Environmental Modules"
teaching: 45
exercises: 15
questions:
- "How to load modules to access software that I want to use for my research"
objectives:
- "Learn about *modules*, how to search, load and unload modules"
keypoints:
- "You can preload modules for each login by adding the load line on your .bashrc"
---

## Environmental Modules

The modules software package allows you to dynamically modify your user environment by using “modulefiles.”

Each modulefile contains the information needed to configure the shell for an application. After the modules software package is initialized, the environment can be modified on a per-module basis using the module command, which interprets modulefiles. Typically, modulefiles instruct the module command to alter or set shell environment variables such as PATH, MANPATH, and others. The modulefiles can be shared by many users on a system, and users can have their own collection to supplement or replace the shared modulefiles.

As a user, you can add and remove modulefiles from the current environment. The environment changes contained in a modulefile can also be summarized through the module show command. You are welcome to change modules in your .bashrc or .cshrc, but be aware that some modules print information (to standard error) when loaded, this should be directed to a file or /dev/null when loaded in an initialization script.

More information on modules can be found by typing module help on the NICS systems. Ignore the module init* commands – these modify a .modulerc file which is incompatible with the way NICS modules are set up. If you run into any issues, remove any .modulerc and log in again.

## Basic arguments

The following table lists the most common module command options

| Command	| Description |
|:--------|:------------|
| module list	  | Lists modules currently loaded in a user's environment. |
| module avail  | Lists all available modules on a system. |
| module show	  | Shows environment changes that will be made by loading a given module. |
| module load	  | Loads a module. |
| module unload	| Unloads a module. |
| module help	  | Shows help for a module. |
| module swap	  | Swaps a currently loaded module for an unloaded module. |

## Creating a private repository

On day 3 we will show and example of how to create a private module.
With private modules you or your research group can have control on the software
of interest for the group.

The basic procedure is to locate modules on a folder accessible by relevant users
and add the variable `MODULEPATH` to your `.bashrc`

MODULEPATH controls the path that the module command searches when looking for
modulefiles.  
Typically, it is set  to a  default  value by the bootstrap procedure.  
MODULEPATH can be set using ’module use’ or by the module initialization
script to search group or personal modulefile directories before  or  after
the master modulefile directory.

## Modules on Spruce

~~~
---------------------------------------------- /usr/share/Modules/modulefiles ----------------------------------------------
dot     modules null    use.own

----------------------------------------------- /usr/share/Modules/software ------------------------------------------------
atomistic/abinit/8.0.8_ompi2.0.1_intel15 genomics/blast/2.3.0                     genomics/plink
atomistic/abinit/8.2.3_intel17           genomics/bowtie                          genomics/qiime
atomistic/lammps/2016.11.17              genomics/bowtie2                         genomics/repeatexplorer
atomistic/octopus/6.0_gcc63              genomics/breakdancer                     genomics/repeatmasker
atomistic/vasp/5.3.3_ompi2.0.1_intel15   genomics/bwa/0.7.10                      genomics/rsem
chemistry/amber/12                       genomics/bwa/0.7.12                      genomics/samtools/0.1.19
chemistry/amber/14                       genomics/celera                          genomics/samtools/1.2
chemistry/amber/16                       genomics/clumpp                          genomics/sga
chemistry/autodock_vina                  genomics/cufflinks                       genomics/shapeit
chemistry/gamess                         genomics/delly                           genomics/sickle
chemistry/gaussian/g03                   genomics/distruct                        genomics/soapdenovo
chemistry/gaussian/g09                   genomics/dwgsim                          genomics/sratoolkit
chemistry/gromacs/4.6.5                  genomics/eigensoft                       genomics/structure
chemistry/gromacs/5.0.5                  genomics/emboss                          genomics/svseq
chemistry/gromacs/5.0.5-gpu              genomics/errcorr_tools                   genomics/tabix
chemistry/gromacs/5.1.2                  genomics/express                         genomics/tablet
chemistry/gromacs/5.1.2-gpu              genomics/falcon                          genomics/tophat2
chemistry/namd/ibverbs/2.10              genomics/fasta36                         genomics/trf
chemistry/namd/ibverbs/2.11              genomics/fastqc                          genomics/trinity/2.0.6
chemistry/namd/ibverbs/2.9               genomics/fastx_toolkit                   genomics/trinity/2.2.0
chemistry/namd/mpi                       genomics/gatk/2.8                        genomics/vcftools/0.1.11
chemistry/orca                           genomics/gatk/3.5                        genomics/vcftools/0.1.14
chemistry/schrodinger                    genomics/genometools                     gnu/coreutils
data/cdf/3.5.0.2                         genomics/hmmer                           gnu/parallel
data/hdf5/1.8.12                         genomics/htslib                          mae/cmg/2014.10
data/sqlite/3.9.2                        genomics/igv                             mae/cmg/2015.10
engineering/damask/2.0.1                 genomics/lastz                           mae/elk/2.2.10
genomics/abyss/1.3.6                     genomics/ltrfinder                       mae/elk/2.3.16
genomics/abyss/1.9.0                     genomics/mrsfast                         statistics/matlab/2013b
genomics/allpaths                        genomics/muscle                          statistics/matlab/2014a
genomics/bamtools                        genomics/pbdagcon                        statistics/rstudio/0.97.551
genomics/beagle                          genomics/phase                           visualization/paraview
genomics/bedtools                        genomics/phrap                           visualization/visit/2.10
genomics/bioperl                         genomics/picard-tools                    visualization/visit/2.10.2
genomics/blasr                           genomics/pindel/0.2.5b1                  visualization/vtk/7.0.0
genomics/blast/2.2.28                    genomics/pindel/0.2.5b8

---------------------------------------------- /usr/share/Modules/development ----------------------------------------------
compilers/binutils/2.26              compilers/swig/3.0.7                 libraries/netcdf/4.4.1.1_gcc63
compilers/cuda/7.5                   environment/gcc-mpi                  libraries/netcdf/fortran-4.4.4_gcc63
compilers/cython/0.23.4              environment/gcc-serial               libraries/openfoam/3.0+
compilers/gcc/4.8.2                  environment/intel                    libraries/petsc/3.7.3
compilers/gcc/4.9.0                  git/2.8.3                            libraries/Qt/4.7.3
compilers/gcc/5.3.0                  libraries/bioconductor/3.2           libraries/Qt/5.5.1
compilers/gcc/6.3.0                  libraries/boost/1.47.0               libraries/R/Rhipe
compilers/idl/8.5.1                  libraries/boost/1.55.0               libraries/sqlite/3.9.2
compilers/intel/13.0.1               libraries/boost/1.57.0               linalg/armadillo/7.600.2
compilers/intel/14.0                 libraries/bupc/2.2                   linalg/armadillo/7.800.1
compilers/intel/15.0.1               libraries/DFS/myhadoop               linalg/openblas/0.2.19
compilers/intel/17.0.1               libraries/fftw/2.1.5                 mpi/intel/4.1.0.024
compilers/java/jre1.8.0              libraries/fftw/3.3.4                 mpi/intel/4.1.1.036
compilers/julia/0.3.11               libraries/fftw/3.3.4-mpi             mpi/intel/5.0.3.048
compilers/julia/0.5.1                libraries/fftw/3.3.6_gcc63           mpi/mpich2/1.2.1
compilers/python/2.7.10              libraries/gsl/2.1                    mpi/mvapich2/1.9
compilers/python/2.7.13              libraries/gtest/1.7.0                mpi/mvapich2/2.0.1
compilers/python/2.7.3               libraries/hdf5/1.8.12                mpi/mvapich2/2.2.0
compilers/python/3.5.1               libraries/hdf5/1.8.13_intel          mpi/openmpi/1.6.5
compilers/python/3.6.0               libraries/hdf5/1.8.17_intel          mpi/openmpi/1.6.5-intel
compilers/python/virtualenv          libraries/hdf5/1.8.18_gcc63          mpi/openmpi/1.8.4
compilers/R/3.1.0                    libraries/jemalloc/3.6.0             mpi/openmpi/2.0.1
compilers/R/3.2.1                    libraries/libgd/2.2.4                mpi/openmpi/2.0.1_intel15
compilers/R/3.2.2                    libraries/log4cpp/1.1.2              mpi/openmpi/2.0.2_gcc63
compilers/R/3.3.2                    libraries/mkl/11.2.1                 xalt/0.6.0
compilers/ruby/2.2.3                 libraries/mkl/4.1.1.036

~~~
{: .source}


{% include links.md %}
