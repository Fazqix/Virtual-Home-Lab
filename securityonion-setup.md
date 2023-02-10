<h1 align="center"><img height="150" src="./images/securityonion/SecurityOnionLogo.png" /><br> Security Onion Walkthrough</h1>

<p align="center">
  <b>Download Link to Security Onion ISO file : https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md</b>
  <br>
  <sub>At the time of writing this, the latest version of Security Onion is 2.3.210-20230202.<sub>
</p>

## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Disk Size** : 20 GB `Split virtual disk into multiple files`
* **Memory** : 2 GB or 2048 MB

Additional Network Adapter Settings :

* **Network Adapter 1** : `NAT`
* **Network Adapter 2** : `VMnet2`
* **Network Adapter 3** : `VMnet3`
* **Network Adapter 4** : `VMnet4`
* **Network Adapter 5** : `VMnet5`
* **Network Adapter 6** : `VMnet6`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.
    
## Inferface Configurations

`Accept all defaults` and allow pfSense reboot. More specifically this means clicking `Enter` through the options until pfSense auto reboots.

Once the pfSense reboots with the default configured settings, you should come to a screen similar to this :
    
![pfSenseInterfaces](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/images/pfsense/pfSenseInterfaces.png)

From here, type "1" to select `1) Assign Interfaces` after the `Enter an option:` prompt.
    
It will ask you if VLANs should be set up now, type "n" for no.
    
Next,
    
  - Type "em0" to assign it to the `WAN interface`
  - Type "em1" to assign it to the `LAN interface`
  - Type "em2" to assign it to the `Optional 1 interface`
  - Type "em3" to assign it to the `Optional 2 interface`
  - Type "em4" to assign it to the `Optional 3 interface`
  - Type "em5" to assign it to the `Optional 4 interface`
    
Then type "y" to `proceed`. These changes will be made and the menu from the **screenshot above** should pop back up.
    
---
