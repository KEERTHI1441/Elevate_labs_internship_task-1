
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

## ✅ Outcome

* Discovered devices and open ports using Nmap
* Saved results in multiple formats for documentation
* Filtered and observed specific service traffic in Wireshark



---

