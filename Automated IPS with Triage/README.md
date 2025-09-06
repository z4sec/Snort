Phase 3: Snort IPS Mode with Triage 🛑
   ## Overview
   Configures **Snort** in inline IPS mode to block **DNS amplification** attacks (port 53). Logs forwarded to **Splunk** via Forwarder. Includes alerts, dashboard, and triage report.

   ## Setup
   1. **Snort Inline Mode**:
      - Edit `/etc/snort/snort.conf`: `config policy_mode: inline`
      - Add to `local.rules`:
        ```bash
        drop udp any any -> any 53 (msg:"DNS Amplification Attack - BLOCKED"; content:"|00 01 00 00|"; sid:1000004;)
        ```
   2. **Run Snort**:
      - `snort -Q -c /etc/snort/snort.conf -A fast`
   3. **Attack**:
      - Kali: `dig @192.168.67.128 google.com`
   4. **Splunk**:
      - Forward logs to `192.168.67.130:9997`.
      - Alert for `"DNS Amplification Attack - BLOCKED"`.
      - Update dashboard.
   5. **Triage**:
      - Analyze in `triage.txt`.

   ## Files
   - 📜 **Configs**:
     - `configs/snort.conf`
     - `configs/local.rules`
   - 🛠️ **Scripts**:
     - `scripts/dig.txt`: `dig @192.168.67.128 google.com`
   - 📝 **Triage**:
     - `triage.txt`: DNS attack analysis
   - 📸 **Screenshots**:
     - `1- snort.conf edited.png`: Inline mode.
     - `2- local.rules configured.png`: DNS rule.
     - `3- attack from kali.png`: Dig attack.
     - `4- IPS detected.png`: Block confirmation.
     - `5- splunk index.png`: Splunk index.
     - `6- edit alert.png`: Alert creation.
     - `7- alert triggered.png`: DNS alert.
     - `8- Triage.png`: Triage process.
     - `9- triage report.txt`: Original triage report.

   ## Triage Summary
   - **Attack**: DNS amplification attack.
   - **Snort**: Dropped UDP packets.
   - **Splunk**: Logged drop events, visualized in dashboard.
   - **Analysis**: In `triage.txt`.
