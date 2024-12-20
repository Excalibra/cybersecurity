# Target Specification Review

## Target Specification Review

### What is the Target?
The target refers to the host or hosts being scanned using Nmap. This could be in the form of:
- IPv4 address
- IPv6 address
- Fully Qualified Domain Name (FQDN)
- An entire network using ranges, lists, or CIDR notation

### Where Should I Place the Target in the Nmap Command?
Placement is flexible and a personal preference. Placing it towards the end of the command can simplify edits in case of errors using the "up" arrow to modify the target.

---

### Common Target Specifications

```bash
nmap <ip address>
# Example: nmap 192.168.1.1

nmap <ip address range>
# Example: nmap 192.168.1-50

nmap <network in CIDR notation>
# Example: nmap 192.168.1.0/24

nmap <fqdn>
# Example: nmap scanme.nmap.org

nmap <domain in CIDR notation>
# Example: nmap nmap.org/24
````

---

Additional Target Options:

````
nmap <ip1 ip2 ip3>
# Example: nmap 192.168.1.1 192.168.1.10 192.168.1.254

nmap -iL <targets.txt>
# Example: nmap -iL targetlist.txt (reads targets from a file)

nmap -iR <number of targets>
# Example: nmap -iR 20 (randomly selects targets outside your network)

nmap --exclude <ip>
# Example: nmap 192.168.1.0/24 --exclude 192.168.1.254

nmap --excludefile <exclude.txt>
# Example: nmap 192.168.1.0/24 --excludefile exclude.txt
````

Reference: Nmap Target Specification Documentation

---

## Target Specification Lab: 

**Lab Examples:**

````
nmap <ip address>
nmap <ip1> <ip2>
nmap -F <ip>-50
# -F: Fast scan of the most popular 100 ports, scanning IP addresses 1 to 50
````

**Ping Sweep:**

**A ping sweep scans a subnet in CIDR notation, sending:**

- ICMP Echo Request
- TCP SYN to port 43
- TCP ACK to port 80
- ICMP Timestamp Request

This method identifies active IP addresses rapidly.

**Example:**

`nmap -sn 192.168.1.0/24`

**Using a target list for a ping sweep:**

`nmap -sn -iL targetlist.txt`

**Example workflow:**

cd /usr/share/nmap
sudo mkdir targets
cd targets
sudo nano targetlist.txt

---

**Random Target Selection:**

````
nmap -iR 10
# Randomly selects 10 IP addresses outside your network perimeter
# Not recommended to perform from home or work
````

---

**Quiet Scan Example:**

````
nmap -sS -p 80 -T2 -iR 50
# -sS: SYN scan (default)
# -p: Specifies the port to scan (e.g., 80)
# -T2: Timing template (slower and stealthier)
# -iR: Random target selection, scanning 50 IP addresses
````

---

**Excluding Targets:**
````
nmap -sn 192.168.1.0-40 --exclude 192.168.1.1
nano excludelist.txt
nmap -sn 192.168.1.0/24 --excludefile excludelist.txt
````

---

## Scan Techniques

### What is a "Scan Technique"?

**Protocols and Flags:**

- Defines which protocol to use, such as TCP, UDP, or IP.
- Allows crafting of packets with specific options and flags to investigate the target's response.

**Reference Protocols:**

- IETF RFC 793: TCP protocol definition.
- IETF RFC 1180: Explanation of the TCP/IP protocol suite.

---

## Popular Scan Techniques

````
nmap -sS
# TCP SYN Scan (half-open scan), Default

nmap -sT
# TCP Connect Scan, used when raw packet privileges are unavailable

nmap -sU
# UDP Scan, can be combined with -sS for TCP and UDP scanning

nmap -sO
# IP Protocol Scan, identifies supported IP protocols
````

---

## Advanced Scan Techniques

````
nmap -sY
# SCTP INIT scan, reliable but rarely used outside telecom networks

nmap -sA
# TCP ACK scan, used for firewall rule mapping

nmap -sW
# TCP Window scan, examines TCP Window field in RST packets

nmap -sM
# TCP Maimon scan, used on older BSD systems
````

## Stealthier Scan Techniques

````
nmap -sN
# Null Scan, all TCP flags set to zero

nmap -sF
# FIN Scan, sends a TCP FIN packet to determine host responses

nmap -sX
# Xmas Scan, sets FIN, PSH, and URG flags for stealthy probing

nmap -b
# FTP Bounce Scan, exploits an FTP vulnerability for internal probing

4.5 Scan Techniques Lab
TCP SYN Scan (Default)

nmap -sS -p 1-100 192.168.1.10 -oN output.nmap
# -sS: SYN scan
# -p: Ports 1 to 100
# -oN: Output saved to output.nmap
````

## TCP Connect Scan

````
nmap -sT -F 192.168.1.1 -oX output.xml
# -F: Fast scan for common ports
````

## UDP Scan

````
nmap -sU 192.168.1.10
nmap -sU -F 192.168.1.254
nmap -sU -sS -F 192.168.1.10
# Combine UDP (-sU) and TCP (-sS) scans
````

## IP Protocol Scan

````
nmap -sO 192.168.1.254
# Identifies supported IP protocols
````









