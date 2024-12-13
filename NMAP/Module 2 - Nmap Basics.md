# Module 2 - Nmap Basics
## 2.9 Getting Help - VM
All operating systems: "nmap -V" shows nmap version, this is helpful for comparison purposes and shows what platform you're running on and how it was compiled. "namp" or "nmap-h" reminds you of scan options available to you and sample scans. 
"nmap --script-help <script name>" will give details of any nmap scripting engine script does, the amount of detail is completely up to the author. 

Linux/UNIX/macOS: "man nmap" for manual of the nmap. 
Nmap Docs - nmap.org.docs.html, 
Reference Guide - nmap.org/book/man.html, 
Zenmap GUI Help - nmap.org/book/zenmap.html, 
Book - nmap.org/book, 
Subscribe to Nmap Hackers - nmap.org/download.html. 

Social Media & Conferences: 
Facebook: facebook.com/nmap, 
Twitter: twitter.com/nmap, 
USENIX: usenix.org, D
EF CON: defcon.org, 
Blackhat: blackhat.com. 

## 2.10 Phases of the Nmap Scan - NM
### What are the scan phases?:
- Phase 1 - Script pre-scanning: Occurs only while running NSE scans. For script which only have to be run once per Nmap execution.
- Phase 2 - Target enumeration: Occurs with EVERY scan, Determines every host to scan, Passing IP addresses is faster than FQDN.
- Phase 3 - Host discovery: Also known as "Ping Scanning", Determines which targets are online, Can be skipped, Turning off may increase performance if not neccessary.
- Phase 4 - Reverse-DNS resolution: Occurs by default when specifying IPs, A host's name pay provide clues, May be skipped, May be forced.
- Phase 5 - Port scanning: The most popular reason people use Nmap, Though significant, only one component, Probes are sent, responses are evaluated, Performed by default in every Nmap scan, Also can be skipped.
- Phase 6 - Version detection: Port open = determine server software, Compares responses to signatures, Can be enabled on any scan.
- Phase 7 - OS detection: This phase is optional, but run on several default scans, Can be run in any scan, Similar to version detection; responses are compared to signatures/behaviours, Provides a degree of likelihood, Can be enhanced with several NSE script scans. 
- Phase 8 - Traceroute: Enhanced traceroute engine, Can be forced on any scan, Nmap determines route to target, then runs reverse-DNS lookup, Reverse-DNS lookups occur in parallel in order to improve performance.
- Phase 9 - Script scanning: Where most NSE scripts run, NSE will be covered in detail later.
- Phase 10 - Output: Final phase in most scans, Outputs result to screen or file(s), Sometimes considered the most important, Nmap can provide both searchable and report quality output.
- Phase 11 - Script post-scanning: Mostly theoretical at this point, this process would occur if you lean the LUA programming language with post scanning processes, Can process results and deliver final reports and statistics, Not currently used by any official NSE scripts, Likely to change in the future.
  
## 2.11 Constructing an Nmap Scan - NM
Reminder on how to get help:
Refer back to lesson 2.9,
Command line options: "nmap-h","nmap--script-help <script name>", or "man nmap",
Nmap website, especially - nmap.org/book/man.html,
Online Book - nmap.org/book,
Create or find a Cheat Sheet.

Basic requirements of an Nmap scan:
Open command-prompt as privilaged user,
Path considerations,
Basic scan - "nmap <target>" have a target, no matter how sofisticated your scan is, without a target you will fail.

Two important options:
Target: hostname(s), IP address(es), networks,
Output (file format): -oN, -oX, -oS, -oG, -oA, -v or -vv. (-v and -vv is to increase level of detail).

Regular vs script scan:
Regular scan:"nmap <options><target>",
Script scan: nmap <options> sC <target>, nmap <options> --script-<script name><target>

