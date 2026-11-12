# PENETRATION TESTING REPORT
### Footprinting & Reconnaissance Phase

**W2-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Field | Details |
|---|---|
| Program | Cybersecurity & Ethical Hacking |
| Organization | Networkwalks |
| Week | 02 |
| Date | 12 November 2026 |
| Operating System | Kali Linux |
| Target Domain | networkwalks.com |
| Permission | Authorized educational practical |

---

## 1. Liability Disclaimer

All activities documented in this repository were performed as part of an educational cybersecurity practical within the assigned authorized scope.

The techniques and tools demonstrated are intended strictly for educational and research purposes. Unauthorized testing against systems or networks without appropriate permission is prohibited.

The author is not responsible for any misuse of the information provided in this repository.

---

## 2. Introduction

This report documents the practical implementation of footprinting and reconnaissance techniques using multiple Kali Linux tools as part of Week 02 of the Cybersecurity & Ethical Hacking program at Networkwalks.

The objective was to understand how publicly available information about a domain can be collected and analyzed using different reconnaissance tools.

During this practical, I used six tools:

- WHOIS
- WhatWeb
- Nslookup
- cURL
- DNSRecon
- Wafw00f

Each tool was used to gather a different category of information, including domain registration details, DNS records, server information, web technologies, HTTP response headers, and Web Application Firewall identification.

The findings were documented with terminal screenshots as practical evidence.

---

## 3. Tools Used

| Tool | Purpose |
|---|---|
| WHOIS | Collect domain registration information. |
| WhatWeb | Identify website technologies and CMS information. |
| Nslookup | Resolve domain names into IP addresses. |
| cURL | Inspect HTTP response headers. |
| DNSRecon | Enumerate DNS records. |
| Wafw00f | Identify Web Application Firewall technologies. |

---

## 4. Activities Performed

### 4.1 WHOIS – Domain Information Gathering

**Command:**

```bash
whois networkwalks.com
```

**Objective:**

To collect publicly available domain registration information.

**Observations:**

- Registrar: GoDaddy.com, LLC
- Domain creation date: 06 November 2019
- Domain expiry date: 06 November 2027
- Name servers:
  - NS6135.HOSTGATOR.COM
  - NS6136.HOSTGATOR.COM
- DNSSEC: Unsigned

**Result:**

WHOIS provided information about domain registration, registrar details, domain status and associated name servers.

**Evidence:**

![WHOIS Output](screenshots/01-whois.png)

---

### 4.2 WhatWeb – Website Technology Fingerprinting

**Command:**

```bash
whatweb networkwalks.com
```

**Objective:**

To identify the technologies and software used by the target website.

**Observations:**

- Web Server: Apache
- CMS: WordPress 7.1.4
- WordPress Download Manager: 3.3.76
- Bootstrap: 7.1.4
- jQuery: 3.7.1
- Website IP: 192.232.216.135
- HTTP Status: 200 OK (HTTPS)

**Result:**

WhatWeb successfully identified several technologies and components associated with the website.

**Evidence:**

![WhatWeb Output](screenshots/02-whatweb.png)

---

### 4.3 Nslookup – DNS Lookup

**Command:**

```bash
nslookup networkwalks.com
```

**Objective:**

To resolve the domain name into its corresponding IP address.

**Observations:**

- DNS Server: 8.8.8.8
- Domain: networkwalks.com
- Resolved IP Address: 192.232.216.135

**Result:**

The command successfully resolved the domain name and returned its associated IP address.

**Evidence:**

![Nslookup Output](screenshots/03-nslookup.png)

---

### 4.4 cURL – HTTP Header Analysis

**Command:**

```bash
curl -I https://networkwalks.com
```

**Objective:**

To inspect the HTTP response headers returned by the website.

**Observations:**

- HTTP Response: 200 OK
- Web Server: Apache
- Content-Type: text/html
- Server technology information was exposed.
- WordPress REST API endpoint was identified: `/wp-json/`
- Additional security and caching headers were observed.

**Result:**

