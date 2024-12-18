## Nmap & IPv6

In your Nmap scanning, you may come across local or remote targets that are configured exclusively with IPv6. Unless your scanning station is correctly set up, you won't be able to run Nmap scans against these targets. This lesson focuses on the key aspects of running Nmap scans against IPv6 targets.

Here are the learning objectives for this lesson: First, we'll explore some general IPv6 information related to Nmap. Next, we'll discuss Nmap's requirements for using IPv6. Finally, we'll review the command-line options you need to be familiar with in order to perform Nmap scans against IPv6 targets.

### General Nmap & IPv6 Information
- Nmap has supported IPv6 since 2002
- IPv6 scanning works with Nmap's most popular features
- Best to use hostname instead of address for simplicity
- Output looks the same

![image](https://github.com/user-attachments/assets/1ec46c36-6b06-4ef9-a892-e6a224973fcd)

### Nmap IPv6 requirements
- Source and target must be configured for IPv6
- If your ISP doesn't provide IPv6, use a tunnel broker service
- Another approach is by using 6-to-4 tunneling
- Free service: tunnelbroker.net
  
### Command-line syntax & important options
- (For using IPv6 on Nmap, simply need to add -6 option or --ipv6

`Nmap -6 <target>` or `Nmap --ipv6 <target>`


`nmap -6 -S <source><target>` (-S allows you to specify source address other than your own which is IPv6 spoofing)


`nmap -6 --hop-limit` (Sets the hop limit field and packets sent from your scanning stations)


nmap.org/book/nping-man-ip6-options.html covers guide in this lesson.
