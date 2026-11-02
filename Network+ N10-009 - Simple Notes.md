# CompTIA Network+ (N10-009) – Simple Notes
*Follows the Professor Messer N10-009 course order, from domain 1.0 to 5.0. Every term has a definition and an example (📌).*

| Domain | Weight |
|---|---|
| 1.0 Networking Concepts | 23% |
| 2.0 Network Implementation | 20% |
| 3.0 Network Operations | 19% |
| 4.0 Network Security | 14% |
| 5.0 Network Troubleshooting | 24% |

Exam: up to 90 questions, 90 minutes, passing score 720/900. Includes performance-based questions (PBQs).

---

## 1.0 NETWORKING CONCEPTS

### 1.1 OSI Model
**"Please Do Not Throw Sausage Pizza Away"** (Layer 1 → 7)

| # | Layer | What it does | Example | Data unit |
|---|---|---|---|---|
| 7 | Application | What the user's app talks to | HTTP, DNS, FTP | Data |
| 6 | Presentation | Encryption, formatting | SSL/TLS, JPEG | Data |
| 5 | Session | Opens and closes conversations | RPC, control protocols | Data |
| 4 | Transport | Ports, reliability | TCP, UDP | Segment / Datagram |
| 3 | Network | IP addresses, routing | IP, routers | Packet |
| 2 | Data Link | MAC addresses, switching | Switches, Ethernet | Frame |
| 1 | Physical | Cables, signals | Cables, hubs | Bits |

- **Encapsulation** – adding a header at each layer as data goes down the stack. **Decapsulation** – removing them going up.
  📌 Your web request gets a TCP header (L4), then an IP header (L3), then an Ethernet frame (L2) before it leaves your PC.
- **Troubleshooting with OSI** – start at Layer 1 and work up.
  📌 Check that the cable is plugged in (L1) before blaming DNS (L7).

### 1.2 Network Appliances & Functions
- **Router** – connects *different* networks and forwards traffic using IP addresses (Layer 3).
  📌 Your home router connects your 192.168.1.0 network to the internet.
- **Switch** – connects devices *inside* one network using MAC addresses (Layer 2).
  📌 A 24-port switch connecting all PCs and printers in one office.
- **Layer 3 switch** – a switch that can also route between VLANs.
  📌 A core switch routing between the HR VLAN and the Sales VLAN.
- **Firewall** – allows or blocks traffic based on rules.
  📌 A rule blocking all incoming traffic except HTTPS (port 443) to the web server.
- **NGFW (Next-Gen Firewall)** – a firewall that understands applications (Layer 7).
  📌 Blocking Facebook games while still allowing Facebook messaging.
- **IDS (Intrusion Detection System)** – watches traffic and *alerts* on attacks.
  📌 Sends an email to IT when it sees a port scan.
- **IPS (Intrusion Prevention System)** – watches traffic and *blocks* attacks.
  📌 Automatically drops packets matching a known exploit.
- **Load balancer** – spreads traffic across several servers.
  📌 Amazon sends shoppers to 50 different web servers so none gets overloaded.
- **Proxy** – makes requests to websites on behalf of users (filtering, caching).
  📌 A school proxy that blocks gaming sites and caches popular pages.
- **NAS (Network Attached Storage)** – file-level storage shared over the network.
  📌 A Synology box holding a shared "Documents" folder.
- **SAN (Storage Area Network)** – block-level storage that looks like a local drive to servers.
  📌 A database server whose D: drive actually lives on a SAN.
- **Wireless AP (Access Point)** – lets Wi-Fi devices join the wired network.
  📌 The ceiling-mounted Wi-Fi device in a classroom.
- **Wireless LAN controller** – manages many APs from one place.
  📌 Changing the Wi-Fi password on 200 campus APs at once.
- **CDN (Content Delivery Network)** – copies content to servers close to users.
  📌 Netflix serves you video from a server in your city, not California.
- **VPN (Virtual Private Network)** – an encrypted tunnel over the internet.
  📌 Working from home and securely reaching company file shares.
- **QoS (Quality of Service)** – gives priority to important traffic.
  📌 Zoom calls get priority over someone downloading a big file.
- **TTL (Time to Live)** – a counter that drops by 1 at each router; packet is discarded at 0, so it can't loop forever.
  📌 A packet starts with TTL 64; after 64 hops it is thrown away.
- **Physical vs. virtual appliance** – a hardware box vs. the same function running as software.
  📌 A physical Palo Alto firewall vs. a Palo Alto VM running in AWS.

### 1.3 Cloud Concepts
- **NFV (Network Functions Virtualization)** – running network devices as virtual machines.
  📌 Running a virtual router on a VMware server instead of buying a Cisco box.
- **VPC (Virtual Private Cloud)** – your own private, isolated network inside a public cloud.
  📌 An AWS VPC with the range 10.0.0.0/16 for your company's servers.
- **Network security group** – firewall rules attached to cloud resources.
  📌 An Azure rule allowing only port 22 from your office IP to a VM.
- **Network security list** – firewall rules applied to a whole cloud subnet.
  📌 Blocking all inbound traffic to the "database" subnet.
- **Internet gateway** – lets cloud resources talk to the internet both ways.
  📌 A public web server in AWS reachable from anywhere.
- **NAT gateway** – lets private cloud resources reach the internet *outbound only*.
  📌 A private database server downloading updates but not reachable from outside.
- **VPN connection (cloud)** – encrypted tunnel from your office to the cloud over the internet.
  📌 Office firewall builds an IPsec tunnel to Azure.
- **Direct Connect** – a private, dedicated line to the cloud provider (not over the internet).
  📌 A bank leasing a fiber link straight into AWS.
- **Public cloud** – shared provider infrastructure available to anyone.
  📌 AWS, Azure, Google Cloud.
- **Private cloud** – cloud infrastructure used by one organization only.
  📌 A hospital running its own OpenStack cloud in its data center.
- **Hybrid cloud** – mix of public and private.
  📌 Customer records stay on-site; the website runs in AWS.
