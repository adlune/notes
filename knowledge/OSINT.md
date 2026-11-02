---
tags:
  - note
---
# OSINT

OSINT (Open Source Intelligence) is the process of collecting and analyzing publicly available information about a target (a person, company, domain, etc.). It's mostly passive reconnaissance.

## How it works

1. **Planning:** define what you're looking for.
2. **Collection:** gather info from public sources.
3. **Analysis:** connect the pieces, check them against other sources and discard what's false or irrelevant.
4. **Reporting:** write down findings.

The value of OSINT comes from linking things together, like pulling on a string until you find the source.

### Common sources

- **Search engines:** use filters to find better, more concrete results.
- **Social media:** usernames, photos, connections, posting times.
- **Domains:** WHOIS records, DNS, subdomains from certificate transparency logs.
- **Archives:** old versions of websites on the Wayback Machine.
- **Internet-connected devices**
- **Leaks:** breached accounts, credentials or keys pushed to public GitHub repos.
- **Files and images:** metadata (EXIF) can leak sensitive data. Although most modern platforms strip this metadata from the file, some exceptions exist and a lot of users don't know about it.
- **Job postings:** often reveal the tech stack a company uses.

## Commands / usage

```
whois [domain]
dig [domain] any
theHarvester -d [domain] -b all
sherlock [username]
exiftool [image]
```

- `whois`: domain registration info
- `dig`: DNS records
- `theHarvester`: collects emails, subdomains and hosts from public sources
- `sherlock`: searches a username across hundreds of sites
- `exiftool`: reads file/image metadata

Google dorks:

```
site:[domain] filetype:pdf
site:[domain] -www
intitle:"index of"
inurl:admin site:[domain]
```

## Things to try

- Look up subdomains of a domain on crt.sh, they can reveal dev sites not linked.
- Reverse image search and geolocate photos using details in the picture.
- Practice geolocating on platforms like OpenGuessr
- Check old versions of a site on the Wayback Machine.
- Practice on OSINT CTFs.
- Use a separate account when browsing social media so you don't leave traces with your own.

## Things to keep in mind

- Only use public information.
- Some techniques can cross the passive line without being too obvious.
- Always verify info.

## Related

- [Enumeration](Enumeration.md)
- [Telnet](Telnet.md)
