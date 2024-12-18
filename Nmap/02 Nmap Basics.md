# Nmap Basics

## Getting Help - VM

### General Commands:
- `nmap -V`: Displays the Nmap version, helpful for comparison and understanding the platform used.
- `nmap` or `nmap -h`: Provides a list of available scan options and examples.
- `nmap --script-help <script_name>`: Details the function of a specific NSE script.

### Platform-Specific Help:
- **Linux/UNIX/macOS**: Use `man nmap` to access the Nmap manual.

### Additional Resources:
- [Nmap Docs](https://nmap.org/docs.html)  
- [Reference Guide](https://nmap.org/book/man.html)  
- [Zenmap GUI Help](https://nmap.org/book/zenmap.html)  
- [Book](https://nmap.org/book)  
- [Subscribe to Nmap Hackers](https://nmap.org/download.html)

### Social Media & Conferences:
- [Facebook](https://facebook.com/nmap)  
- [Twitter](https://twitter.com/nmap)  
- [USENIX](https://usenix.org)  
- [DEF CON](https://defcon.org)  
- [Blackhat](https://blackhat.com)

---

## Phases of the Nmap Scan - NM

### Scan Phases Overview:
1. **Script Pre-Scanning**: Runs NSE scripts that only execute once per Nmap session.
2. **Target Enumeration**: Identifies all hosts to scan. IPs are processed faster than FQDNs.
3. **Host Discovery (Ping Scan)**: Determines online targets. Can be skipped to enhance performance.
4. **Reverse DNS Resolution**: Resolves hostnames from IPs. Skipping this step may also increase speed.
5. **Port Scanning**: Sends probes to detect open ports. A core feature of Nmap.
6. **Version Detection**: Identifies server software using signature matching.
7. **OS Detection**: Compares responses to OS signatures for likelihood estimates.
8. **Traceroute**: Maps routes to targets with parallel reverse DNS lookups.
9. **Script Scanning**: Executes most NSE scripts for additional details.
10. **Output**: Generates results on-screen or in files, supporting both searchable and report-quality outputs.
11. **Script Post-Scanning** (Future): Intended for Lua post-processing and advanced reporting.

---

## Constructing an Nmap Scan - NM

### Getting Help:
- Command-line: `nmap -h`, `nmap --script-help <script_name>`, or `man nmap`.
- Online: [Nmap Reference Guide](https://nmap.org/book/man.html), [Nmap Book](https://nmap.org/book).
- Cheat Sheets: Create or use an existing Nmap cheat sheet.

### Key Requirements:
1. Open the terminal as a **privileged user**.
2. Ensure proper **path considerations**.
3. Always specify a **target**:
   - Example: `nmap <target>` (no target = scan failure).

### Important Options:
- **Target Types**: Hostnames, IP addresses, or networks.
- **Output Formats**:  
  `-oN`, `-oX`, `-oS`, `-oG`, `-oA`.  
  Add verbosity with `-v` or `-vv`.

### Regular vs Script Scans:
- **Regular**: `nmap <options> <target>`  
- **Script**: `nmap <options> -sC <target>` or `nmap <options> --script <script_name> <target>`

---

## Constructing an Nmap Scan Lab

### Target Types:
- Basic: `nmap <target>`  
  Example: `nmap 192.168.1.254` or `nmap 192.168.1.1-25`
- Network Range (CIDR):  
  Example: `nmap 192.168.1.0/24`
- Smaller Network Range:  
  Example: `nmap nmap.org/29`

### Output Types:
1. Create a directory for results:
   - Windows: `mkdir C:\Results`
   - Linux: Use appropriate terminal commands like `mkdir`.
2. Save results to different formats:
   - Normal: `nmap 192.168.1.254 -oN results1.nmap`
   - XML: `nmap -O scanme.nmap.org -oA results2`
3. Experiment with command order:
   - Example: `nmap -oN results3.nmap 192.168.1.254 -O`
   - Example: `nmap -O -v 193.168.1.254 -oN results6.nmap`

---

## General Considerations

### GUI vs Command Line:
- **Start with Command Line**:  
  - Zenmap may not always be available.  
  - Use batch files for scripting.
- **Benefits of Zenmap**:  
  - Easier for beginners.  
  - Save custom profiles.  
  - Learn NSE scripts.

### Learning Zenmap:
1. Read the [Zenmap Guide](https://nmap.org/book/zenmap.html).
2. Use on your home network as a privileged user.
3. Save scan results and explore features.

### Practical Zenmap Use:
- **Command Section**: Equivalent to terminal commands.  
- Example: `nmap scanme.nmap.org`  
- Add targets and profiles for custom scans.

---

## Custom Scan Profiles

### Creating Profiles:
1. **Profile Editor**: Use the `Profile` tab.
2. **Naming Convention**: Start names with `Custom: ...`.
3. **Flexible Targets**: Leave the target field blank for reuse.

### Example Custom Profiles:
1. **WhoIs IP?**  
   - Add `whois-ip` script and verbosity level (`-v`).
2. **WhoIs Domain?**  
   - Add `whois-domain` script.
3. **Quick OS Detection**:  
   - Enable OS detection (`-O`) and aggressive timing (`-T4`).
   - Add `smb-os-discovery` script for detailed results.
