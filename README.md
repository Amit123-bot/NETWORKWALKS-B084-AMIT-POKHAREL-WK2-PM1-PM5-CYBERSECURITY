# Networkwalks Cybersecurity & Ethical Hacking Internship – Week 2

**Intern:** Amit Pokharel  
**Batch:** B084  
**Program:** Cybersecurity & Ethical Hacking Internship  
**Organization:** Networkwalks  
**Week:** 02  
**Modules:** W2-PM1 and W2-PM5

---

## 1. Introduction

This repository contains my Week 2 practical activities completed during the Cybersecurity & Ethical Hacking Internship at Networkwalks.

The activities focused on two main areas:

- **W2-PM1 – Footprinting and Reconnaissance:** Collecting publicly available information about the assigned domain using six Kali Linux tools.
- **W2-PM5 – Network Scanning with Zenmap:** Discovering active hosts on my own local Wi-Fi network and generating a network topology.

This repository includes command outputs, screenshots, network scanning evidence, and the final penetration testing report.

## 2. Objectives

- Understand the fundamentals of footprinting and reconnaissance.
- Learn how to collect domain registration and DNS information.
- Identify publicly visible web technologies.
- Inspect HTTP response headers.
- Understand Web Application Firewall detection.
- Perform local network host discovery using Zenmap.
- Interpret scan results and network topology.
- Document technical observations and potential security risks.

## 3. Tools and Technologies Used

| Tool | Purpose |
|---|---|
| Kali Linux | Linux environment for reconnaissance |
| WHOIS | Domain registration information |
| WhatWeb | Website technology fingerprinting |
| NSLookup | DNS resolution |
| cURL | HTTP response header inspection |
| Wafw00f | Web Application Firewall detection |
| DNSRecon | DNS information gathering |
| Zenmap | Network scanning and visualization |
| Nmap | Host discovery |
| Windows CMD | Local network configuration |

## 4. Practical Activities

### W2-PM1 – Footprinting and Reconnaissance

I used six Kali Linux tools to collect publicly observable information about the assigned domain.

**Activities performed:**

1. WHOIS – Collected domain registration information.
2. WhatWeb – Identified publicly detectable website technologies.
3. NSLookup – Checked domain name resolution.
4. cURL – Inspected HTTP response headers.
5. Wafw00f – Checked for a detectable Web Application Firewall.
6. DNSRecon – Collected DNS records and infrastructure information.

**Evidence location:**

`W2-PM1-Footprinting/`

- `Outputs/` – Contains six tool output files.
- `Screenshots/` – Contains screenshots documenting the practical activities.

### W2-PM5 – Network Scanning with Zenmap

I used Windows CMD to identify my local network configuration and selected the Ping Scan profile in Zenmap.

**Command used:**

```bash
nmap -sn [REDACTED – LOCAL SUBNET]
```

**Scan results:**

| Item | Result |
|---|---|
| Scan type | Ping Scan |
| IP addresses scanned | 256 |
| Live hosts discovered | 6 |
| Scan duration | 8.43 seconds |
| Network tool | Zenmap / Nmap |

After completing the scan, I reviewed the discovered hosts and generated a network topology PDF.

**Evidence location:**

`W2-PM5-Zenmap/`

- `Outputs/` – Contains the ping scan output and network topology PDF.
- `Screenshots/` – Contains Windows IP configuration, Zenmap scan, and topology screenshots.

## 5. Risk Analysis

The practical activities helped identify the following potential information-exposure and network-management concerns:

- Publicly identifiable website technologies.
- Visible DNS and domain infrastructure information.
- HTTP response header information.
- Detectable Web Application Firewall technology.
- Multiple active devices on a local network.

These observations do not confirm the existence of vulnerabilities. No exploitation or vulnerability validation was performed.

## 6. Recommendations

1. Regularly review publicly exposed website information.
2. Keep CMS platforms and plugins updated.
3. Review HTTP security headers and cookie settings.
4. Maintain accurate DNS records.
5. Properly configure and monitor Web Application Firewall rules.
6. Perform regular internal network discovery.
7. Investigate unknown devices on owned networks.
8. Maintain updated network documentation.
9. Perform security testing only with appropriate authorization.

## 7. Repository Structure

```text
NETWORKWALKS-AMIT-POKHAREL-WK2-PM1-PM5-CYBERSECURITY/
│
├── README.md
│
├── W2-PM-FINAL-REPORT/
│   └── Networkwalks_W2-PM-FINAL_Report_Formatted_Amit_Pokharel.docx
│
├── W2-PM1-Footprinting/
│   ├── Outputs/
│   │   ├── 01-WHOIS.txt
│   │   ├── 02-WhatWeb.txt
│   │   ├── 03-NSLookup.txt
│   │   ├── 04-cURL.txt
│   │   ├── 05-Wafw00f.txt
│   │   └── 06-DNSRecon.txt
│   │
│   └── Screenshots/
│       ├── 01-WHOIS.png
│       ├── 02-WHOIS.png
│       ├── 03-WhatWeb.png
│       ├── 04-NSLookup.png
│       ├── 05-cURL.png
│       ├── 06-Wafw00f.png
│       └── 07-DNSRecon.png
│
└── W2-PM5-Zenmap/
    ├── Outputs/
    │   ├── 02-Ping-Scan-Output.txt
    │   └── 03-Network-Topology.pdf
    │
    └── Screenshots/
        ├── 01-Windows-IPConfig.png
        ├── 02-Zenmap-Ping-Scan.png
        └── 03-Network-Topology.png
```

## 8. Learning Outcomes

Through these practical exercises, I gained experience in:

- Using different Kali Linux reconnaissance tools.
- Understanding domain registration and DNS records.
- Identifying website technologies through fingerprinting.
- Reading HTTP response headers.
- Understanding WAF detection.
- Performing network discovery using Nmap and Zenmap.
- Reviewing live hosts and MAC vendor information.
- Creating and documenting network topology.
- Understanding the importance of authorization and responsible security testing.

## 9. Disclaimer

This repository is intended for educational and research purposes as part of my cybersecurity internship.

The network scanning activity was limited to my own local Wi-Fi network. The footprinting activity involved collecting publicly observable information about the assigned target.

No exploitation, brute-force attempts, authentication attempts, or unauthorized changes were performed.

Technical findings and evidence are subject to the approved testing and disclosure scope. Sensitive network identifiers and personal information have been redacted from the public materials.

## 10. Conclusion

Week 2 helped me develop practical knowledge of footprinting, reconnaissance, and network scanning. By working with six Kali Linux tools and Zenmap, I learned how to collect information, identify active hosts, interpret technical results, and document security observations.

This repository serves as a record of my practical learning and progress during the Networkwalks Cybersecurity & Ethical Hacking Internship.

---

**Author:** Amit Pokharel  
**Role:** Cybersecurity Intern  
**Batch:** B084  
**Program:** Networkwalks Cybersecurity & Ethical Hacking Internship

**LinkedIn:** https://www.linkedin.com/in/amit-pokharel-008210321/
