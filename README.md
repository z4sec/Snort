Snort IDS/IPS Home Lab with Splunk Integration 🛡️
   ![GitHub repo size](https://img.shields.io/github/repo-size/z4sec/Snort) ![GitHub last commit](https://img.shields.io/github/last-commit/z4sec/Snort) ![License](https://img.shields.io/github/license/z4sec/Snort)

   ## Overview
   This **Security Operations Center (SOC)** home lab showcases **Snort** for intrusion detection/prevention and **Splunk** for log analysis, demonstrating skills in rule creation, log forwarding, attack simulation, alerting, dashboard design, and incident triage for a SOC analyst role.

   - **Virtual Machines**:
     - 🐉 **Kali Linux**: Simulates attacks (ICMP ping, port scans, FTP brute force, DNS amplification).
     - 🐧 **Ubuntu**: Runs Snort (IDS/IPS), Splunk Forwarder, vsftpd (FTP server).
     - 🖥️ **Windows**: Hosts Splunk Enterprise for indexing, alerts, dashboards.
   - **Tools**:
     - 🔍 Snort: IDS/IPS for detection/blocking.
     - 📊 Splunk: SIEM for monitoring/visualization.
     - 🚀 Splunk Forwarder: Log transfer (port 9997).
     - ⚔️ Hydra: FTP brute force.
     - 🔎 Dig: DNS amplification.
     - 🐍 Python: HTTP server (Phase 1).

   ## Project Phases
   | Phase | Description | Key Features | Details |
   |-------|-------------|--------------|---------|
   | 🔧 Basic IDS | Manual Snort IDS for ICMP/port scan detection. | Custom rules, Python server, manual Splunk upload. | [Snort Basic with Splunk Visualization](Snort%20Basic%20with%20Splunk%20Visualization/README.md) |
   | 🤖 Automated IDS | Automated log forwarding, FTP brute force detection. | Splunk Forwarder, Hydra attack, dashboards. | [Automated IDS](Automated%20IDS/README.md) |
   | 🛑 IPS Mode | Inline IPS for DNS amplification blocking. | Drop rules, dig attack, triage report. | [Automated IPS with Triage](Automated%20IPS%20with%20Triage/README.md) |

   ## Lab Architecture
   - **Network**: Kali attacks Ubuntu (`<TARGET_IP>`); logs sent to Splunk (`<SPLUNK_IP>`).
   - **Data Flow**:
     - Phase 1: Logs served via Python server, manually uploaded to Splunk.
     - Phases 2–3: Logs forwarded via Forwarder to Splunk.
   - **Attacks**:
     - 🔔 ICMP: `ping 192.168.67.128`
     - 🔑 FTP brute force: `hydra -l <FTP_USER> -P /usr/share/wordlists/rockyou.txt ftp://<TARGET_IP>`
     - 📡 DNS amplification: `dig 192.168.67.128 google.com`

   ## Setup Instructions
   1. **VMs**:
      - Kali: Install `nmap`, `hydra`, `dig`.
      - Ubuntu: Install Snort (`sudo apt-get install snort`), `vsftpd`, Splunk Forwarder.
      - Windows: Install Splunk Enterprise.
   2. **Snort**:
      - Configure `/etc/snort/snort.conf` and `local.rules` per phase.
      - Example (Phase 1):
        ```bash
        alert icmp any any -> 192.168.67.128 any (msg:"ICMP Ping Detected"; sid:1000001;)
        ```
   3. **Splunk**:
      - Phase 1: Manually upload logs.
      - Phases 2–3: Configure Forwarder (`inputs.conf`) and receiver (port 9997).
   4. **Attacks**: Run from Kali (see phase READMEs).
   5. **Monitoring**: Set Splunk alerts/dashboards.

   ## Files
   - 📜 **Configs**: `snort.conf`, `local.rules`, `inputs.conf`, `firewall.txt`.
   - 🛠️ **Scripts**: Python server, Hydra, dig commands.
   - 📸 **Screenshots**: Setup, attacks, logs, alerts, dashboards.
   - 📝 **Triage**: DNS attack analysis (Phase 3).

   ## Challenges
   - 📝 **Naming**: Fixed typos (e.g., “Detcted” to “Detected”) and organized files.

   ## Future Improvements
   - 🗺️ Map alerts to MITRE ATT&CK.
   - 🔍 Add Wireshark packet analysis.
   - 🤖 Automate triage with Python.
   - ⚔️ Simulate SQL injection attacks.

   ## Contact
   👤 LinkedIn: [Zeeshan Alam](https://www.linkedin.com/in/zeeshan-alam-073102246)

   ⭐ If you find this project useful, please star the repository!