- **SaaS (Software as a Service)** – you just use the finished app.
  📌 Gmail, Microsoft 365, Salesforce.
- **PaaS (Platform as a Service)** – you bring the code; the provider runs the platform.
  📌 Deploying a Flask app to Heroku or Google App Engine.
- **IaaS (Infrastructure as a Service)** – you rent servers/storage and manage the OS yourself.
  📌 Launching an AWS EC2 Linux server.
- **Scalability** – ability to grow to handle more load.
  📌 Adding more servers before Black Friday.
- **Elasticity** – automatically growing *and* shrinking with demand.
  📌 Servers go from 5 to 50 during a sale, then back to 5 at night.
- **Multitenancy** – many customers share the same hardware, kept separate.
  📌 Your VM and another company's VM run on the same AWS host.

### 1.4 Ports & Protocols (MEMORIZE)

| Port | Protocol | What it does | Example |
|---|---|---|---|
| 20/21 | FTP | File transfer (20 = data, 21 = control) | Uploading website files with FileZilla |
| 22 | SSH / SFTP | Secure remote login / file transfer | `ssh admin@10.0.0.1` |
| 23 | Telnet | Insecure remote login (plain text) | Old switch config (avoid!) |
| 25 | SMTP | Sending email between servers | Mail server relaying an email |
| 53 | DNS | Name → IP (UDP & TCP) | google.com → 142.250.x.x |
| 67/68 | DHCP | Auto IP assignment (67 server, 68 client) | Laptop gets an IP on Wi-Fi |
| 69 | TFTP | Simple file transfer, no login (UDP) | Switch downloading its config file |
| 80 | HTTP | Unencrypted web | http://example.com |
| 123 | NTP | Time sync (UDP) | PCs syncing clocks to time.windows.com |
| 161/162 | SNMP | Monitoring (161 queries, 162 traps) | Tool checks router CPU usage |
| 389 | LDAP | Directory lookups | Looking up users in Active Directory |
| 443 | HTTPS | Encrypted web | Online banking |
| 445 | SMB | Windows file/printer sharing | `\\server\shared` |
| 514 | Syslog | Sending logs (UDP) | Firewall logs going to a log server |
| 587 | SMTP (TLS) | Secure email submission | Outlook sending your email |
| 636 | LDAPS | Encrypted LDAP | Secure Active Directory queries |
| 1433 | MS SQL | Microsoft database | App connecting to SQL Server |
| 3389 | RDP | Windows remote desktop | Remote into a Windows server |
| 5060/5061 | SIP | VoIP call setup (5061 = encrypted) | Office desk phones making calls |

- **ICMP** – error and test messages. 📌 `ping` and `traceroute`.
- **GRE** – a simple, unencrypted tunnel. 📌 Carrying routing traffic between two sites.
- **IPsec** – encrypts IP traffic. **AH** = integrity only; **ESP** = encryption + integrity. **IKE** = sets up the keys.
  📌 Site-to-site VPN between two offices.
- **TCP** – connection-oriented, reliable, uses a 3-way handshake (SYN → SYN/ACK → ACK).
  📌 Loading a webpage or downloading a file – every byte must arrive.
- **UDP** – connectionless, fast, no delivery guarantee.
  📌 Video calls, online gaming, DNS lookups.
- **Unicast** – one to one. 📌 Your PC loading a website.
- **Multicast** – one to a group that signed up. 📌 IPTV streaming to subscribed devices.
- **Anycast** – to the *nearest* of many servers sharing one IP. 📌 Google DNS 8.8.8.8 answers from the closest location.
- **Broadcast** – one to everyone on the network (IPv4 only). 📌 A DHCP Discover asking "is there a DHCP server?"

### 1.5 Transmission Media & Transceivers
- **802.11** – the Wi-Fi standards. 📌 Your laptop on Wi-Fi 6 (802.11ax).
- **Cellular** – mobile network data. 📌 A 5G hotspot as a backup internet link.
- **Satellite** – internet via satellite; high latency (traditional), lower with LEO. 📌 Starlink at a rural farm.
- **802.3** – the Ethernet (wired) standards. 📌 1000BASE-T = 1 Gbps over copper.
- **UTP (Unshielded Twisted Pair)** – common copper cable, max ~100 m. 📌 Cat 6 cable from your PC to the wall jack.
- **STP (Shielded Twisted Pair)** – copper with shielding against interference. 📌 Cable run next to factory machines.
- **Cable categories** – Cat 5e (1 Gbps), Cat 6 (10 Gbps up to 55 m), Cat 6a (10 Gbps 100 m), Cat 8 (25–40 Gbps, 30 m). 📌 Cat 6a for a new office build.
- **Coax** – round cable with a single copper core. 📌 Cable TV / cable modem internet.
- **Twinax** – short copper cable with transceivers built on, used in data centers. 📌 A 3 m DAC cable between a server and top-of-rack switch.
- **Plenum cable** – fire-resistant jacket, low smoke; required in air-handling spaces. 📌 Cable run above a drop ceiling.
- **Single-mode fiber (SMF)** – thin core, laser light, *long distances* (km). 📌 Connecting two buildings miles apart.
- **Multimode fiber (MMF)** – thicker core, LED light, *short distances* (hundreds of meters). 📌 Fiber between floors in one building.
- **SFP** – small pluggable transceiver, 1 Gbps. 📌 Adding a fiber port to a switch.
- **SFP+** – 10 Gbps version. 📌 10 Gb uplink from an access switch to the core.
- **QSFP / QSFP+** – quad, 40 Gbps+. 📌 Data center spine links.
- **Connectors:**
  - **RJ45** – 8-pin Ethernet. 📌 PC network cable.
  - **RJ11** – 4/6-pin phone. 📌 DSL / landline phone cord.
  - **F-type** – screw-on coax. 📌 Cable modem.
  - **SC** – square push-pull fiber. 📌 Older fiber patch panels.
  - **LC** – small fiber connector ("Little Connector"). 📌 Plugs into an SFP module.
  - **ST** – round twist-lock fiber ("Stick and Twist"). 📌 Legacy campus fiber.
  - **MPO** – many fibers in one connector. 📌 40/100 Gb data center links.

