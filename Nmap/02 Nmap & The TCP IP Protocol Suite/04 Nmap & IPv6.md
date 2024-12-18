## Nmap & IPv6

In your Nmap scanning, you may come across local or remote targets that are configured exclusively with IPv6. Unless your scanning station is correctly set up, you won't be able to run Nmap scans against these targets. This lesson focuses on the key aspects of running Nmap scans against IPv6 targets.

Here are the learning objectives for this lesson: First, we'll explore some general IPv6 information related to Nmap. Next, we'll discuss Nmap's requirements for using IPv6. Finally, we'll review the command-line options you need to be familiar with in order to perform Nmap scans against IPv6 targets.

### General Nmap & IPv6 Information

- **Nmap has supported IPv6 since 2002.**
- **IPv6 scanning works with Nmap's most popular features:**  
  Most of Nmap's scanning features work seamlessly with IPv6 addresses. For instance, **TCP-only ping scanning**, **connect scanning**, and **service and application version detection** are all fully supported when using IPv6.

- **Best to use hostname instead of address for simplicity:**  
  One of the most important pieces of advice I can offer is to run Nmap scans against IPv6 targets using their **hostname** rather than their **IPv6 address**. The reason for this is simple: IPv6 addresses are much longer and more complicated to type. I'll go over the syntax in more detail later.

- **Output looks the same:**  
  When you run your IPv6 scans, you'll find that the output looks exactly the same as with IPv4 scans. The only difference is that you'll see an **IPv6 address** at the top of your scan results. This is helpful because, once you become familiar with reading Nmap scan results, the difference between IPv4 and IPv6 scans is minimal. I've included a screenshot here from an IPv6 scan, with the address highlighted for clarity:

  ![image](https://github.com/user-attachments/assets/1ec46c36-6b06-4ef9-a892-e6a224973fcd)

---

### Nmap IPv6 Requirements

Here are some requirements for running scans against IPv6 targets.

- **Source and target must be configured for IPv6:**  
  First, both your scanning station and your target must be configured for IPv6. When scanning a local network, this usually isn't an issue—you can scan **link-local** or **site-local addresses** without any problems.

- **If your ISP doesn't provide IPv6, use a tunnel broker service:**  
  However, when scanning a remote host, you might encounter more challenges. Even if both your scanning station and the remote target are configured with IPv6, your scan may fail. This could be due to your ISP not providing you with an IPv6 address, or your router or firewall not being configured to support IPv6. In other words, your Nmap scanning station must be able to successfully route to your target using IPv6. If your ISP hasn't provided an IPv6 address, you can use a **tunnel broker service**. There are many good and free services available that will allow you to set up an account and configure your computer or internet access device with IPv6 routing capabilities. The last bullet point on this slide provides a link to a good tunnel broker service, but feel free to search for others and try them out.

- **Another approach is by using 6-to-4 tunnelling:**  
  Another way to achieve this is by using **6to4 IPv6 tunnelling**, as described in **RFC 3036**. This method enables the encapsulation of IPv6 packets into IPv4 for transport across an IPv6 network. For those using **Cisco devices**, this is essentially done through **dual stacking**, which is relatively easy to set up.

- **Free service:**  
  [tunnelbroker.net](https://www.tunnelbroker.net)

---

### Command-Line Syntax & Important Options

Here are the command-line options for using IPv6 with Nmap.

- **`Nmap -6 <target>` or `Nmap --ipv6 <target>`:**  
  As mentioned earlier, when running an Nmap scan against a target that uses IPv6, you simply need to add the `-6` option. Alternatively, you can use `--ipv6` if you prefer to type out the option.

- **`nmap -6 -S <source> <target>`**  
  The `-S` option allows you to specify the **source address** other than your own, which is **IPv6 spoofing**. This lets you set a source address different from your own for the scan.

- **`nmap -6 --hop-limit`**  
  The `--hop-limit` option sets the **hop limit** field in packets sent from your scanning station. This determines how long datagrams are allowed to exist on the network and represents the number of hops a packet can take before being dropped. It works similarly to **TTL (Time-to-Live)** in IPv4.

- For more details, visit:  
  [nmap.org/book/nping-man-ip6-options.html](https://nmap.org/book/nping-man-ip6-options.html)  
  This online Nmap book offers additional IPv6 command-line options for those interested in learning more.
