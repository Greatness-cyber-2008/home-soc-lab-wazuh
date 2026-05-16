# 🛡️ Home SOC Lab — Wazuh SIEM Deployment

> "I built this lab because I got tired of just reading about cybersecurity. I wanted to actually do it."

**Greatness Ajibola Alawode** · Cybersecurity Student, Bowen University Iwo · TS Academy Fellow

---

## 📖 About This Project

This is a fully working Security Operations Centre (SOC) home lab that I set up from scratch.

I deployed Wazuh SIEM, configured a monitored agent, and integrated intrusion detection tools — all on my personal machine. Every problem I hit, I solved myself.

---

## 🏗️ What I Built
Docker Compose

Container deployment

Kali Linux

SIEM server host

Ubuntu

Monitored agent endpoint

Suricata

Network intrusion detection

VirusTotal

Threat intelligence

VirtualBox

Virtualisation

**💾 Resource Allocation**

VM

RAM

CPU

**Note**

Kali Linux (SIEM Server)

4096 MB

2 cores
Always launch first

Ubuntu (Agent)

1024 MB

1 core

Launch after Kali

## ▶️ How to Start the Lab
Open VirtualBox, start Kali first, then Ubuntu. Then run this on Kali:

Bash
cd ~/wazuh-docker/single-node
sudo docker compose up -d

Once the containers are up, open the Wazuh dashboard at https://192.168.56.102 and log in.

All three containers must show as running before the dashboard is usable:
wazuh.manager

wazuh.indexer

wazuh.dashboard

## 🔧 Problems I Hit and How I Fixed Them
This is the part most people skip. I'm including it because solving these taught me more than the setup itself.

**Problem 1 —** Docker Downloads Kept Cutting Out
My hotspot was unstable and kept interrupting image pulls mid-download.

Fix: Used docker compose pull and let it resume each time rather than restarting from scratch.

**Problem 2 — Dashboard Wouldn't Load After Startup**
The dashboard container was starting before the indexer was fully ready.

Fix: Monitored the indexer logs with sudo docker logs wazuh.indexer to confirm it was fully up before opening the dashboard.

**Problem 3 — Wazuh API Showing as Offline**
The manager service wasn't fully initialised even though the container showed as running.

Fix: Restarted the manager service directly:
Bash
**sudo docker exec -it wazuh.manager /var/ossec/bin/wazuh-control restart**
Then refreshed the dashboard and the API came back online.

**Problem 4 — VMs Couldn't See Each Other**
The default NAT adapter doesn't allow VM to VM communication.

Fix: Switched both VMs to a Host-Only Adapter and assigned Kali a static IP of 192.168.56.102 on eth1. Agent connected immediately after.

## ✅ What This Lab Can Do

With this setup running I can:

**Monitor a live endpoint for security events in real time**

**Analyse logs from the Ubuntu agent through the Wazuh dashboard**

**Detect network intrusion attempts via Suricata**

**Correlate suspicious files and hashes against VirusTotal**

**Practice incident response workflows in a safe environment**

It is not a lab I set up once and left. I actually use it.

## 🧠 Skills Demonstrated

Wazuh SIEM Suricata IDS Docker

Kali Linux Ubuntu Linux CLI 

VirtualBox Network Configuration

Log Analysis 

Threat Detection 

Incident Response VirusTotal

## 📚 Other Things I've Been Learning

**Through TS Academy I have covered:**

SOC fundamentals and SOC technology stack

Networking Basics I and II

Wireshark practical walkthroughs

Cisco Packet Tracer simulations

VulnHub lab setup on Ubuntu

Incident Response I and II

Hidden process detection

## Certifications:
ISC2 Cybersecurity CC — course completion certificate

Cisco Academy certifications

ISC2 CC proctored exam booked for September 2026

## Education:
BSc Cybersecurity, Bowen University 
Iwo — Year 1

TS ACADEMY- CYBER SECURITY Track

3MTT Programme — Cloud Computing track
Two tracks at once, Both intentional.

## 👤 About Me
I am a first-year student who does not want to wait until graduation to be useful. Everything in this repo is real work I did on my own machine with my own hands. I am open to remote opportunities — junior SOC analyst roles, security internships, or apprenticeships.

**Greatness Ajibola Alawode**

Cybersecurity Student · SOC Analyst in Training · Nigeria
## 📬 Connect With Me
🌐 Hello.cv: [Add your Hello.cv link here]

💼 LinkedIn: [https://www.linkedin.com/in/greatness-alawode-1071b62bb?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app]

🐦 X (Twitter): [https://x.com/Bad_Unitedfan]
