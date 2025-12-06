## Network Security Assessment – Task 10 (Oasis Infobyte) ##

# This project contains a full network security assessment performed on the Metasploitable2 vulnerable machine using Nmap and Wireshark. #

✔ Tools Used

Nmap

Wireshark

Kali Linux

Metasploitable2 VM

✔ What This Task Includes

Host discovery

Full port scanning (65535 ports)

Service & version enumeration

OS fingerprinting

Vulnerability scanning with Nmap NSE scripts

Packet capture and analysis

Professional security assessment report

✔ Files Included
File Name	Description
network_security_assessment.md	Full professional report
nmap_port_scan.txt	Nmap full port scan results
nmap_version_scan.txt	Service & script scan
nmap_vuln_scan.txt	Nmap vulnerability scan
wireshark_capture.pcap	Complete packet capture
screenshots/	All screenshots used in the assessment
✔ How to Run Scans
Host Discovery:
nmap -sn 192.168.1.14

All Ports Scan:
nmap -p- -sS 192.168.1.14

Version Scan:
nmap -sV -sC 192.168.1.14

Vulnerability Scan:
nmap --script=vuln 192.168.1.14

✔ Wireshark Filters

http

ftp

telnet

✔ Author

Rajesh Nandi
Oasis Infobyte Cybersecurity Internship
