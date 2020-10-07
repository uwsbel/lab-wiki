# Using the CAE Workstations

_Some Linux workstations and all Windows workstations in ME4150 are maintained by SBEL, but use CAE servers for authentication._

#### Authorized Users
Individuals who match one or more of the categories below can feel free to use any of these workstations as needed.

- Any member of SBEL
- Anybody working on an SBEL project
- Visiting researchers (if they have their own CAE account)
- Students attending office hours in ME4150

These workstations are provided for the convenience of everybody in lab, and as such, they should only be used temporarily by any single user. Users who require a long-term solution should request access to a dedicated workstation.

#### Logging In

The login procedure varies slightly between Windows and Linux workstations, so please read the appropriate guidelines below.

##### Windows Machines (Local)
Log in to windows from the sign-in screen using your CAE username and password.

> **If there is no option to enter a username...** \
> Click on the screen where it says "Other user" to enter the correct dialog.

When signing in, the user should ensure that the text below the password prompt reads "Sign in to: **ENGR**".

> **If the listed domain is not ENGR...** \
> Type your username as `ENGR\user` where "user" is replaced with your CAE account name.

##### Windows Machines (Remote)
You can use Remote Desktop Connection to log-in to the windows machine (Washington) remotely, with the same credentials as above. If you get an error about not being authorized for remote login, send an email to [Josh](https://directory.engr.wisc.edu/services/Staff/Jankowski_Joshua/) and cc Dan.

![Remote Desktop Connection](/lab-wiki/images/technical/washington-login.png)

##### Linux Machines (Local)
SBEL's Linux workstations typically use GDM as a login manager in order to provide users with a more consistent UI. This may, however, lead to confusion for new users who aren't yet familiar with the interface. Logging in should be as easy as entering a CAE Username and Password.

> **If the displayed username is incorrect...** \
> Click the "Cancel" button below the password prompt to return to user selection.

Users who have previously used a given workstation may be able to select their name from the list of available accounts.

> **If your name is not listed...** \
> Click on the words "Not listed?" below the list of names to enter your credentials manually.

##### Linux Machines (Remote)
SBEL's Linux workstations are also available via SSH. They should be visible from within the CAE or ME networks, so it should be possible to connect from the [Engineering VPN](https://kb.wisc.edu/cae/84859).

Most machines hostnames are `<name>.sbel.wisc.edu` so `wilson.sbel.wisc.edu`.
Tesla happens to be different and is  `tesla.sbel.wisc.edu.engr.wisc.edu`. 

##### Remote Display Forwarding (Linux -> Windows)

There may be cases where you want to compile code on Linux (e.g. when [editing code remotely](https://github.com/uwsbel/lab-wiki/blob/master/technical/vscode.md#setting-up-remote-access), but display the output on a Windows home machine or laptop. 
You can do this with XForwarding, ssh will send the X11 graphics display commands via ssh to a waiting X11 server running on your home machine (that you will have to set up) which will then display the output of these commands. 
**Note** this will not work for OptiX-based graphics, only for Irrlicht (or say, Firefox, but what's the point in that?). 
This section written by Jay, send all complaints to him.

###### Local Machine steps
1. Download and install [XMing](https://sourceforge.net/projects/xming/) on your Windows machine
2. Start the server when you want to XForward
3. When connecting via ssh, pass the Y flag, `ssh -Y user@myhost`. You can also include the line `ForwardX11 yes` in the block for your host within your `~/.ssh/config` file.

###### Remote Machine steps
1. `echo $DISPLAY` should return `localhost:10.0`, if it does not you can `export DISPLAY=localhost:10.0` 
2. You may also need to edit your `/etc/ssh/sshd_config` file since X11 Forwarding is likely disabled there by default
3. After editing the sshd file you should restart the ssh daemon with `sudo systemctl restart sshd`

##### Remote Display Forwarding (Linux -> OS X)

_If you have done this, please fill in this section!_

#### Adding New Software
On Linux Machines, SBEL members should be able to use the appropriate package manager (_e.g._ `dnf`, `apt`, `pacman`) to install new software. Non-SBEL folks will need to contact a system administrator in order to have the software installed.

Windows machines may or may not allow the installation of new software, depending on the configuration of the user's CAE account. For these systems, it is best to just contact a system administrator with any software requests.
