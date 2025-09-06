   ## Overview
   Configures **Snort** in IDS mode on Ubuntu to detect **ICMP ping** and **port scan** attacks from Kali. Logs (`/var/log/snort/alert.fast`) are served via a Python HTTP server and manually uploaded to Splunk for indexing and alerting.

   ## Setup
   1. **Install Snort**:
      - Ubuntu: `sudo apt-get install snort`
      - Verify: `snort -V`
   2. **Configure Snort**:
      - Edit `/etc/snort/snort.conf` to include `local.rules`.
      - Add to `local.rules`:
        ```bash
        alert icmp any any -> 192.168.67.128 any (msg:"ICMP Ping Detected"; sid:1000001;)
        alert tcp any any ->  192.168.67.128 any (msg:"Port Scan Detected"; flags:S; sid:1000002;)
        ```
   3. **Run Snort**:
      - `snort -c /etc/snort/snort.conf -A fast`
   4. **Server Logs**:
      - `python3 -m http.server 8000`
      - Download from `http://<TARGET_IP>:8000`
   5. **Splunk**:
      - Upload `alert.fast` to Splunk.
      - Create index (`snort_basic`).
      - Set alerts for `"ICMP Ping Detected"`, `"Port Scan Detected"`.
   6. **Attacks**:
      - Kali:
        ```bash
        ping 192.168.67.128
        hping3 192.168.67.128
        ```

   ## Files
   - 📜 **Configs**:
     - `configs/snort.conf`
     - `configs/local.rules`
   - 🛠️ **Scripts**:
     - `scripts/server.txt`: `python3 -m http.server 8000`
   - 📸 **Screenshots**:
     - `screenshots/1. local.rules.png`: Rules setup.
     - `screenshots/2. ping check.png`: Ping from Kali.
     - `screenshots/3. snort logging.png`: Snort logs.
     - `screenshots/4. scanning ports.png`: Nmap scan.
     - `screenshots/5. snort logging.png`: Duplicate logs.
     - `screenshots/6. python server.png`: Python server.
     - `screenshots/7. ICMP index.png`: Splunk index.
     - `screenshots/8. Ping Detected.png`: Ping alert.
     - `screenshots/9. port scan detected.png`: Port scan alert.

   ## Notes
   - 📊 Add dashboard for visualization.
