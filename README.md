# Unauthenticated and Authenticated scans with Tenable

In this lab I aim to become familiar with using Tenable and perform two vulnerabilty scans. One unauthenticated (without credentials), and an authenticated one (with credentials) and see the differences.  

## Unauthenticated Scan
An unauthenticated scan looks at the external section of systems. Anything that is internet-facing and does not include anything internal vulnerabilities as to see those a credential would be required.  

First of all to perform the scan I set up a Windows 11 Virtual Machine (VM) which I could test the scans on.  
After this I created a new scan on Tenable where I assigned the IP address of the VM as the target machine for the scans. Additionally under the discovery tab I made sure to uncheck the "Ping remote host" option, so that it does a detailed scan and checks even ports which might not respond to an ICMP ping. Additionally because this was going to be an unauthenticated scan I left the credentials tab without any input.

**Video 1: Creating the initial unauthenticated scan**  
  
https://github.com/user-attachments/assets/527f35f1-89e8-4af3-971d-732226e0dace

**Image 1: The results of the unauthenticated scan**
<img width="772" height="388" alt="Képernyőkép 2026-05-15 175213" src="https://github.com/user-attachments/assets/3882d0ae-3dce-4edf-8409-ce9217331149" />

After having completed the first scan I was wondering if it would give a different results if I would chose to disable the firewall on the VM. My reason for experimenting was that in many tutorial videos when I was researching this topic others disabled the firewall as  it is a closed system and to ensure all scanning can get through and wouldn not be blocked. In a real production environment however, this would be an unsafe practice.  

**Image 2: The results of the unauthenticated scan with the firewall disabled**
<img width="776" height="420" alt="Képernyőkép 2026-05-15 181400" src="https://github.com/user-attachments/assets/3377c404-bde4-49a9-9173-526f5227f7e5" />

The scan without the firewall did return more information points as well as an additional low vulnerability. This specific vulnerability "ICMP Timestamp Request Remote Date Disclosure" was able to happen as the firewall was not available to block timestamp requests. This vulnerability can be used to find out about uptime patterns, or use it for to exploit older time-based authentication weaknesses. It is not dangerous for modern systems though.  
the additional information points also relate to reaching services which are usually would be blocked by firewall e.g.: SMB authentication request.  

## Authenticated Scan
In this scan the only difference is that this time I provided the password of the VM system for the scanner. Enabling it to scan for internal vulnerabilities as well.
