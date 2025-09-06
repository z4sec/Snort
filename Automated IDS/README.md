Phase 2: Automated Snort IDS with Splunk Forwarder

Overview

This phase automates Snort IDS log forwarding to Splunk using a Splunk Forwarder on Ubuntu (port 9997). A custom rule detects FTP brute force attempts (port 21) from a Kali Linux attacker using Hydra. Alerts for ICMP, port scan, and FTP brute force are visualized in a Splunk dashboard.

Setup and Steps





Install Splunk Forwarder on Ubuntu: Download and configure to send logs to <SPLUNK_IP>:9997.



Configure Forwarder to monitor /var/log/snort/alert.fast (edit inputs.conf).



On Windows, configure Splunk to receive data on port 9997 (Settings > Data Inputs > TCP > New) and add Windows firewall inbound rule for 9997.



Add Snort rule for FTP brute force in local.rules:





Example: alert tcp any any -> 192.168.67.128 21 (msg:"FTP Brute Force Attempt"; content:"USER"; sid:1000003;).



Configure Ubuntu firewall: sudo ufw allow 21/tcp.



Create FTP user on Ubuntu: sudo adduser <FTP_USER>.



Simulate attack from Kali: hydra -l <FTP_USER> -P /usr/share/wordlists/rockyou.txt ftp://192.168.67.128 -t 4 -V.



In Splunk, create alerts for ICMP, port scan, and FTP brute force events.

Screenshots :- 

Notes :- 



Dashboard combines ICMP, port scan, and FTP alerts for real-time SOC monitoring.



Hydra attack uses rockyou.txt for password guessing.



Build a dashboard in Splunk to visualize all alerts (XML or dashboard editor).
