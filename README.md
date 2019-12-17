This Repository contains get started instruction how to use NEURON + NetPyNE. 
This README contains installation instruction. For more information check Wiki page on GitHub.

# Prerequisites

## Ubuntu
NEURON > 7.5 requires readline library:

* `sudo apt-get install libreadline6 libreadline6-dev`

## CentOS

* `module load common/mpi/openmpi/3.1.4_gnu-7.3`
* `module load common/compilers/gcc/7.3.1`
* `rpm -q ncurses`


# Anaconda
Since some libs may have conflicting version with NetPyNE it's better to create a new env called neuron with Python 3.6

* `conda create --name neuron python=3.6`
* `conda activate neuron`
* `pip install matplotlib`
* `pip install scipy`

# NEURON

## Ubuntu

* Download `*.deb` from https://www.neuron.yale.edu/neuron/download
* `dpkg -i neuron.deb`
* add to ~/.bashrc: 
`export PYTHONPATH="$PYTHONPATH:/usr/local/nrn/lib/python/"`

## CentOS

* Download `nrn*.tar.gz` from https://neuron.yale.edu/ftp/neuron/versions/
* extract to `nrn_source`
### If without GUI
* `cd nrn_source`
* `./configure --prefix=$HOME/nrn --without-iv --with-nrnpython=python --with-paranrn`
### If with GUI
* Download `iv*.tar.gz` from https://neuron.yale.edu/ftp/neuron/versions/
* extract to `iv_source`
* `cd iv_source`
* `./configure`
* `make -j`
* `sudo make install -j`
* `cd ..`

* `cd nrn_source`
* `./configure --prefix=$HOME/nrn --with-iv=/where/is/iv --with-nrnpython=python --with-paranrn`
* `make`
* `make install`
* add to ~/.bashrc: 
`export PYTHONPATH="$PYTHONPATH:$HOME/nrn/lib/python/"`
`export PATH="$PATH:$HOME/nrn/x86_64/bin/"`

## All Linux versions
* Test NEURON Python in console:
  * `python`
  * `from neuron import h`
  * if you see that NEURON has started - it works fine

# NetPyNE
Install NetPyNE

* `pip install netpyne`

## If with GUI
* `pip install netpyne-ui`

# Test all

* If you want to run it from IDE, preferably start IDE from the console to make sure PYTHONPATH is correctly loaded.
* run `t1.py`

# Documentations

* NEURON: https://www.neuron.yale.edu/neuron/docs
* NetPyNE: http://netpyne.org/


# Add Python NEURON to PyCharm

![PyCharm](add_path_to_pycharm.png)

* Setting -> Project Interpreter -> click on interpreter list and select "Show All" -> Add or select your interpreter -> click "Show paths for the selected interpreter"
* add the path: /usr/local/nrn/lib/python

# Issues
* for problem with CentOS refer to: https://www.neuron.yale.edu/neuron/download/compile_linux

* If during compiling *.mod file you have an error: `/usr/bin/ld: cannot find -lreadline`
* `sudo apt-get install libreadline6 libreadline6-dev`
