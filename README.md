# Unauthenticated and Authenticaated scans with Tenable

In this lab I aim to become familiar with using Tenable and perform two vulnerabilty scans. One unauthenticated (without credentials), and an authenticated one (with credentials) and see the differences.  

## Unauthenticated Scan
An unauthenticated scan looks at the external section of systems. Anything that is internet-facing and does not include anything internal vulnerabilities as to see those a credential would be required.  

First of all to perform the scan I set up a Windows 11 Virtual Machine (VM)) which I could test the scans on. Beyond the initial set up of the VM I made sure that traffic from the IP address of the scanner would be allowed through with an inbound Windows Defender firewall rule. 


