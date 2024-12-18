# IP, TCP, UDP, and ICMP Headers
- Encapsulation & the TCP 3-way handshake
  
  ![image](https://github.com/user-attachments/assets/3e18e84f-d48c-4898-ab5c-cc6f46e09677)<br>
  [Data Encapsulation OSI TCPIP - YouTube video](https://www.youtube.com/watch?v=xaKvGnnuYmk)

Some of you might be wondering why encapsulation and a TCP three-way handshake are covered in the same guide. Well, I don’t have a compelling explanation except that these two concepts are high-level mechanisms that must be understood to conceptualise what happens when Nmap scans are carried out. However, the truth is that encapsulation and the TCP three-way handshake are not inherently connected, aside from the fact that they are both part of the traditional TCP/IP stack and are both fundamental.

Encapsulation is the process of adding headers and trailers to data. Many people describe it in terms of wrappers, like sweet wrappers. The concept is that lower layers add headers, and in some cases trailers, to higher-layer packets in such a way that they are effectively "wrapped" within them.

The image below highlights the two most important OSI or TCP/IP model layers on the left, in the context of Nmap: the transport and network layers.

![image](https://github.com/user-attachments/assets/4fe0b0b7-5549-4222-bf90-30726c17ecc7)<br>
[What Is a Three-Way Handshake in TCP? - YouTube video](https://www.youtube.com/watch?v=LyDqA-dAPW4)

The next image below illustrates which protocols operate within these layers, as well as the names assigned to datagrams at each layer.

![image](https://github.com/user-attachments/assets/3e18e84f-d48c-4898-ab5c-cc6f46e09677)<br>
[Data Encapsulation OSI TCPIP - YouTube video](https://www.youtube.com/watch?v=xaKvGnnuYmk)

At the transport layer, which corresponds to Layer 4 of the OSI model, a datagram is referred to as a segment, and it can utilise either TCP or UDP. At the network layer, or Layer 3, a datagram is called a packet. I wanted to begin with this because we’ll delve further into how Nmap leverages these layers by manipulating their headers during its scans.

The second concept here is the TCP three-way handshake. Some of you might be wondering why this section of the guide doesn’t include a UDP handshake. The reason is simple: no such handshake exists. As we mentioned earlier, UDP does not provide connection-oriented (reliable) end-to-end communication. Instead, it offers best-effort or connectionless communication between hosts. TCP’s three-way handshake, however, is what enables connection-oriented communication.

As depicted in the diagram, user A’s computer initiates communication with server B by sending a TCP segment with the SYN flag set. Server B responds with both the SYN and ACK flags set, and finally, user A’s computer replies with an ACK. This completes the handshake, establishing the connection and allowing communication to proceed.

This concept is crucial in the context of Nmap, as both Nmap and its users—like yourself—can craft scans that manipulate TCP flags in different ways to elicit specific responses, enabling you to critically assess the results.

This functionality is integrated into Nmap as part of its packet-crafting tool, Nping. If you’re interested in learning more about encapsulation and the TCP three-way handshake, I’ve included links to some informative videos below the images.

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
