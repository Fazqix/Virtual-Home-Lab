# Initial Setup Walkthrough

This is the full walkthrough of the initial setup for this virutal home lab. The order of some parts of this walkthrough is important to the success of other parts working correctly.

---
---

<br><h1 align="center"><img height="250" src="../Images/KaliLinuxLogo.png" /><br><br> Kali Linux Setup</h1>

<p align="center">
  <b>Download Link to Kali Linux ISO file : <br> https://www.kali.org/get-kali/#kali-virtual-machines</b>
  <br>
  <sub>At the time of writing this, the latest version of Kali Linux is 2022.4.<sub>
</p>

---
    
## Virtual Machine Setup

This walkthrough assumes that you already know how to import a virtual machine file within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Disk Size** : 80 GB `Store virtual disk as a single files`
* **Memory** : 4 GB or 4,096 MB
* **Processors** : 4

Additional Network Adapter Settings :

* **Network Adapter 1** : `NAT`
* **Network Adapter 2** : `VMnet2`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.

This concludes the setup for Kali Linux.
    
---

<br><h1 align="center"><img height="250" src="../Images/pfSenseLogo.png" /><br><br> PfSense Setup</h1>

<p align="center">
  <b>Download Link to pfSense ISO file : <br> https://www.pfsense.org/download/</b>
  <br>
  <sub>At the time of writing this, the latest version of pfSense is 2.6.0. 
   I selected AMD64  (64-Bit). I also selected the DVD Image (ISO) Installer and the Austin, TX USA Mirror.<sub>
</p>

---
    
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
    
## PfSense Setup

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
    
##### OPT1 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT1 interface` which is number 3.

  - Assign **192.168.2.1** as the `LAN IPv4 Address`.
  - Assign **24** as the new `LAN IPv4 Subnet Bit Count`.
  - Click **Enter** for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type **n** to enable the DHCP server on LAN.
  - Type **n** to not revert to HTTP as the webConfigurator protocol.

##### OPT2 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT2 interface` which is number 4.

  - Assign "192.168.3.1" as the `LAN IPv4 Address`.
  - Assign "24" as the new `LAN IPv4 Subnet Bit Count`.
  - Click "Enter" for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type "n" to enable the DHCP server on LAN.
  - Type "n" to not revert to HTTP as the webConfigurator protocol.
  
##### OPT3 Interface
Leave OPT3 Interface without an IP address as it is going to have traffic that will be monitored by Security Onion.
    
##### OPT4 Interface
From here, type "2" again to select `2) Set interface(s) IP address` after the `Enter an option:` prompt.
    
Start with picking the `OPT4 interface` which is number 6.

  - Assign "192.168.4.1" as the `LAN IPv4 Address`.
  - Assign "24" as the new `LAN IPv4 Subnet Bit Count`.
  - Click "Enter" for both of the next options (IPv4 Upstream Gateway and IPv6).
  - Type "n" to enable the DHCP server on LAN.
  - Type "n" to not revert to HTTP as the webConfigurator protocol.

After all those changes to each interface, the interface list at the main menu should look like this :

![pfSenseInterfaceList](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseInterfaceList.png)

The `WAN Interface` IP address will most likely be different so don't panic :)
    
This marks the end of the configurations on the pfSense virutal machine. Additional changes will come through the Kali Linux Virtual Machine during the section of steps below. PfSense is safe to shut down from here by typing "6" to `Halt System`.

## PfSense Web Setup and Configuration

Start up your Kali virtual machine for this next part.

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

Next, configurations need to be made to the interfaces.

Click on the `Interfaces` tab and select `LAN` on the dropdown menu.

For interface `LAN`, change the description from "LAN" to "Kali".

*(This is to label the interfaces of what devices are running on what)*

Click `Save` at the bottom.

Repeat this process for all other interfaces (excluding em0/WAN interface).

- Keep `WAN` as "WAN"
- Change `LAN` to "Kali"
- Change `OPT1` to "VictimNetwork"
- Change `OPT2` to "SecOnion"
- Change `OPT3` to "SpanPort"
- Ensure that `OPT3` or now `SpanPort` interface is enabled.
- Change `OPT4` to "Splunk"

To confirm these changes, the interface list should match the screenshot below :

![pfSenseWebInterfaceList](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseWebInterfaceList.png)

While in the `Interfaces Assignment` list, switch to the `Bridges` tab.

Click `Add`.

