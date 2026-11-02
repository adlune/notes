---
tags:
  - note
---
# Enumeration

Enumeration is the process of probing the target for access, open ports, versions, etc. Basically doing active and direct reconnaissance, analyzing the responses from the target.

## Passive vs active reconnaissance

- **Passive:** gathering info without touching the target directly (public records, DNS lookups, search engines, leaked data). It serves as the primary technique of [OSINT](OSINT.md).
- **Active:** interacting with the target directly (port scans, banner grabbing, logging in). It can show up in the target's logs.

## Usual first steps

1. Scan for open ports and service versions with [nmap](nmap.md).
2. Research each service/version found for known vulnerabilities or misconfigurations.

## Things to try

- Run a quick scan first, then a full port scan (`-p-`). You can miss some services with the standard 1000 port scan.
- Don't forget UDP (`-sU`). Services like SNMP (161) or DNS (53) only show up there.
- Grab banners manually with `nc [target_ip] [port]` or `telnet [target_ip] [port]`, sometimes the service tells you exactly what it is and which version.
- Look up versions with `searchsploit [service] [version]` or by searching "[service] [version] exploit/CVE".
- Check for default credentials (e.g. [Telnet](Telnet.md) with `root` and a blank password) and anonymous access (anonymous FTP, SMB null sessions).
- Take notes of everything found as you go, even things that look useless at first.

## Related

- [nmap](nmap.md)
- [OSINT](OSINT.md)
- [Telnet](Telnet.md)
- [Meow](../writeups/htb/Meow.md)
