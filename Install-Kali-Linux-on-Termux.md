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
