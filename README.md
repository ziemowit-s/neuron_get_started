This README contains instruction how to install NEURON and solve some troubles with Ubuntu and CentOS.
The repository also contains file to test the installation on all operating systems.

NEURON should work with: most Linux distributions, Windows and OSX, however prerequisites 
installations and trouble solving concentrate here on Ubuntu.

#### NEURON Documentation
https://www.neuron.yale.edu/neuron/docs

## Prerequisites

#### Python

* Works with Python: 3.5 and 3.6 
* It is recommended to work with Python 3.6

* Python > 3.6 may work but it also may have different issues, eg: 
  * Python 3.7 have problem with libpython3.7 and pycairo on Ubuntu. 
  * It is possible to work with 3.7 but running from PyCharm may be error prone

#### Ubuntu

* Ubuntu 16.04 install:
  `sudo apt install libreadline5 python-lxml`

* Ubuntu 18.04 install:
  `sudo apt install libreadline-gplv2-dev python-lxml`

#### CentOS
Follow those procedures:
* `module load common/mpi/openmpi/3.1.4_gnu-7.3`
* `module load common/compilers/gcc/7.3.1`
* `rpm -q ncurses`
* `wget http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/p/python36-Cython-0.28.5-1.el7.x86_64.rpm`

#### Anadonda

* It is recommended to install Anaconda: https://www.anaconda.com/products/individual

* Then create a new env:
  * `conda create --name neuron python=3.6`
  * `conda activate neuron`
  * `cd neuron_netpyne_get_started`
  * `pip install -r requirements.txt`

## NEURON Installation

#### Ubuntu

* Download `*.deb` from https://www.neuron.yale.edu/neuron/download
* `dpkg -i neuron.deb`
* add to ~/.bashrc: 
`export PYTHONPATH="$PYTHONPATH:/usr/local/nrn/lib/python/"`

#### CentOS

* Download `nrn*.tar.gz` from https://neuron.yale.edu/ftp/neuron/versions/
* extract to `nrn_source`
* Download `iv*.tar.gz` from https://neuron.yale.edu/ftp/neuron/versions/
* extract to `iv_source`
* `cd iv_source`
* `./configure --prefix=$HOME/iv`
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

#### Test NEURON installation for all OS:
  * run `python neuron_example.py`
  * if you see no errors - it works fine

## How to use NEURON with PyCharm

![PyCharm](add_path_to_pycharm.png)

The image above shows where you need to go through settings, you can also follow the instruction below: 
  * Setting -> Project Interpreter
  * click on interpreter list and select "Show All"
  * Add or select your interpreter 
  * click "Show paths for the selected interpreter"
  * add the path: /usr/local/nrn/lib/python

## Known issues

### CentOS 
Refer to: https://www.neuron.yale.edu/neuron/download/compile_linux

### libreadline5 issue:
  * during compiling *.mod file you have an error: `/usr/bin/ld: cannot find -lreadline`
  * during nrngui run from console you have an error: error while loading shared libraries: libreadline.so.5: cannot open shared object file: No such file or directory
  * during Python `from neuron import h` you have an error:
  ```bash
  Traceback (most recent call last):
    File "/usr/local/nrn/lib/python/neuron/__init__.py", line 110, in <module>
      import neuron.hoc
  ImportError: libreadline.so.5: cannot open shared object file: No such file or directory

  During handling of the above exception, another exception occurred:

  Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    File "/usr/local/nrn/lib/python/neuron/__init__.py", line 112, in <module>
      exec("import neuron.hoc%d%d as hoc" % (sys.version_info[0], sys.version_info[1]))
    File "<string>", line 1, in <module>
  ModuleNotFoundError: No module named 'neuron.hoc37'
  ```
  
  Install in bash console:
  ```bash
  sudo apt-get install libreadline5
  ```
  
  #### Helvetica warning
  * During each NEURON run you may face error such as: 
  `nrniv: unable to open font "*helvetica-medium-r-normal*--14*", using "fixed"`
  
  * To solve it you must install helvetica font specified in the warning
  
  ###### For Ubuntu:
  ```
  sudo apt-get install xfonts-100dpi
  ```
  * Then logout and login again
