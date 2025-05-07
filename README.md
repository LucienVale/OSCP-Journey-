# OSCP-Journey continue 
OSCP Journey – Chapter 2: ARP Spoofing with Python

Book: Ethical Hacking – A Hands-On Introduction to Breaking In by Daniel G. Graham
Author of Report: Luis  (aka Lucien Vale)
Environment: Kali Linux, VirtualBox, Host-Only Networking (Kali, Metasploitable2, pfSense)

⸻

Objective

This exercise focused on developing a Python-based ARP spoofer that executes a man-in-the-middle (MITM) attack by poisoning the ARP tables of both a victim and a router. The goal was to send spoofed ARP replies in a continuous loop, impersonating each device to the other, effectively redirecting traffic through the attacker’s machine.

⸻

Python Script Overview

The script uses Scapy to craft ARP packets and spoofs both the victim and the router:
	•	Defines arp_spoof() and arp_restore() functions
	•	Collects victim and router IPs from the command line
	•	Resolves MAC addresses using getmacbyip()
	•	Loops indefinitely to maintain spoofing until interrupted
	•	Restores the ARP tables gracefully on KeyboardInterrupt
  
  Usage
  sudo python3 arpspoof.py <victim_ip> <router_ip>
 
  Example:
  sudo python3 arpspoof.py 192.168.X.X 192.168.X.X
![Kali](https://github.com/user-attachments/assets/d38d9a9e-ed8c-4f5d-ba16-44fe8d062e3f)

  Terminal Output:
  Sending spoofed ARP packets

  Pressing CTRL + C restores the ARP tables:
  Restoring ARP Tables

  System Setup
	•	Verified that Kali, Metasploitable2, and pfSense were all reachable and in the same virtual network
	•	Enabled IP forwarding to allow Kali to relay traffic:
   echo 1 > /proc/sys/net/ipv4/ip_forward
  •	Ran the script successfully and confirmed that ARP replies were being sent

  Troubleshooting
	•	Fixed a SyntaxError due to using expect instead of except for exception handling
	•	Validated script behavior by watching continuous ARP packet injection
	•	Confirmed that all machines could ping each other pre- and post-spoofing

⸻

Key Takeaways
	•	Learned how to craft and inject ARP packets with Scapy
	•	Understood how ARP cache poisoning works at the protocol level
	•	Practiced clean exception handling and MAC resolution in Python
	•	Saw the importance of restoring state (ARP tables) after attacks
	•	Built confidence in running a full network-layer MITM setup

⸻

Next Chapter

Move on to Chapter 3, which focuses on traffic analysis using tools like tcpdump and Wireshark to capture and inspect packets routed through the attacker’s machine.

