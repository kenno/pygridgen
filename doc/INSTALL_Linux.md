# Setting up a fresh linux box for grid generation

## Basics linux stuff
```
$ sudo apt-get update && sudo apt-get upgrade
$ sudo apt-get autoremove libreoffice-common
$ sudo apt-get install git vim build-essential gfortran
```

## Getting miniconda and creating an environment
```
$ wget http://repo.continuum.io/miniconda/Miniconda-latest-Linux-x86_64.sh -O miniconda.sh
$ chmod +x miniconda.sh
$ ./miniconda.sh -b
$ export PATH=/home/grid/miniconda/bin:$PATH
$ conda update conda
$ conda create --name=gridgen python=2.7 pip nose matplotlib numpy --yes
$ source activate gridgen
```

### Dealing with projected data:
If you're on 64-bit linux:

```
$ conda install -c https://conda.binstar.org/rsignell pyproj --yes
```

Or if you're on 32-bit linux:
```
$ conda install basemap --yes
```

## Cloning repos from github

```
$ mkdir sources && cd sources
$ git clone https://github.com/geosyntec/pygridgen.git
```

## Building C/C++ dependencies

`$ cd pygridgen/external`

### nearest neighbors
```
$ cd nn
$ ./configure && sudo make install
$ cd ..
```

### CSA
```
$ cd csa
$ ./configure && sudo make install
$ cd ..
```

### gridutils
```
$ cd gridutils
$ ./configure CFLAGS="-g -O2 -Wall -pedantic -fPIC"
$ sudo make install
$ cd ..
```

### gridgen-C
```
$ cd gridgen
$ ./configure
$ sudo make
$ sudo make lib
$ sudo make shlib
$ sudo make install
$ cd ..
```

## Install pygridgen
```
$ cd ~/sources/pygridgen
$ source activate gridgen
$ python setup.py install
```
