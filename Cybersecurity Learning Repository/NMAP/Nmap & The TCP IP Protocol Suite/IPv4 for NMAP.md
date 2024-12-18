# IPv4 for Nmap

## Overview of TCP/IP v4:
- **TCP/IP Protocol Suite**:
  - IP, TCP, UDP, ICMP protocols
  - Local & remote IP addressing
  - How Nmap integrates with TCP/IP v4

## IP Addressing:
- **Binary to Decimal Conversion**
  - In IP addressing, numbers are typically presented in their decimal form, such as 192.168.1.1. There are four groups of numbers separated by decimal points. These numbers are interpreted by network devices in their binary form. Each group is referred to as an octet. It is called an octet because the maximum value in each group is two to the power of eight minus one, since zero can also be used as a value. In other words, the maximum value assignable to each octet is 255. In binary, 255 is represented as 11111111, or eight ones. Most of you are already familiar with this, so I won’t delve into too much more detail.
- **Structure**: Composed of 4 octets.
- **Subnetting**: Understanding Subnets and Their Role in Networking

  The process of subnetting is often one of the first mathematical challenges that network administrators must master—it’s a rite of passage. At its core, subnetting is simply an addressing methodology that allows network administrators to determine which part of an IP address designates the network and which part identifies the host. This is achieved by assigning a combination of an IP address and a subnet mask.

  On many LANs, a common subnet mask for each VLAN is 255.255.255.0. This mask indicates that the first three octets of the IP address define the network, while the fourth octet specifies the host. All devices on the same VLAN will share the same first three octets, such as 192.168.1, and each device will have a unique and distinct fourth octet.

  In Nmap, it is helpful to understand private addressing schemes and how to identify the network you are scanning from. On a Windows system, you can find your network details by running ipconfig in the Command Prompt and checking your IP address and subnet mask. On Linux, Unix, and macOS, you can determine this by running ifconfig from a terminal.

  One particularly important point in Nmap is understanding how to determine a device’s physical or MAC address. This can only be done when your scanning station is on the same network as the target device. In other words, there is no way to determine the MAC address of a remote host unless you have administrative privileges on the router or switch to which the device is connected. The sole exception to this rule is when your scanning station is connected to a span or mirrored port.
- **CIDR Notation**:
  - **What is CIDR?**  
    CIDR, short for Classless Inter-Domain Routing, simplifies IP addressing by combining an IP address with a `/` followed by a number that represents the network portion of the address (also known as the subnet mask).

    For example, 192.168.1.0/24 indicates that 24 bits of the IP address are allocated for the network portion. This notation is a concise and flexible way to define networks without being confined to traditional class-based IP address schemes.
    
  - Example: `192.168.1.0/24` indicates 24 bits are used for the network portion.

## Name Resolution:
- **DNS**: Resolving human-readable names into IP addresses.
- **Nmap & Name Resolution**: How Nmap utilizes DNS for scanning.


