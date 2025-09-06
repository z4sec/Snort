Phase 1: Basic Snort IDS

Overview

This phase configures Snort in IDS mode on Ubuntu to detect ICMP ping and port scan attempts from a Kali Linux attacker. Logs are served via a Python HTTP server (python3 -m http.server 8000), manually downloaded to a Windows machine, and uploaded to Splunk for indexing and alerting. This demonstrates foundational SOC workflows for log analysis.

Setup and Steps





Install Snort on Ubuntu: sudo apt-get install snort.



Configure snort.conf and add rules to local.rules for ICMP and port scan detection:





Example ICMP rule: alert icmp any any -> 192.168.67.128 any (msg:"ICMP Ping Detected"; sid:1000001;).



Example port scan rule: alert tcp any any -> 192.168.67.128 any (msg:"Port Scan Detected"; flags:S; sid:1000002;).



Run Snort in IDS mode: snort -c /etc/snort/snort.conf -A fast.



Start Python server on Ubuntu to serve logs: python3 -m http.server 8000.



From Windows, download /var/log/snort/alert.fast via browser (http://192.168.67.128:8000).



In Splunk on Windows, upload logs, create an index, and configure alerts for ICMP and port scan events.

Simulate attacks from Kali: ping 192.168.67.128.

Screenshots :- 

Notes :- Manual log transfer mimics early SOC processes before automation.



Screenshots show raw logs, alert triggers, and Splunk indexing.
