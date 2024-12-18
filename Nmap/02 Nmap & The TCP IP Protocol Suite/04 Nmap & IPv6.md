## Nmap and Wireshark

### About Wireshark

Wireshark is a **network protocol analyser** that allows you to capture and interactively browse traffic on a computer network. While Wireshark is an incredibly powerful tool, the limitations of TCP/IP on a switched network can reduce its effectiveness. Specifically, simply placing a network protocol analyser like Wireshark on a network doesn't guarantee it will capture all traffic.

For Wireshark to monitor **all network traffic**, it must be set to listen in **"promiscuous mode"** and must be operating on a **hub** (which repeats all traffic) or a **span/mirrored port** on a **switch**.

If you're a network administrator, you can configure these settings, but it’s generally not recommended on a **production network** just for the sake of learning Nmap. However, despite this limitation, Wireshark remains a highly effective tool. In this lab, we will set up Wireshark on the **target host**, run some scans, and then filter and evaluate the results.

---

### Why Use Wireshark?

- **Ideal for Network Administrators & InfoSec Professionals**
- **Great for Troubleshooting**
- **Effective for Investigation & Mitigation**
- **Admissible as Documentary Network Forensic Evidence**

---

### Why Use Wireshark with Nmap?

- Can be used on **Scanning Station** or **Target Host**
- Informative and **educational**
- Allows you to **read raw packets** to evaluate how they are crafted, received, and responded to
- Helps **appreciate Nmap's efficiency** and speed

---

### Lab: Using Wireshark with Nmap

1. **Running a Wireshark Capture**
   - Select the correct adapter
   - Set it to **promiscuous mode**

2. **Difference Between a Capture Filter and Display Filter**
   
3. **Running Nmap Scans and Filtering Results in Wireshark**
   - Perform 3 simple Nmap scans

---

### Basic Wireshark Filtering Syntax

- **Wireshark Cheat Sheet**:  
  [StationX Wireshark Cheat Sheet](https://www.stationx.net/wireshark-cheat-sheet/)

---

### Lab on Running Wireshark and Nmap Together

In this lab, you're on the **Nmap scanning station**, and the target host is running **Wireshark**.

#### Steps:

1. **Find the IP Address of the Machine Running the Nmap Scan**  
   Run:  
   `ip a` (or `ipconfig` on Windows)

2. **Set Up Wireshark on the Target Host**  
   - Open Wireshark
   - Select the adapter
   - Go to the **Capture** tab, click on **Options**, and ensure the **"Promiscuous"** mode is checked

3. **Ping the Host and Run Nmap**  
   - Ping the hostname on the VM to find the IP address
   - Run:  
     `nmap <ip_address>`

4. **Use Wireshark Display Filter**  
   In the display filter search bar, type: `ip.addr==<ip_address> && ip.proto!=UDP && tcp.flags.syn==1`
   (Where `proto!=UDP` filters out UDP, and `tcp.flags.syn==1` filters for a **SYN scan**.)

5. **UDP Scan Example**  
Run:  
`nmap -sU -p 53,88,123,137,138 192.168.1.10`  
(-p for ports, followed by common UDP ports that may be open on a 2012 R2 server, particularly if it's a domain controller.)

6. **Wireshark Display Filter for UDP**  
On Wireshark’s display filter: `ip.addr==192.168.1.167 && ip.proto==UDP && udp.dstport!=3389 && udp.scrport!=3389`

(Filters for **UDP traffic** excluding the **3389 RDP port**.)

7. **Xmas Scan with Nmap**  
Run:  
`nmap -sX 192.168.1.10`  
On Wireshark, apply the filter: `ip.addr==192.168.1.167 && ip.proto==TCP && tcp.flags.fin==1 && tcp.flags.push==1 && tcp.flags.urg==1`

(This filter identifies **TCP Xmas scan flags**: FIN, PUSH, and URG.)



