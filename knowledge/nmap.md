---
tags:
  - note
  - tool
---
# nmap

nmap (Network Mapper) is a port scanner, used to find open ports and the services behind them.

## How it works

nmap sends packets to the target's ports and reads the responses to figure out each port's state:

- **open:** a service is listening and accepting connections.
- **closed:** nothing listening (reachable).
- **filtered:** no response.

By default it scans the 1000 most common TCP ports. When run with sudo it does a SYN scan (`-sS`, doesn't complete the full handshake which is quieter). Without root it does a TCP connect scan (`-sT`).

## Commands

commonly:

```
nmap -sC -sV [target_ip]
```

- `-sC`: run the default set of scripts
- `-sV`: detect service versions

### Other useful flags

- `-p-`: scan all 65535 ports (`-p 22,80` for specific ones)
- `-sU`: UDP scan (slow, needs sudo)
- `-O`: try to detect the OS (needs sudo)
- `-A`: aggressive, combines `-O`, `-sV`, `-sC` and traceroute
- `-Pn`: skip host discovery and treat the host as up, useful when the target blocks ping
- `-sn`: only host discovery (find live hosts)
- `-T4`: faster timing (goes from `-T0` to `-T5`, the higher the noisier)
- `--min-rate 1000`: send at least 1000 packets per second
- `-oA [name]`: save the output in all formats
- `-v` / `--reason`: more verbose output / show why a port got its state

### Things to try

A common workflow in labs is a fast full scan, then a detailed scan on discovered ports:

```
sudo nmap -p- --min-rate 1000 -T4 [target_ip]
sudo nmap -p [ports_found] -sC -sV -oA scan [target_ip]
```

nmap also has its own scripting engine (NSE), the scripts are in `/usr/share/nmap/scripts/`. To find and run scripts for a specific service:

```
ls /usr/share/nmap/scripts | grep telnet
nmap -p 23 --script telnet-ntlm-info [target_ip]
```

## Related

- [Enumeration](Enumeration.md)
- [Telnet](Telnet.md)
- [Meow](../writeups/htb/Meow.md)