Select `VictimNetwork`.

![pfSenseDisplayAdvanced](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/pfSenseDisplayAdvanced.png)

Click `Display Advanced`.

Scroll down to the `Advanced Configuration` Section and select `SPANPORT` for Span Port.

Then click `Save` at the bottom of the page.

Now click the `Rules` option in the dropdown menu of the `Firewall` tab.

Click the `Add` button with the arrow that points downward.

Under the `Edit Firewall Rule` section, select `Any` for the `Protocol` rule and then click `Save` at the buttom of the page.

This concludes all of the setups and configurations made to the pfSense firewall for this home lab walkthrough.

---

<br><h1 align="center"><img height="250" src="../Images/SecurityOnionLogo.png" /><br><br> Security Onion Setup</h1>

<p align="center">
  <b>Download Link to Security Onion ISO file : <br> https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md</b>
  <br>
  <sub>At the time of writing this, the latest version of Security Onion is 2.3.210-20230202.<sub>
</p>

---
    
## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Version** : Linux `CentOS 7 64-bit`
* **Disk Size** : 200 GB `Store virtual disk as a single files`
* **Memory** : 16 GB or 16,384 MB
* **Processors** : 4

Additional Network Adapter Settings :

* **Network Adapter 1** : `NAT`
* **Network Adapter 2** : `VMnet4`
* **Network Adapter 3** : `VMnet5`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.
    
---
    
## Security Onion Setup

Once the initial stages of loading are complete, type "yes" when prompted with this screen :

![SecurityOnionPrompt](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionPrompt.png)

Set a `username` and `password` when prompted and wait until Security Onion reboots.

When Security Onion reboots, login and a setup screen like the one below will pop up. Click `<Yes>` to this prompt and proceed.

![SecurityOnionPrompt](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionPrompt.png)

Click `Enter` while highlighting the `Install` option.

Select the `EVAL` option by using spacebar and then click `Enter`.

Type "AGREE" and accept the Elastic License to continue.

Set the `Hostname` to "SecOnion" or whatever is best to identify this machine and click `Enter`.

Select `ens32` displayed in the screenshot below using the spacebar again and click `<Ok>`.

![SecurityOnionENS](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionENS.png)

Select `DHCP`, then `<Ok>`.

Click `Enter` to confirm and `Enter` again to continue.

Select `Standard` on the prompt seen below and click `Enter`.

![SecurityOnionStandard](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionStandard.png)

Select `Direct`, click `Enter`, and let the configurations load.

Select `ens34` displayed in the screenshot below using the spacebar and click `<Ok>`.

![SecurityOnionENS2](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionENS2.png)

Select `Automatic` for the OS patch schedule and click `<Ok>`.

Leave the home networks listed in the text box as default and click `<Ok>`.

Select all options in the screenshot below using the spacebar and click `<Ok>`.

Click `<Yes>` to keeping the default Docker IP range.

Enter an email address and password for your administrator account and click `<Ok>`.

Select `IP` for web interface access and click `<Ok>`.

Select `<Yes>` to configure NTP servers.

Click `<Ok>` to defualt input for NTP servers to use.

Select `<No>` to running `so-allow` for now.

I recommend noting or screenshotting the options set screen seen below for future reference before clicking `<Yes>`.

![SecurityOnionOptionsSet](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionOptions.png)

Proceed and wait for Security Onion to initialize all the configuration steps. (This may take a while)

---

<br><h1 align="center"><img height="250" src="../Images/UbuntuLogo.png" /><br><br> Ubuntu Setup</h1>

<p align="center">
  <b>Download Link to Ubunut ISO file : <br> https://ubuntu.com/download/desktop</b>
  <br>
  <sub>At the time of writing this, the latest version of Ubuntu is 22.04.1 LTS.<sub>
</p>

## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Disk Size** : 20 GB `Split virtual disk into multiple files`
* **Memory** : 4 GB or 4,096 MB

Additional Network Adapter Settings :

* **Network Adapter 1** : `NAT`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.
    
---
    
## Ubuntu Setup and Security Onion Web Interface Access

Start up the Ubuntu virtual machine. Once logged in, the home screen should appear :

![UbuntuHome](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuHome.png)

Open up the `Terminal` in Ubuntu and run "ifconfig" so that the information below displays :

![UbuntuConfig](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuConfig.png)

*If an error appears referring to `net-tools` run this command :

```
sudo apt install net-tools 
```

