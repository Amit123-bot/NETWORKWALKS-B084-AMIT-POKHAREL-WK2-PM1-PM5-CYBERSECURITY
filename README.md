# PENETRATION TESTING REPORT

### Footprinting & Network Scanning Phases

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| **Field** | **Detail** |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | **Amit Pokharel** |
| **Program/Batch** | B084 – Networkwalks |
| **Date** | 13 November 2026 |
| **Modules completed** | W2-PM1 (Multiple Kali Tools)  <br>W2-PM5 (Zenmap Scanning) |
| **Client/Target** | 1. Networkwalks (`networkwalks.com`)  <br>2. My own local Wi-Fi network |
| **Permission secured from client?** | Yes |
| **Phases covered** | **Phase 1:** Reconnaissance & Footprinting  <br>**Phase 2:** Scanning & Network Discovery  <br>**Phases 3–5:** Not covered in this report |

# 1. Liability Disclaimer

I performed these activities for the assigned educational cybersecurity internship exercises. The network scanning activity was limited to my own local Wi-Fi network, and the footprinting activity focused on collecting publicly observable information about the assigned domain.

No exploitation, brute-force attempts, authentication attempts, or unauthorized changes to the target website were performed.

All materials are intended for educational and research purposes only. Security testing should only be performed on systems and devices where appropriate authorization has been obtained. The student is responsible for complying with applicable laws, internship rules, and the approved testing scope.

# 2. Introduction

This report covers footprinting the `networkwalks.com` domain using multiple Kali Linux tools (W2-PM1) and scanning my own local network using Zenmap (W2-PM5).

The first activity focused on collecting publicly available information about a domain, including registration details, website technologies, HTTP response headers, Web Application Firewall information, and DNS records.

The second activity focused on identifying active hosts on my own Wi-Fi network, reviewing their network information, and generating a network topology.

These activities form the Week 2 part of my Cybersecurity & Ethical Hacking Internship at Networkwalks.

All footprinting commands were executed in Kali Linux. The local network discovery activity was performed using Zenmap on a Windows PC. This report documents the commands used, observations, potential security implications, and collected evidence.

# 3. Tools Used

The following table lists the tools used during the two practical modules.

| **Tool** | **Purpose** |
|---|---|
| Kali Linux & Windows | Operating systems used for reconnaissance and network discovery |
| WHOIS | Find publicly available domain registration information, registrar, registration dates, and name servers |
| WhatWeb | Fingerprint visible website technologies, server information, CMS, plugins, and IP address |
| NSLookup | Resolve a domain name to an IP address using DNS |
| cURL -I | Read HTTP response headers from the website |
| Wafw00f | Identify whether a Web Application Firewall is detected |
| DNSRecon | Collect DNS information such as SOA, NS, MX, A, TXT, and SRV records |
| Zenmap (Nmap GUI) | Perform a ping scan to identify live hosts and MAC/vendor information |
| Nmap | Perform network host discovery |
| Windows CMD | Identify local network configuration using the ipconfig command |

# 4. Activities Performed

## 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the `networkwalks.com` domain using six Kali Linux tools: **WHOIS, WhatWeb, NSLookup, cURL, Wafw00f, and DNSRecon**.

Each tool collected a different type of publicly observable information about the target.

### 4.1.1 WHOIS

**Command used:**

```bash
whois networkwalks.com
```

The WHOIS result identified GoDaddy.com, LLC as the domain registrar. The domain creation date was 6 November 2019, and the registry expiry date was 6 November 2027.

The registered name servers were:

- NS6135.HOSTGATOR.COM
- NS6136.HOSTGATOR.COM

The registrant details were privacy-protected through Registration Private / Domains By Proxy, LLC. The result also reported that DNSSEC was unsigned.

**Why it matters:** WHOIS information helps build an initial profile of domain registration, registrar information, domain status, and name-server infrastructure.

### 4.1.2 WhatWeb

**Command used:**

```bash
whatweb networkwalks.com
```

WhatWeb identified Apache as the web server and detected the website's IP address.

The detected technologies included:

- WordPress 7.1.4
- WordPress Download Manager 3.3.76
- jQuery 3.7.1
- Bootstrap 7.1.4
- Google Tag Manager

The page title was identified as Networkwalks Academy.

The HTTP URL returned **301 Moved Permanently**, while the HTTPS URL returned **200 OK**.

The output also displayed the contact email address `info@networkwalks.com`.

**Why it matters:** Technology fingerprinting helps administrators understand which software and services are publicly identifiable. A detected software version alone does not prove that the software is vulnerable.

### 4.1.3 NSLookup

**Command used:**

```bash
nslookup networkwalks.com
```

The DNS query used Google DNS server `8.8.8.8` and returned a non-authoritative answer.

The domain resolved to the following IPv4 address:

`192.232.216.135`

**Why it matters:** DNS resolution identifies the IP address associated with a domain and helps map the publicly visible network location of a web service.

### 4.1.4 cURL -I

**Command used:**

```bash
curl -I https://networkwalks.com
```

The HTTPS endpoint returned:

`HTTP/1.1 200 OK`

The response identified Apache as the server and `text/html; charset=UTF-8` as the content type.

The response headers also included:

- X-nginx-cache: WordPress
- X-Endurance-Cache-Level: 0
- Referrer-Policy
- A Secure and HttpOnly `__wpdm_client` cookie
- A WordPress REST API link at `/wp-json/`

**Why it matters:** HTTP response headers provide information about server behavior, caching, cookies, content type, and application endpoints. This information can assist technology fingerprinting.

### 4.1.5 Wafw00f

**Command used:**

```bash
wafw00f networkwalks.com
```

Wafw00f version 2.4.2 identified the website as being behind a **ModSecurity (SpiderLabs) Web Application Firewall**.

The tool reported that it made two requests during the detection process.

**Why it matters:** Identifying a WAF provides information about a defensive layer in front of a web application. Detection does not measure the WAF's effectiveness or prove that it blocks every malicious request.

### 4.1.6 DNSRecon

**Command used:**

```bash
dnsrecon -d networkwalks.com
```

DNSRecon collected several DNS-related records and infrastructure details.

The findings included:

- SOA information for `ns6135.hostgator.com`.
- Two name servers: `ns6135.hostgator.com` and `ns6136.hostgator.com`.
- DNS software version information reported as `9.16.23-RH`.
- An MX record for `mail.networkwalks.com`.
- An A record for `networkwalks.com`.
- TXT records, including a Google site-verification value and SPF information.
- Eight `_autodiscover._tcp` SRV records pointing to cPanel email discovery endpoints on port 443.
- No answer returned for the DNSSEC query, consistent with the unsigned DNSSEC status observed in WHOIS.

**Why it matters:** DNS records help map domain infrastructure, mail services, and service-discovery configuration. The reported DNS software version and DNSSEC status are observations, not proof of vulnerabilities.

## 4.2 Network Scanning with Zenmap

For the second activity, I used Zenmap to perform host discovery on my own local Wi-Fi network.

First, I used the Windows `ipconfig` command to identify the active Wi-Fi adapter, IPv4 address, subnet mask, and default gateway.

**Command used:**

```cmd
ipconfig
```

Based on the local network configuration, I selected the corresponding `/24` subnet as the Zenmap scan target.

In Zenmap, I selected the **Ping Scan** profile.

**Original Nmap command:**

```bash
nmap -sn 192.168.1.0/24
```

The scan produced the following results:

- 256 IP addresses scanned.
- Six hosts discovered as up.
- Total scan duration of 8.43 seconds.
- Five discovered hosts displayed MAC addresses.
- One host was displayed as up without a MAC address in the scan output.

### Discovered hosts

The following table summarizes the actual Zenmap scan results. Personal network identifiers have been redacted in this public version.

| **Host** | **IP Address** | **MAC Address** | **Vendor Information** |
|---|---|---|---|
| Host 1 | [REDACTED] | [REDACTED] | Hangzhou Ezviz Software |
| Host 2 | [REDACTED] | [REDACTED] | Hangzhou Ezviz Software |
| Host 3 | [REDACTED] | [REDACTED] | Unknown |
| Host 4 | [REDACTED] | [REDACTED] | Nokia Solutions and Networks India Private Limited |
| My Windows PC | [REDACTED – MY PC IP] | Not shown in scan output | Not identified |
| Default Gateway | [REDACTED – GATEWAY IP] | [REDACTED – ROUTER MAC] | Nokia Shanghai Bell |

The scan identified six live hosts on the local network. The Windows PC's IP address and the default gateway matched the network configuration identified through Windows CMD.

MAC vendor labels are based on address-prefix identification and do not establish the exact device model or owner.

After completing the scan, I opened the **Topology** section in Zenmap, enabled the legend, and saved the network topology as a PDF as required by the practical task.

# 5. Risk Analysis / Impact

Based on the information collected during the footprinting and network scanning activities, I identified the following potential risks.

| **#** | **Risk / Finding** | **Evidence / Observation** | **Potential Impact** | **Risk Level** |
|---|---|---|---|---|
| 1 | Web technology information exposed | WhatWeb detected Apache, WordPress 7.1.4, and WordPress Download Manager 3.3.76 | Public technology and version information may help an attacker identify components for further research | **Medium** |
| 2 | Server IP address identifiable | NSLookup and WhatWeb identified the website's public IP address | Provides information about the public network location of the website | **Low** |
| 3 | HTTP technical information exposed | cURL returned HTTP response headers and a `/wp-json/` REST API link | May assist technology fingerprinting and further public enumeration | **Low** |
| 4 | WAF technology identifiable | Wafw00f identified ModSecurity (SpiderLabs) | Reveals information about a defensive component in the web application architecture | **Low** |
| 5 | DNS infrastructure information exposed | DNSRecon identified SOA, NS, MX, A, TXT, and SRV records and DNS software version information | DNS information can help build a broader infrastructure profile | **Medium** |
| 6 | Multiple live hosts visible on local network | Zenmap identified six live hosts on the local network | Unexpected devices, if any, may create asset-management or access-control concerns | **Medium** |