### 1.6 Topologies & Architectures
- **Star (hub-and-spoke)** – all devices connect to a central point. 📌 Every PC plugs into one switch.
- **Mesh** – every device connects to many/all others; very redundant. 📌 Core routers of an ISP all linked together.
- **Hybrid** – a mix of topologies. 📌 Star at each branch, mesh between headquarters routers.
- **Point-to-point** – a direct link between two devices. 📌 A leased line between two offices.
- **Three-tier architecture** – Core (fast backbone) → Distribution (routing/policy) → Access (users plug in). 📌 A large university campus network.
- **Collapsed core** – core and distribution combined into one layer. 📌 A small company with one main switch stack.
- **Spine and leaf** – every leaf switch connects to every spine switch; low, predictable latency. 📌 Modern data centers.
- **North-South traffic** – traffic into or out of the data center. 📌 A user on the internet visiting your website.
- **East-West traffic** – traffic between servers inside the data center. 📌 Web server querying the database server.

### 1.7 IPv4 Addressing
- **Public IP** – routable on the internet. 📌 8.8.8.8.
- **Private IP (RFC 1918)** – used inside networks, not routed on the internet. 📌 Your laptop at 192.168.1.25.
  - 10.0.0.0/8
  - 172.16.0.0/12 (172.16 – 172.31)
  - 192.168.0.0/16
- **APIPA** – self-assigned 169.254.x.x when DHCP fails. 📌 A PC showing 169.254.12.4 = can't reach the DHCP server.
- **Loopback** – 127.0.0.1, the device talking to itself. 📌 `ping 127.0.0.1` tests your network stack.
- **Classes:** A (1–126), B (128–191), C (192–223), D (224–239 multicast), E (240–255 experimental). 📌 10.1.1.1 is Class A; 192.168.1.1 is Class C.
- **Subnet mask** – shows which part of the IP is the network and which part is the host. 📌 255.255.255.0 → first 3 numbers are the network.
- **CIDR** – writing the mask as a slash number. 📌 192.168.1.0/24 = mask 255.255.255.0.
- **VLSM** – using different subnet sizes in one network. 📌 /26 for a 50-person office, /30 for a router-to-router link.

**Subnetting Cheat Sheet**

| CIDR | Mask | Usable hosts |
|---|---|---|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 (point-to-point links) |

- Usable hosts = **2ⁿ − 2** (n = host bits). The −2 is the network ID and the broadcast address.
  📌 **192.168.1.0/26**: network = 192.168.1.0, usable = .1 – .62, broadcast = .63. Next subnet starts at .64.

### 1.8 Modern Network Environments
- **SDN (Software-Defined Networking)** – separates the control plane (decisions) from the data plane (forwarding), managed by a central controller. 📌 Cisco ACI controller pushing rules to every data center switch.
- **SD-WAN** – a smart WAN that picks the best link per application. 📌 A branch sends Zoom over fiber and email over LTE automatically.
- **Zero-touch provisioning** – new devices configure themselves when plugged in. 📌 A branch router ships to a store, gets plugged in, and downloads its config.
- **VXLAN** – stretches Layer 2 networks over a Layer 3 network. 📌 A VM moves between two data centers and keeps its IP.
- **Zero Trust Architecture (ZTA)** – "never trust, always verify"; every request is checked. 📌 Even on the office network, you need MFA to open the HR app.
- **SASE / SSE** – networking and security delivered from the cloud. 📌 Remote workers' traffic goes through Zscaler for filtering.
- **Infrastructure as Code (IaC)** – configure networks with scripts/templates. 📌 An Ansible playbook configuring 100 switches the same way.
- **Configuration drift** – devices slowly changing from the standard config. 📌 Someone manually opens a port on one switch and never documents it.
- **IPv6** – 128-bit hexadecimal addresses. 📌 `2001:0db8:0000:0000:0000:0000:0000:0001` → `2001:db8::1`.
  - `::` replaces one run of zeros (only once). Leading zeros can be dropped.
  - No broadcast (uses multicast instead).
- **SLAAC** – IPv6 devices create their own address automatically. 📌 A phone joins Wi-Fi and builds an IPv6 address from the router's prefix.
- **Dual stack** – running IPv4 and IPv6 at the same time. 📌 Your laptop has both 192.168.1.5 and 2001:db8::5.
- **Tunneling (6to4)** – IPv6 packets carried inside IPv4. 📌 IPv6 traffic crossing an IPv4-only ISP.
- **NAT64** – translates between IPv6 and IPv4. 📌 An IPv6-only phone reaching an IPv4-only website.

---

## 2.0 NETWORK IMPLEMENTATION

### 2.1 Routing
- **Static routing** – routes typed in manually. 📌 `ip route 10.2.0.0 255.255.0.0 192.168.1.2` on a small branch router.
- **Dynamic routing** – routers learn routes from each other automatically. 📌 A link fails and traffic reroutes on its own.
  - **OSPF** – link-state, picks paths by cost. 📌 Routing inside a company campus.
  - **EIGRP** – Cisco's advanced distance-vector protocol. 📌 An all-Cisco enterprise network.
  - **BGP** – path-vector, routes *between* organizations. 📌 Your ISP exchanging routes with other ISPs on the internet.
- **Default route** – where traffic goes when nothing more specific matches (0.0.0.0/0). 📌 Home router sends all unknown traffic to the ISP.
- **Route selection** – most specific prefix wins, then administrative distance, then metric. 📌 A /24 route beats a /16 route to the same address.
- **Administrative distance** – how trusted a route source is; lower is better. 📌 Static (1) beats OSPF (110).
- **FHRP (VRRP / HSRP)** – two routers share a virtual gateway IP; one takes over if the other fails. 📌 PCs use 10.0.0.1, which moves to Router B if Router A dies.
- **NAT** – translates private IPs to public IPs. 📌 Your 192.168.1.10 appears as 73.45.12.8 on the internet.
- **PAT (NAT overload)** – many devices share one public IP using different port numbers. 📌 Every device in your house uses one public IP.
- **Subinterface / router on a stick** – one physical port split into many logical ones, one per VLAN. 📌 G0/0.10 for VLAN 10 and G0/0.20 for VLAN 20.

