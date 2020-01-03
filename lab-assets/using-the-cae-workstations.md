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

##### Windows Machines
Log in to windows from the sign-in screen using your CAE username and password.

> **If there is no option to enter a username...** \
> Click on the screen where it says "Other user" to enter the correct dialog.

When signing in, the user should ensure that the text below the password prompt reads "Sign in to: **ENGR**".

> **If the listed domain is not ENGR...** \
> Type your username as `ENGR\user` where "user" is replaced with your CAE account name.

##### Linux Machines (Local)
SBEL's Linux workstations typically use GDM as a login manager in order to provide users with a more consistent UI. This may, however, lead to confusion for new users who aren't yet familiar with the interface. Logging in should be as easy as entering a CAE Username and Password.

> **If the displayed username is incorrect...** \
> Click the "Cancel" button below the password prompt to return to user selection.

Users who have previously used a given workstation may be able to select their name from the list of available accounts.

> **If your name is not listed...** \
> Click on the words "Not listed?" below the list of names to enter your credentials manually.

##### Linux Machines (Remote)
SBEL's Linux workstations are also available via SSH. They should be visible from within the CAE or ME networks, so it should be possible to connect from the [Engineering VPN](https://kb.wisc.edu/cae/84859).

#### Adding New Software
On Linux Machines, SBEL members should be able to use the appropriate package manager (_e.g._ `dnf`, `apt`, `pacman`) to install new software. Non-SBEL folks will need to contact a system administrator in order to have the software installed.

Windows machines may or may not allow the installation of new software, depending on the configuration of the user's CAE account. For these systems, it is best to just contact a system administrator with any software requests.