**Risk level key:** Critical | High | Medium | Low

The ratings above are qualitative observations for this educational report.

The practical exercises primarily involved information gathering and host discovery. No exploitation or vulnerability validation was performed.

Therefore, the presence of a software version, IP address, DNS record, or live host does not by itself mean that the system is vulnerable. Further authorized security testing would be required to confirm any actual vulnerability.

# 6. Recommendations

Based on the observations from these activities, I recommend the following security improvements:

1. **Review publicly exposed technology information**  
   Organizations should regularly review what information about their web technologies, CMS, and plugins is publicly visible.

2. **Keep software updated**  
   CMS platforms, plugins, and other web technologies should be maintained through the administrator's normal patching and security-review process.

3. **Review HTTP headers**  
   Response headers and cookie attributes should be reviewed to confirm that they match the organization's security requirements.

4. **Review DNS records regularly**  
   Public DNS records, mail records, and service-discovery records should be checked periodically to ensure they are accurate and required.

5. **Properly configure and monitor the WAF**  
   Keep ModSecurity maintained, review its rules and logs, and validate its effectiveness through authorized testing.

6. **Perform regular internal network discovery**  
   Organizations should periodically scan their own networks to maintain an accurate inventory of active devices.

7. **Investigate unknown devices**  
   Any unexpected device discovered during network scanning should be investigated and verified against the approved device inventory.

8. **Maintain network documentation**  
   Network topology and device information should be documented and updated regularly.

9. **Perform security testing with authorization**  
   Reconnaissance and scanning should only be performed against systems and networks where appropriate authorization has been provided.

# 7. Conclusion

During Week 2 of my Cybersecurity & Ethical Hacking Internship, I completed practical activities covering footprinting, reconnaissance, and network scanning.

In the footprinting activity, I used six Kali Linux tools to collect publicly available information about `networkwalks.com`. I learned how WHOIS provides domain registration information, WhatWeb identifies web technologies, NSLookup resolves domain names, cURL inspects HTTP headers, Wafw00f detects a WAF, and DNSRecon collects DNS information.

In the network scanning activity, I used Windows `ipconfig` to identify my local network configuration and Zenmap to discover active hosts on my own Wi-Fi subnet. The Ping Scan identified six live hosts on the `/24` network. I also reviewed MAC address and vendor information and generated a network topology PDF.

These exercises showed me that information gathering is an important part of cybersecurity. Security professionals can learn about a domain and network by carefully analyzing publicly available information and network responses.

I also learned that technical findings must be documented clearly and interpreted carefully. A good cybersecurity report should explain what was performed, what was discovered, what the observation means, what potential risk it may create, and what can be done to reduce that risk.

Finally, I learned that reconnaissance and scanning must always remain within an authorized scope.

# 8. Evidences Collected

The following screenshots, output files, and documents were collected during the practical activities.

### W2-PM1 – Footprinting & Reconnaissance

**WHOIS output**

`W2-PM1-Footprinting/Screenshots/01-whois.png`

**WHOIS additional evidence**

`W2-PM1-Footprinting/Screenshots/02-whois.png`

**WhatWeb output**

`W2-PM1-Footprinting/Screenshots/03-whatweb.png`

**NSLookup output**

`W2-PM1-Footprinting/Screenshots/04-NSLookup.png`

**cURL output**

`W2-PM1-Footprinting/Screenshots/05-cURL.png`

**Wafw00f output**

`W2-PM1-Footprinting/Screenshots/06-Wafw00f.png`

**DNSRecon output**

`W2-PM1-Footprinting/Screenshots/07-DNSRecon.png`

**Command output files**

- `W2-PM1-Footprinting/Outputs/01-WHOIS.txt`
- `W2-PM1-Footprinting/Outputs/02-WhatWeb.txt`
- `W2-PM1-Footprinting/Outputs/03-NSLookup.txt`
- `W2-PM1-Footprinting/Outputs/04-cURL.txt`
- `W2-PM1-Footprinting/Outputs/05-Wafw00f.txt`
- `W2-PM1-Footprinting/Outputs/06-DNSRecon.txt`

### W2-PM5 – Network Scanning with Zenmap

**Windows IP configuration**

`W2-PM5-Zenmap/Screenshots/01-Windows-IPConfig.png`

**Zenmap Ping Scan**

`W2-PM5-Zenmap/Screenshots/02-Zenmap-Ping-Scan.png`

**Network topology screenshot**

`W2-PM5-Zenmap/Screenshots/03-Network-Topology.png`

**Scan output**

`W2-PM5-Zenmap/Outputs/02-Ping-Scan-Output.txt`

**Network topology PDF**

`W2-PM5-Zenmap/Outputs/03-Network-Topology.pdf`

---

**End of Report**

**Author:** Amit Pokharel  
**Cybersecurity Intern | Batch B084**  
**Organization:** Networkwalks  
**LinkedIn:** https://www.linkedin.com/feed/update/urn:li:activity:7527145073239724032/
