# Network Commands: Deep Concepts (Markdown Guide)

## 1. Introduction

Networking commands are diagnostic, investigative, and configuration tools that operate across OSI layers. Understanding **what layer** a command touches and **what data** it exposes is critical for deep mastery.

---

# 2. OSI Layer View of Commands

|OSI Layer|Relevant Commands|Conceptual Use|
|---|---|---|
|Layer 1 – Physical|`ethtool`, `dmesg`, `nmcli dev status`|Link state, cable, NIC properties|
|Layer 2 – Data Link|`ip link`, `arp`, `brctl`, `macchanger`|MAC mapping, link setup, bridges|
|Layer 3 – Network|`ip addr`, `ip route`, `ping`, `traceroute`|IP configuration, routing, reachability|
|Layer 4 – Transport|`ss`, `netstat`, `nmap`|Ports, sockets, connection states|
|Layer 7 – Application|`curl`, `wget`, `dig`, `nslookup`|HTTP, DNS, service-level debugging|

---

# 3. Layer-2 Commands and Concepts

## 3.1 `ip link`

Shows and manages network interfaces (NICs).  
Layer: L2 – Interface state and MAC-level config.

`ip link show ip link set eth0 up ip link set eth0 down`

**Deep Concept:**  
The NIC transitions across **operstate** states (up, down, dormant). Setting a NIC UP does not imply connectivity; it only enables the kernel to bind the interface.

---

## 3.2 `arp` / `ip neigh`

ARP resolves **IPv4 → MAC** bindings.

`arp -a ip neigh`

**Deep Concept:**  
ARP table = kernel cache of L2 adjacency.  
Stale entries cause intermittent connectivity.  
ARP poisoning manipulates this table to reroute traffic.

---

## 3.3 Ethernet Inspection Tools

### `ethtool`

Shows link speed, duplex, driver capabilities.

`ethtool eth0`

**Deep Concept:**  
Speed mismatches (100 vs 1000) cause duplex mismatches → collisions → degraded throughput.

---

# 4. Layer-3 Commands and Concepts

## 4.1 `ip addr`

Inspect and assign IPv4/IPv6 addresses.

`ip addr show ip addr add 192.168.1.10/24 dev eth0`

**Deep Concept:**  
Every IP belongs to a **subnet**, and subnet masks define L3 adjacency.  
If two hosts share the prefix → direct L2 communication; otherwise → routed.

---

## 4.2 `ip route`

Routing table inspection and modification.

`ip route ip route add default via 192.168.1.1`

**Deep Concept:**  
Routing = **longest prefix match (LPM)**.  
Routing table entries:

- Connected routes (auto-created)
    
- Static routes (manual)
    
- Dynamic routes (via protocols: OSPF, BGP)
    

---

## 4.3 `ping`

Basic reachability using ICMP Echo.

`ping 8.8.8.8`

**Deep Concept:**  
Ping measures:

- **DNS resolution** (if hostname is used)
    
- **Routing availability**
    
- **ICMP filtering** (firewalls may drop)
    
- **Round Trip Time (RTT)**
    

RTT indicates latency but not throughput.

---

## 4.4 `traceroute` / `tracepath`

Displays hop-by-hop L3 forwarding path.

`traceroute google.com`

**Deep Concept:**  
Uses TTL expiration. Each hop returns:

- ICMP TTL exceeded
    
- ICMP unreachable (final hop)
    

Traceroute reveals path asymmetry.

---

## 4.5 `ipcalc`

Subnet calculation.

`ipcalc 10.1.2.3/17`

**Deep Concept:**  
CIDR notations help network aggregation → reduces routing table size.

---

# 5. Layer-4 Commands and Socket Analysis

## 5.1 `ss` (socket statistics)

Modern replacement for `netstat`.

`ss -tulnp`

Flags:

- `t` → TCP
    
- `u` → UDP
    
- `l` → listening
    
- `n` → numeric
    
- `p` → process
    

**Deep Concept:**  
TCP connections have states:

- SYN_SENT
    
- SYN_RECV
    
- ESTABLISHED
    
- FIN_WAIT
    
- TIME_WAIT
    

High TIME_WAIT indicates heavy short-lived connections.

---

## 5.2 `netstat` (legacy)

`netstat -plant`

---

## 5.3 `nc` (netcat)

Swiss-army knife for TCP/UDP.

`# Start listener nc -l 9000 # Connect nc server 9000`

**Deep Concept:**  
Used to test raw transport connectivity before L7.

---

# 6. DNS Commands and Concepts

## 6.1 `dig`

Modern detailed DNS query tool.

`dig google.com dig @8.8.8.8 google.com A`

**Deep Concept:**  
DNS resolution involves:

- Root servers
    
- TLD servers
    
- Authoritative name servers
    
- Local caching resolver
    

---

## 6.2 `nslookup` (older)

`nslookup github.com`

---

## 6.3 `host`

Simple DNS lookup.

---

# 7. HTTP / Application Layer Tools

## 7.1 `curl`

High-level protocol interactions (HTTP, FTP, SMTP).

`curl -I https://example.com curl -v https://api.example.com`

**Deep Concept:**  
Inspect:

- TLS handshake
    
- Request headers
    
- Response headers
    
- Status codes (2xx, 3xx, 4xx, 5xx)
    

---

## 7.2 `wget`

File retrieval.

---

# 8. Packet Capture and Deep Inspection

## 8.1 `tcpdump`

`tcpdump -i eth0 tcpdump -nnvvXSs 0 host 10.0.0.5`

Flags meaning:

- `-nn` → no DNS/port name resolution
    
- `-X` → hex + ASCII
    
- `-s 0` → capture full packet
    

**Deep Concept:**  
tcpdump operates at **L2 → L7**, capturing frames before firewall NAT translation.

---

## 8.2 Wireshark

GUI deep packet analysis.

---

# 9. Connection Testing and Path Debugging

## 9.1 `mtr`

Real-time traceroute + ping.

`mtr google.com`

**Deep Concept:**  
Shows latency patterns and packet loss over time.

---

# 10. Network Configuration Tools

### Linux NetworkManager

`nmcli dev status nmcli con show nmcli con up id "Wired connection 1"`

---

# 11. Advanced Tools

### `iptables` / `nft`

Firewall and NAT inspection.

### `ifconfig` (deprecated)

Legacy interface tool.

### `ssldump`, `openssl s_client`

TLS inspection.

---

# 12. Summary Table (Cheat Sheet)

|Command|Layer|Purpose|
|---|---|---|
|ip link|L2|Interface state, MAC|
|arp / ip neigh|L2|ARP table|
|ip addr|L3|IP addressing|
|ip route|L3|Routing|
|ping|L3|ICMP reachability|
|traceroute|L3|Hop tracing|
|ss|L4|Socket analysis|
|netcat|L4|Raw TCP/UDP tests|
|dig|L7|DNS|
|curl|L7|HTTP/TLS debugging|
|tcpdump|L2–L7|Packet capture|

---

If you'd like, I can also generate:

- A **PDF cheat-sheet**
    
- A **mindmap diagram**
    
- A **practical lab with real examples**
    
- A **deep-dive into routing, ARP, subnetting, iptables/nftables, or packet capture**
    

Tell me what format you want next.