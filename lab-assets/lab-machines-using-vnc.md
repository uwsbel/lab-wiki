# Lab Machines Using VNC

---
layout: page
title: Euler Documentation - Privacy
description: Euler Documentation
permalink: /lab-wiki/lab-assets/lab-machines-using-vnc.html
share: false
---

#### Steps to Accessing SBEL Lab Machines Through VNC
* Add an entry to your .ssh/config for lab machines you are trying to access.
	* Set up so that you may login with a CAE VPN account, example below.
	```Host [machine name]
	User [cae username]
	Hostname %h.sbel.wisc.edu
	ProxyCommand ssh euler -W %h:%p%```
* SSH directly to the machine and forward the port for VNC. The VNC server will run on port 5900.
	* ```ssh -L 5900:machine:5900 machine```
	* You will be asked for a password, use your CAE password to log in.
* Now that you are able to connect to the machine, download a VNC viewer.
	* The VNC viewer at [Tiger VNC](https://bintray.com/tigervnc/stable/tigervnc/1.10.1) is a sufficeint client.
* Finally, login to a SBEL lab machine like above, and open your VNC viewer.
	* Connect to viewer to the VNC server open on the localhost port you selected.
	* ```localhost:5900```
