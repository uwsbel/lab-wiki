# Chrono On CSL Minisim

## Acquire Keys to CSL

You can request keys to the lab from Professor John Lee through the standard UW [key request form](https://keylime.engr.wisc.edu/request), the room is ME 3018.

## SBEL Workstation in CSL

### Software setup

The machine name is `lbj.sbel.wisc.edu`, it runs CentOS. Most Chrono dependencies are available through `module load`. A notable exception is OptiX which you must install yourself (`module load groupmods/optix` will not work). 

Until CMakePresets are available on Euler, these should be the Variables that you need to update

````
GLFW_INCLUDE_DIR    /usr/local/glfw/x86_64/3.3.2/include
GLFW_LIBRARY        /usr/local/glfw/x86_64/3.3.2/lib64/libglfw3.a
IRRLICHT_LIBRARY    /usr/local/irrlicht/1.8.3/lib/libIrrlicht.so
IRRLICHT_ROOT       /usr/local/irrlicht/1.8.3/include/irrlicht
OptiX_INSTALL_DIR   $env{HOME}/libraries/NVIDIA-OptiX-SDK-6.5.0-linux64
````

### Hardware setup

Bring your own keyboard, mouse, ...