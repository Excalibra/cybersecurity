# IPv4 for Nmap

---

## Overview of TCP/IP v4:
- **TCP/IP Protocol Suite**:
  - IP, TCP, UDP, ICMP protocols
  - Local & remote IP addressing
  - How Nmap integrates with TCP/IP v4

---

## IP Addressing:

### **Binary to Decimal Conversion**
In IP addressing, numbers are typically presented in their decimal form, such as `192.168.1.1`. There are four groups of numbers separated by decimal points. These numbers are interpreted by network devices in their binary form. Each group is referred to as an **octet**. 

It is called an octet because the maximum value in each group is `2^8 - 1` (since zero can also be used). In other words, the maximum value assignable to each octet is `255`. In binary, `255` is represented as `11111111`, or eight ones. Most of you are already familiar with this, so I won’t delve into too much more detail.

---

### **Structure**
- Composed of **4 octets** : `XXX.XXX.XXX.XXX`.

---

### **Subnetting**: Understanding Subnets and Their Role in Networking
The process of subnetting is often one of the first mathematical challenges that network administrators must master—it’s a rite of passage. At its core, subnetting is simply an addressing methodology that allows network administrators to determine:
- Which part of an IP address designates the **network**, and 
- Which part identifies the **host**.  

This is achieved by assigning a combination of an IP address and a **subnet mask**.

#### **Example**:
On many LANs, a common subnet mask for each VLAN is `255.255.255.0`. This mask indicates:
- The first three octets of the IP address define the **network**.
- The fourth octet specifies the **host**.

All devices on the same VLAN will share the same first three octets (e.g., `192.168.1`), and each device will have a unique and distinct fourth octet.

#### **Nmap Relevance**:
- **Private Addressing Schemes**:  
  - On Windows: Run `ipconfig` in the Command Prompt to check your IP address and subnet mask.  
  - On Linux, Unix, and macOS: Run `ifconfig` in a terminal to determine your network details.  

- **MAC Address Discovery**:
  - This can only be done when your scanning station is on the **same network** as the target device. 
  - There is no way to determine the MAC address of a remote host unless you have administrative privileges on the router or switch to which the device is connected. 
  - The sole exception to this rule is when your scanning station is connected to a span or mirrored port.

---

### **CIDR Notation**
- **What is CIDR?**  
  CIDR, short for **Classless Inter-Domain Routing**, simplifies IP addressing by combining an IP address with a `/` followed by a number that represents the **network portion** of the address (also known as the subnet mask).

#### **Example**:
- `192.168.1.0/24`: Indicates that 24 bits of the IP address are allocated for the **network portion**.  
- This notation is a concise and flexible way to define networks without being confined to traditional class-based IP address schemes.

---

## Name Resolution:

### **DNS**
DNS stands for **Domain Name System**. It serves as a translator, converting human-readable names into IP addresses. As discussed earlier, you can use a fully qualified domain name (FQDN), such as `scanme.nmap.org`, as a target for a scan. This makes it easier to identify and interact with devices on a network without needing to remember their numerical IP addresses.

---

### **Nmap & Name Resolution**
By default, Nmap relies on your computer’s **name servers** when performing a scan. However, you can specify alternate name servers for Nmap to use. This can be particularly useful if:
- You do not trust your own name servers, or 
- You wish to compare how different name servers resolve domain names.

One key reason for using alternate name servers is to investigate whether a network or DNS server has been compromised by an attacker. Understanding the mechanics of DNS can greatly enhance your ability to use Nmap effectively, particularly in scenarios involving **security assessments** or **troubleshooting**.