cURL successfully retrieved the HTTP response headers and provided information about the website's server and application configuration.

**Evidence:**

![cURL Output](screenshots/04-curl-headers.png)

---

### 4.5 DNSRecon – DNS Enumeration

**Command:**

```bash
dnsrecon -d networkwalks.com
```

**Objective:**

To enumerate DNS records associated with the target domain.

**Observations:**

DNSRecon identified the following record categories:

- SOA Records
- NS Records
- A Records
- MX Records
- TXT Records
- SRV Records

The tool also identified DNS server software version information.

**Additional Observation:**

The DNSSEC query returned no answer during enumeration.

**Result:**

DNSRecon successfully completed general DNS enumeration and reported 8 records found.

**Evidence:**

![DNSRecon Output](screenshots/05-dnsrecon.png)

---

### 4.6 Wafw00f – Web Application Firewall Detection

**Command:**

```bash
wafw00f networkwalks.com
```

**Objective:**

To identify whether a Web Application Firewall protects the target website.

**Observations:**

- WAF Detection: Successful
- Identified WAF: ModSecurity (SpiderLabs)
- Number of Requests: 2

**Result:**

Wafw00f identified ModSecurity (SpiderLabs) as the Web Application Firewall protecting the website.

**Evidence:**

![Wafw00f Output](screenshots/06-wafw00f.png)

---

## 5. Risk Analysis / Impact

Based on the information collected during reconnaissance, the following potential observations were identified.

| No. | Finding | Potential Impact | Risk Level |
|---|---|---|---|
| 1 | Website technology information exposed | Helps identify software and technologies for further security review. | Medium |
| 2 | Server IP address identifiable | Provides information about the hosting infrastructure. | Low |
| 3 | HTTP headers expose technical information | May assist technology fingerprinting. | Low |
| 4 | WAF technology identifiable | Reveals information about the website's security architecture. | Low |
| 5 | DNS infrastructure information exposed | Helps build a broader infrastructure profile. | Medium |

**Note:** These observations do not confirm the presence of security vulnerabilities. No exploitation or vulnerability validation was performed.

---

## 6. Recommendations

Based on the observations, the following security improvements are recommended:

1. Regularly review publicly exposed website technology information.
2. Keep CMS platforms, plugins and server software updated.
3. Review HTTP response headers to minimize unnecessary information disclosure.
4. Regularly review publicly accessible DNS records.
5. Properly configure and monitor the Web Application Firewall.
6. Conduct periodic security assessments within an authorized scope.
7. Monitor infrastructure and investigate unexpected changes.

---

## 7. Conclusion

During Week 02 of the Cybersecurity & Ethical Hacking program at Networkwalks, I performed practical exercises involving domain footprinting and reconnaissance using multiple Kali Linux tools.

I learned how WHOIS provides domain registration information, WhatWeb identifies website technologies, Nslookup resolves domain names, cURL examines HTTP headers, DNSRecon enumerates DNS records, and Wafw00f detects Web Application Firewalls.

These exercises helped me understand the importance of reconnaissance in cybersecurity and how publicly available information can provide valuable insights into a target's digital infrastructure.

I also gained practical experience using Kali Linux and interpreting the output generated by different cybersecurity tools.

---

## 8. Evidence Collected

All practical screenshots are available in the `screenshots/` directory.

The screenshots demonstrate the actual commands executed and their corresponding outputs.

---

## 9. Repository Structure

```text
WEEK-02-PENETRATION-TESTING/
│
├── README.md
├── screenshots/
│   ├── 01-whois.png
│   ├── 02-whatweb.png
│   ├── 03-nslookup.png
│   ├── 04-curl-headers.png
│   ├── 05-dnsrecon.png
│   └── 06-wafw00f.png
│
└── report/
    └── Week-02-Penetration-Testing.pdf
```

---

**Author:** Gaurav Vijay Ambare

**Program:** Cybersecurity & Ethical Hacking

**Organization:** Networkwalks

**Week:** 02

*Educational and research purposes only.*
