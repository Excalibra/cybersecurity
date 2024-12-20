## Target Specification Review

### What is the Target?
The target refers to the host or hosts to be scanned using Nmap. It can take the form of:
- IPv4 address
- IPv6 address
- Fully Qualified Domain Name (FQDN)
- An entire network using ranges, lists, or CIDR notation

### Where Should I Place the Target in the Nmap Command?
Placement is flexible and a matter of personal preference. Placing it towards the end of the command can make it easier to edit in case of errors using the "up" arrow to modify the target.

---

### Common Target Specifications
````
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

### Additional Target Options
````
nmap <ip1 ip2 ip3>
# Example: nmap 192.168.1.1 192.168.1.10 192.168.1.254
# IP addresses can also be hostnames or domain names as separate targets.

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

Target Specification Lab: 

Lab Examples
````
nmap <ip address>
nmap <ip1> <ip2>
nmap -F <ip>-50
# -F: Fast scan of the most popular 100 ports, scanning IP addresses from 1 through 50
````

Ping Sweep:

A ping sweep scans a subnet in CIDR notation, sending:

    ICMP Echo Request
    TCP SYN to port 43
    TCP ACK to port 80
    ICMP Timestamp Request

This process is rapid and identifies active IP addresses. Example:

`nmap -sn 192.168.1.0/24`

To use a target list for a ping sweep:

`nmap -sn -iL targetlist.txt`

Example workflow:

cd /usr/share/nmap
sudo mkdir targets
cd targets
sudo nano targetlist.txt

---

Random Target Selection:

````
nmap -iR 10
# Randomly selects 10 IP addresses outside your network perimeter and scans them
# Not recommended to perform from home or work.
````

---

Quiet Scan Example:

````
nmap -sS -p 80 -T2 -iR 50
# -sS: SYN scan (default)
# -p: Specifies the port to scan (e.g., 80)
# -T2: Timing template (slower and stealthier)
# -iR: Random target selection, scanning 50 IP addresses
# Suggested to avoid this at work/school due to potential detection.
````

---

Excluding Targets:

````
nmap -sn 192.168.1.0-40 --exclude 192.168.1.1
nano excludelist.txt
nmap -sn 192.168.1.0/24 --excludefile excludelist.txt
````




