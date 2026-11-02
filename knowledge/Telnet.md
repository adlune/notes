---
tags:
  - note
  - protocol
---
# Telnet

- **Port:** 23/TCP

Telnet is a network protocol for remote access which is text-based. It got replaced by SSH and is a legacy protocol. It's less secure (traffic is sent in plaintext) and more susceptible to attacks.

## How it works

Client opens a TCP connection to the server and everything typed is sent in plaintext (information immediately readable), including the username and password. There's no encryption and no way for the client to verify the server's identity, which is why anyone in the middle can read or tamper with the session.

It's still found on old Linux boxes, routers, switches and IoT devices, often with default credentials left on. The Mirai botnet (2016) spread mainly by brute-forcing telnet on IoT devices with a short list of default logins.

## Connecting

```
telnet [target_ip] 23
```

## Things to try

- Generic credentials with blank or common passwords.
- The banner/login prompt can leak the OS, hostname or device model.
- Run the nmap telnet scripts against the port (see [nmap](nmap.md)):

  ```
  nmap -p 23 --script "telnet-*" [target_ip]
  ```

- Brute-force with a default credentials list:

  ```
  hydra -l root -P [wordlist] telnet://[target_ip]
  ```

- Capture a login in Wireshark and use "Follow TCP Stream" to see the credentials in plaintext.
- The telnet client can also connect to other TCP services to talk to them manually.

## Mitigation

- Disable telnet and use SSH instead.
- Set strong passwords and disable direct root login.
- If it can't be removed restrict who can reach port 23 with a firewall.

## Related

- [Enumeration](Enumeration.md)
- [nmap](nmap.md)
- [Meow](../writeups/htb/Meow.md)