### 2.2 Switching
- **VLAN** – splits one physical switch into separate logical networks. 📌 VLAN 10 = Staff, VLAN 20 = Guests on the same switch.
- **Native VLAN** – the VLAN for untagged traffic on a trunk (change it from VLAN 1 for security). 📌 Setting native VLAN to 999 (unused).
- **Voice VLAN** – a separate VLAN for VoIP phones. 📌 Phone on VLAN 50, PC plugged into the phone on VLAN 10.
- **802.1Q** – standard for tagging frames with a VLAN ID on trunks. 📌 A frame tagged "VLAN 20" crossing between switches.
- **Access port** – carries one VLAN, connects end devices. 📌 Port 5 for a printer on VLAN 10.
- **Trunk port** – carries many VLANs between switches/routers. 📌 Uplink from an access switch to the core.
- **Link aggregation (LACP)** – bundles several ports into one faster, redundant link. 📌 Four 1 Gbps ports acting as one 4 Gbps link.
- **Spanning Tree Protocol (STP, 802.1D)** – blocks redundant paths to stop switching loops. 📌 Two cables between switches – STP blocks one until the other fails.
- **MTU** – largest frame size allowed (1500 bytes standard). 📌 VPN overhead causes fragmentation if MTU is too big.
- **Jumbo frames** – frames up to ~9000 bytes. 📌 Used on storage (iSCSI) networks for efficiency.
- **Speed / duplex** – link speed and whether it sends and receives at the same time (full) or takes turns (half). 📌 One side full, other side half = duplex mismatch → slow link and errors.

### 2.3 Wireless

| Standard | Name | Band | Example |
|---|---|---|---|
| 802.11a | – | 5 GHz | Very old business Wi-Fi |
| 802.11b/g | – | 2.4 GHz | Old home routers |
| 802.11n | Wi-Fi 4 | 2.4 / 5 GHz | 2010-era routers |
| 802.11ac | Wi-Fi 5 | 5 GHz | Common home routers |
| 802.11ax | Wi-Fi 6 / 6E | 2.4 / 5 / 6 GHz (6E) | Newest laptops and phones |

- **2.4 GHz** – longer range, slower, more interference. Non-overlapping channels: **1, 6, 11**. 📌 Three APs in a hallway set to 1, 6 and 11.
- **5 GHz** – faster, shorter range, more channels. 📌 Streaming 4K in the same room as the router.
- **Channel width** – how much spectrum a channel uses; wider = faster but more interference. 📌 80 MHz in a house, 20 MHz in a crowded office.
- **SSID** – the Wi-Fi network name. 📌 "Starbucks WiFi".
- **BSSID** – the MAC address of an AP's radio. 📌 aa:bb:cc:11:22:33.
- **ESSID** – one SSID across many APs so users can roam. 📌 "eduroam" across a whole campus.
- **Ad hoc** – devices connect directly with no AP. 📌 Two laptops sharing files.
- **Infrastructure mode** – devices connect through an AP. 📌 Normal home Wi-Fi.
- **Mesh** – APs connect wirelessly to each other to extend coverage. 📌 Eero or Google Nest Wi-Fi.
- **Omnidirectional antenna** – signal in all directions. 📌 AP in the middle of an office.
- **Directional antenna** – focused beam in one direction. 📌 Yagi antenna linking two buildings.
- **WPA2** – Wi-Fi security using AES. 📌 Most home routers.
- **WPA3** – newest, strongest Wi-Fi security (SAE replaces the PSK handshake). 📌 New routers' default setting.
- **Personal (PSK)** – everyone uses one shared password. 📌 Home Wi-Fi password.
- **Enterprise (802.1X)** – each user logs in with their own credentials via RADIUS. 📌 Logging into campus Wi-Fi with your university username.
- **Captive portal** – a web page you must accept/login to before getting access. 📌 Hotel or airport Wi-Fi login page.
- **Autonomous AP** – configured one by one. 📌 A single home router.
- **Lightweight AP** – managed by a wireless controller. 📌 Hundreds of Cisco APs in a hospital.

### 2.4 Physical Installations
- **Rack unit (U)** – 1U = 1.75 inches of rack height. 📌 A 2U server takes 3.5 inches.
- **Patch panel** – organizes copper cables in a rack. 📌 Wall jacks terminate at a patch panel, then patch cables go to the switch.
- **Fiber distribution panel** – the same thing for fiber. 📌 Building-to-building fiber terminates here.
- **IDF (Intermediate Distribution Frame)** – a wiring closet on each floor. 📌 The 3rd-floor network closet.
- **MDF (Main Distribution Frame)** – the main wiring room where the ISP connects. 📌 Basement server room.
- **UPS** – battery backup for short outages. 📌 Keeps the router running for 20 minutes during a blackout.
- **PDU** – power strip for racks, often remotely managed. 📌 Rebooting a server by turning off its PDU outlet.
- **Generator** – long-term backup power. 📌 Hospital diesel generator.
- **Hot aisle / cold aisle** – racks face so cold air enters the front and hot air exits the back. 📌 Data center rows alternate cold and hot aisles.
- **Fire suppression** – puts out fires without water damage. 📌 Clean-agent gas system in a server room.
- **Humidity control** – too dry = static; too wet = corrosion. 📌 Dehumidifier in a server room.

---

## 3.0 NETWORK OPERATIONS

