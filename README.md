Installation of gromacs and pymol on win64 instructions

# GROMACS

**1) Download GROMACS source code**

https://manual.gromacs.org/documentation/

**2) Download Visual Studio 2019 community edition**

https://visualstudio.microsoft.com/it/vs/older-downloads/

Select “Desktop development with C++”.

**3) Download Intel OneAPI**

https://www.intel.com/content/www/us/en/developer/tools/oneapi/base-toolkit-download.html

Perform a customized installation and select “Intel oneAPI Math Kernel Library”

**4) From Windows search bar open "x64 Native Tools Command Prompt for VS 2019"**

CD to gromacs **root** (p.s. not the "src") folder.

**5) Generate build files**

- Be sure to se cl.exe is the MSVC++ compiler:
```
$ set CC=cl
$ set CXX=cl
```

- Finally generate build files:
```
$ cmake -G"NMake Makefiles" -S. -B./build -DGMX_GPU=off -DGMX_FFT_LIBRARY=mkl -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=off -DMKL_INCLUDE_DIR="C:/Program Files (x86)/Intel/oneAPI/mkl/2022.0.0/include" -DMKL_LIBRARIES="C:/Program Files (x86)/Intel/oneAPI/mkl/2022.0.0/lib/intel64/mkl_intel_lp64.lib;C:/Program Files (x86)/Intel/oneAPI/mkl/2022.0.0/lib/intel64/mkl_sequential.lib;C:/Program Files (x86)/Intel/oneAPI/mkl/2022.0.0/lib/intel64/mkl_core.lib"
```
Note: be sure to match the Intel oneAPI mkl current version and the installation path! For example:

>-DMKL_INCLUDE_DIR="**C:/Program Files (x86)**/Intel/oneAPI/mkl/**2022.0.0**/include"


**6) Compilation using cmake (takes a long time)**

```
$ cd build
$ nmake
```

**7) Copy the GROMACS library**

- Create a new folder
- Copy "bin, lib, share" folder from "build" into the newly created folder.
- Create a .bat file with the following content:

```
 @set "PATH=[path\to\Gromacs]\bin;%PATH%"
 @set GMXDATA=[path\to\Gromacs]\share\gromacs
 @cmd
 ```
 Be sure to change [path\to\Gromacs] accordingly.
 
 
 # PyMOL (Python 3.7.x)
 
 **1) Download and install the required python libraries**
 
- Download PyMOL launcher, PyMOL and Pmw from 
https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymol-open-source

cp37=python 3.7
cp38=python 3.8... and so on.

- Install them in the following order:
```
pip install Pmw‑[version]‑py3‑none‑any.whl
pip install pymol‑[version]‑cp37‑cp37‑win_amd64.whl
pip install pymol_launcher‑[version]‑cp37‑cp37‑win_amd64.whl
```
Other dependecies: numpy

**2) Install AutoDock Vina**

https://vina.scripps.edu/downloads/

Add AutoDock Vina to the system variables (add the path to Vina to the Path list). 
 
