# Testing on Windows (Washington)

To connect to Washington, see the description [here](https://projects.sbel.org/lab-wiki/lab-assets/using-the-cae-workstations.html#windows-machines-remote).

## Repositories

You can use `git-bash` to navigate and clone repositories as you would do on Linux. If you want to share a repository among several users (for example, the most recent version of a feature branch), `C:/Users/Public/chrono_repos` is a good place for it. If you aren't sharing a repo, you should clone it somewhere on your personal I drive, which will be shared across any CAE computer that you log into.

## Windows build process

The [Project Chrono installation guide](http://api.projectchrono.org/tutorial_install_chrono.html) has Windows screenshots to help you through the process.

On Washington specifically, many files will be on the C drive while others (e.g. your copy of the repo) will be on the I drive. This causes a problem with CMake where it can't properly read some files.

## Dependencies and CMake Flags

### Chrono core

For header-only libraries or libraries with pre-compiled binaries, check in `C:/Users/Public/chrono_libraries` first and if not, download and copy the library to that folder so that others don't have to download and maintain the same files.

Dependencies that need to be installed will required admin permissions, for this you should ask Colin.

### Chrono::Sensor

CUDA is installed in `C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/<version>` and its variables should populate automatically. OptiX 6.5.0 is installed in `C:/ProgramData/NVIDIA Corporation/OptiX SDK 6.5.0`.

```
OPTIX_INSTALL_DIR=C:\ProgramData\NVIDIA Corporation\OptiX SDK 6.5.0
optix_DLL=C:\ProgramData\NVIDIA Corporation\OptiX SDK 6.5.0\bin64\optix.6.5.0.dll
optix_LIBRARY=C:\ProgramData\NVIDIA Corporation\OptiX SDK 6.5.0\lib64\optix.6.5.0.lib

GLEW_INCLUDE_DIR=C:\Users\Public\chrono_libraries\glew-2.1.0\include
GLEW_LIBRARY=C:\Users\Public\chrono_libraries\glew-2.1.0\lib\<build type>\x64\glew32.lib
GLFW_INCLUDE_DIR=C:\Users\Public\chrono_libraries\glfw-3.3.2.bin.WIN64\include
GLFW_LIBRARY=C:\Users\Public\chrono_libraries\glfw-3.3.2.bin.WIN64\lib-vc2019\glfw3.lib
```

`optix_prime_DLL/LIBRARY` and `optixu_DLL/LIBRARY` follow the same format as the regular `optix` variables.

### SynChrono

Intel-MPI is installed at `C:/Program Files (x86)/IntelSWTools/` the variables should auto-populate from there. Flatbuffers is already in the `...\chrono_libraries` folder but you will have to fill in two variables.

```
Flatbuffers_DIR=C:\Users\Public\chrono_libraries\flatbuffers\CMake
Flatbuffers_INCLUDE_DIR=C:\Users\Public\chrono_libraries\flatbuffers\include
```