### 3.1 Documentation & Processes
- **Physical diagram** – shows where devices and cables actually are. 📌 Floor plan showing switch locations.
- **Logical diagram** – shows how traffic flows (IPs, VLANs, routing). 📌 Diagram showing VLAN 10 and VLAN 20 connected to a router.
- **Rack diagram** – what sits in each rack unit. 📌 "U1–U2 firewall, U3 switch, U4–U5 server".
- **Cable map** – which cable goes where. 📌 Patch panel port 12 → office 204 wall jack.
- **Layer 1/2/3 diagrams** – diagrams showing cables (L1), switches/VLANs (L2), routing/IPs (L3).
- **Asset inventory** – list of hardware, software, licenses, warranties. 📌 Spreadsheet of every switch with serial number and warranty date.
- **IPAM (IP Address Management)** – tracks which IPs are used. 📌 Infoblox shows 10.0.5.20 is assigned to the printer.
- **SLA (Service Level Agreement)** – promise of service level from a provider. 📌 ISP guarantees 99.9% uptime.
- **Wireless survey / heat map** – maps Wi-Fi signal strength. 📌 Red zones near the lobby, blue (weak) zones in the warehouse.
- **EOL (End of Life)** – the vendor stops selling the product. 📌 A switch model is discontinued.
- **EOS (End of Support)** – the vendor stops patches and support. 📌 No more security updates → replace it.
- **Decommissioning** – safely removing a device. 📌 Wiping configs before recycling a router.
- **Change management** – formal process: request → approve → test → implement → document, with a **rollback plan**. 📌 Submitting a ticket to change a firewall rule on Saturday night.
- **Production config** – what's running now. 📌 `show running-config`.
- **Backup config** – a saved copy to restore. 📌 Nightly config backup to a server.
- **Baseline / golden config** – the approved standard config. 📌 Template every new switch must match.

### 3.2 Monitoring
- **SNMP** – protocol to monitor and manage devices. 📌 PRTG polling a switch for bandwidth.
  - **v1/v2c** – use community strings, no encryption. 📌 Community string "public" (insecure default).
  - **v3** – adds authentication and encryption. 📌 Use this on the exam's "secure" answer.
  - **MIB** – database of what can be monitored. 📌 A list of a router's monitorable values.
  - **OID** – the ID of one item in the MIB. 📌 1.3.6.1.2.1.1.3 = system uptime.
  - **Trap** – the device sends an alert on its own. 📌 Switch sends a trap when a port goes down.
- **Flow data (NetFlow)** – summary of who talks to whom and how much. 📌 Shows one PC uploading 50 GB to an unknown IP.
- **Packet capture** – copies full packets for analysis. 📌 Capturing traffic in Wireshark to see failed logins.
- **Port mirroring (SPAN)** – copies one switch port's traffic to another port. 📌 Mirroring the firewall port to an IDS.
- **Baseline** – what "normal" performance looks like. 📌 Normal is 30% bandwidth; today is 95% → investigate.
- **Anomaly detection** – alerting when something differs from the baseline. 📌 Traffic at 3 AM from a server that's usually idle.
- **Syslog** – sends logs to a central server. Severity 0 (Emergency) → 7 (Debug). 📌 All routers send logs to one Syslog server.
- **SIEM** – collects and correlates logs from everywhere and alerts. 📌 Splunk links 50 failed logins + VPN from another country.
- **API integration** – tools sharing data automatically. 📌 A monitoring tool opens a ServiceNow ticket when a link goes down.
- **Metrics** – temperature, CPU, memory, bandwidth, latency, jitter, uptime. 📌 Alert if the router CPU stays above 90%.

### 3.3 Disaster Recovery
- **RPO (Recovery Point Objective)** – max *data* you can afford to lose. 📌 Backups every 4 hours → RPO = 4 hours.
- **RTO (Recovery Time Objective)** – max *time* until you're back online. 📌 "Email must be back within 2 hours."
- **MTTR (Mean Time to Repair)** – average time to fix something. 📌 Switch failures take 1 hour to fix on average.
- **MTBF (Mean Time Between Failures)** – average time a device runs before failing. 📌 A drive rated at 1,000,000 hours.
- **Cold site** – empty space with power; slowest. 📌 Rented empty office; bring your own servers.
- **Warm site** – some equipment ready, needs data restored. 📌 Servers installed, but backups must be loaded.
- **Hot site** – fully running copy, ready immediately; most expensive. 📌 Second data center with live data replication.
- **Active-active** – both systems handle traffic at once. 📌 Two data centers both serving users.
- **Active-passive** – one system waits as backup. 📌 Backup firewall takes over only if the main fails.
- **Tabletop exercise** – team talks through a disaster scenario. 📌 "Ransomware hit – what do we do?" meeting.
- **Validation test** – actually test the recovery. 📌 Restoring last night's backup to make sure it works.

### 3.4 IPv4 & IPv6 Network Services
- **DHCP** – automatically gives devices IP settings. **DORA** = Discover → Offer → Request → Acknowledge. 📌 Your phone gets an IP the moment it joins Wi-Fi.
  - **Scope** – range of addresses to hand out. 📌 192.168.1.100 – 192.168.1.200.
  - **Lease time** – how long a device keeps the IP. 📌 8 hours at a coffee shop.
  - **Exclusion** – addresses DHCP won't give out. 📌 .1 – .20 saved for servers.
  - **Reservation** – a device always gets the same IP (by MAC). 📌 The printer always gets 192.168.1.50.
  - **Options** – extra settings like gateway and DNS. 📌 Option 3 = gateway, option 6 = DNS.
  - **DHCP relay / IP helper** – forwards DHCP requests to a server on another network. 📌 Router forwards requests from VLAN 20 to the DHCP server on VLAN 10.
- **SLAAC** – IPv6 auto-addressing without DHCP. 📌 Device builds its IPv6 address from the router advertisement.

| DNS Record | Purpose | Example |
|---|---|---|
| A | Name → IPv4 | example.com → 93.184.216.34 |
| AAAA | Name → IPv6 | example.com → 2606:2800::1 |
| CNAME | Alias to another name | www.example.com → example.com |
| MX | Mail server for a domain | example.com → mail.example.com |
| TXT | Text info (SPF, DKIM, verification) | "v=spf1 include:_spf.google.com" |
| NS | Which name servers hold the zone | ns1.example.com |
| PTR | IP → name (reverse lookup) | 93.184.216.34 → example.com |

