# IP, TCP, UDP, and ICMP Headers
- Encapsulation & the TCP 3-way handshake
  ![image](https://github.com/user-attachments/assets/4fe0b0b7-5549-4222-bf90-30726c17ecc7)
  
  [What Is a Three-Way Handshake in TCP? - YouTube video](https://www.youtube.com/watch?v=LyDqA-dAPW4)

  ![image](https://github.com/user-attachments/assets/3e18e84f-d48c-4898-ab5c-cc6f46e09677)
  
  [Data Encapsulation OSI TCPIP - YouTube video](https://www.youtube.com/watch?v=xaKvGnnuYmk)

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
