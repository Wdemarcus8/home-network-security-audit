# Home Network Security Audit – Findings  
**Date:** December 2025  
**Author:** Demarcus Williams  

---

## 1. Overview
This document summarizes the results of a home network audit performed using Nmap.  
The goal was to identify devices on the network, detect open services, and find potential security risks.

A total of **16 active devices** were discovered on the subnet `192.168.1.0/24`.

---

## 2. Key Findings Summary

### 2.1 Router (192.168.1.254)
**Open Ports:**
- 53 (DNS)
- 80 (HTTP – Lighttpd 1.4.69)
- 443 (HTTPS – Lighttpd 1.4.69)

**Risk Notes:**
- Web interface exposed on HTTP and HTTPS.
- No high‑risk or unusual ports detected.
- Running Linux kernel 4.x–5.x (normal for AT&T gateways).

**Severity:** Low  
**Notes:** Router appears standard and not misconfigured based on visible ports.

---

### 2.2 Android Device (192.168.1.245)
**Identified As:** Android device or Amazon‑based embedded OS  
**Open Port:**
- 8009 (common for ADB / debugging / media communication)

**Risk Notes:**
- Single open port, not a typical high‑risk port.
- Device name confirmed via AT&T app (“Android‑1”).

**Severity:** Low  
**Notes:** Normal for an Android phone. No suspicious ports detected.

---

### 2.3 IoT Devices
Several IoT devices were detected, including:
- Amazon devices (Fire TVs, Echo, etc.)
- Resideo/Honeywell device (likely thermostat or security accessory)
- Texas Instruments chipset devices (often smart home or automation hardware)
- Roku TV
- Ring Chime Pro

**Risk Notes:**
- IoT devices typically expose more ports but were not individually scanned in-depth.
- IoT devices often receive fewer security updates.

**Severity:** Medium  
**Notes:** IoT devices should be on a guest VLAN when possible.

---

### 2.4 Windows Laptop (192.168.1.251)
**Open Ports from Full Scan (`-p- -sV -sC`):**
- 135 (MSRPC)
- 137 (NetBIOS – filtered)
- 139 (NetBIOS session service)
- 445 (SMB)
- 902, 912 (VMware services)
- Several randomized MSRPC ports (49664–49672)
- 5040 (unknown)

**Risk Notes:**
- These are normal for Windows, but SMB exposure on a local network is common lateral‑movement target.
- VMware services visible indicate virtual networking enabled.
- No dangerous or unexpected remote‑administration services detected.

**Severity:** Medium  
**Notes:** Expected for Windows 10/11 — just keep firewall enabled.

---

## 3. General Observations
- Most devices responded as expected for a home network.
- No evidence of:
  - Rogue access points  
  - Unknown servers  
  - Open remote‑access services (SSH/RDP exposed externally)
  - Malware beaconing or abnormal ports

- The presence of **16 active devices** indicates a typical home IoT‑heavy environment.

---

## 4. Security Concerns Identified
### ❗ IoT Devices on Main Network
IoT devices often lack strong security and should ideally be segmented.

### ❗ SMB/NetBIOS Exposed Internally
Normal for Windows, but if another compromised device were on the network, SMB could be used for lateral movement.

### ❗ Router Using HTTP Interface
HTTP (port 80) is accessible, meaning:
- Login page is not encrypted  
- Credentials could be intercepted **inside** the network  

Not a major issue but worth noting.

---

## 5. Overall Severity Rating
**Low to Medium Risk**

Your network is behaving normally.  
The main risks come from IoT devices and typical Windows internal services.

Nothing appears malicious or abnormal.

---

## 6. Next Steps
For more secure home networking:

1. **Enable WPA3 or strong WPA2 password on Wi‑Fi**  
2. **Separate IoT devices onto a Guest or IoT VLAN** (if supported)  
3. **Disable unused router services (if available)**  
4. **Keep firmware updated**  
5. **Run this scan monthly and document any changes**  

---

End of report.
