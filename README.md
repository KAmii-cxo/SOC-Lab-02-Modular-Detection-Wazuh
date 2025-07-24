# 🛡️ SOC Lab 02 – Modular Detection Lab (Wazuh Custom Rules)

This lab simulates post-exploitation behavior and maps each attack technique to MITRE ATT&CK TTPs. Custom Wazuh rules are created to detect privilege escalation, persistence, obfuscation, credential access, and reverse shell activity.

The goal: build a modular detection set that can be reused in any SOC lab, blue team drill, or purple team exercise.

---

## 🧪 Lab Environment

- **Wazuh Manager + Agent** (Manual CLI install)
- **Ubuntu Server CLI-only** (VirtualBox/Proxmox)
- **Dual NIC**: Bridged (Internet) + Host-only (Lab)
- **Logs Enabled**:
  - Auditd (system calls)
  - FIM (File Integrity Monitoring)
  - Command log decoding

---

## 🔥 Attack Simulation Modules (10 Drafts)

| Draft | Technique | MITRE TTP |
|-------|-----------|-----------|
| 1 | Privilege Escalation via Cron + Fake Binary (`cp`) | `T1053.003`, `T1036.005` |
| 2 | Persistence via `.bashrc` or `.bash_profile` | `T1547.001` |
| 3 | Credential Access via `/etc/shadow`, `/etc/passwd` | `T1003.008` |
| 4 | Fileless Execution via Bash one-liners | `T1059.004` |
| 5 | Lateral Movement via SSH (password reuse/keys) | `T1021.004` |
| 6 | Reverse Shell via bash/ncat/python | `T1071.001` |
| 7 | Cron Persistence (`@reboot`, `/etc/cron.d/`) | `T1053.003` |
| 8 | Correlation: Shadow Access + Reverse Shell | `T1027`, Custom Correlation |
| 9 | Obfuscated Persistence via base64 `.bashrc` | `T1027`, `T1547.001` |
| 10 | Cleanup & Trace Removal (`bash_history`, logs) | `T1070.004` |

---

## 🧩 Detection Rules & Setup

- All rules saved in: `/var/ossec/etc/rules/local_rules.xml`
- Rule ID range: `100100 – 100900`
- Grouping: `custom`, `persistence`, `execution`, `correlation`, `cleanup`, etc.

### How to Use:
1. Paste rules into `local_rules.xml`
2. Restart Wazuh Manager  
   `sudo systemctl restart wazuh-manager`
3. Simulate behavior on the monitored endpoint
4. Monitor logs:  
   `tail -f /var/ossec/logs/alerts/alerts.json`

---

## 🔍 Detection & Validation

- Real attacker behavior is executed manually
- Wazuh Agent detects and triggers custom rules
- Alerts correlated in dashboard (OpenSearch)
- All detections mapped to MITRE ATT&CK
- Supports purple team simulation & validation

---

## 📂 Files & Documentation

- 📘 [Full Lab Document (Google Doc)](https://docs.google.com/document/d/1Y2FkC6LkYLrOxYcMcoFkI49VS0gGtKHXH5pqHC79rRs/edit?usp=drive_link)
- 📄 [Wazuh Custom Rules – Persistence Detection (MITRE-based)](https://docs.google.com/document/d/175FfMyy9H1UmCG0DwcVPYH6uuwDrMY47_bgvIxVnBQI/edit?usp=drive_link)

> Includes setup checklist, custom rules, full simulation steps, screenshots, alert logs, and cleanup steps.

---

> _This modular lab is part of a real-world SOC simulation effort using open-source detection tools._

---

## 🖋️ Report by Kamii (Hashim Zulkifli)

Built, simulated, detected, and documented by Kamii – Blue Team / Purple Team learner focused on threat detection, rule tuning, and post-exploitation defense.

🔗 [GitHub](https://github.com/Kamii-cxo)  
🔗 [LinkedIn](https://linkedin.com/in/hashim-zulkifli)  
📂 [Cybersecurity Portfolio Vault](https://drive.google.com/drive/folders/17wl9kDajrwSZJJOf9uIVusCxLa_jdcz7?usp=drive_link)

> _"Real rules. Real alerts. Modular detection done right."_
