## Introduction to Networking (032026-YWR)

[返回总 README](../README.md)

Networking 有 mock test 截图，以下 “高频” 项目需要优先掌握。

### 高频考点：Mock Test 已覆盖/高度相关

- OSI model 与 TCP/IP model：
  - OSI 7 layers 顺序与功能。
  - TCP/IP model layers 与 OSI mapping。
  - PDU names：data、segment、packet、frame、bits。
  - encapsulation / de-encapsulation。
- protocols and standards：
  - protocol 的作用：addressing、reliability、flow control、sequencing、error detection。
  - standards bodies：IETF、ICANN、IEEE、IANA 等。
- IPv4 addressing and subnetting：
  - network portion / host portion。
  - subnet mask 与 prefix notation。
  - 给定 IP + mask，计算 network address、broadcast address、first/last usable host、number of hosts。
  - 判断两个 IP 是否在同一 subnet。
  - default gateway 的作用。
- Ethernet / MAC / ARP：
  - MAC address 长度、格式、作用。
  - frame basics。
  - ARP：IPv4 address 到 MAC address 的解析。
  - ARP table / ARP cache。
- switching basics：
  - switch 依据 MAC address table 转发。
  - unknown unicast / broadcast / flooding。
  - collision domain 与 broadcast domain。
- transport layer：
  - TCP vs UDP。
  - TCP reliable delivery、acknowledgement、sequence number、flow control。
  - UDP connectionless、low overhead、best effort。
  - port number 的作用。
- application layer protocols and ports：
  - HTTP 80、HTTPS 443。
  - FTP control 21 / data 20。
  - SMTP 25、POP3 110、IMAP 143。
  - DNS 53。
  - DHCP 67/68。
  - SSH 22、Telnet 23。
- DHCP：
  - DHCP Discover、Offer、Request、ACK。
  - DHCP 分配 IPv4 address、subnet mask、gateway、DNS。
  - static vs dynamic addressing。
- DNS：
  - FQDN 到 IP address 的解析。
  - records：A、AAAA、NS、MX。
  - `nslookup` 用途。
- small network troubleshooting：
  - `ping`、`tracert`/`traceroute`。
  - `ipconfig`/`ifconfig`。
  - `arp -a`。
  - Cisco show commands：`show running-config`、`show interfaces`、`show ip interface brief`、`show arp`、`show ip route`、`show protocols`、`show version`。
- network security basics：
  - 常见 threat：malware、unauthorized access、DoS、data theft。
  - security controls：firewall、ACL、authentication、encryption、patching、backup。

### Chapter-by-Chapter 考点

#### Chapter 1: Networking Today

- network components：
  - end devices：PC、server、printer、IP phone。
  - intermediary devices：switch、router、wireless AP、firewall。
  - network media：copper、fiber、wireless。
- host roles：client、server、peer-to-peer。
- LAN vs WAN：
  - LAN limited area, usually single organization。
  - WAN larger geographic area, connects LANs, often service provider managed。
- internet / intranet / extranet。
- network representations：
  - NIC、physical port、interface。
  - physical topology vs logical topology。
- reliable network characteristics：
  - fault tolerance、scalability、QoS、security。
- trends：BYOD、cloud、online collaboration、video communication。

#### Chapter 2: Protocols and Models

- communication rules：
  - message encoding、formatting、size、timing、delivery option。
  - unicast、multicast、broadcast。
- protocol suite 的概念。
- OSI model layer functions。
- TCP/IP model layer functions。
- data encapsulation process。
- local vs remote communication：
  - local network 用 MAC 直接交付。
  - remote network 交给 default gateway。

#### Chapter 3: IPv4

- IPv4 dotted decimal 与 binary conversion。
- subnet mask 的意义。
- network, host, broadcast address。
- private IPv4 ranges：
  - `10.0.0.0/8`
  - `172.16.0.0/12`
  - `192.168.0.0/16`
- public vs private IP。
- unicast、broadcast、multicast。
- APIPA：`169.254.0.0/16`。
- subnetting 必练：
  - `/24`、`/25`、`/26`、`/27`、`/28`、`/29`、`/30`
  - block size
  - usable host count: `2^host_bits - 2`

#### Chapter 4: Physical Layer

- physical layer function：传输 bits。
- bandwidth、throughput、goodput。
- copper media：
  - UTP、STP、coaxial。
  - EMI/RFI、crosstalk。
- fiber media：
  - light pulses、long distance、high bandwidth。
  - single-mode vs multimode basic difference。
- wireless media：
  - radio frequency。
  - interference、coverage、security concern。
- encoding/signaling 的基本概念。

#### Chapter 5: Data Link Layer

- data link layer function：
  - framing
  - media access control
  - error detection
- LLC vs MAC sublayers。
- frame fields：header、data、trailer。
- access control methods：
  - contention-based
  - controlled access
- topology：
  - physical topology
  - logical topology
- WAN data link basics。

#### Chapter 6: Ethernet

- Ethernet frame 与 MAC address。
- MAC address：48-bit / 12 hex digits。
- destination MAC / source MAC。
- switch MAC address table learning：
  - source MAC 学习。
  - destination MAC 查表转发。
  - unknown destination flooding。
- ARP request 是 broadcast，ARP reply 是 unicast。
- Ethernet switching forwarding methods：
  - store-and-forward
  - cut-through
- auto-MDIX、duplex、speed 等基础概念。

#### Chapter 7: IPv6

