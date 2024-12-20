## TCP & UDP Port Scanning

### What is Port Scanning?
- Nmap is the most popular and widely used port scanning tool in the world. This makes sense because it has been around for a very long time, is very refined, sophisticated, it's free, and began as a port scanner. Port scanning is the core and foundation upon which everything else in Nmap is built.
- Ports are used by layer 4 protocols, namely TCP and UDP, to help distinguish between communication channels. IP, at layer 3, uses IP addresses to do this. We spoke about the TCP and UDP headers in a previous lesson and I showed you what the packets look like in Wireshark. They're important for us because they are simple ways for us to determine what services, applications, and sometimes even operating systems of the host we're interested in.
- Port numbers go from 1-65,535. There are three types of ports:
  1. **Well-known ports** (1-1,023): Reserved for specific services by IANA. Examples: TCP port 80 (HTTP), UDP port 53 (DNS).
  2. **Registered ports** (1,024-49,151): Registered with IANA but less commonly used than well-known ports. Examples: TCP port 3389 (RDP), UDP port 1434 (SQL Server).
  3. **Dynamic/private ports** (49,152-65,535): Used for proprietary or ephemeral services.

**Definition of Port Scanning:** The creator of Nmap defines it as the act of remotely testing numerous ports to determine what state they're in. Nmap simplifies this process, handling the scanning and evaluation while requiring the user to critically analyze the results.

For more details, refer to the [Nmap book on port scanning](https://nmap.org/book/port-scanning.html).

### Port States Recognized by Nmap
Nmap can probe TCP or UDP ports on selected targets quickly to determine their states. Six port states recognized by Nmap:

1. **Open:** An application or service is actively accepting connections or packets on the port.
2. **Closed:** The port is accessible but has no application listening. Useful for host discovery and OS detection.
3. **Filtered:** Packet filtering prevents probes from reaching the port, offering minimal information and slowing scans.
4. **Unfiltered:** The port is accessible, but Nmap cannot determine if it is open or closed. Used in ACK scans.
5. **Open|Filtered:** Nmap cannot tell if the port is open or filtered (e.g., UDP, FIN, NULL, Xmas scans).
6. **Closed|Filtered:** Nmap cannot determine if the port is closed or filtered, typically seen with IP ID autoscan.

### Why Scan Ports?
- **Provides insight for network admins and security professionals:** Port scanning aids in identifying services and applications that may expose vulnerabilities.
- **Determines attack surface:** Identifies services that attackers can exploit.
- **Exploitation opportunities:** Open ports may allow attackers to breach systems using tools like `Metasploit`.
- **Asset tracking and policy compliance:** Helps inventory network hardware/software and debug network issues.

### How Do I Scan TCP & UDP Ports in Nmap?
- `nmap <target>`: Scans 1,000 most popular TCP ports using the SYN scan.
- `nmap -F <target>`: Scans 100 most popular TCP ports using the SYN scan.
- `nmap -p <ports or service name> <target>`: SYN scan of specified ports.
- `nmap -sU -p <ports or service name> <target>`: UDP scan of specified ports.
- `nmap -sS -sU -p <ports> <target>`: TCP SYN and UDP scan of specified ports.
- `nmap <scan technique> -p <ports> <target>`: Scans ports according to the specified technique.

---

## TCP & UDP Port Scanning Lab

### Lab: Port Scanning in Nmap

#### Typical Nmap Scans
- Scan a Windows 2012 R2 server.
- Regular Nmap scan:
  ```
  nmap 192.168.1.10
  ```
- Fast scan of 100 most popular TCP ports:
  ```
  nmap -F 192.168.1.10
  ```
- Scan 1,000 most popular UDP ports:
  ```
  nmap -sU 192.168.1.10
  ```

#### Default Nmap Scan Using Various Port Combinations
- Combine fast UDP and TCP scans:
  ```
  nmap -sS -sU -F 192.168.1.10
  ```
- TCP SYN scan on specific ports:
  ```
  nmap -p 53 192.168.1.10
  nmap -p 53,80,135 192.168.1.10
  nmap -p 53,80-138 192.168.1.10
  ```
- Scan all 65,535 ports:
  ```
  nmap -p- 192.168.1.10
  ```
- Specify ports by service name:
  ```
  nmap -p http,domain,msrpc 192.168.1.10
  ```

#### UDP Scans Using Various Port Combinations
- UDP scan of specific ports:
  ```
  nmap -sU -p 53 192.168.1.10
  nmap -sU -p 53,88,111 192.168.1.10
  ```
- Scan UDP ports by range and service names:
  ```
  nmap -sU -p 53,88-162 192.168.1.10
  nmap -sU -p domain,kerberos-sec,rpcbind 192.168.1.10
  ```

#### TCP & UDP Scans Simultaneously
- TCP SYN and UDP scans of specific ports:
  ```
  nmap -sS -sU -p 53 192.168.1.10
  nmap -sS -sU -p 53,80-88 192.168.1.10
  ```
- Scan different TCP and UDP ports simultaneously:
  ```
  nmap -sS -sU -p T:21-139,U:53-88 192.168.1.10
  ```
- Specify services and port numbers in the same scan:
  ```
  nmap -sS -sU -p T:http,domain,3389,U:53,rpcbind 192.168.1.10
  ```

### Key Takeaways
- Use `-p` to specify ports or services.
- For simultaneous TCP and UDP scans, explicitly define both.
- Combine flexibility and precision to tailor scans for the target environment.

