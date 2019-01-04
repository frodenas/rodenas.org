---
title: 'VMware Workstation 6: Remote Debugging easier from Eclipse and VS'
author: ferdy
date: 2007-02-13T23:59:27+00:00
url: /blog/2007/02/14/vmware-workstation-6-remote-debugging-easier-from-eclipse-and-vs/
b2007:
  - 02
bcategories:
  - Eclipse
  - Visual Studio

---
[VMWare Workstation][1] Version 6 will include a new feature that simplifies the process of debugging applications running on a virtual machine instance from Eclipse and Visual Studio.

> **Integrated Virtual Debugger**
> 
> With the new Workstation IDE (integrated development environment) plug‐ins, software developers are provided with a configurable interface between their virtual machines and Visual Studio (Windows only) or Eclipse (Windows or Linux) that lets them easily test, run, and debug programs in virtual machines.
> 
> You can specify settings such as the location of the virtual machine, which setup or clean‐up scripts to execute, the location of shared folders, and (in Visual Studio) directories to be copied between the host and guest.
> 
> When configured, the integrated virtual debugger finds the virtual machine, powers it on if necessary, sets up the environment based on your configuration settings, and launches or attaches to the application. All breakpoints, watch points, and so on that you set in your IDE will function as if you were running your application on the host computer.
> 
> Depending on the configuration setting you specify, when the application finishes running, the virtual machine is powered off, suspended, reverted to a snapshot, or left in its current state.

You can try now this new feature downloading the just released beta version at the [VMware Workstation 6 Beta Program][2].

Tony, the developer of the Eclipse plugin, explains some of the project details in his post [Making remote debugging easier to use][3], so drop him a comment if you like this new feature.

(Via [EclipseZone][4])

 [1]: http://www.vmware.com/products/ws/
 [2]: http://www.vmware.com/products/beta/ws/
 [3]: http://quikchange.livejournal.com/170570.html
 [4]: http://www.eclipsezone.com/eclipse/forums/t90510.html

## Comments

### Comment by Sahil Ebrahim on 2010-03-11 11:33:15 +0000
Near impossible to setup even once you have set the username and passwords the same on both the host and the guest machine.