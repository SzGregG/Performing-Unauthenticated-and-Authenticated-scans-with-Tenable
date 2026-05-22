# Unauthenticated and Authenticated scans with Tenable

In this lab I aim to become familiar with using Tenable and perform two vulnerabilty scans. One unauthenticated (without credentials), and an authenticated one (with credentials) and see the differences.  

## Unauthenticated Scan
An unauthenticated scan looks at the external section of systems. Anything that is internet-facing and does not include internal vulnerabilities as to see those a credential would be required.  

First of all to perform the scan I set up a Windows 11 Virtual Machine (VM) which I could test the scans on. After the initial set up I also set an inbound firewall rule to allow through traffic from the IP address of the local tenable scanner which was located on the same network. For external/unauthenticated scans however a firewall rule is not always necessary. Under the discovery tab when setting up a scan if the option "Ping remote host" is left unchecked it will still perform the scan and check every port even if it might take longer. The reason for this is because otherwise the scanner will ping every port and if there is no response then it would assume there is no machine there and proceed to not scan it. A no response after a ping howevever can also occur when the firewall just drops the packet as a defense mechanism. Without either the firewall rule or the discovery option of disabling pings the scan would just complete around a minute and return 0 vulnerabilities or information points. Alternatively disabling the firewall would also allow the scan to be completed successfully, in a real production environment however, this would be an unsafe practice.  

**Image 1: Creating the inbound firewall rule for the IP address of the scanner**
<img width="1039" height="780" alt="Képernyőkép 2026-05-22 144218" src="https://github.com/user-attachments/assets/69343063-bbc0-4d34-a5ad-4d0e41a20be5" />

As a lessons learned, this being my first case of setting up firewall rules on windows I have learned the hard way that list for Local IP address was meant to be the destination IP address and Remote IP address list meant to be source IP addresses of traffic instead of having a list differentiated between private IP addresses located on the network and public IP addresses from the internet. Due to this for quite a while my scans were failing as I put the scanner's IP under the local IP address list which meant the firewall kept blocking my scans. After lots of trial and error and research I manage to figure it out though thankfully.  
  
After this I created a new scan on Tenable where I assigned the IP address of the VM as the target machine for the scans. Additionally because this was going to be an unauthenticated scan I left the credentials tab without any input. Now my scan was ready to launch.

**Video 1: Creating the initial unauthenticated scan**  
  
https://github.com/user-attachments/assets/527f35f1-89e8-4af3-971d-732226e0dace

**Image 2: The results of the first successful unauthenticated scan**
<img width="772" height="388" alt="Képernyőkép 2026-05-15 175213" src="https://github.com/user-attachments/assets/3882d0ae-3dce-4edf-8409-ce9217331149" />

After 12 minutes of run time the result of the unauthenticated scan came back with a few medium vulnerabilities, but nothing high or critical. Now it was time to see how does the authenticated scan compares.

## Authenticated Scan
In this scan the only difference is that this time I provided the password of the VM system for the scanner under the credentials tab. Enabling it to scan for internal vulnerabilities as well.

**Image 3: The results of the authenticated scan**  
<img width="667" height="540" alt="image" src="https://github.com/user-attachments/assets/9193203e-0b72-4bc0-ac83-cb91dda6959d" />

On this occasion the scan took 19 minutes. There is a very clear difference in the number vulnerabilities as well with the the total points being 156 instead of just 26 and there being also 4 high severity vulnerabilities as well. 
