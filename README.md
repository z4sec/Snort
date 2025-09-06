Snort IDS/IPS Home Lab with Splunk Integration

Overview

This project is a Security Operations Center (SOC) home lab demonstrating intrusion detection and prevention using Snort and log analysis with Splunk. Designed as a portfolio piece for a SOC analyst role, it showcases skills in rule creation, log forwarding, attack simulation, alerting, dashboard visualization, and incident triage across three phases.





Virtual Machines:





Kali Linux: Attacker simulating ICMP ping, port scans, FTP brute force, and DNS amplification.



Ubuntu: Hosts Snort (IDS/IPS), Splunk Forwarder, and vsftpd (FTP server).



Windows: Runs Splunk Enterprise for log indexing, alerts, and dashboards.



Tools:





Snort: IDS/IPS for detection and blocking.



Splunk: SIEM for monitoring and visualization.



Splunk Forwarder: Automates log transfer (port 9997).



Hydra: FTP brute force tool.



DIIG (likely dig): DNS amplification tool.



Python: HTTP server for manual log transfer.



Skills Demonstrated: Snort configuration, Splunk integration, rule writing, attack simulation, alert creation, dashboard design, and incident triage.

Project Phases







Phase



Description



Key Features



Details





Basic IDS



Manual Snort IDS for ICMP ping and port scan detection.



Custom rules, Python HTTP server, manual Splunk upload, basic alerts.



Snort Basic with Splunk Visualization





Automated IDS



Automated log forwarding, FTP brute force detection.



Splunk Forwarder, Hydra attack, Splunk dashboard for ICMP/port scan/FTP alerts.



Automated IDS





IPS Mode



Inline Snort IPS to block DNS amplification attacks.



Drop rules, DIIG attack, Splunk alerts, triage report.



Automated IPS with Triage

Lab Architecture





Network: Kali attacks Ubuntu (<TARGET_IP>, e.g., 192.168.67.128); logs sent to Splunk on Windows (<SPLUNK_IP>).



Data Flow:





Phase 1: Snort logs (/var/log/snort/alert.fast) served via Python server, manually uploaded to Splunk.



Phases 2–3: Logs forwarded via Splunk Forwarder (port 9997) to Splunk for real-time monitoring.



Attacks:





ICMP ping: ping <TARGET_IP>.



Port scan: nmap <TARGET_IP>.



FTP brute force: hydra -l <FTP_USER> -P /usr/share/wordlists/rockyou.txt ftp://<TARGET_IP>.



DNS amplification: diig @<TARGET_IP> google.com.

Setup Instructions





VM Setup:





Kali Linux: Install nmap, Hydra, DIIG (or dig).



Ubuntu: Install Snort (sudo apt-get install snort), vsftpd, Splunk Forwarder.



Windows: Install Splunk Enterprise.



Snort Configuration:





Edit /etc/snort/snort.conf and local.rules per phase.



Example rule (Phase 1):

alert icmp any any -> <TARGET_IP> any (msg:"ICMP Ping Detected"; sid:1000001;)



Splunk:





Phase 1: Manually upload logs.



Phases 2–3: Configure Forwarder (inputs.conf) and Splunk receiver (port 9997).



Attacks: Simulate from Kali as described in phase READMEs.

Files and Organization





Configs: snort.conf, local.rules, inputs.conf (Splunk Forwarder), firewall.txt (UFW commands).



Scripts: Commands for Python server, Hydra, DIIG.



Screenshots: Visuals for setups, attacks, logs, alerts, dashboards.



Triage: Report in Phase 3 analyzing DNS amplification block.



Monitoring: Create Splunk alerts and dashboards.

Future Improvements





Map alerts to MITRE ATT&CK framework.



Add Wireshark for packet analysis.



Automate triage with Python.



Simulate more attacks (e.g., SQL injection).

Contact

LinkedIn: Zeeshan Alam
This project reflects my hands-on experience in IDS/IPS, SIEM, and SOC workflows.
