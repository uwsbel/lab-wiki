# Chrono On CSL Minisim

## Acquire Keys to CSL

You can request keys to the lab from Professor John Lee through the standard UW [key request form](https://keylime.engr.wisc.edu/request), the room is ME 3018.

## SBEL Workstation in CSL

### Software setup

The machine name is `lbj.sbel.wisc.edu`, it runs CentOS and you can log in with your CAE account. Most Chrono dependencies are available through `module load`. A notable exception is OptiX which you must install yourself (`module load groupmods/optix` will not work). 

Until CMakePresets are available on Euler, these should be the Variables that you need to update

````
GLFW_INCLUDE_DIR    /usr/local/glfw/x86_64/3.3.2/include
GLFW_LIBRARY        /usr/local/glfw/x86_64/3.3.2/lib64/libglfw3.a
IRRLICHT_LIBRARY    /usr/local/irrlicht/1.8.3/lib/libIrrlicht.so
IRRLICHT_ROOT       /usr/local/irrlicht/1.8.3/include/irrlicht
OptiX_INSTALL_DIR   $env{HOME}/libraries/NVIDIA-OptiX-SDK-6.5.0-linux64
````

### Hardware setup

There should be a keyboard and mouse in CSL that you can use. It certainly doesn't hurt to bring your own wireless mouse as there isn't a great place to sit. The controls for the three big monitors are three buttons towards the center on the bottom (right around the 'Sony' text). The center button is the power button if you hold it but also changes the input if you tap it once. The input should default to HDMI2 which is what lbj is connected to.

## MiniSim

### Steering Wheel and Pedals

The steering wheel and brake should be automatically connected to lbj and properly send their inputs to Irrlicht. The gas pedal (throttle) is not automatically connected and still needs some changes/bug fixes in the Irrlicht Driver to get working properly.
