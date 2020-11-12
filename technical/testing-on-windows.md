# Testing on Windows (Washington)

To connect to Washington, see the description [here](https://projects.sbel.org/lab-wiki/lab-assets/using-the-cae-workstations.html#windows-machines-remote).

## Repositories

You can use `git-bash` to navigate and clone repositories as you would do on Linux. If you want to share a repository among several users (for example, the most recent version of a feature branch), `C:/Users/Public/chrono_repos` is a good place for it. If you aren't sharing a repo, you should clone it somewhere on your personal I drive, which will be shared across any CAE computer that you log into.

## Windows build process

The [Project Chrono installation guide](http://api.projectchrono.org/tutorial_install_chrono.html) has Windows screenshots to help you through the process.

On Washington specifically, many files will be on the C drive while others (e.g. your copy of the repo) will be on the I drive. This causes a problem with CMake where it can't properly read some files, failing with an error along the lines of `CMake Error: Unable to open check cache file for write. .../some_directory/.../CMakeFiles/CMakeTmp/CMakeFiles/cmake.check_cache`. You should be able to resolve it by issuing this command from a terminal:
```bash
mkdir ...\path_to\...\chrono_build\CMakeFiles\CMakeTmp\CMakeFiles
start cmd /c "cd /d ...\path_to\...\chrono_build\CMakeFiles\CMakeTmp\CMakeFiles && pause"
```
My understanding of this issue came from [here](https://gitlab.kitware.com/cmake/cmake/-/issues/18086).

## Dependencies and CMake Flags

### Chrono core

For header-only libraries or libraries with pre-compiled binaries, check in `C:/Users/Public/chrono_libraries` first and if not, download and copy the library to that folder so that others don't have to download and maintain the same files.

Dependencies that need to be installed will required admin permissions, for this you should ask Colin.

### Chrono::Irrlicht

`IRRLICHT_ROOT` seems to always get incorrectly auto-populated. It should be `C:/Users/Public/chrono_libraries/irrlicht-1.8.4` (as described in the normal [Project Chrono installation guide](http://api.projectchrono.org/tutorial_install_chrono.html)).

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

# What to do differently on Windows

There is no substitute for testing and confirming that your code works on Windows, but maybe this short list can help catch some common mistakes.

## \_\_declspec(dllimport/export) via CH\_\<module name\>\_API

On Windows you must explicitly tell the compiler which symbols to export to and import from the dlls that are built. This is done with the `__declspec(dllimport)` and `__declspec(dllexport)`, which in Chrono are aliased via macros (see `ChPlatform.h` and e.g. `ChApiGranular.h`) to properly expand to the correct version of import or export depending on what you are doing. The long and short is that _generally_ all you need to do is declare your classes like
````c++
class CH_GRANULAR_API ChMyGranularClassHere {
    ...
}
````
where `CH_GRANULAR_API` would be replaced by `CH_<other module name>_API` if you are working somewhere else. The specific name for your module is probably in `/src/chrono_somemodule/ChApiSomeModule.h`.

**One exception** is that when you have a class that is fully declared in a header, you **must not** use the `CH_<module name>_API` in the class declaration.

## DLL copying when adding a new external dependency

If you are adding an external dependency to a Chrono module (e.g. Irrlicht, OptiX, etc...) which has a shared library (e.g. `irrlicht.dll`), that dll either needs to be on the user's path or needs to be in the working directory that they launch programs from (the directory that contains `.exe`'s). 

To make the user's life easier, you should add code to our CMake to automatically copy the dll for the user into their build directory. See examples in `src/chrono_modulename/CMakeLists.txt`, e.g. [Chrono::Sensor (OptiX, GLEW)](https://github.com/projectchrono/chrono/blob/452fe87e3451ffe000c2f54b39cf965a0e157315/src/chrono_sensor/CMakeLists.txt#L455). The DLLs should also get added into the list of DLLs that are exported that is maintained in `cmake/ChronoConfig.cmake.in` using `list(APPEND CHRONO_DLLS "@DLL_NAME_HERE@")` in the section appropriate for the specific module.