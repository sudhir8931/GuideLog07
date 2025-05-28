 Installing Quantum ESPRESSO in a conda environment, without root/sudo.

Step 1: Install Miniconda

Download and install Miniconda:

wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash Miniconda3-latest-Linux-x86_64.sh

Step 2️: Create and activate Conda environment

Create an environment for QE (named qe-env):

conda create -n qe-env -y

conda activate qe-env

Step 3️: Install necessary compilers and libraries via Conda

conda install -c conda-forge gcc gfortran mpich openblas cmake -y

This gives you:
•	gcc and gfortran for compiling
•	mpich for MPI
•	openblas for BLAS/LAPACK

Step 4️: Download and extract Quantum ESPRESSO

Get the QE source (example for QE 7.4.1):

wget https://github.com/QEF/q-e/releases/download/qe-7.4.1/qe-7.4.1-ReleasePack.tar.gz

mkdir -p ~/src

tar -xzf qe-7.4.1-ReleasePack.tar.gz -C ~/src

cd ~/src/qe-7.4.1

Step 5️: Configure QE

From the QE source directory:

./configure --prefix=$HOME/local \
    MPIF90=mpif90 \
    F90=mpif90 \
    CC=mpicc \
    BLAS_LIBS="-lopenblas" \
    LAPACK_LIBS="-lopenblas"

Step 6️: Build QE

make all -j$(nproc)

 Step 7️: Install QE (locally)

make install

Step 8️: Update PATH and LD_LIBRARY_PATH

Add this to your ~/.bashrc:

export PATH=$HOME/local/bin:$PATH

export LD_LIBRARY_PATH=$HOME/local/lib:$HOME/local/lib64:$LD_LIBRARY_PATH

Reload it:

source ~/.bashrc

Step 9️: Verify Installation

Check if pw.x is accessible:

which pw.x

pw.x -h



