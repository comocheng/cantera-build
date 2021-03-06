# Cantera-build

A repo to help build Cantera.

Based on instructions from https://cantera.org/compiling/installation-reqs.html


To create and activate the conda environment
```
conda env create -f environment.yaml
conda activate cantera-dev
```

To update the conda env
```
conda env update -f environment.yaml --prune
conda activate cantera-dev
```

To get cantera code:
```
cd ..
git clone --recursive https://github.com/Cantera/cantera.git
cd cantera
```

To update cantera code:
```
cd ../cantera/
git checkout main
git pull
git submodule update
```

To configure and build, on a computer with 6 cores
```
scons build -j6
```
and with the documentation
```
scons build -j6 doxygen_docs=y sphinx_docs=y 
```
Note that this will save the `doxygen_docs` and `sphinx_docs` settings in your `cantera.conf` file so all future scons builds will also have them, until you clear or edit that file.

To test
```
scons test -j6
```
if it fails the output might be easier to read without the parallelization 
(so you should remove the `-j6`)


To install permanently you could do 
```
scons install
```

but may be preferable to just add the python stuff to the python path
```
conda install conda-build 
conda develop build/python
```

this creates a .pth file in your conda environment with a link to the built python files.
To remove it, do
```
conda develop -u build/python
```


### MATLAB
To build with MATLAB you must install MATLAB then 
```
scons build matlab_path="/Applications/MATLAB_R2022a.app"
```
Note that this will save the `matlab_path` settings in your `cantera.conf` file so all future Scons builds will also have it, until you clear or edit that file.
After building you will need to install
```
scons install
```

