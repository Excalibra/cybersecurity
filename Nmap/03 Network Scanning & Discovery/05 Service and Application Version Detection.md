## 4.11 + 4.12 Service and Application Version Detection

### What is Service & Application Version detection?
- Determines what services and applications are running on target hosts
- Dependent on appropriate port scanning
- Will attempt to determine the version of those services and applications
- Can uncover services and application versions running on non-standard ports
- Uses both internal `nmap-service-probes` database and CPE database

  Determines what services and applications are running on target hosts, additionally Nmap will attempt to determine the version of those services and applications. It does this by analyzing data from port scans and taking a step further by interrogating those ports to determine the service or applications running on them. This is similar to but far more sophisticated and accurate than typical banner-grabbing techniques. 

  Nmap achieves this by comparing responses to port scans with its built-in `nmap-service-probes` database. Essentially, it queries its database to match expressions from responses. Nmap tries to determine:
  - Service protocol
  - Application name
  - Version number
  - Host name
  - Device type
  - OS family

  More advanced operating system discovery will be performed in the next scanning phase, which will be discussed later.

  Sometimes, network admins or software companies run apps and services on non-standard ports. Nmap can often uncover these. Additionally, Nmap uses NIST's Common Platform Enumeration (CPE) database to report services and applications in a standardized format. The NIST defines CPEs as a structured naming scheme for IT systems, software, and packages. It includes:
  - A formal name format
  - A method for checking names against systems
  - A description for binding text and tests to a name

  **Learn More:**
  - [NIST Common Platform Enumeration](https://nvd.nist.gov/products/cpe)
  - [Nmap Service and Application Version Detection](https://nmap.org/book/vscan.html)

---

### Why is it relevant and important?
- Licensing, compliance, and vulnerability analysis for Network Administrators
- Vulnerability testing and exploit preparation for Penetration Testers
- Critical information for successful offense or defense
- Help Nmap and the community by submitting unmatched fingerprints

---

### When and how do I use it?

![Example Image](https://github.com/user-attachments/assets/4e26df68-5266-4d67-b070-6f97868da0e1)

- **Typical phases in an Nmap scan**
- **Basic Command:** `nmap -sV <target>`
- **Better Command Structure:** `nmap <scan technique> <ports> -sV <target>`
- **Example:** `nmap -sS -sU -p T:21,25,80,443,3389,U:88,123 -sV 192.168.1.10`

---

### Other command-line options available
- `--version-intensity <level>`: Adjust the aggressiveness of the version scan (default is `7`).
  - Lower levels are effective against common services; higher levels are useful against less common ones.
  - **Tradeoff:** Higher intensity increases scan time and noise.
- `--version-light`: Shorthand for `--version-intensity 2`, which is faster and sufficient for many cases.
- `--version-all`: Tries all probes (equivalent to `--version-intensity 9`).
- `--version-trace`: Displays extensive debugging information during version detection scanning.

---

### Lab: Services & Application Version detection

**What we will be doing:**
1. Host discovery scan
2. Port scan
3. Service and Application Version Detection

#### Example Commands
**1. Ping sweep:**

`nmap -sn 192.168.1.10`

**2. Fast TCP and UDP scan:**

`nmap -sS -sU -F 192.168.1.10`

**3. Basic version detection scan:**

`nmap -sV 192.168.1.10`

*Took 142 seconds for results.*

**4. Sophisticated and targeted scan:**

`nmap -sS -sU -p T:80,88,135,139,389,443,U:123,137 -sV 192.168.1.10`

*Took 18.71 seconds, yielding more detailed and actionable information.*
