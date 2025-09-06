Phase 2: Automated Snort IDS with Splunk Forwarder 🤖
   ## Overview
   Automates **Snort** log forwarding to **Splunk** via Forwarder (port 9997). Detects **FTP brute force** attacks using Hydra from Kali. Includes Splunk alerts and dashboards for ICMP, port scan, and FTP events.

   ## Setup
   1. **Splunk Forwarder**:
      - Ubuntu: Install Forwarder, configure to `192.168.67.130:9997`.

   2. **Splunk Receiver**:
      - Windows: Data Inputs > TCP > New (port 9997).
      - Firewall:
        ```powershell
        New-NetFirewallRule -DisplayName "Splunk 9997" -Direction Inbound -Protocol TCP -LocalPort 9997 -Action Allow
        ```
   3. **Snort Rules**:
      - Add to `local.rules`:
        ```bash
        alert tcp any any -> <TARGET_IP> 21 (msg:"FTP Brute Force Attempt"; content:"USER"; sid:1000003;)
        ```
      - Run: `snort -c /etc/snort/snort.conf -A fast`
   4. **FTP Setup**:
      - `sudo apt-get install vsftpd`
      - `sudo adduser <FTP_USER>`
      - `sudo ufw allow 21/tcp`
   5. **Attack**:
      - Kali:
        ```bash
        hydra -l ftpuser -P /usr/share/wordlists/rockyou.txt ftp://192.168.67.128 -t 4 -V
        ```
   6. **Splunk**:
      - Alerts for `"ICMP Ping Detected"`, `"Port Scan Detected"`, `"FTP Brute Force Attempt"`.
      - Dashboard for event visualization.

   ## Files
   - 📜 **Configs**:
     - `configs/inputs.conf`
     - `configs/local.rules`
     - `configs/firewall.txt`: `sudo ufw allow 21/tcp`
   - 🛠️ **Scripts**:
     - `scripts/hydra.txt`: Hydra command
   - 📸 **Screenshots**:
     - `1- splunk forwarder.png`: Forwarder setup.
     - `2- added monitor of snort logs.png`: `inputs.conf`.
     - `3- splunk receive data.png`: Receiver (port 9997).
     - `4- windows defender configuration.png`: Firewall rule.
     - `5- test indexed.png`: Test data.
     - `6- ubuntu firewall configured.png`: UFW.
     - `7- local.rules updated.png`: FTP rule.
     - `8- attacked from kali.png`: Hydra attack.
     - `9- ubuntu logged.png`: FTP logs.
     - `10- indexed.png`: Splunk index.
     - `11- edit alert.png`: Alert creation.
     - `12- alert triggered.png`: FTP alert.
     - `13- New Dashboard.png`: Dashboard creation.
     - `14- Dashboard Port scan.png`: Port scan visualization.
     - `15- Dashboard FTP.png`: FTP visualization.
     - `16- Dashboard ICMP.png`: ICMP visualization.

   ## Notes
   - Dashboard combines ICMP, port scan, and FTP alerts for real-time SOC monitoring.
   - Hydra attack uses rockyou.txt for password guessing.

   
