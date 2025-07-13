Suricata – Live Attack Detection Lab

This project documents my hands-on SOC analyst lab activity using Suricata to detect live network threats and validate alert visibility across common cyberattacks. The goal was to simulate offensive attacks from Kali Linux and confirm whether Suricata can identify, log, and classify the threats in real-time.

Target Systems

    DVWA (Victim) – 192.168.56.109

    Windows (Victim) – 192.168.56.111

    Kali (Attacker) – 192.168.56.102

Attacks Performed & Alerts Generated

1. SMB Brute-Force Attack

    Tool Used: Hydra v9.5

    Target: 192.168.56.111 (Windows)

    Protocol: SMB (Port 445)

    Command Executed:
    hydra -l admin -P /usr/share/wordlists/rockyou.txt smb://192.168.56.111

Suricata Alert from fast.log:

    Signature: ET SCAN Possible Nmap User-Agent Observed

    Alert Priority: 3

    Source IP: 192.168.56.102

    Destination IP: 192.168.56.111

    Classification: Web Application Attack

    Timestamp: 2025-06-29

2. ICMP Sweep & Ping Scan Attack

    Tool Used: Nmap

    Command Used:
    nmap -sn 192.168.56.0/24

Suricata Alert from fast.log:

    Signature: SURICATA ICMPv4 type 8 code 0

    Alert Priority: 3

    Source IP: 192.168.56.102

    Destination IP: 192.168.56.110

    Classification: Multi

    Timestamp: 2025-06-29

Findings

    Suricata successfully detected brute-force attempts against the Windows SMB service.

    ICMP scan and ping sweep attacks were flagged instantly with accurate logs.

    SOC Box internal traffic was logged and traced with clarity for escalation and review.

Security Recommendations

    Apply account lockout policies or rate-limiting on authentication services to prevent brute-force login attempts.

    Restrict ICMP traffic across internal zones unless explicitly required.

    Continuously monitor and tune IDS/IPS rules to reduce noise and focus on actionable events.

    Isolate high-value assets like the SOC Box behind internal firewalls or segmented VLANs.

Screenshots Included in the Repo

    Suricata-Live-Attack-Detection-FastLog.png

    Suricata-Detection-SMB.png

    Suricata-ICMP-Sweep-Detection-1.png

    Suricata-ICMP-Sweep-Detection-2.png
