
---

# 🛡️ Task 1: Local Network Port Scanning & Service Analysis

## 🧪 Steps Performed

### ✅ 1. Identified Local IP Range
Used the following command to check my local IP address and subnet:
```bash
ip a
````

From the output, I determined that my network range is:

```
192.168.1.125/24
```

---

### ✅ 2. Ran TCP SYN Scan Using Nmap

Performed a stealth SYN scan to discover live devices and their open ports:

```bash
sudo nmap -sS 192.168.1.125/24
```

🔹 `-sS`: Performs a stealthy SYN scan (half-open scan)
🔹 `192.168.1.125/24`: Scans all IPs in the subnet (from `.1` to `.254`)

---

### ✅ 3. Saved Scan Results in Different Formats

#### 📄 Save in Text Format

```bash
sudo nmap -sS 192.168.1.125/24 -oN scan_results.txt
```

🔹 `-oN`: Saves output in **Normal (human-readable)** text format
🔹 `scan_results.txt`: Output file to store the results

---

#### 📄 Save in XML Format

```bash
sudo nmap -sS 192.168.1.125/24 -oX scan_results.xml
```

🔹 `-oX`: Saves output in **XML format** (machine-readable)

---

#### 🌐 Convert XML to HTML for Visual Report

```bash
xsltproc scan_results.xml -o scan_results.html
```

🔹 `xsltproc`: Tool to convert XML to HTML using XSLT
🔹 Creates a visual HTML version of your scan report for easier viewing in a browser

---

### ✅ 4. Analyzed Port 3306 in Wireshark

Captured packets and used this display filter in Wireshark:

```wireshark
ip.addr == 192.168.1.121 && tcp.port == 3306
```

🔹 Filters traffic **to or from IP `192.168.1.121`**
🔹 Only shows packets where **TCP port is 3306** (MySQL service)

---
### ✅ 5. Common Services on Open Ports

Based on the Nmap scan results, the following common services were found on various IPs in the local network:

| IP Address    | Port  | Service     | Description                                     |
| ------------- | ----- | ----------- | ----------------------------------------------- |
| 192.168.1.1   | 22    | SSH         | Secure remote login                             |
|               | 80    | HTTP        | Web interface (likely router admin panel)       |
|               | 1900  | UPNP        | Universal Plug and Play (auto device discovery) |
| 192.168.1.106 | 49152 | -           | High/random port, used by apps/devices          |
|               | 62078 | iPhone-sync | Apple device communication                      |
| 192.168.1.121 | 135   | MSRPC       | Windows Remote Procedure Call                   |
|               | 3306  | MySQL       | MySQL database service                          |

---

### ✅ 6. Potential Security Risks from Open Ports

Here are the potential security risks identified from the scanned open ports:

* **SSH (Port 22)** — If weak passwords are used, this service could be brute-forced.
* **HTTP (Port 80)** — Web interfaces without HTTPS can expose credentials and are vulnerable to MITM attacks.
* **UPNP (Port 1900)** — Known for being insecure; may allow unauthorized port forwarding.
* **iPhone-sync (Port 62078)** — May expose private data if synced with untrusted hosts.
* **MSRPC (Port 135)** — Targeted by many Windows-based exploits; should be behind a firewall.
* **MySQL (Port 3306)** — Should never be exposed publicly without firewall and authentication; vulnerable to database leaks.

> ✅ These services should be monitored, restricted, or disabled if not needed, especially in unsecured or public-facing networks.

## ✅ Outcome

* Discovered devices and open ports using Nmap
* Saved results in multiple formats for documentation
* Filtered and observed specific service traffic in Wireshark

---

## ✅ Outcome

* Discovered devices and open ports using Nmap
* Saved results in multiple formats for documentation
* Filtered and observed specific service traffic in Wireshark
* Identified exposed services and evaluated their risk level


---