## 2.12 Constructing an Nmap Scan Lab Part 1 - NM
Help reminder - "nmap -h" or "nmap"
Target types:
- Nmap <target> for example nmap 192.168.1.254 or a range nmap 192.168.1.1-25
- Nmap will also accept entire network range in CIDR notation: nmap 192.168.1.0/24. That will scan every host on the 191.168.1.0 network which is a subnet mask of 255.255.255.0
- "nmap nmap.org/29" will do an entire domain in CIDR notation of nmap.org in /29 which is a lot smaller network than a /24 since there's 29 bits in the subnet mask; meaning that there's 29 bits assigned to the network portion of the IP address.
## 2.13 Constructing an Nmap Scan Lab Part 2 - NM
### Output types:
- First thing he does is creates a directory called "Results" on Win10 cmd in the root of C. 
- Within "C: \results>" nmap -h to see output types.  (will need to find the correct command for Linux, such as dir and creating these folders via terminal).
- Normal scan, normal file type: "nmap 192.168.1.254 -oN results1.nmap" calling the file results1.nmap.
- If you want to see the output quickly, "notepad results1.nmap"
- Now with -O, "nmap -O scanme.nmap.org -oA results2 (-O is for operating system scan, and -oA will output 3 main file types (nmap, XML, grepable format), notice that we didn't put the file extension to "results2" because nmap will do that for you). 
- You can put options, scan types, target and output in different locations in the command line and all of them will work the exact same.: "nmap -oN results3.nmap 192.168.1.254 -O". In the course video, it shows results. This is only to prove that there's no "correct" order on command line.
 - Example test "nmap -O 192.168.1.254 -oX results5.xml" the output and target are at the end
 - Example test: "nmap -O -v 193.168.1.254 -oN results6.nmap" v stands for verbosity, which adds detail either with -v or -vv. You can see the difference in bites number when using dir on terminal.
 - Example test: "nmap -O -vv 193.168.1.254 -oN results7.nmap" 
## 2.14 General Considerations - NM
- GUI, or Command line?
  - Start with Nmap Command Line
    - Zenmap may not be available
    - Using batch files in Windows
    - Test both, evaluate performance
  - Benefits of Using Zenmap
    - Point & click environment
    - Graphical environments may be easier
    - Can create and save custom scan profiles
    - Good way to learn Nmap
    - NSE scripts (easier to learn to read what it does)
- Best Way to Learn Zenmap
   - Read the book - nmap.org/book/zenmap.html
   - Run as priviledged user
   - Try it on your home network
   - Play around with it
   - Save scan results
- Lab: Using Zenmap
  - Target, Profile, Command
  - Output,Ports/Hosts,Topology,Host Details,Scans
  - NSE Script Help

### Practical section:
"Command:" section is exactly the same as what you would put as the command line on terminal. So "nmap  scanme.nmap.org" and clicking on "Scan" button shows results. You can add target IP and profile type and the command line will be built for you: Ex. Target: 192.168.1.254, Profile: Intense scan (nmap -T4 -A -v 192.168.1.254) 4 for aggressive, -A for advanced scan, -v for verbosity increase/detail shown in the output. After the scan is complete, you can click on "scan" on top.

## 2.15 Custom Scan Profiles Part 1 - NM
### Profile editor
Profile tab/New profile or command. 
### Naming convention
Give profile name "Custom:..." to differentiate default and custom scan profiles. Then sellect which one to run, e.g. Ping/ICMP ping (-PE).
### Leave target blank
Leaving it blank will let you keep the target section empty to use on different targets
### Custom Profile 1: WhoIS IP?
Profile tab/New profile or command. (name it Custom: WhoIS IP?). Scripting/(type whois and select whois-ip). For verbosity: Other, check the box for Verbosity level (-v) and add "1". 
### Custom Profile 2: WhoIS Domain?
Profile tab/New profile or command. (Name it Custom: WhoIS Domain?). Scripting/(type whois and select whois-domain). 
### Custom Profile 3: Quick Detailed OS Detection
Profile tab/New profile or command. Scan/(tick box "Operating system detection (-O). Sellect "Timing Template" as "Agressive (-T4) (NOTE: when using aggressive, it makes it work a lot faster, but it is more intruisive, so when doing this to an outside or unknown IP address, it could be flagged by an IDS or firewall). Scripting/(type smb and sellect smb-os-discovery)
