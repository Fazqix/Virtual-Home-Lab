
<h1 align="center">pfSense Walkthrough</h1>

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
    
## Assigning Interfaces

`Accept all defaults` and allow pfSense reboot.

Once the pfSense reboots with the default configured settings, you should come to a screen similar to this :
    
<p alight="center">
  <a href="https://github.com/fazqix/virtual-home-lab/main/images/pfsensebootup.png">
</p>

```
1. Once the 
1. Enter Option 1
2. Type "n" to the VLAN Setup Prompt
3. Enter "em0, em1, em2, em3, em4 & em5" respectively for each consecutive question. (em0 should be WAN, em1 should be LAN, em2 should be OPT1, em3 should be OPT2, em4 should be OPT3, em5 should be OPT4)
4. Type "y" to "Do you want to proceed"

1. Enter Option 2
2. Click "2" (this is for LAN interface)
3. Enter "192.168.1.1" for LAN IPv4 address > 24 for subnet > "Enter" > "Enter" > "y" for enabling DHCP server on LAN > "192.168.1.11" for the start of the range > "192.168.1.200" for the end of the range > "n" to reverting to HTTP as the webConfigurator protocol

1. Enter Option 2
2. Click "3" (this is for OPT1 interface)
3. Enter "192.168.2.1" for LAN IPv4 address > 24 for subnet > "Enter" > "Enter" > "n" for enabling DHCP server on OPT 1 > "n" to reverting to HTTP as the webConfigurator protocol

1. Enter Option 2
2. Click "4" (this is for OPT2 interface)
3. Enter "192.168.3.1" for LAN IPv4 address > 24 for subnet > "Enter" > "Enter" > "n" for enabling DHCP server on OPT 1 > "n" to reverting to HTTP as the webConfigurator protocol

*Leave the OPT3 interface without an IP as it is going to have the span port with traffic that Security Onion will be monitoring.*

1. Enter Option 2
2. Click "6" (this is for OPT1 interface)
3. Enter "192.168.4.1" for LAN IPv4 address > 24 for subnet > "Enter" > "Enter" > "n" for enabling DHCP server on OPT 1 > "n" to reverting to HTTP as the webConfigurator protocol
```
