<br><h1 align="center"><img height="250" src="../Images/SecurityOnionLogo.png" /><br><br> Security Onion Walkthrough</h1>

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

![UbuntuLogo](https://raw.github.com/Fazqix/Virtual-Home-Lab/master/Images/UbuntuLogo.png)

## Ubuntu Machine Setup

<b>Download Link to Ubunut ISO file : https://ubuntu.com/download/desktop</b>
<br>
<sub>At the time of writing this, the latest version of Ubuntu is 22.04.1 LTS.<sub>

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

Once the information appears, take note of the IP address listed :

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

This concludes the security onion walkthrough setup.