- IPv6 address 长度：128-bit。
- hexadecimal notation，colon-separated。
- zero compression：
  - leading zero 可省略。
  - consecutive zero groups 可用 `::`，但只能用一次。
- IPv6 address types：
  - global unicast
  - link-local
  - multicast
  - anycast
- IPv6 没有 broadcast。
- prefix length，例如 `/64`。
- SLAAC、DHCPv6、router advertisement 的基本概念。
- IPv4 vs IPv6 差异。

#### Chapter 8: Transport Layer

- transport layer responsibilities：
  - tracking individual conversations
  - segmentation and reassembly
  - identifying applications via port numbers
  - multiplexing
- TCP：
  - connection-oriented
  - reliable
  - ordered delivery
  - flow control
  - three-way handshake
- UDP：
  - connectionless
  - no guarantee
  - lower overhead
  - used for DNS, DHCP, streaming, VoIP 等场景。
- port ranges：
  - well-known ports: 0-1023
  - registered ports: 1024-49151
  - dynamic/private ports: 49152-65535

#### Chapter 9: Application Layer

- application / presentation / session layer in OSI 对应 TCP/IP application layer。
- client-server model vs peer-to-peer。
- HTTP methods：GET、POST、PUT。
- email protocols：
  - SMTP send mail。
  - POP retrieve and usually remove from server。
  - IMAP retrieve while keeping mail on server。
- DNS hierarchy 与 DNS message sections。
- DHCP operation。
- FTP two connections：control and data。
- SMB file/printer sharing。

#### Chapter 10: Build a Small Network

- small network topology and device selection。
- IP addressing plan。
- redundancy and traffic management。
- QoS concept。
- verifying connectivity：
  - ping
  - extended ping
  - traceroute/tracert
- network baseline。
- host commands and Cisco IOS show commands。
- troubleshooting methodology：
  1. identify the problem
  2. establish theory
  3. test theory
  4. establish plan and implement
  5. verify and prevent
  6. document findings
- common scenarios：
  - wrong IP/subnet mask
  - wrong/missing default gateway
  - DHCP issue
  - APIPA address

#### Chapter 11: Network Security Fundamentals

- security goals：confidentiality、integrity、availability。
- threat actors and attacks。
- malware types and social engineering basics。
- access control and authentication。
- firewall, ACL, VPN, encryption basics。
- device hardening：
  - strong passwords
  - disable unused services
  - update/patch
  - backup
  - secure remote access with SSH instead of Telnet。

## 推荐教程与覆盖判断

### 结论

Networking 最重要的是跟 mock test 对齐：OSI/TCP-IP、IPv4 subnetting、Ethernet/MAC/ARP、TCP/UDP、DNS/DHCP、常见端口、troubleshooting commands。视频可以帮你理解，但必须自己刷 subnetting 题。

### B站视频

- [王道 计算机网络 速成](https://search.bilibili.com/all?keyword=%E7%8E%8B%E9%81%93%20%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%BD%91%E7%BB%9C%20%E9%80%9F%E6%88%90)：适合补 OSI、TCP/IP、数据链路层、网络层、传输层。
- [子网划分 IP 地址 速成](https://search.bilibili.com/all?keyword=%E5%AD%90%E7%BD%91%E5%88%92%E5%88%86%20IP%E5%9C%B0%E5%9D%80%20%E9%80%9F%E6%88%90)：必须看，mock test 高概率考计算。
- [Cisco Packet Tracer 入门](https://search.bilibili.com/all?keyword=Cisco%20Packet%20Tracer%20%E5%85%A5%E9%97%A8)：适合理解小型网络、路由器、交换机、IP 配置。
- [ARP MAC Ethernet 交换机 B站搜索](https://search.bilibili.com/all?keyword=ARP%20MAC%20Ethernet%20%E4%BA%A4%E6%8D%A2%E6%9C%BA)：补 mock test 里常见的 MAC/ARP/switching。

### YouTube 视频

- [Computer Networking full course OSI TCP/IP subnetting](https://www.youtube.com/results?search_query=computer+networking+full+course+OSI+TCP+IP+subnetting)：系统复习网络基础。
- [Subnetting tutorial for beginners](https://www.youtube.com/results?search_query=subnetting+tutorial+for+beginners)：专攻子网划分。
- [Cisco CCNA basics OSI IPv4 Ethernet](https://www.youtube.com/results?search_query=Cisco+CCNA+basics+OSI+IPv4+Ethernet)：与你的 Cisco 风格课件比较接近。

### 文字教程/博客

- [Cisco Networking Basics](https://www.netacad.com/courses/networking-basics)：与课程体系最接近。
- [GeeksforGeeks Computer Network Tutorial](https://www.geeksforgeeks.org/computer-network-tutorials/)：适合查 OSI、TCP/UDP、IP、DNS、DHCP 等概念。
- [Practical Networking Subnetting](https://www.practicalnetworking.net/series/subnetting/subnetting/)：子网划分讲得很清楚。

### 最短学习路线

1. 先刷 subnetting：network address、broadcast、usable range、host count。
2. 背 OSI/TCP-IP layer order、PDU、encapsulation。
3. 背常见协议端口：HTTP/HTTPS/FTP/SMTP/POP3/IMAP/DNS/DHCP/SSH/Telnet。
4. 看 mock test 截图，把每道错题对应回 lecture chapter。
5. 考前复习 troubleshooting commands：`ping`、`tracert`、`ipconfig`、`arp -a`、Cisco `show` commands。
