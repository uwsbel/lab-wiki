# Lab Machines Using VNC

#### Connecting to College of Engineering VPN
* To access SBEL lab machines, you must connect to the College of Engineering VPN.

* For Windows or MacOS users, you will have to download a VPN client, GlobalProtect is recommended. There are two portal addresses available to Graduate Students and Staff: `engr-full.vpn.wisc.edu` and `engr-split.vpn.wisc.edu`. More information on accessing COE VPN can be found [here](https://kb.wisc.edu/cae/page.php?id=5573).

* Linux users may use a VPN client, such as OpenConnect as an altenative to GlobalProtect. Use the same portal addresses as above to connect. 

#### Steps to Accessing SBEL Lab Machines Through VNC
* Download and install a VNC viewer, which will be used to connect to the VNC servers running on SBEL lab machines.
	* The VNC viewer at [Tiger VNC](https://bintray.com/tigervnc/stable/tigervnc/1.10.1) is a sufficient client.
* SSH directly to the machine and forward the port for VNC. The VNC server will be open to port 5900.
	* ```ssh -L 5900:localhost:5900 user@machine```
* Connect your VNC viewer to the VNC port now open on localhost. For the example above, type ```localhost:5900``` and connect.
* You may now login through the Desktop Enviornment of the machine as you would normally.