
<h1 align="center"><img height="250" src="../Images/pfSenseLogo.png" /><br> PfSense Walkthrough</h1>

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
    
![pfSenseInterfaces](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseInterfaces.png)

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

![pfSenseInterfaceList](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseInterfaceList.png)

The `WAN Interface` IP address will most likely be different so don't panic :)
    
This marks the end of the configurations on the pfSense virutal machine. Additional changes will come through the Kali Linux Virtual Machine during the section of steps below. PfSense is safe to shut down from here by typing "6" to `Halt System`.
    
## PfSense Web Setup and Configuration

After a Kali Linux virtual machine is configured (via KaliLinux-Setup.ed).

Once the Kali Linux machine is started, you can use the default credentials (if not yet changed).

- Username : "kali"
- Password : "kali"

Navigate to the web browser and search "https://192.168.1.1"

If successfully connected to the pfSense firewall, a screen like the one below should show up :

![pfSenseWebWarning](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseWebWarning.png)

Click the `Advanced...` button and a new screen confirming to accept the risk will pop up.

Click the `Accept the Risk and Continue` button. The pfSense screen matching the one below will appear :

![pfSenseWebLogin](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseWebLogin.png)

Sign into this pfSense login page with the default credentials.

- Username : "admin"
- Password : "pfsense"

Click "Next" on the initial screen to start the pfSense web setup and a bar saying `Step 1 of 9` should appear at the top.

Click "Next" again to proceed to `Step 2 of 9`.

- Leave the `Hostname` and `Domain` boxes empty.
- Set 8.8.8.8 as the `Primary DNS Server`.
- Set 4.4.4.4 as the `Secondary DNS Server`.
- Leave the `Override DNS` checkbox checked.

Click "Next" to proceed to `Step 3 of 9`.

- Leave the `Time Server Hostname` box empty.
- Set `Timezone` to your specific timezone.

Click "Next" to proceed to `Step 4 of 9`.

- Leave all options listed as default except the last two checked boxes.
- Uncheck the last two boxes.

![pfSenseUntickOptions](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseUntickOptions.png)

Click "Next" to proceed to `Step 5 of 9`.

- Leave all options default.

Click "Next" to proceed to `Step 6 of 9`.

- Set a new Admin Password.

Click "Next" to proceed to `Step 7 of 9`.

Click "Reload" to proceed to `Step 8 of 9`.

Click "Finish" to complete the web configuration process.

After the web setup process is complete, the pfSense dashboard will now be available.

![pfSenseDashboard](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseDashboard.png)