**Once the information appears, take note of the IP address listed.**

## Security Onion Web Configuraiton

Click back onto the security onion host and log back in if not already.

Type this command :

```
sudo so-allow
```

Confirm your login password to proceed.

Next type "a" to select the first option.

Enter in the IP address of your Ubuntu machine that was noted in the previous screenshot and wait for it to update. This tells security onion to allow web interface access from that Ubuntu machine.

If everything was done right, your screen should look like the one below :

![SecurityOnionSoAllow](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/SecurityOnionSoAllow.png)

Click back on the Ubuntu machine and open the web browser.

Type the security onion host IP address into the address bar. This can be found in the options screenshot recommendation from the last step of the security onion setup section.

Once requested, the website with a risk warning should appear like the screenshot below :

![UbuntuWebWarning](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuWebWarning.png)

Click the `Advanced...` button and a new screen confirming to accept the risk will pop up.

Click the `Accept the Risk and Continue` button. The security onion login screen matching the one below will appear :

![UbuntuWebLogin](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuWebLogin.png)

Log in using the security onion login created previously and the dashboard containing security alerts can now be accessed like shown below :

![UbuntuAlerts](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuAlerts.png)

This concludes the security onion setup.

---

<br><h1 align="center"><img height="250" src="../Images/WindowsServer2019.png" /><br><br> Windows Server 2019 Setup</h1>

<p align="center">
  <b>Download Link to Windows Server 2019 ISO file : <br> https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019 </b>
  <br>
</p>

---
    
## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Disk Size** : 60 GB (Default)
* **Memory** : 2 GB or 4,048 MB (Default)

Additional Network Adapter Settings :

* **Network Adapter 1** : `VMnet3`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.

---

## Windows Server Setup and Domain Configuration

Power on the virtual machine and immediately click any key to boot from drive.

Click `Next`.

Click `Install Now`.

A screen like the one below should pop up listed with 4 options :

![WindowsServerSelection](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerSelection.png)

Select the `Windows Server 2019 Standard Evaluation (Desktop Experience)` and click `Next`.

Accept the License Terms.

Click `Next`.

Select `Custom: Install Windows only (advanced)`.

Click `New` with the yellow sun symbol and then `Apply`. The screen should then look like the visual below :

![WindowsServerDrives](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerDrives.png)

Click `Ok`.

Click `Next` and a window with installation status should appear like the one below :

![WindowsServerInstall](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerInstall.png)

When the installation is complete, create a password for the Administration account and the machine should reboot.

Log in using the Administrator account details in the screen below :

![WindowsServerLogin](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerLogin.png)

After logging in, the dashboard of the server manager should automatically pop up as displayed below :

![WindowsServerDashboard](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerDashboard.png)

Next the new server needs to be renamed. Navigate to `Settings` using the windows search bar.

Search "pc name" in the settings search bar.

The about page in settings will appear. Click the `Rename this PC` button.

Type a name to identify this PC as and click `Next`. The screen should've look similar to the one below :

![WindowsServerRename](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerRename.png)

After the server automatically reboots, the server manager will pop back up.

Up in the top right corner of the server manager, Click `Manage` for a dropdown menu so your screen looks like the screen below :

![WindowsServerRoles](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerRoles.png)

Select `Add Roles and Features` so a new windows pops up.

Click `Next` until you get to the `Server Roles` section of the wizard.

Check the `Active Directory Domain Services` box in the long list and click `Add Features` like in the screenshot below :

![WindowsServerADDS](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerADDS.png)

Click `Next` until you get to the `Confirmation` section of the wizard.

Now click `Install`

An installation progress screen will show the status of the installation until completetion like the one below :

![WindowsServerRoleInstall](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerRoleInstall.png)

After the install, click `Close`.

In the server manager, click the flag buton with the yellow caution triangle in the top right corner.

Click `Promote this server to a domain controller`

An Active Directory Domain Services Configuration Wizard should appear.

In the `Deployment Configuration` section, select `Add a new forest`.

Choose a domain name like the screenshot below :

![WindowsServerForest](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerForest.png)

Click `Next` and set a domain forest password.

Click the `Next` button until you get to the `Prerequisites Check` section.

Wait for the check to register which will display some yellow cautions in the results box like the display below :

![WindowsServerPrereq](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerPrereq.png)

Click `Install` and wait for the reboot.

After the reboot, log back in.

Select the `Manage` button in the top right again and select `Add Roles and Features`.

