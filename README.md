Home SOC Lab — Wazuh SIEM Deployment
I built this lab because I got tired of just reading about cybersecurity. I wanted to actually do it.
This is a fully working Security Operations Centre home lab that I set up from scratch — deploying Wazuh SIEM, configuring a monitored agent, and integrating intrusion detection tools. Every problem I hit, I solved myself. This README documents the whole thing honestly, including the parts that broke.
Greatness Ajibola Alawode · Cybersecurity Student, Bowen University Iwo · TS Academy Fellow
What I Built
A virtualised SOC environment running inside VirtualBox on my personal machine. The setup has two VMs talking to each other over a Host-Only network — one running the Wazuh SIEM stack on Kali Linux, the other running Ubuntu as a monitored endpoint sending logs back to the server.
Code
VirtualBox (Host Machine)

   Kali Linux VM                    Ubuntu VM
   (Wazuh SIEM Server)    <----    (Monitored Agent)
   Wazuh v4.10.3                    Wazuh Agent installed
   Docker single-node               192.168.56.x
   192.168.56.102 (eth1)

        Both connected via Host-Only Adapter
Tools and Technologies
Wazuh SIEM v4.10.3 running via Docker Compose on Kali Linux. Ubuntu as the agent endpoint. Suricata handling network intrusion detection. VirusTotal integrated for threat intelligence. VirtualBox for virtualisation across the whole setup.
Resource Allocation
I'm working within real hardware constraints so I had to be deliberate about this:
The Kali Linux VM (SIEM server) runs on 4096MB RAM and 2 CPU cores. The Ubuntu agent VM runs on 1024MB RAM and 1 CPU core. Kali always has to start first before the Ubuntu VM, otherwise the agent can't connect to the server.
How to Start the Lab
Bash
cd ~/wazuh-docker/single-node
sudo docker compose up -d
Once the containers are up, open the Wazuh dashboard at https://192.168.56.102 and log in. All three containers need to show as running before the dashboard is usable — wazuh.manager, wazuh.indexer, and wazuh.dashboard.
Problems I Hit and How I Fixed Them
This is the part most people skip in their writeups. I'm including it because these were real obstacles and solving them taught me more than the setup itself.
Docker downloads kept cutting out. My hotspot connection was unstable and kept interrupting the image pulls mid-download. I learned to use docker compose pull and let it resume rather than restarting everything from scratch each time.
The dashboard wouldn't load properly after startup. The wazuh.dashboard container was initialising before the indexer was fully ready. I started monitoring container logs with sudo docker logs wazuh.indexer to know exactly when it was safe to open the dashboard instead of just guessing.
Wazuh API kept showing as Offline. This one took me a while. The manager service wasn't fully initialised even though the container showed as running. The fix was restarting the manager service directly and then refreshing the dashboard:
Bash
sudo docker exec -it wazuh.manager /var/ossec/bin/wazuh-control restart
The VMs couldn't see each other. Default NAT adapter doesn't allow VM-to-VM communication. I switched both VMs to a Host-Only Adapter and assigned Kali a static IP of 192.168.56.102 on eth1. After that the agent connected without issues.
What This Lab Can Do
With this setup running I can monitor a live endpoint for security events, analyse logs coming in from the Ubuntu agent through the Wazuh dashboard, detect network intrusion attempts through Suricata, correlate suspicious files and hashes against VirusTotal, and practice incident response workflows in a safe environment.
It's not a lab I set up once and left. I actually use it.
What I Know From Building This
Working with Wazuh SIEM end to end. Docker container management and troubleshooting. Linux networking — static IPs, Host-Only Adapters, interface configuration. Log analysis and alert triage. Suricata IDS setup and integration. VirusTotal threat intelligence correlation. VirtualBox VM management under hardware constraints.
Other Things I've Been Learning
Alongside this lab I've been going through the TS Academy cybersecurity programme covering SOC fundamentals, networking basics, Wireshark, Cisco Packet Tracer, VulnHub, and incident response. I also hold the ISC2 Cybersecurity CC course completion certificate and Cisco Academy certifications. I'm sitting the official ISC2 CC proctored exam in September 2026.
Separately I'm in Year 1 of a BSc in Cybersecurity at Bowen University, Iwo, and I'm also part of the 3MTT programme on the cloud computing track.
Two tracks at once. Both intentional.
About Me
I'm a first-year student who doesn't want to wait until graduation to be useful. Everything in this repo is real work I did on my own machine with my own hands. If you're a recruiter or someone building a security team and you want someone who's genuinely hungry to learn and contribute, let's talk.
I'm open to remote opportunities junior SOC analyst roles, security internships, or apprenticeships.
Greatness Ajibola Alawode
Cybersecurity Student · SOC Analyst in Training
Nigeria · Available for Remote Work
Hello.cv: [Add your Hello.cv link here]
LinkedIn: [https://www.linkedin.com/in/greatness-alawode-1071b62bb?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app
X: [https://x.com/Bad_Unitedfan]
