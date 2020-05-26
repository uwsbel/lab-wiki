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

#### Connecting

##### Port Redirection

With your account set up, you are now ready to connect up to RStudio.
The first step is to configure port-forwarding to tell your browser where to look for RStudio.
For that you should again go to your terminal and type the command `ssh -C -L 8787:curie:8787 jay@euler.wacc.wisc.edu`.
You will have to type in your password twice, once to connect to the headnode and again to connect to Curie.

![Port-redirection](/lab-wiki/images/projects/port-redirection.png)

When this command completes you will be left on Euler, it is a good practice to ssh over to Curie, but we are done using the command line for now.

##### Connect to RStudio

Open up your favorite browser and go to [localhost:8787](http://localhost:8787/). 

##### RStudio Points

_Screenshot here that points out key features of the interface..._

#### Other Resources

- [Wisconsin Applied Computing Center (WACC)](https://wacc.wisc.edu/about/)
- [RCpp Documentation](http://www.rcpp.org/)
- [Project Chrono homepage](https://projectchrono.org/)