## Host Discovery

### What is "Host Discovery" and where should options be placed?
- **Purpose**:
  - Scan entire network blocks quickly to determine available devices or hosts.
  - Narrow down potential targets.
- **Placement in Nmap Scan Statement**:

`nmap [host discovery] [ports] [options/features] [target] [output]`


- **Do I have to use any host discovery option?**
- No, it won’t run any by default.
- **When should I use it?**
- Host discovery scans are often the first step for network administrators or security professionals targeting large ranges of network devices.
- For network administrators, host discovery may be the only scan needed.

- **Reference**: [Nmap Host Discovery Documentation](https://nmap.org/book/man-host-discovery.html)

### Most Popular and Useful Host Discovery Options

1. **List Scan (`-sL`)**: `nmap -sL`

- Lists each host of a network without sending any packets to target hosts.
- Performs reverse DNS resolution to learn hostnames.
- Non-intrusive, ideal for reconnaissance against public address spaces.

2. **Ping Scan (`-sn`)**: `nmap -sn`

- Does not perform a port scan after discovery.
- Sends ICMP echo requests, TCP SYN to port 443, TCP ACK to port 80, and ICMP timestamp requests by default.
- Quick and unobtrusive, providing valuable information like hostnames, MAC addresses, and manufacturer details.

3. **No Ping Scan (`-Pn`)**: `nmap -Pn`

- Skips Nmap's discovery stage and scans all specified targets, even inactive ones.
- ARP scanning is performed unless `--disable-arp-ping` or similar options are specified.
- Slower when scanning a wide range without additional options.

4. **Additional Features**:
- `-n` : Disable DNS resolution.
- `-R` : Force resolution of all hostnames.
- `--traceroute` : Trace the path to hosts.
- `--dns-servers <server1>,<server2>,...` : Specify custom DNS servers.

### Other Host Discovery Options

1. **TCP/UDP/SCTP/IP Protocol Pings**: `nmap -PS -PA -PU -PY -PO`

- `-PS`: TCP SYN ping
- `-PA`: TCP ACK ping
- `-PU`: UDP ping
- `-PY`: SCTP init ping
- `-PO`: IP protocol ping

2. **ICMP Pings**: `nmap -PE -PP -PM`

- Sends ICMP pings (echo requests, timestamp requests, etc.).

3. **ARP Ping (`-PR`)**: `nmap -PR`

- Identifies MAC addresses of hosts in the same broadcast domain.

4. **Other Features**:
- `--disable-arp-ping`: Disables ARP and IPv4 neighbor discovery.
- `--system-dns`: Uses scanning station's name servers for reverse resolution.

---

### Lab: Host Discovery

1. **List Scan Example**: `nmap -sL`

- Example: `nmap -sL nmap.org/24`
- Performs reverse DNS lookups for all identified targets.

**Sample Output**:

Nmap scan report for li392-237.members.linode.com (50.116.1.237) Nmap scan report for 50-116-1-238.ip.linodeusercontent.com (50.116.1.238) ...

2. **Ping Sweep Example**: `nmap -sn`

- Example: `nmap -sn 192.168.0.0/24`
- Quickly identifies responding hosts, providing names, IP addresses, MAC addresses, and manufacturers.

3. **No Ping Scan Example**: `nmap -Pn`

- Example: `nmap -Pn -p 80 192.168.0.0/24`
- Skips host discovery and scans all specified devices, focusing on specific ports.

**Sample Output**: 256 IP addresses (2 hosts up) scanned in 3.37 seconds.

---

### Key Takeaways:
- Use **`-sL`** for non-intrusive reconnaissance.
- Use **`-sn`** for quick identification of live hosts.
- Use **`-Pn`** to force scans on all targets, regardless of active status.
- Combine options to optimize scan speed and relevance.




















