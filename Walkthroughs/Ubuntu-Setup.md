
<br><h1 align="center"><img height="250" src="../Images/UbuntuLogo.png" /><br><br> Ubuntu Walkthrough</h1>

<p align="center">
  <b>Download Link to Ubunut ISO file : https</b>
  <br>
  <sub>At the time of writing this, the latest version of Ubuntu is 22.04.1 LTS.<sub>
</p>

---
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
## Ubuntu Setup

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
