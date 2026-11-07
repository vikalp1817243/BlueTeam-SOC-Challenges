# 🛡️ K.A.V.A.C.H — Blue Team & SOC Challenges

[![Community](https://img.shields.io/badge/Community-K.A.V.A.C.H-blue?style=for-the-badge&logo=shield)](https://github.com/vikalp1817243/Kavach-Blue-Team)
[![Domain](https://img.shields.io/badge/Domain-SOC%20%7C%20Blue%20Team%20%7C%20DFIR-darkgreen?style=for-the-badge)](#)
[![Difficulty](https://img.shields.io/badge/Levels-Easy%20%7C%20Medium%20%7C%20Hard-orange?style=for-the-badge)](#)
[![Platform Ready](https://img.shields.io/badge/Web%20Portal-Ready%20for%20Integration-success?style=for-the-badge)](#)

> **K.A.V.A.C.H**: The official cybersecurity community and student defense cell.  
> This repository hosts practical, scenario-driven Security Operations Center (SOC) and Blue Team challenges created for members of the **K.A.V.A.C.H Community** and designed for direct integration into the official **K.A.V.A.C.H Website**.

---

## 📌 About The Project

The goal of this project is to provide college students and aspiring security analysts with hands-on exposure to defensive cybersecurity. Instead of theoretical quizzes, each challenge places the player in the shoes of a **Tier-1 / Tier-2 SOC Analyst** responding to simulated real-world intrusions.

### 🎯 Key Skills & Domains Covered
- 📜 **Log Analysis**: Windows Event Logs (`.evtx`), Sysmon, Linux `auth.log`, Nginx/Apache access logs.
- 🌐 **Network Forensics**: PCAP packet inspection using Wireshark, TShark, and Zeek.
- 🔍 **Endpoint & Artifact Forensics**: MFT, Prefetch, Registry, Shimcache, and memory dumps.
- 🏹 **Threat Hunting**: Detecting brute-force attempts, lateral movement, persistence, and C2 beacons.
- 🛡️ **MITRE ATT&CK Mapping**: Associating observed behaviors with adversary tactics and techniques.

---

## 📂 Repository Structure

Challenges are grouped by difficulty. Each folder follows a consistent standard so community members can solve them offline and web developers can programmatically ingest them into the website:

```text
Kavach-Blue-Team/
├── Easy-Challenges/
│   ├── Challenge-01-The-Failed-Login/
│   │   ├── README.md               # Challenge overview and navigation
│   │   ├── evidence/               # Sample logs (.evtx, .log, .pcap, etc.)
│   │   ├── questions.md            # Short-form participant question sheet
│   │   ├── soc-lab-challenge.md    # Reasoning-focused practical SOC lab
│   │   └── organizer/              # Private answer key and evaluation prompts
│   └── ...
├── Medium-Challenges/
│   └── ...
├── Hard-Challenges/
│   └── ...
└── README.md                       # Main repo guide & master catalog
```

---

## 💻 Web Developer Integration Guide

If you are a developer integrating these challenges into the **K.A.V.A.C.H Community Website**, each challenge folder is designed to include a machine-readable `challenge.json` (or standard markdown frontmatter) with the following structure:

```json
{
  "id": "BT-EASY-01",
  "title": "The Failed Login",
  "difficulty": "Easy",
  "category": "Log Analysis",
  "points": 100,
  "author": "Vikalp Pratap Yadav",
  "tags": ["Authentication", "Brute Force", "Windows Event Logs"],
  "scenario": "Brief description of the simulated incident...",
  "artifacts": [
    {
      "name": "Security.evtx",
      "download_url": "/assets/challenges/01/Security.evtx"
    }
  ],
  "questions": [
    {
      "id": 1,
      "question": "What is the IP address of the attacking machine?",
      "points": 25,
      "hint": "Filter for Event ID 4625"
    }
  ]
}
```

---

## 🏆 Challenge Catalog

| ID | Challenge Name | Difficulty | Domain / Focus | Points | Status |
|:---:|:---|:---:|:---|:---:|:---:|
| `01` | [The Failed Login](Easy-Challenges/Challenge-01-The-Failed-Login) | 🟢 `Easy` | Linux SSH Authentication Analysis | 100 pts | 🚧 In Development |
| `02` | *Web Intrusion Alert* | 🟢 `Easy` | Web Server Log Forensics & Web Shells | 100 pts | ⏳ Planned |
| `03` | *Beacon in the Dark* | 🟡 `Medium` | Network Traffic Analysis & C2 Hunting | 250 pts | ⏳ Planned |
| `04` | *Ghost in the Process* | 🟡 `Medium` | Sysmon Logs & Process Injection | 250 pts | ⏳ Planned |
| `05` | *Operation Kavach Breached* | 🔴 `Hard` | Multi-Stage Incident Response & Kill Chain | 500 pts | ⏳ Planned |

---

## 🧰 Recommended Toolset for Students

To solve these challenges, students are encouraged to use free and open-source defensive tools:

- **Log Parsers:** [Chainsaw](https://github.com/WithSecureLabs/chainsaw), [Hayabusa](https://github.com/Yamato-Security/hayabusa), [EvtxECmd](https://ericzimmerman.github.io/#!index), Event Viewer
- **Network Analysis:** [Wireshark](https://www.wireshark.org/), [TShark](https://tshark.dev/), [Brim / Zui](https://zui.brimdata.io/)
- **SIEM / Search:** Splunk Free, ELK Stack, [Wazuh](https://wazuh.com/)
- **Triage & De-obfuscation:** [CyberChef](https://gchq.github.io/CyberChef/), `grep`, `jq`, Python

---

## 🚀 Getting Started (For Members)

1. **Clone the Repo:**
   ```bash
   git clone https://github.com/vikalp1817243/Kavach-Blue-Team.git
   cd Kavach-Blue-Team
   ```
2. **Select a Challenge:** Pick any folder under `Easy-Challenges/`, `Medium-Challenges/`, or `Hard-Challenges/`.
3. **Download Evidence:** Obtain the logs or artifacts provided in the challenge's `evidence/` folder.
4. **Analyze & Submit:** Open the challenge folder's `README.md`, choose the appropriate participant brief, and submit your answers on the K.A.V.A.C.H community portal.

---

## ⚠️ Safe Lab Guidelines

- All logs and PCAP samples are sanitized or generated in safe virtual lab environments.
- **Always run analysis inside an isolated VM or sandbox environment** as a best security practice.

---

## 👥 Community & Contributions

Created by: Vikalp Pratap Yadav https://github.com/vikalp1817243  from  K.A.V.A.C.H Community - CYBER DOMAIN Core Team Member.

- **Community Portal:** *(To be added)*
- **Contributing:** Have an idea for an incident scenario? Feel free to submit a PR or reach out to the club leads!

---

## 📄 License

Unless otherwise noted, this repository's original challenge materials are licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](LICENSE).
You may share and adapt them with appropriate attribution, provided that adaptations are distributed under the same or a compatible CC BY-SA license.
