# Home Network Security Audit

This project is a complete security audit of a home network, performed using industry-standard tools and methodologies. The goal was to identify active devices, analyze open ports and services, detect potential vulnerabilities, and recommend security improvements.

This project demonstrates practical skills needed for entry-level security roles, including:
- Network scanning and enumeration
- OS and service fingerprinting
- IoT device identification
- Basic vulnerability analysis
- Windows host exposure review
- Documentation and reporting

---

## 🛠️ Tools Used
- **Nmap** — device discovery, port scanning, OS detection
- **Windows (Command Prompt / PowerShell)**
- **Wi-Fi router admin portal (AT&T dsldevice)**

---

## 🧭 Scope of the Audit
The audit targeted the home LAN:
- Subnet: **192.168.1.0/24**
- Gateway: **192.168.1.254**
- Devices discovered: **16**

Devices included:
- Windows desktop/laptop
- Android phone
- Amazon IoT devices
- Ring / Chime Pro devices
- Smart home sensors (Resideo)
- Router

---

## 🔍 Key Findings Summary

### ✔ 1. **Router Access & Exposure**
- Web services detected on ports **80** and **443**
- Running **lighttpd 1.4.69**
- Port **53** open for DNS
- Router endpoints appear standard for AT&T gateways

**Risk:** Low → Medium  
**Action:** Ensure router credentials are strong and firmware is up to date.

---

### ✔ 2. **Windows Device Exposure**
Open ports included:
- **135 / 139 / 445** → Microsoft RPC, NetBIOS, SMB
- Several dynamic RPC ports (**49664–49672**)
- VMware ports (**902 / 912**) — related to virtualization tools

**Risk:** Medium  
**Why it matters:**  
SMB/NetBIOS exposure is common on internal networks, but these services can be abused by malware or lateral movement if any device becomes compromised.

**Action:**  
- Disable SMBv1  
- Restrict sharing services unless needed  
- Ensure Windows Firewall is active  
- Keep system patched  

---

### ✔ 3. **IoT Devices Detected**
Several devices from:
- Amazon Technologies  
- Texas Instruments  
- Sercomm  
- Resideo  
- Roku TV  

IoT devices often have:
- Default credentials  
- Poor patching  
- Long-term vulnerabilities  

**Risk:** Medium  
**Action:**  
- Place IoT devices on a **guest network** if possible  
- Disable unused features  
- Update firmware  

---

## 📂 Project Files
- **scans.txt** — Full Nmap results  
- **findings.md** — Detailed analysis of each device  
- **network-diagram.png** (optional)  

---

## 📘 What I Learned
- How to perform professional network enumeration  
- How to interpret and analyze open ports  
- OS/service fingerprinting  
- Identifying IoT device vendors by MAC address  
- Assessing basic network security posture  
- Documenting and presenting findings for a technical audience  

---

## 🚀 Next Steps
This project is the first part of a growing cybersecurity portfolio. Additional planned projects include:
- Wireshark network traffic analysis  
- Malicious packet investigation  
- Cloud fundamentals (AZ-900)  
- Basic SOC-style alert analysis  


