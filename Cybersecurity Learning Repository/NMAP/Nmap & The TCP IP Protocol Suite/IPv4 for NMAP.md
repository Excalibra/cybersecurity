# IPv4 for Nmap

## Overview of TCP/IP v4:
- **TCP/IP Protocol Suite**:
  - IP, TCP, UDP, ICMP protocols
  - Local & remote IP addressing
  - How Nmap integrates with TCP/IP v4

## IP Addressing:
- **Binary to Decimal Conversion**
  - In IP addressing, numbers are usually seen in their decimal forms, such as 192.168.1.1. There are four sets of numbers separated by decimal points. These numbers are read by network devices in
their binary form. Each set is called an octet. It's called an octet because the maximum value in each set is two to the eighth power minus one, because zero can be assigned as a value. In other words, 255 is the maximum value that can be assigned in each octet. 255 in binary is 11111111 or eight ones. Most of you have knowledge
and experience with this, so I'm not going to go into too much more detail about it.
- **Structure**: Composed of 4 octets.
- **Subnetting**: Understanding subnets and their role in networking.
- **CIDR Notation**:
  - **What is CIDR?**  
    IP address followed by `/` and a number representing the network portion of the address (subnet mask).
  - Example: `192.168.1.0/24` indicates 24 bits are used for the network portion.

## Name Resolution:
- **DNS**: Resolving human-readable names into IP addresses.
- **Nmap & Name Resolution**: How Nmap utilizes DNS for scanning.
