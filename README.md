# POSICS-MC

This project is use for the Monte Carlo simulation of the POSICS-II project

## Installation

The following instruction explain how to install the required software for Monte Carlo simulation.
The instructions are provided for baobab.unige.ch HPC cluster.

Once logged in to baobab, we assume that you are in the folder `/path/to/` (where you want to install the software)

```angular2html
cd /path/to/
```

Create a environment setup file `setup_GATE.sh`

```angular2html
touch /path/to/setup_GATE.sh
```

### Install Geant4

Download the Geant4 v11.0.2 and unpack the tarball archive:

```angular2html
wget https://github.com/Geant4/geant4/archive/refs/tags/v11.0.2.tar.gz
tar -xvf v11.0.2.tar.gz
```

Create a build directory and move to this directory:
```angular2html
mkdir /path/to/geant4-v11.0.2-build/
cd /path/to/geant4-v11.0.2-build/
```

Load the required software from baobab:

```angular2html
module purge
module load GCC/11.2.0 CMake/3.21.1 Qt5/5.15.2 Boost/1.77.0 Python/3.9.6
```

Run CMake:

```angular2html
cmake -DGEANT4_INSTALL_DATA=ON -DGEANT4_USE_OPENGL_X11=ON -DGEANT4_USE_QT=ON -DCMAKE_INSTALL_PREFIX=/path/to/geant4-11.0.2-install /path/to/geant4-11.0.2/
```

Compile and install Geant4:

```angular2html
make -j8
make install
```
For more information on the installation of Geant4, please visit https://geant4-userdoc.web.cern.ch/UsersGuides/InstallationGuide/html/index.html

Add a command to `setup_GATE.sh` for the software:

```angular2html
echo 'source /path/to/geant4-11.0.2-install/bin/geant4.sh' >> /path/to/setup_GATE.sh
```
### Install GATE

Go to your installation path `/path/to`:

```angular2html
cd /path/to/
```

Load required modules for the installation:

```angular2html
module purge
module load GCC/11.2.0 OpenMPI/4.1.1 CMake/3.21.1 Qt5/5.15.2 ROOT/6.24.06
```

Load Geant4:

```angular2html
source /path/to/setup_GATE.sh
```
Download and unzip GATE:

```angular2html
wget https://github.com/OpenGATE/Gate/archive/v9.2.zip
unzip v9.2.zip
```
Create two directories to build and install GATE then move to the build directory:

```angular2html
mkdir gate-9.2-build gate-9.2-install
cd gate-9.2-build
```

Configure the installation (this command will open a screen)

```angular2html
ccmake ../Gate-9.2
```

press `c` then wait for finish an then press `e`.

On the screen, change set the following option:

- `BUILD_TESTING=ON`
- `CMAKE_INSTALL_PREFIX=/path/to/gate-9.2-install/`
- `GATE_USE_OPTICAL=ON`

press `c` then wait for finish, press `e` and then press `g` to generate.

Compile and install GATE:

```angular2html
make -j8
make install
```

Finally and these commands to your `setup_GATE.sh` file:

```angular2html
echo 'export PATH=/path/to/gate-9.2-install/bin:$PATH' >> /path/to/setup_GATE.sh
echo 'module load GCC/11.2.0 OpenMPI/4.1.1 Qt5/5.15.2 ROOT/6.24.06' >> /path/to/setup_GATE.sh
```

## Running GATE

Login to the baobab and execute the `setup_GATE.sh` file.

```angular2html
source /path/to/setup_GATE.sh
```

Run Gate:

```angular2html
Gate
```






