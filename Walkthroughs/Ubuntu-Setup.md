<br><h1 align="center"><img height="250" src="../Images/UbuntuLogo.png" /><br><br> Ubuntu Walkthrough</h1>

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

Refer back to the SecurityOnion-Setup walkthrough.
