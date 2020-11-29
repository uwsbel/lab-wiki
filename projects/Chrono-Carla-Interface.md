# Chrono-Carla Interface

Follow the build instructions [here](https://carla.readthedocs.io/en/latest/build_linux/) until you have a working Unreal setup. Clone Carla as well, but then you'll have to make some changes

## Acquire Clang 8

Arch's rolling release paradigm means you will likely have a newer version of Clang installed rather than Clang 8. Colin can help you install Clang 8 on your Arch Linux install

## Create Symlinks

Carla's makefiles look for Clang 8 in a very specific directory which is likely not where you have them installed. Symlink `/usr/bin/clang`, `/usr/bin/clang++` and `/usr/bin/clang++-8` to `/opt/llvm-8/bin/clang-8` (or wherever else you have clang 8 installed). For example
````bash
ln -s /opt/llvm-8/bin/clang-8 /usr/bin/clang++-8
````

## File changes

You'll have to make changes to two files. In the future these will be installed in an SBEL-specific fork of the Carla repo. 

### `setup.py`

First, add your distribution (e.g. `arch linux`) to the if-statement in `carla/PythonAPI/carla` like so:

```python
# carla/PythonAPI/carla/setup.py

if linux_distro.lower() in ["ubuntu", "debian", "deepin", "arch linux"]:
```

If you aren't on arch, you can run the following to get your exact distro name
```
python3 -c "import distro; print(distro.linux_distribution()[0].lower())"
```

### `setup.sh`

Next, change the `LLVM_INCLUDE` and `LLVM_LIBPATH` lines to point to your clang 8 install (from above). For example old:
```bash
LLVM_INCLUDE=${PWD}/${LLVM_BASENAME}-install/include/c++/v1
LLVM_LIBPATH=${PWD}/${LLVM_BASENAME}-install/lib
```

New:
```bash
LLVM_INCLUDE=/opt/llvm-8/include/c++/v1
LLVM_LIBPATH=/opt/llvm-8/lib
```

## Build PythonAPI

You can now go back to Carla's build guide from the link above. The only catch is that Carla is tied to Python 3.7. The easiest way to run Python 3.7 is likely through conda, so make sure that you run `make PythonAPI` and `make launch` from within a conda environment.