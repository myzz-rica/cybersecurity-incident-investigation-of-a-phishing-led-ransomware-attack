# Investigating a Phishing-Led Ransomware Attack on a University Learning Management System

**Track:** Incident Investigation
**Program:** Women Techsters Sprint, Cybersecurity Track
**Author:** Erica Gyamfuaa Fordjour

## Overview

This capstone investigates a fictional ransomware incident at **Rexmi State University (RSU)**, a hypothetical mid-sized university. A junior staff member clicked a phishing link disguised as an urgent IT notice. The attacker used that access to encrypt the Learning Management System (LMS) overnight. By morning, students and faculty had lost access to coursework, grades, and communication, near the end of the semester.

The project reconstructs how the attack happened, finds the root cause, and recommends specific fixes.

## Key Findings

The attack went from phishing click to full LMS encryption in under nine hours. It succeeded because five controls were missing or too weak:

1. **No email filtering or request verification** at the point of entry
2. **No SSL/TLS inspection**, so encrypted command-and-control traffic went unseen
3. **Unpatched domain controller** (CVSS 9.9, Critical), which gave the attacker domain admin access
4. **Detection tuned too late**, so the SIEM alert fired after admin access was gained
5. **Backups not isolated**, so shadow copies and backup catalogs were destroyed

## Attack Flow

1. Phishing email clicked (8:45 PM)
2. Credentials and MFA token captured (8:45 PM)
3. Persistence and command-and-control established (8:47 PM)
4. Domain admin access gained (9:30 PM)
5. Lateral movement to LMS servers (9:45 to 10:15 PM)
6. Backups and shadow copies deleted (11:00 PM)
7. LMS files encrypted (11:30 PM to 5:00 AM)
8. Ransom note discovered (8:00 AM)

![alt text](https://github.com/myzz-rica/cybersecurity-incident-investigation-of-a-phishing-led-ransomware-attack/blob/main/Images/RSU_Incident_Flow_Diagram.png)

## Recommendations

- Email security gateway with link sandboxing, plus out-of-band verification for urgent requests
- SSL/TLS inspection at the firewall or proxy
- Formal patch management, with domain controllers prioritized
- SIEM rules that flag privilege escalation in real time
- 3-2-1 backup strategy with an offline, isolated copy
- Regular signature updates for the firewall, IDS, and IPS
- Weekly (or more frequent) offline backups
- A documented and rehearsed incident response plan

## Frameworks and Methods Used

- **MITRE ATT&CK** for mapping each attack stage to techniques

![alt text](https://github.com/myzz-rica/cybersecurity-incident-investigation-of-a-phishing-led-ransomware-attack/blob/main/Images/Mitre%20Attack.png)

- **NIST Incident Response framework** for the response actions
- **CIA Triad** for impact analysis
- **CVSS v3.1** for scoring the domain controller vulnerability

![alt text](https://github.com/myzz-rica/cybersecurity-incident-investigation-of-a-phishing-led-ransomware-attack/blob/main/Images/cvss.png)

- **Log analysis** of a reconstructed Auth, Firewall, System, and WebServer log set

![alt text](https://github.com/myzz-rica/cybersecurity-incident-investigation-of-a-phishing-led-ransomware-attack/blob/main/Images/logs%20.png)

## Deliverables in This Repository

- Final capstone report
- Presentation slides
- Problem statement
- AI usage report
- Attack flow diagram

## Note

Rexmi State University is a fictional organization. Any resemblance to a real institution is coincidental.
