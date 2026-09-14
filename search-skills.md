# Search Skills
- **Link:** https://tryhackme.com/room/searchskills
- **Date:** 2026-09-14

## What I learned
- Shodan is a search engine for internet-connected devices — not just IoT. It continuously scans the internet and indexes what's running where: networking equipment, industrial control systems, traffic cameras, web servers
- Banner grabbing: servers advertise software versions in their HTTP headers (e.g. `Server: Apache/2.4.58 (Ubuntu)`), and Shodan indexes that — so you can search the whole internet by software version
- Searching a version like `apache 2.4.1` returns every server advertising it, broken down by country, organisation, and port — extremely useful during a pentest or vulnerability assessment when paired with a known CVE affecting that version
- Shodan has query filters to narrow results, e.g. `country:IE` restricts to a country code
- Practiced on TryScanMe: searched `apache` (2,047,582 results), picked a host and read its profile — IP, location, ISP/ASN, hostnames, open ports, response headers, and SSL certificate details

## Key searches
- `apache` — example host found: 185.243.115.47 (Amsterdam, DigitalOcean, AS14061)
- Host profile showed: hostname `webserver-tryhackme`, domain `tryhackme.thm`, open ports 22 / 80 / 443 / 8080
- Response headers: `HTTP/1.1 200 OK`, `Server: Apache/2.4.58 (Ubuntu)`, `X-Powered-By: PHP/8.2.10`
- SSL cert: TLS 1.3, cipher TLS_AES_256_GCM_SHA384, issuer Let's Encrypt
- `country:IE` — filter syntax example for narrowing by country

## Notes
- Version disclosure in banners is information leakage — as a defender, check what your own organisation exposes on Shodan (attack surface management)
- This is recon/OSINT work: the same skill attackers use to find targets is what SOC analysts use to understand exposure

## TryDetectMe (VirusTotal simulation)
- Searched the suspicious file `invoice_payment.exe` on TryDetectMe, a VirusTotal simulation
- Result: 52/72 security vendors flagged it as malicious, community score -15
- The vendor labels told the story: Microsoft `Trojan:Win32/Agent`, Kaspersky `Trojan-Spy.Win32.Agent`, Norton `Infosteal`, Malwarebytes `Spyware.Agent`, ESET `Win32/Spy` — consistent trojan + spyware/infostealer verdicts across vendors = high-confidence malicious
- Lesson: read the labels, not just the count. Consistent malware family names across many vendors means strong consensus; a handful of generic flags with a neutral community score could be a false positive
- SOC angle: `invoice_payment.exe` is a textbook phishing lure filename. This is Tier 1 triage in miniature — file lookup → detection consensus → verdict labels → escalate or block

## Vulnerability database (NVD simulation)
- Looked up `CVE-2026-1337` in TryHackMe's vulnerability database: a critical SQL injection in Apache WebPortal, exploitable without authentication via the `userId` parameter, leading to unauthorized access to credentials and session tokens
- CVSS score: 10/10 (HIGH/CRITICAL), vector `AV:N/AC:L/Au:N/C:C/I:C/A:C`, weakness CWE-89 (SQL Injection)
- How to read the vector: Attack Vector NETWORK (exploitable remotely) + Authentication NONE (no login needed) + complete loss of Confidentiality, Integrity, Availability = worst case, hence a perfect 10
- Lesson: the CVE ID names the vulnerability, CVSS scores its severity, CWE names the weakness type, and the vector string explains *why* it scored that way — four pieces that together tell the full story
- This closes the loop with the Shodan task: Shodan finds exposed software versions → the vuln database tells you whether that version has a known CVE and how bad it is. That pairing is the core of vulnerability assessment
