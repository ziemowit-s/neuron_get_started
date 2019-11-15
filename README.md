This Repository contains get started instruction how to use NEURON + pyNeuroML + NetPyNE. 
This README contains installation instruction. For more information check Wiki page on GitHub.

# Anaconda
Since some libs may have conflicting version with NetPyNE it's better to create a new env called neuron with Python 3.6

* `conda create --name neuron python=3.6`
* `conda activate neuron`

# NeuroML
Install NeuroML before NEURON and NetPyNE

* go to https://github.com/NeuroML/jNeuroML/releases and download jNeuroML.zip
* `sudo unzip jNeuroML.zip -d /usr/local`
* `sudo ln -s /usr/local/jNeuroMLJar/jnml /usr/local/bin/jnml`
* add to ~/.bashrc: 
`export JNML_HOME="/usr/local/jNeuroMLJar"`
* `sudo apt-get install python-lxml`
* `pip install pyneuroml`

# NEURON
Install NEURON

* Download `neuron.deb` from https://www.neuron.yale.edu/neuron/download
* `dpkg -i neuron.deb`
* `nrnpyenv.sh`
* add to ~/.bashrc: 
`export PYTHONPATH="$PYTHONPATH:/usr/local/nrn/lib/python/"`
* Test NEURON Python in console:
  * `python`
  * `from neuron import h, gui`
  * if you see that NEURON has started - it works fine

# NetPyNE
Install NetPyNE

* `pip install netpyne`
* `pip install netpyne-ui`

# Test all
If you want to run it from IDE, preferably start IDE from the console to make sure PYTHONPATH is correctly loaded.

* clone the repository: 

