NETWORK SECURITY ASSESSMENT REPORT

Target Machine: Metasploitable2 (192.168.1.14)
Prepared For: Oasis Infobyte Cybersecurity Internship
Prepared By: Rajesh Nandi
Tools Used: Nmap, Wireshark
Date: 7 th December 2025

1. Executive Summary
A network security assessment was conducted on a Metasploitable2 machine hosted at IP 192.168.1.14. The purpose of this assessment was to identify open ports, running services, potential vulnerabilities, and analyze network traffic to understand risks associated with unencrypted protocols.
During the assessment, numerous outdated and vulnerable services were discovered, including FTP, Telnet, SSH, HTTP, SMB, and databases such as MySQL and PostgreSQL. Wireshark analysis revealed clear-text transmission of usernames and passwords via FTP and Telnet, confirming high-risk vulnerabilities.
This report outlines the methodology, findings, risk levels, and recommendations required to improve the security posture of the target system.

2. Scope of Assessment
The assessment covered:
    • Host discovery
    • Network scanning (all ports)
    • Service and version detection
    • OS fingerprinting
    • Vulnerability scanning with Nmap NSE
    • Network traffic capture and analysis
    • Reporting of identified risks
Out of scope:
    • Actual exploitation (covered in Task 9)
    • Privilege escalation
    • Persistence
    • Social engineering

3. Methodology
3.1 Host Discovery
nmap -sn 192.168.1.14
3.2 Full Port Scan
nmap -p- -sS 192.168.1.14
3.3 Version & Script Scan
nmap -sV -sC 192.168.1.14
3.4 OS Detection
nmap -O 192.168.1.14
3.5 Vulnerability Scan (NSE Scripts)
nmap --script=vuln 192.168.1.14
3.6 Wireshark Traffic Capture
Filters used:
    • http
    • ftp
    • telnet

4. Nmap Results
4.1 Open Ports Identified
Common ports detected on Metasploitable2:
Port	Service	Version	Risk
21	FTP	vsftpd 2.3.4	High
22	SSH	OpenSSH 4.7	Medium
23	Telnet	Linux telnetd	High
25	SMTP	Postfix smtpd	Medium
53	DNS	ISC Bind	Medium
80	HTTP	Apache 2.2.8	Medium
111	RPCbind	RPC	Medium
139/445	SMB	Samba smbd 3.x	High
3306	MySQL	MySQL 5.0.51a	High
5432	PostgreSQL	8.3.x	Medium
5900	VNC	VNC Protocol	Medium

5. Vulnerability Findings (Nmap NSE)
5.1 High-Risk Vulnerabilities
    • Anonymous FTP login allowed
    • Telnet service exposes credentials in plaintext
    • SMB vulnerabilities (CVE-2007-2447)
    • Outdated Apache HTTP Server
    • Weak SSH key exchange & deprecated algorithms
    • MySQL service allows weak authentication
5.2 Medium-Risk Vulnerabilities
    • Outdated PostgreSQL version
    • DNS information disclosure
    • Open RPC services (potential for brute-force or misconfigurations)
5.3 Low-Risk Vulnerabilities
    • Banner disclosure
    • Directory listing
    • Version information exposure

6. Wireshark Findings
6.1 HTTP Traffic
Captured unencrypted HTTP requests:
    • GET /, POST requests visible
    • Server header reveals Apache 2.2.8
    • Potential for MITM sniffing attacks
6.2 FTP Credentials (Cleartext)
Captured using filter ftp:
USER anonymous
PASS testpass
➡ Username and password fully visible in network packets.
6.3 Telnet Credentials (Cleartext)
Captured using filter telnet:
msfadmin
msfadmin
➡ Telnet transmits all data unencrypted.

7. Risk Assessment
Risk Level	Issues Found
High	FTP anonymous login, Telnet, SMB CVEs, MySQL exposure
Medium	SSH deprecated algorithms, RPC services, Apache version
Low	Banner disclosure, HTTP directory listing

8. Recommendations
8.1 Remove or Disable High-Risk Services
    • Disable Telnet → Replace with SSH
    • Disable or restrict FTP → Replace with SFTP
    • Restrict external access to MySQL, PostgreSQL, SMB
8.2 Update All Services
    • Update Apache, MySQL, SSH, Samba, and PostgreSQL
    • Apply latest security patches
8.3 Enforce Network Segmentation
    • Block unused ports in firewall
    • Isolate vulnerable services using VLANs
8.4 Enable Encryption Everywhere
    • Use HTTPS instead of HTTP
    • Use FTPS/SFTP instead of FTP
    • Remove all plaintext protocols
8.5 Monitoring & Logging
    • Enable audit logs
    • Monitor SSH, FTP, HTTP logs
    • Use IDS tools like Snort or Suricata

9. Conclusion
The assessment revealed that the target system (Metasploitable2) contains numerous outdated and vulnerable services that expose the network to high-risk attacks including credential theft, privilege escalation, and remote code execution. Immediate action is required to disable unnecessary services and apply security hardening.
This report provides actionable recommendations to mitigate the identified risks and improve the overall security posture.
