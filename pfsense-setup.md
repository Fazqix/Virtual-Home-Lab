
<h1 align="center"><img height="150" src="./images/pfsense/pfSenseLogo.png" /><br> pfSense Walkthrough</h1>

<p align="center">
  <b>Download Link to pfSense ISO file : https://www.pfsense.org/download/</b>
  <br>
  <sub>At the time of writing this, the latest version of pfSense is 2.6.0. 
   I selected AMD64  (64-Bit). I also selected the DVD Image (ISO) Installer and the Austin, TX USA Mirror.<sub>
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
    
##### LAN Interface
From here, type "2" to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `LAN interface` which is number 2.

  - Assign "192.168.1.1" as the `LAN IPv4 Address`.
  - Assign "24" as the new `LAN IPv4 Subnet Bit Count`.
  - Click "Enter" for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type "y" to enable the DHCP server on LAN.
  - Set the start address of the IPv4 range as "192.168.1.11".
  - Set the end address of the IPv4 range as "192.168.1.200".
  - Type "n" to not revert to HTTP as the webConfigurator protocol.
    
---
    
##### OPT1 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT1 interface` which is number 3.

  - Assign **192.168.2.1** as the `LAN IPv4 Address`.
  - Assign **24** as the new `LAN IPv4 Subnet Bit Count`.
  - Click **Enter** for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type **n** to enable the DHCP server on LAN.
  - Type **n** to not revert to HTTP as the webConfigurator protocol.

---   
    
##### OPT2 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT2 interface` which is number 4.

  - Assign "192.168.3.1" as the `LAN IPv4 Address`.
  - Assign "24" as the new `LAN IPv4 Subnet Bit Count`.
  - Click "Enter" for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type "n" to enable the DHCP server on LAN.
  - Type "n" to not revert to HTTP as the webConfigurator protocol.

---
    
##### OPT3 Interface
Leave OPT3 Interface without an IP address as it is going to have traffic that will be monitored by Security Onion.
    
---
    
##### OPT4 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT4 interface` which is number 6.

  - Assign "192.168.4.1" as the `LAN IPv4 Address`.
  - Assign "24" as the new `LAN IPv4 Subnet Bit Count`.
  - Click "Enter" for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type "n" to enable the DHCP server on LAN.
  - Type "n" to not revert to HTTP as the webConfigurator protocol.

---    

After all those changes to each interface, the interface list at the main menu should look like this :

![pfSenseInterfaceList](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/images/pfsense/pfSenseInterfaceList.png)

The `WAN Interface` IP address will most likely be different so don't panic :)
    
This marks the end of the configurations on the pfSense virutal machine. Additional changes will come through the Kali Linux Virtual Machine during the section of steps below. PfSense is safe to shut down from here by typing "6" to `Halt System`.
    
## WebConfigurator Changes and Firewall Rules
