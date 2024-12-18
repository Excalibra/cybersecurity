# IP, TCP, UDP, and ICMP Headers
- Encapsulation & the TCP 3-way handshake

![image](https://github.com/user-attachments/assets/68e97b5f-8d0b-4496-9ced-3f33d1b9b555)


- TCP header
    - Layer 4 protocol
      - Source Port
      - Destination Port
    - TCP Flags
     - Nmap -sS(TCP SYN scan)
     - Nmap -sA(TCP ACK scan
     - Nmap -sT(TCP connect scan)


    - UDP header
      - Layer 4 protocol
      - Source Port
      - Destination Port
    - Nmap -sU (UDP scan)


    - IP header
      - Layer 3 Protocol
      - Version
      - Protocol
    - Source & Destination Address - IP addresses


    - ICMP header
      - Layer 3 protocol, kinda
      - Type
      - Code
    - Ping Scan !=ICMP
      - Nmap -sn -PE (uses ICMP)
