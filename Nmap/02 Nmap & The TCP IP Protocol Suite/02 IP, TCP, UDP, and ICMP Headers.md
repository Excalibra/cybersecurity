# IP, TCP, UDP, and ICMP Headers

## Encapsulation & the TCP 3-Way Handshake

Some of you might be wondering why encapsulation and a TCP three-way handshake are covered in the same guide. Well, I don’t have a compelling explanation except that these two concepts are high-level mechanisms that must be understood to conceptualise what happens when Nmap scans are carried out. However, the truth is that encapsulation and the TCP three-way handshake are not inherently connected, aside from the fact that they are both part of the traditional TCP/IP stack and are both fundamental.

Encapsulation is the process of adding headers and trailers to data. Many people describe it in terms of wrappers, like sweet wrappers. The concept is that lower layers add headers, and in some cases trailers, to higher-layer packets in such a way that they are effectively "wrapped" within them.

The image below highlights the two most important OSI or TCP/IP model layers on the left, in the context of Nmap: the transport and network layers.

![image](https://github.com/user-attachments/assets/4fe0b0b7-5549-4222-bf90-30726c17ecc7)  
[What Is a Three-Way Handshake in TCP? - YouTube](https://www.youtube.com/watch?v=LyDqA-dAPW4)

The next image below illustrates which protocols operate within these layers, as well as the names assigned to datagrams at each layer.

![image](https://github.com/user-attachments/assets/912bd24b-74df-42cb-a219-2df98f272b0b)  
[Data Encapsulation OSI TCPIP - YouTube](https://www.youtube.com/watch?v=xaKvGnnuYmk)

At the transport layer, which corresponds to Layer 4 of the OSI model, a datagram is referred to as a segment, and it can utilise either TCP or UDP. At the network layer, or Layer 3, a datagram is called a packet. I wanted to begin with this because we’ll delve further into how Nmap leverages these layers by manipulating their headers during its scans.

The second concept here is the TCP three-way handshake. Some of you might be wondering why this section of the guide doesn’t include a UDP handshake. The reason is simple: no such handshake exists. As we mentioned earlier, UDP does not provide connection-oriented (reliable) end-to-end communication. Instead, it offers best-effort or connectionless communication between hosts. TCP’s three-way handshake, however, is what enables connection-oriented communication.

As depicted in the diagram, user A’s computer initiates communication with server B by sending a TCP segment with the SYN flag set. Server B responds with both the SYN and ACK flags set, and finally, user A’s computer replies with an ACK. This completes the handshake, establishing the connection and allowing communication to proceed.

This concept is crucial in the context of Nmap, as both Nmap and its users—like yourself—can craft scans that manipulate TCP flags in different ways to elicit specific responses, enabling you to critically assess the results.

This functionality is integrated into Nmap as part of its packet-crafting tool, Nping. If you’re interested in learning more about encapsulation and the TCP three-way handshake, I’ve included links to some informative videos below the images.

---

## TCP Header

TCP is a transport layer protocol (Layer 4 of the OSI model) that provides reliable, connection-oriented communication and is passed down to be encapsulated by IP. From Nmap’s perspective, the most important elements of the TCP header to understand are the source port, the destination port, and the TCP flags. While other aspects can be modified with Nmap using Nping, these are the ones you’ll primarily work with when using Nmap.

In a standard Nmap scan, the source port is ephemeral, meaning your scanning station automatically determines which port it opens for communication, typically selecting a higher-level, non-well-known port—one above 1024. Conversely, the destination port is either specified by you in your scan command or selected by Nmap. For example, a regular Nmap scan examines 1,000 commonly used ports, whereas a fast scan checks the 100 most popular ports. To execute a fast scan, you can use the `-F` command-line switch or explicitly specify the ports you want to scan. I’ll demonstrate this later.

Another powerful feature of Nmap is that it doesn’t require a full TCP connection (i.e., a three-way handshake) to perform a scan. By default, Nmap conducts a TCP SYN scan, setting the SYN flag but not completing the handshake with a SYN-ACK. This is because SYN scan responses are just as reliable as full connect scans but are quieter and more discreet. For example:

- `nmap -sS` initiates a SYN scan.  
- `nmap -sA` initiates an ACK scan.  
- `nmap -sT` performs a full connect scan.  

Other notable TCP flags include:

- `U` for Urgent  
- `P` for Push  
- `R` for Reset  
- `F` for Finish  

You can also conduct a so-called **“Christmas tree scan”** or **X-mas scan** using the `-sX` switch. This sets all the TCP flags in the header, effectively “lighting up” the TCP segment like a Christmas tree. While responses to this type of scan can provide valuable information, they are far from discreet.

### TCP Header Overview

- **Layer 4 protocol**  
  - Source Port  
  - Destination Port  
- **TCP Flags**  
  - `nmap -sS` (TCP SYN scan)  
  - `nmap -sA` (TCP ACK scan)  
  - `nmap -sT` (TCP connect scan)  

![image](https://github.com/user-attachments/assets/e5cae681-918b-447a-915c-c0476ff21848)

---

## UDP Header

- **Layer 4 protocol**  
  - Source Port  
  - Destination Port  

Nmap can perform UDP scans using `nmap -sU`.

---

## IP Header

- **Layer 3 protocol**  
  - Version  
  - Protocol  
  - Source Address  
  - Destination Address  

---

## ICMP Header

- **Layer 3 protocol, kinda**  
  - Type  
  - Code  

### Ping Scan vs ICMP

- **Ping Scan**: `nmap -sn -PE` (uses ICMP)
