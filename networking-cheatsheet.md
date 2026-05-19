# Network Cheatsheet

---

## The OSI Model

> Top to bottom. Most attacks happen at layers 3, 4, and 7.

| Layer | Name | What it does |
|-------|------|--------------|
| 7 | Application | What the user sees — HTTP, FTP, DNS, SSH |
| 6 | Presentation | Encoding and encryption — SSL/TLS |
| 5 | Session | Opens and maintains connections |
| 4 | Transport | Ports live here — TCP and UDP |
| 3 | Network | IP addresses and routing |
| 2 | Data Link | MAC addresses, switches |
| 1 | Physical | Cables and signals |

---

## Ports to Know Cold

| Port | Service | Why it matters |
|------|---------|----------------|
| 21 | FTP | File transfer — check for anonymous login |
| 22 | SSH | Secure shell — brute force target |
| 23 | Telnet | Unencrypted shell — dead but shows up in CTFs |
| 25 | SMTP | Email — check for open relay |
| 53 | DNS | Name resolution — try zone transfers |
| 80 | HTTP | Web traffic |
| 139/445 | SMB | Windows file sharing — huge attack surface |
| 443 | HTTPS | Encrypted web |
| 3306 | MySQL | Database — should never be public |
| 3389 | RDP | Windows Remote Desktop — brute force target |

---

## Key Concepts

| Term | Plain English |
|------|---------------|
| IP Address | Your device's address on a network |
| MAC Address | Hardware address burned into your network card |
| Subnet / CIDR | Defines the size of a network — `/24` = 256 addresses |
| Gateway | Your router — where traffic goes to leave the network |
| DNS | Phonebook that turns domain names into IP addresses |
| DHCP | Automatically hands out IP addresses to devices |
| NAT | Lets multiple devices share one public IP |
| Port | A numbered door on a device (0–65535) |
| TTL | How many hops a packet can survive before being dropped |

---

## Windows Commands

| Command | What it does |
|---------|-------------|
| `ipconfig` | Shows your IP, subnet, and gateway |
| `ipconfig /all` | Full detail including MAC and DNS servers |
| `ipconfig /flushdns` | Clears DNS cache |
| `ping <host>` | Tests if a host is reachable |
| `tracert <host>` | Shows every hop between you and the destination |
| `netstat -an` | All active connections and open ports |
| `netstat -anb` | Same but shows which process owns each connection |
| `nslookup <domain>` | DNS lookup |
| `arp -a` | Shows IP to MAC address mappings on your network |
| `net view` | Lists computers and shares on the local network |
| `whoami /all` | Your current user, groups, and privileges |

---

## Linux Commands

| Command | What it does |
|---------|-------------|
| `ip a` | Shows all interfaces and IP addresses |
| `ip r` | Shows the routing table and default gateway |
| `ifconfig` | Legacy version of `ip a` — still common in CTFs |
| `ping -c 4 <host>` | Pings 4 times then stops |
| `netstat -tulpn` | All listening ports with process names |
| `ss -tulpn` | Faster modern version of netstat |
| `traceroute <host>` | Same as Windows tracert |
| `dig <domain>` | DNS lookup with full detail |
| `dig <domain> +short` | DNS lookup, just the IP |
| `curl -I <url>` | Fetches HTTP headers only — shows server info |
| `wget <url>` | Downloads a file |
| `cat /etc/hosts` | Local DNS overrides — always check this |
| `cat /etc/resolv.conf` | Shows configured DNS servers |

---

## Nmap Basics

> Default scan: `nmap <target>`

```bash
nmap 10.10.10.10              # Basic scan — top 1000 ports
nmap -p- 10.10.10.10          # All 65535 ports (slow, use in CTFs)
nmap -sV 10.10.10.10          # Detect service versions
nmap -sC 10.10.10.10          # Run default scripts
nmap -A 10.10.10.10           # Everything — versions, scripts, OS detection
nmap -T4 10.10.10.10          # Faster scan (good for CTFs)
nmap 10.10.10.0/24            # Scan entire subnet
```

---

## Netcat Basics

> The Swiss army knife — connect to anything, listen for anything.

```bash
nc 10.10.10.10 80             # Connect to a host on a port
nc -lvnp 4444                 # Start a listener on port 4444 (catch reverse shells)
nc -zv 10.10.10.10 1-1000     # Quick port scan
```

---

## Quick Reference — Protocols

| Protocol | Type | Key fact |
|----------|------|----------|
| TCP | Connection-based | Guarantees delivery — 3-way handshake (SYN, SYN-ACK, ACK) |
| UDP | Connectionless | No guarantee — faster, used for DNS, streaming, VoIP |
| ICMP | Neither | Used by ping and traceroute — often blocked by firewalls |
| ARP | Layer 2 | Resolves IPs to MAC addresses on a local network |