Click `Next` until you get to the `Server Roles` section.

Check the `Active Directory Certificate Services` box in the long list and click `Add Features` like in the screenshot below :

![WindowsServerADCS](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerADCS.png)

Click `Next` until you get to the `Confirmation` section of the wizard.

Check the `Restart the destination server automatically if required` box and click `Yes`.

Click `Install`.

After the installation, click `Close` seen in the screenshot below :

![WindowsServerADCSProgress](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerADCSProgress.png)

In the server manager, click the flag buton with the yellow caution triangle in the top right corner.

Click `Configure Active Directory Certificate Services on the destination server` under the `Post-deployment Configuration` alert.

An AC CS Configuration Wizard should appear.

Click `Next` through the `Credentials` section.

Within the `Roles Services` section, check the `Certification Authority` box.

Click `Next` until you get to the `Validity Period` section. Change the number to `99 Years` like the screenshot below :

![WindowsServerADCSValidity](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerADCSValidity.png)

Click `Next` until the `Confirmation` section. Click the `Configure` button, then `Close`.

Manually reboot the server using the Windows button for all changes to take effect.

Log back into the server.

In the top right of the server manager, click the `Tools` tab to view the dropdown menu.

Select `Active Directory Users and Computers` to open manager.

Click the arrow next to the domain name on the directory list on the left side of the manager.

Right click on the `Users` folder, hover over `New`, and select `User`.

Your screen should match the screenshot below before clicking :

![WindowsServerAddUser](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerAddUser.png)

Enter a First, Last, & User Logon name for the new user like the window below :

![WindowsServerExampleUser](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerExampleUser.png)

(In `User logon name:`, type the "-WIN10" after the initials of the user)

Click `Next` when finished.

Assign a password to the new account and check the `Password never expires` box. Click `Next`.

Click `Finish`.

Right click the new user created and click copy like the screenshot below :

![WindowsServerUserCopy](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerUserCopy.png)

Created another user with the same method as the first. Instead of adding "-WIN10", add "-WIN7" after the initials.

Now, go to the Windows search bar and search "Windows Defender Firewall".

Click `Turn Windows Defender Firewall on or off`. Turn the firewall off for all networks to match the screenshot below :

![WindowsServerFirewall](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerFirewall.png)

Click `OK`.

The last configuration to the domain is to set the default gateway to the PfSense firewall.

Go to the Windows search bar and search "Control Panel".

Once the windows opens, click `Network and Internet`.

Click `View Network Connections`.

Right click on `Ethernet0` and select `Propterties`.

Double click on `Internet Protocol Version 4 (TCP/IPv4)`.

Enter the following and match the screenshot below :

![WindowsServerGateway](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/WindowsServerGateway.png)

Click `OK` twice and reboot the server to update the changes.

---

<br><h1 align="center"><img height="200" src="../Images/Windows10Logo.png" /><br><br> Windows 10 Walkthrough</h1>

<p align="center">
  <b>Download Link to Windows 10 ISO file : <br> https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise</b>
  <br>
</p>

---
    
## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Disk Size** : 60 GB (Default)
* **Memory** : 2 GB or 4,048 MB (Default)

Additional Network Adapter Settings :

* **Network Adapter 1** : `VMnet3`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.

---

## Joining the Windows 10 PCs to the Domain Server
    



---

<br><h1 align="center"><img height="250" src="../Images/SplunkLogo.png" /><br><br> Splunk Walkthrough</h1>

<p align="center">
  <b>Download Link to Security Onion ISO file : https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md</b>
  <br>
  <sub>At the time of writing this, the latest version of Security Onion is 2.3.210-20230202.<sub>
</p>

---
## Virtual Machine Setup

This walkthrough assumes that you already know how to set up and create a virtual machine within the virutalization application of your choice (VirutalBox or VNware Workstation).
    
The recommended settings for this virtual machine are :

* **Version** : Linux `CentOS 7 64-bit`
* **Disk Size** : 200 GB `Store virtual disk as a single files`
* **Memory** : 16 GB or 16,384 MB
* **Processors** : 4

Additional Network Adapter Settings :

* **Network Adapter 1** : `NAT`
* **Network Adapter 2** : `VMnet4`
* **Network Adapter 3** : `VMnet5`

`All other settings can be left at default.`
    
Once these settings have been adjusted, start the virtual machine.
    
---
## Inferface Configurations