- **Forward zone** – name → IP lookups. 📌 Looking up google.com.
- **Reverse zone** – IP → name lookups. 📌 Email servers checking who 8.8.8.8 is.
- **Primary zone** – the editable master copy. **Secondary zone** – read-only copy. 📌 Main DNS server + backup DNS server.
- **Recursive lookup** – the DNS server does all the work and returns the final answer. 📌 Your ISP's DNS server finds google.com for you.
- **Iterative lookup** – the server replies "ask this other server." 📌 Root server says "ask the .com servers."
- **DNSSEC** – digitally signs DNS records so they can't be faked. 📌 Prevents DNS poisoning.
- **DoH / DoT** – DNS encrypted over HTTPS (443) / TLS (853). 📌 Firefox using DoH to hide your lookups.
- **hosts file** – local file that overrides DNS. 📌 Adding `127.0.0.1 facebook.com` to block it.
- **NTP** – syncs device clocks (port 123). 📌 All servers sync to pool.ntp.org.
- **PTP** – much more precise time sync. 📌 Stock trading systems needing microsecond accuracy.
- **NTS** – NTP with authentication (secure). 📌 Prevents attackers from faking time.

### 3.5 Network Access & Management
- **Site-to-site VPN** – connects two whole networks. 📌 Branch office permanently linked to HQ.
- **Client-to-site VPN** – one user connects to the company network. 📌 Using GlobalProtect or AnyConnect from home.
- **Full tunnel** – *all* traffic goes through the VPN. 📌 Even your YouTube goes through the company.
- **Split tunnel** – only company traffic uses the VPN. 📌 Company apps via VPN, Netflix directly to the internet.
- **Clientless VPN** – VPN through a web browser, no software. 📌 Logging into a company portal over HTTPS.
- **SSH** – secure command-line management. 📌 `ssh admin@switch1`.
- **GUI** – web/graphical management. 📌 Logging into the router at https://192.168.1.1.
- **API** – managing devices with code. 📌 A Python script changing VLANs through a REST API.
- **Console** – direct cable connection to the device. 📌 Console cable to set up a brand-new switch.
- **Jump box / jump host** – a hardened server you go through to reach other servers. 📌 Admins SSH into the jump box first, then into the routers.
- **In-band management** – managing over the normal network. 📌 SSH to a router over the company LAN.
- **Out-of-band management** – separate management path that works when the network is down. 📌 Console server with a cellular modem.

---

## 4.0 NETWORK SECURITY

### 4.1 Security Concepts
- **Confidentiality** – only authorized people see data. 📌 Encrypting customer records.
- **Integrity** – data isn't changed without permission. 📌 Hashing a file to make sure it wasn't tampered with.
- **Availability** – systems are up when needed. 📌 Redundant servers so the website never goes down.
- **Data in transit** – data moving across the network. 📌 HTTPS protects your login.
- **Data at rest** – stored data. 📌 BitLocker encrypting a laptop drive.
- **PKI / certificates** – prove identity using trusted certificates. 📌 The padlock in your browser on a bank site.
- **Self-signed certificate** – created by yourself, not trusted by default. 📌 Browser warning on a router's admin page.
- **Authentication** – proving who you are. 📌 Username + password + phone code.
- **MFA** – two or more different factor types: something you know / have / are / where you are. 📌 Password + Duo push.
- **SSO** – log in once, access many apps. 📌 One Microsoft login for Outlook, Teams, and SharePoint.
- **RADIUS** – central authentication, common for Wi-Fi/VPN; encrypts only the password. 📌 Enterprise Wi-Fi checks your login against RADIUS.
- **TACACS+** – Cisco central authentication for device admins; encrypts everything. 📌 Network admins log into switches through TACACS+.
- **LDAP** – protocol for querying directories. 📌 Apps looking up users in Active Directory.
- **SAML** – web-based SSO standard. 📌 "Sign in with your company account" on a cloud app.
- **Authorization** – what you're allowed to do. 📌 Interns can read files but not delete them.
- **Least privilege** – give only the access needed. 📌 Help desk can reset passwords but not change firewall rules.
- **RBAC** – permissions based on job role. 📌 Everyone in "Accounting" gets access to the finance share.
- **Accounting** – logging what users did. 📌 Logs show who changed a router config at 2 PM. (Authentication + Authorization + Accounting = **AAA**)
- **Geofencing** – rules based on location. 📌 Block logins from outside the U.S.
- **Honeypot** – fake system to lure attackers. 📌 A fake "payroll" server that alerts when touched.
- **Honeynet** – a whole fake network of honeypots. 📌 Research network studying attacker behavior.
- **Risk** – chance something bad happens × its impact. 📌 Unpatched server = high risk.
- **Vulnerability** – a weakness. 📌 Default admin password left on a router.
- **Exploit** – a method that takes advantage of a weakness. 📌 Malware using an unpatched Windows bug.
- **Threat** – who or what could cause harm. 📌 Hackers, insiders, floods.
- **PCI DSS** – rules for handling credit cards. 📌 Online stores must encrypt card data.
- **GDPR** – EU privacy law. 📌 EU users can ask for their data to be deleted.
- **Data locality** – data must stay in certain countries. 📌 German customer data must stay on German servers.
- **IoT** – internet-connected everyday devices. 📌 Smart cameras on their own VLAN.
- **OT / ICS / SCADA** – systems controlling physical processes. 📌 A water treatment plant's control network, kept isolated.
- **Guest network** – separate network for visitors. 📌 "Company-Guest" Wi-Fi with internet only.
- **BYOD** – Bring Your Own Device policies. 📌 Employees' phones on a separate VLAN with MDM.

