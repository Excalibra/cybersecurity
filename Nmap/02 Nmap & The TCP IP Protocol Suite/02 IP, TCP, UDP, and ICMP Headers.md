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

Some of the same principles that apply to TCP also apply to UDP, although UDP itself is much simpler and involves less overhead than TCP. The most important component of the UDP header is the destination port, while the ephemeral source port is provided by your computer. It is essential to be familiar with constructing UDP scans in Nmap, as some critical services depend on UDP for communication. For instance, DNS uses UDP port 53, NTP uses port 123, NetBIOS uses port 137, and LDAP uses port 389. To initiate a UDP scan, use nmap -sU followed by the ports you wish to scan, specified with the -p switch.

- Layer 4 protocol 
- Source Port  
- Destination Port
- `nmap -sU` (UDP scan)

![image](https://github.com/user-attachments/assets/e8fa4170-8941-45fd-a699-ae8f81955a6b)

---

## IP Header

The IPv4 header is attached to the TCP or UDP header through the process of encapsulation. IP is connectionless and operates at Layer 3, within the network layer. You’ll notice that I have “version” circled in the graphic to the right. The only reason I’ve highlighted it is to avoid confusion. 

In IPv4 communication, this value will always be `4`; however, that doesn’t mean it changes to `6` for IPv6 communication. In fact, IPv6 has an entirely different header. Beyond that, you don’t need to worry about the version field. 

The protocol field defines the protocol used in the creation of the packet. For the most part in Nmap, this will be:  
- **TCP** (`protocol 6`),  
- **UDP** (`protocol 17`), or  
- **ICMP** (`protocol 1`).  

The **source address** is typically your IP address, although it can be altered, while the **destination address** is the address of your target. 

`nmap -sO` allows you to determine which IP protocols are supported by target machines. By default, Nmap will scan all 256 possible protocol values and provide you with the results.  

As with the other slides in this module, I’ve provided a video for a deeper look into the IP header, should you wish to learn more.

### IP Header Overview
- **Layer 3 protocol**  
  - Version  
  - Protocol  
  - Source Address  
  - Destination Address  

![image](https://github.com/user-attachments/assets/1a32ce03-f03f-453c-99db-b22ae9e008f4)  
[IP Header: Networking & TCP/IP Tutorial. TCP/IP Explained](https://www.youtube.com/watch?v=UrO-9Uagn24)

---

## ICMP Header

The Internet Control Message Protocol (ICMP) is widely used by network analysts to:

- Verify whether packets are routing successfully.
- Check if hosts are operational.
- Perform basic latency analysis.

This is typically achieved using the `ping` or `traceroute` commands in your operating system. ICMP is a supporting protocol that behaves similarly to layer 4 protocols but technically operates at **layer 3**. As shown in the graphic, ICMP must be attached to IP because its header does not include an address field. 

The two most important fields in the ICMP header are:

- **Type**
- **Code**

Common responses include types `0`, `3`, `8`, or `11`, such as:

- **Destination Host Unreachable**
- **TTL Exceeded**

### Key Notes:

- When you read about **ping scans in Nmap**, it doesn’t necessarily mean ICMP is being used.
- ICMP primarily supports **TCP** and **UDP** scans in Nmap.
- To specifically initiate an ICMP scan, you must use:  
  ```bash
  nmap -sn -PE
  ```
- Nmap can also use ICMP innovatively, such as creating small ICMP packets to quickly elicit responses from entire networks, which is much more efficient than pinging each device individually.
- Despite this, **TCP** and **UDP scans** are generally more effective, and allowing Nmap to use ICMP as a helper often provides the best results.

### Summary:

- **Layer 3 protocol (kinda)**  
  - `Type`  
  - `Code`
  - `Ping Scan != ICMP`
  - Example ICMP usage: `nmap -sn -PE`

![image](https://github.com/user-attachments/assets/af0a7357-596f-4211-8aa1-5fb192b9b97b)  
[**TCP/IP Tutorial | ICMP Message Types**](https://www.youtube.com/watch?v=FprZF9agJJI)

---

In this guide, we covered two critical concepts in TCP/IP:

1. **Encapsulation**  
2. **The TCP Three-Way Handshake**

We also examined:

- **TCP** and **UDP** headers.
- The **IP header**.
- A discussion on **ICMP and its header**.

