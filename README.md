### Virtual Home Lab Documentation and Details

---

In Cybersecurity, it could be a daunting task to apply and implement security concepts if there is an unavailability of practical and safe infrastructure to carry out these activities.

I approached this project with that in mind. This homelab walks through the process of configuring, optimizing, and securing an I.T infrastructure. Although this will be at a relatively small scale, you will be able to apply the knowledge gained in a real-world large-scale/enterprise infrastructure. his Homelab is an environment in your home that is used to practice and improve your skills in a specific field. This home lab has components and tools similar to large-scale infrastructures. It’s a safe environment to work with these components and learn how they work.

---

### What does this Virtual Home Lab include?
- Using VMware Workstation Pro 17 as the "hypervisor"
- Configuring a pfSense firewall for Network Segmentation & Security
- Configuring Security Onion as an all-in-one IDS, Security Monitoring, and Log Management solution
- Configuring Kali Linux as an attack machine
- Configuring a Windows Server as a Domain Controller
- Configuring Windows desktops
- Configuring Splunk
- Additional Ubuntu/CentOS/Metasploitable/DVWA/Vulnhub machines (Exploitable Network Machines)

---

### Network Layout

```
Hypervisor Host
	VMware Workstation Pro 17
pfSense
	IPv4 : 192.168.1.1
Kali
	IPv4 : 192.168.1.10
	Interface : em1 
Victim Network
	IPv4 : 192.168.2.10
	Interface : em2
Security Onion
	IPv4 : 192.168.3.10
	Interface : em3
Splunk
	IPv4 : 192.168.4.10
	Interface : em5
```

---

All credit for this Home Lab Initial Setup goes to : https://cyberwoxacademy.com/building-a-cybersecurity-homelab-for-detection-monitoring/
