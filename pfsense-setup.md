
### pfSense VM Setup Walkthrough
---
```
Download Link to pfSense ISO file : https://www.pfsense.org/download/

At the time of writing this, the latest version of pfSense is 2.6.0. I selected AMD64 (64-Bit). 
I also selected the DVD Image (ISO) Installer and the Austin, TX USA Mirror.
```
---

### Initial Virtual Machine Steps (VMware Workstation Pro 17)

```
1. Click on "Create a New Virutal Machine"
2. Click "Typical" for the virtual machine configuration type
3. Click "Next"
4. Next click "Installer Disc Image File (ISO)"
5. Click "Browse..."
6. From here select the file downloaded from the website provided above
7. Click "Next" to continue
8. Rename the virtual machine and confirm the location of where the VM will be stored by clicking "Browse..." again
9. Click "Next" to continue
10. Dedicate 20 GB to this VM for the disk size.
11. Ensure that the "Split virtual disk into multiple files" option is selected
12. Click Next
13. Click "Customize Hardware"
14. Click "Memory" and slide the bar to 2 GB or 2048 MB
15. Click the "Add..." button and then "Network Adapter"
16. Select the new network adapter (ex: Network Adapter 2) and change the network option to "Custom" and "VMnet2"
17. Repeat steps 15 and 16 until there are 6 total network adapters corresponding with their VMnet# (Excluding Network Adapter 1)
18. Click "Close" then "Finish"
19. Let the pfSense VM reboot.
```

### Assigning Interfaces

```
1. 
```