### 4.2 Attack Types
- **DoS** – one source overwhelms a service. 📌 One computer flooding a website with requests.
- **DDoS** – many sources (botnet) overwhelm a service. 📌 Thousands of hacked cameras flooding a website.
- **VLAN hopping** – getting traffic into a VLAN you shouldn't reach (switch spoofing or double tagging). 📌 Attacker pretends to be a switch to form a trunk.
- **MAC flooding** – filling the switch's MAC table so it floods all traffic like a hub. 📌 Attacker then sniffs everyone's traffic.
- **ARP spoofing / poisoning** – sending fake ARP replies to link the attacker's MAC with another IP. 📌 Attacker claims to be the gateway and intercepts traffic.
- **DNS spoofing / poisoning** – fake DNS answers. 📌 bank.com resolves to the attacker's fake site.
- **Rogue DHCP server** – unauthorized DHCP handing out bad settings. 📌 Gives out the attacker's IP as the gateway.
- **Rogue AP** – unauthorized AP plugged into your network. 📌 An employee plugs in a cheap Wi-Fi router at their desk.
- **Evil twin** – fake AP with the same name as a real one. 📌 Fake "Airport_Free_WiFi" stealing logins.
- **On-path (man-in-the-middle)** – attacker secretly sits between two parties. 📌 Intercepting traffic on public Wi-Fi.
- **Phishing** – fake messages to trick users. 📌 Email pretending to be IT asking for your password.
- **Dumpster diving** – searching trash for information. 📌 Finding printed passwords in the recycling.
- **Shoulder surfing** – watching someone's screen or keyboard. 📌 Watching someone enter their PIN.
- **Tailgating** – following someone through a secure door. 📌 Walking in behind an employee without badging.
- **Malware** – malicious software. 📌 Ransomware encrypting files and demanding payment.

### 4.3 Defense Techniques
- **Device hardening** – removing anything not needed and securing the rest. 📌 Disabling unused switch ports, changing default passwords, updating firmware.
- **NAC (Network Access Control)** – checks devices before letting them on the network. 📌 A laptop without antivirus gets put on a quarantine VLAN.
- **802.1X** – port-based authentication: supplicant (device) → authenticator (switch/AP) → authentication server (RADIUS). 📌 Plugging in a laptop and logging in before the port opens.
- **Port security** – limits which MAC addresses can use a switch port. 📌 Port shuts down if an unknown device is plugged in.
- **MAC filtering** – allow/deny list by MAC (easy to spoof). 📌 Only listed devices can join home Wi-Fi.
- **Key management** – creating, storing, rotating, and retiring encryption keys. 📌 Rotating VPN keys every year.
- **ACL (Access Control List)** – ordered allow/deny rules; implicit deny at the end. 📌 Allow HTTPS to the web server, deny everything else.
- **URL filtering** – blocks specific websites. 📌 Blocking known malware sites.
- **Content filtering** – blocks categories of content. 📌 Blocking gambling sites at work.
- **Trusted / untrusted zones** – internal network vs. the internet. 📌 LAN = trusted, internet = untrusted.
- **Screened subnet (DMZ)** – zone for public-facing servers, separated from the internal network. 📌 Web and email servers sit in the DMZ.

---

## 5.0 NETWORK TROUBLESHOOTING

### 5.1 Troubleshooting Methodology (MEMORIZE ORDER)
1. **Identify the problem** – gather info, question users, find symptoms, check for recent changes, duplicate the problem.
   📌 "Since when?" – "Since the switch was replaced this morning."
2. **Establish a theory** of probable cause – question the obvious; top-down or bottom-up OSI.
   📌 "Maybe the new switch port is on the wrong VLAN."
3. **Test the theory** – if confirmed, go on; if not, try a new theory or escalate.
   📌 Check the port – it's on VLAN 1 instead of VLAN 10. Confirmed.
4. **Establish a plan of action** and identify potential effects.
   📌 "Changing the port VLAN will briefly disconnect that user."
5. **Implement** the solution or escalate.
   📌 Change the port to VLAN 10.
6. **Verify** full system functionality and implement preventive measures.
   📌 User can reach everything; update the switch template.
7. **Document** findings, actions, outcomes, and lessons learned.
   📌 Write it up in the ticket.

> Memory trick: **"I Eat Tacos, Every Inexpensive Veggie Dish"** – Identify, Establish, Test, Establish plan, Implement, Verify, Document.

### 5.2 Cabling & Physical Issues
- **Wrong cable type** – using the wrong cable for the job. 📌 Straight-through where crossover is needed (most devices auto-fix with Auto-MDIX); Cat 5 on a 10 Gbps link.
- **Crosstalk** – signal bleeding between wire pairs. 📌 Untwisting wires too far at the connector.
- **Interference (EMI)** – outside electrical noise. 📌 Cable run next to fluorescent lights or motors.
- **Attenuation** – signal weakens over distance. 📌 A 150 m copper run (over the 100 m limit).
- **Improper termination** – bad connector install. 📌 Wires in the wrong order in an RJ45.
- **TX/RX transposed** – fiber send/receive strands swapped. 📌 Fiber link shows no light until you swap the two strands.
- **CRC errors** – corrupted frames. 📌 Rising CRC count = bad cable or interference.
- **Runts** – frames smaller than 64 bytes. 📌 Often caused by collisions / duplex mismatch.
- **Giants** – frames bigger than the MTU. 📌 Jumbo frames sent to a port not configured for them.
- **Drops** – frames thrown away. 📌 Interface overloaded during backups.
- **Error-disabled port** – switch shut the port due to a violation. 📌 Port security tripped by an unknown device.
- **Administratively down** – port turned off by an admin. 📌 `shutdown` command on the interface.
- **Suspended port** – port removed from a link aggregation bundle. 📌 LACP mismatch on one member port.
- **PoE (Power over Ethernet)** – power sent over the network cable: PoE 15.4 W, PoE+ 30 W, PoE++ 60–100 W. 📌 A PTZ camera needs PoE++ but the switch only gives PoE+ → it won't fully work.
- **Power budget exceeded** – switch can't power every device. 📌 The 20th AP won't power on.
- **Transceiver mismatch** – incompatible modules on each end. 📌 Single-mode SFP on one side, multimode on the other.

