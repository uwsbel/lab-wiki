# Chrono-R Interface

#### Euler Computing Cluster

Some background on the Euler cluster can be found at the [Euler website](https://wacc.wisc.edu/infrastructure/).
The Chrono-R interface can work on any computer with both Chrono and R installed, but the nice GUI of RStudio is currently installed on one of the development nodes on Euler for easy use.
This has the main benefit of allowing easy collaboration through shared files and a shared configuration that only has to be maintained in one central place.

#### Initial Setup

##### Requesting Access

To request access you can fill out [this form](https://wacc.wisc.edu/resources/request.php). 
Be sure to mention that you are working on the Cyber-Human NSF project.

Approval should not take long, but in the meantime you should read some of the resources on the Euler website, in particular the [FAQ](https://wacc.wisc.edu/resources/docs/faqs.html) and [list of additional rules](https://wacc.wisc.edu/resources/docs/rules.html). 
Neither are comprehensive and you should always exercise good judgement and think before you type.
Euler is a wonderful computational asset, but is of course not immune to abuse and misuse so be careful when accessing it.

##### Shell Setup

To connect up to Euler first open a terminal that has ssh installed. 
On Windows this might be Powershell, cmd or (as the author uses) the nice new [Windows Terminal](https://github.com/microsoft/terminal).
On Mac this will likely be the [Terminal app](https://support.apple.com/guide/terminal/welcome/mac).

My username (and real name) is `jay` so in all the examples below replace `jay` with your username on Euler.
First use the command `ssh jay@euler.wacc.wisc.edu` to connect to Euler, as in the image below.

![Logging in to Euler](/lab-wiki/images/projects/login.png)

The first time that you login you'll be prompted to first enter the temporary password you received in your login email and then to change your password.
With this done, you should see something along these lines:

![Euler head node](/lab-wiki/images/projects/headnode.png)

Whenever you see `euler` in your prompt, you are on the euler head node.
The head node is where all jobs that get dispatched to the cluster are run from, you can think of it like an airport runway, many planes (software jobs) are getting launched and everything needs to run smoothly.
You **must not run anything on the head node**, rather you should switch to a development node (e.g. Curie) and work on any code there (Curie and the head node share a filesystem so any work that you do on Curie will be reflected on the head node). 
Doing work on the head node would be akin to taking apart and working on your airplane's engine in the middle of an airport runway; a huge inconvenience to others, you must go to the airplane shop (development node) to do that and only when finished bring the final plane out to the runway.
For projects that make use of the cluster, the head node serves as a launching-off place for tasks that run on the compute nodes of the cluster, but we are not at that stage yet in this project so there really isn't any reason to linger on the head node.

To switch to a development node, you should use the command `ssh curie`, the name `curie` only being known from within the Euler cluster.
You will have to enter your password again as you switch over to Curie.

![Switch to Curie](/lab-wiki/images/projects/to-curie.png)

##### Link to SynChrono-NSF Directory

Now that you're on Curie, you'll want to create a symbolic link from the shared project directory to a directory in your home directory.
You can do this with:

`ln -sv /srv/home/synchrono-nsf ~/synchrono-nsf`

##### Wrapping up

When you are done using the cluster you can exit by typing `exit` twice, once to leave Curie and again to leave the head node. 
This will leave you back on the terminal for your local computer (typing `exit` here should quit your local terminal also).

#### Connecting to RStudio

##### Port Redirection

With your account set up, you are now ready to connect up to RStudio.
The first step is to configure port-forwarding to tell your browser where to look for RStudio.
For that you should again go to your (local, i.e. neither Euler nor Curie) terminal and type the command `ssh -C -L 8787:curie:8787 jay@euler.wacc.wisc.edu`.
You will have to type in your password twice, once to connect to the headnode and again to connect to Curie.

![Port-redirection](/lab-wiki/images/projects/port-redirection.png)

When this command completes you will be left on Euler, it is a good practice to ssh over to Curie, but we are done using the command line for now.

##### Connect to RStudio

Open up your favorite browser and go to [localhost:8787](http://localhost:8787/), the login credentials are the same ones that you use for Euler.
Once logged in, the interface should look somewhat familiar to the normal RStudio interface.
The main piece of setup you should do is to change your working directory in the bottom right corner to `home/synchrono-nsf/Rtest` which is where all the files for the project will go for now.

![Change working directory](/lab-wiki/images/projects/setwd.png)

Next, to work with the Chrono functions, you'll have to `source` in the `loadChronoR.R` file which links several C++ dynamic libraries and then loads the ChronoR R-package.
When the load completes successfully, you're ready to start calling C++ functions that have been linked over, for example `doLeadFollowerSimulation`.

![Load ChronoR](/lab-wiki/images/projects/load-chrono-R.png)

#### Documentation

There are probably better places for documentation (e.g. within the R package itself), but for now it will live here

##### Available Functions

Currently there are two main functions available:

    data <- doLeadFollowerSimulationData( sim_time, l_times, l_steering, l_throttle, l_braking, f_times, f_steering, f_throttle, f_braking )
    data <- doLeadFollowerSimulationRDriver( sim_time, lead_fn, following_fn )

where the `sim_time` argument is a number in seconds indicating how long the simulation should run for and the arguments to `doLeadFollowerSimulationData` are vectors of numbers indicating the three input parameters for the lead (l) and following (f) vehicles. 

For example

    data <- doLeadFollowerSimulationData(10, c(0, 5), c(0, 0), c(1, 0), c(0, 0), c(0, 5), c(0, 0), c(1, 0), c(0, 0))

will have both the lead and following vehicles go to full throttle starting at time 0 and both completely step off the throttle at time 5. 
They will both drive straight ahead (steering = 0) and never brake.

The arguments for `doLeadFollowerSimulationRDriver` are a function to serve as the brain for the leader and a function to server as the brain for the follower. There is an example function ready to go in `sampleRDrivers.R`, so if you `source("sampleRDrivers.R")` you can then call 

    data <- doLeadFollowerSimulationRDriver(10, lead_fn, following_fn)

Reading the sample function in `sampleRDrivers.R` helps to show the format that a custom function should take. The input arguments will be a list with four entries: longitudinal position, longitudinal speed, the simulation step size and the current simulation time. The output from the custom function should also be a list with three values: throttle, steering and braking. Throttle and braking both be in the range [0, +1] and steering should be in the range [-1, 1] where -1 represents turned fully towards the left.

The output from both functions are the same - a list of four elements; the longitudinal position of the following vehicle, the longitudinal speed of the following vehicle, the times (every time step) that those measurements were taken, and the real time factor that the simulation ran in.

#### Other Resources

- [Wisconsin Applied Computing Center (WACC)](https://wacc.wisc.edu/about/)
- [RCpp Documentation](http://www.rcpp.org/)
- [Project Chrono homepage](https://projectchrono.org/)