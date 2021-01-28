# Debugging and Profiling with ARM Forge

ARM Forge is a great tool for debugging and profiling HPC code in the realm of CUDA/MPI/OpenMP where normal debuggers fail. To get the most out of it you'll want your code compiled with debug symbols (so either `Debug` or `RelWithDebugInfo` if any optimizations are important), otherwise ARM won't be able to point you to the exact places in your code that show up during profiling.

## Download and Install

When browsing the ARM Forge website, remember that you are using the _client_, the _server_ (and related license) is already installed on Euler.

### Arch Linux

You can download the client on [their website](https://developer.arm.com/tools-and-software/server-and-hpc/downloads/arm-forge) the Red Hat Enterprise Linux (RHEL) 8 version works with Arch. After downloading, un-tar and then run the installer. When installing be sure to install to your home directory or `/opt` so that the installation does not compete with pacman.

After installation, you want to run the `forge` binary so something like `path/to/arm/forge/20.2.1/bin/forge`. You can always export this to your `PATH` as well.

### Windows

Setup should be quite similar, simply download the client. _If you have setup ARM Forge on Windows, please add details here_

## Setup steps

Once you've launched the application, you'll want to setup remote connections. You likely will just want one remote connection for Euler and one for a development node.

![Remote Launch Settings](/lab-wiki/images/technical/arm-forge-remote-launch.png)

- __Host Name__: ARM Forge will read from your `.ssh/config` file, so if you type `ssh euler` on the commandline, you should put `euler` here. Note you can do something like `euler curie` to get to one of the development nodes.
- __Remote Installation Directory__: `/usr/local/arm/x86_64/forge/20.2.1`
- __Remote Script__: This will be `source`'ed after ARM Forge connects, so this script file is where you should put any `module load`s that your program needs (see example below)
- __KeepAlive Packets__ and __Proxy through login node__ are good to have on as well

````bash
# Example 'Remote Script' file

#!/usr/bin/env bash
module load eigen/3.3.7;
module load openmpi/4.0.2;
````

## Profiling (MAP)

Profiling will give you an overview of your whole program, detailing what time was spent where in the program. Take note, there are some differences in the setup depending on whether you are submitting to Euler or to a development node.

![Map Setup on Curie](/lab-wiki/images/technical/arm-forge-map-setup.png)

- __Application__: Path to the binary that you want to profile
- __Working Directory__: Ensure that this exists
- __Metrics__: Ensure ones relevant to your application are checked
- __MPI__: Relevant if you are running an MPI application, here you can select the distribution of nodes that you'll use. Note that since this screenshot is from Curie, there is no option for more than one node.
    - __Implementation__: Select Open MPI
- __Submit to Queue__: Unchecked on development nodes since there is no slurm there.

After the setup is complete you should be able to hit run! You should see any output from your program on the screen and you can tell the profiler to stop and collect data at any point

## Debugging (DDT)

_Coming soon..._