### 5.3 Network Service Issues
- **Switching loop / broadcast storm** – traffic loops endlessly without STP. 📌 Someone plugs both ends of a cable into the same switch → network crashes.
- **Incorrect VLAN assignment** – port on the wrong VLAN. 📌 A PC on the Guest VLAN can't reach the file server.
- **ACL blocking traffic** – a rule denies legitimate traffic. 📌 New app fails because port 8443 is blocked.
- **Missing / wrong route** – the router doesn't know the path. 📌 Branch can't reach HQ because a static route was deleted.
- **DHCP pool exhausted** – no addresses left to give. 📌 Conference room full of guests → new devices get 169.254.x.x.
- **Wrong default gateway** – device can talk locally but not to other networks. 📌 Can ping the printer but not google.com.
- **Wrong subnet mask** – device thinks local hosts are remote (or the reverse). 📌 /16 typed instead of /24.
- **Duplicate IP** – two devices with the same IP. 📌 Windows shows "IP address conflict."
- **Duplicate MAC** – two devices with the same MAC (often cloned VMs). 📌 Two cloned VMs keep dropping connection.
- **DNS issue** – names don't resolve. 📌 `ping 8.8.8.8` works but `ping google.com` fails.
- **NTP issue** – wrong time on devices. 📌 Clock is 10 minutes off → Kerberos logins fail, certificates look invalid.
- **Unexpected change outcome** – a change broke something else. 📌 Firewall update last night; VPN broken today → check the change log.

### 5.4 Performance Issues
- **Congestion / contention** – too much traffic for the link. 📌 Everyone streams the company meeting at once.
- **Bottleneck** – the slowest part limits everything. 📌 10 Gbps switches but a 100 Mbps internet link.
- **Bandwidth** – max possible capacity. 📌 A 1 Gbps link.
- **Throughput** – actual speed achieved. 📌 Speed test shows 600 Mbps on that 1 Gbps link.
- **Latency** – delay for data to arrive. 📌 150 ms ping to a game server = lag.
- **Jitter** – variation in latency. 📌 Choppy, robotic voice on a VoIP call.
- **Packet loss** – packets never arrive. 📌 Video freezes and pixelates.
- **Wireless interference** – other signals disrupt Wi-Fi. 📌 Microwave oven killing 2.4 GHz Wi-Fi.
- **Channel overlap** – nearby APs on overlapping channels. 📌 Neighboring APs on channels 3 and 5.
- **Poor antenna placement** – signal doesn't reach users. 📌 AP inside a metal cabinet.
- **Client overload** – too many devices on one AP. 📌 Lecture hall with 300 students on one AP.
- **Roaming issues** – devices don't switch to a closer AP. 📌 Laptop stays stuck on a far-away weak AP ("sticky client").
- **RSSI** – received signal strength (closer to 0 = stronger). 📌 −50 dBm good, −85 dBm poor.
- **SNR (Signal-to-Noise Ratio)** – signal compared to background noise; higher is better. 📌 SNR of 25 dB+ is good for data.

### 5.5 Tools & Commands

**Software tools**
- **Protocol analyzer (Wireshark)** – captures and decodes packets. 📌 Seeing a TCP reset when an app fails.
- **Nmap** – scans for devices and open ports. 📌 `nmap 192.168.1.0/24` finds an unknown device with port 23 open.
- **LLDP / CDP** – discover directly connected neighbor devices (CDP = Cisco only). 📌 `show cdp neighbors` shows which switch port a phone is on.
- **Speed tester** – measures throughput. 📌 speedtest.net to check ISP speed.

**Commands**

| Command | Use | Example |
|---|---|---|
| `ping` | Is the host reachable? (ICMP) | `ping 8.8.8.8` |
| `traceroute` / `tracert` | Show each hop along the path | `tracert google.com` finds where traffic stops |
| `nslookup` / `dig` | Test DNS | `nslookup google.com` |
| `ipconfig` (Win) / `ifconfig`, `ip` (Linux) | Show IP settings | `ipconfig /all` shows DNS and gateway |
| `arp -a` | Show IP → MAC table | Find the MAC of 192.168.1.1 |
| `netstat` | Show active connections and ports | `netstat -an` shows a listening port 3389 |
| `tcpdump` | Command-line packet capture | `tcpdump -i eth0 port 53` |
| `show interface` | Interface status and errors (Cisco) | Spotting CRC errors on Gi0/1 |
| `show running-config` | Current device configuration | Checking a port's VLAN setting |
| `show ip route` | Routing table | Checking if a route to 10.2.0.0 exists |

**Hardware tools**
- **Toner & probe** – sends a tone down a cable so you can find it. 📌 Finding which unlabeled cable in the closet goes to office 204.
- **Cable tester** – checks wiring and continuity. 📌 Shows pairs 3 and 6 are swapped.
- **TDR** – finds the distance to a fault in copper. 📌 "Break at 42 meters."
- **OTDR** – finds the distance to a fault in fiber. 📌 "Fiber break at 1.3 km."
- **Wi-Fi analyzer** – shows channels and signal strength. 📌 Finds every neighbor AP on channel 6.
- **Visual fault locator** – shines red light into fiber to show breaks. 📌 Red glow where a fiber is bent too sharply.
- **Network tap** – hardware that copies traffic from a cable. 📌 Feeding traffic to an IDS.
- **Crimper** – attaches RJ45 connectors to cables. 📌 Making a custom-length patch cable.
- **Punchdown tool** – pushes wires into patch panels/keystone jacks. 📌 Terminating cables at the back of a patch panel.

---

## Quick Last-Minute Review
- OSI: **Please Do Not Throw Sausage Pizza Away** (1 → 7).
- Switch = MAC = Layer 2. Router = IP = Layer 3.
- 169.254.x.x = DHCP failed.
- DORA = DHCP. 3-way handshake = TCP.
- 2.4 GHz non-overlapping: 1, 6, 11.
- /30 = 2 hosts. Usable hosts = 2ⁿ − 2.
- SNMPv3 = secure. Telnet = insecure (use SSH).
- RPO = data loss. RTO = downtime.
- Troubleshooting: Identify → Theory → Test → Plan → Implement → Verify → Document.
- Ping works by IP but not by name → DNS.
