Phase 3: Snort IPS Mode

Overview

This phase configures Snort in inline IPS mode on Ubuntu to block DNS amplification attacks. Logs are forwarded to Splunk via the Forwarder (port 9997), visualized in an updated dashboard, and analyzed in a triage write-up. The attack is simulated using DIIG from Kali Linux.

Setup and Steps





Edit snort.conf on Ubuntu: Set config policy_mode: inline.



Add drop rule for DNS amplification in local.rules:





Example: drop udp any any -> any 53 (msg:"DNS Amplification Attack - BLOCKED content:"|00 01 00 00|"; sid:1000004;).



Run Snort in inline mode: snort -Q -c /etc/snort/snort.conf -A fast.



Simulate attack from Kali: dig @192.168.67.128 google.com.



Verify block in DIG output (communication error).



Ensure Splunk Forwarder sends logs to 192.168.67.130:9997.



In Splunk, create alert for DNS drop events.



Update dashboard to include DNS alert alongside ICMP, port scan, and FTP.



Write triage report analyzing the blocked DNS amplification attack.

Screenshots :- 

Triage Summary





Attack: DNS amplification attempt.



Action: Snort IPS dropped UDP packets, preventing amplification.



Splunk: Logged drop events and visualized in dashboard.



Analysis: Detailed in triage report.txt
