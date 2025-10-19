# Cyber-Security
# Mini Report — Building Your First Attack Surface Map

**Student Name:** Jumanah Alshehri  
**Date & Time:** 19/10/2025 4:00 PM

## Project summary
This repository contains the results and evidence from a small attack surface mapping exercise against a controlled lab target. The objective was to discover live hosts, enumerate open services and versions, and validate whether known vulnerabilities are present. All testing was performed in a contained lab environment.

## Lab environment
- Kali (attacker) IP: `192.168.56.4`  
- Target (Metasploitable2) IP: `192.168.56.3`  
- Virtualization: VirtualBox

## Scope and authorization
Testing was performed only on the isolated lab hosts listed above. This work is for educational purposes and was conducted with explicit authorization for the lab environment. 

## Top findings
1. **Live hosts found**  
   - `192.168.56.4` - Metasploitable2 (Host is up)  
   - `192.168.56.3` - Kali (lab attacker)

2. **Open ports and service versions (top findings)**  
   - `21/tcp` - ftp - **vsftpd 2.3.4**  
   - `22/tcp` - ssh - OpenSSH 4.7p1  
   - `80/tcp` - http - Apache 2.2.8

3. **Confirmed vulnerability**  
   - **Name:** vsftpd 2.3.4 backdoor  
   - **CVE:** CVE-2011-2523  
   - **Evidence:** NSE output file `nse_ftp_vsftpd.txt` and screenshot `05_nse_vsftpd.png` (NSE reported VULNERABLE). See `evidence/` folder for attached files.
   - 
   - ## Raw scan output
Raw Nmap output is available as `metasploitable_nmap.nmap` in this repository.
