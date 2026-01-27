Great. Below are the **four additions** you asked for: **Practice Questions, Cheat Sheet, Binary Method, and 30-Second Exam Method** — organized for fast learning and revision.

---

# ✅ 13. Subnetting Practice Questions

Try these first. Answers are below.

---

### 🔹 Q1

Find details for:

```
192.168.5.34/27
```

- Network?
    
- Broadcast?
    
- Usable range?
    
- Hosts?
    

---

### 🔹 Q2

You need **20 hosts per subnet**.  
Which prefix is required?

---

### 🔹 Q3

How many subnets from:

```
172.16.0.0/20 → /24
```

?

---

### 🔹 Q4 (VLSM)

From `10.0.0.0/24`, allocate:

|Dept|Hosts|
|---|---|
|A|60|
|B|25|
|C|10|

---

### ✅ Answers

**Q1**

```
/27 → 255.255.255.224
Block = 32

Subnets: 0,32,64,96...

34 ∈ 32–63

Network = 192.168.5.32
Broadcast = 192.168.5.63
Usable = .33 – .62
Hosts = 30
```

---

**Q2**

```
2⁵ - 2 = 30 ✅

/27
```

---

**Q3**

```
/20 → /24 = 4 bits borrowed

2⁴ = 16 subnets
```

---

**Q4 (VLSM)**

|Dept|CIDR|Range|
|---|---|---|
|A|/26|10.0.0.0–63|
|B|/27|10.0.0.64–95|
|C|/28|10.0.0.96–111|

---

# ✅ 14. Subnetting Cheat Sheet (Quick Memory)

### 🔹 Common CIDR

|CIDR|Mask|Hosts|
|---|---|---|
|/24|255.255.255.0|254|
|/25|255.255.255.128|126|
|/26|255.255.255.192|62|
|/27|255.255.255.224|30|
|/28|255.255.255.240|14|
|/29|255.255.255.248|6|
|/30|255.255.255.252|2|

---

### 🔹 Powers of 2

|Power|Value|
|---|---|
|2⁴|16|
|2⁵|32|
|2⁶|64|
|2⁷|128|
|2⁸|256|

---

### 🔹 Formulas

```
Subnets = 2ⁿ
Hosts = 2ʰ - 2
Prefix = 32 - h
Block = 256 - mask
```

---

# ✅ 15. Binary Subnetting Method (Deep Understanding)

Used when decimal method fails.

---

### Example

```
IP: 192.168.1.130/26
```

---

### Step 1: Convert Last Octet to Binary

130 → Binary:

```
128 64 32 16 8 4 2 1
 1   0  0  0 0 0 1 0
```

So:

```
10000010
```

---

### Step 2: Apply Mask

/26 → First 26 bits = Network

Last octet mask:

```
11111100
```

---

### Step 3: AND Operation

```
IP   = 10000010
Mask = 11111100
----------------
Net  = 10000000 (128)
```

---

### Step 4: Results

```
Network = .128
Broadcast = .191
Range = .129 – .190
```

---

### ✅ Binary Rule

```
1 AND 1 = 1
Else = 0
```

---

# ✅ 16. 30-Second Exam-Speed Subnetting Method

This is the **fastest** technique.

---

## 🔹 Step 1: Memorize This Table

|CIDR|Block|
|---|---|
|/25|128|
|/26|64|
|/27|32|
|/28|16|
|/29|8|
|/30|4|

---

## 🔹 Step 2: Find Block

Example:

```
IP: 192.168.2.77/27
```

/27 → Block = 32

---

## 🔹 Step 3: Jump Multiples

```
0,32,64,96,128...
```

77 ∈ 64–95

---

## 🔹 Step 4: Answer

```
Network = 64
Broadcast = 95
Usable = 65–94
```

DONE in < 30 sec.

---

# ✅ 17. Mental Math Trick (No Calculator)

Find closest lower multiple.

Example:

```
IP = 142
Block = 32
```

Multiples:

```
32×4 = 128
32×5 = 160 ❌
```

So:

```
Network = 128
```

---

# ✅ 18. Subnetting Workflow (Always Follow This)

When solving any problem:

### Step 1

Find prefix (/26, /27…)

### Step 2

Find mask

### Step 3

Find block size

### Step 4

Find subnet range

### Step 5

Find network & broadcast

### Step 6

Find usable IPs

---

# ✅ 19. Real-World Usage

Subnetting is used in:

### 🏢 Enterprises

- HR, IT, Finance separated
    

### ☁ Cloud (AWS/Azure/GCP)

- VPC subnets
    

### 🏫 Universities

- Labs, WiFi, Admin
    

### 🏠 ISPs

- Customer networks
    

---

# ✅ 20. Final Master Summary

|Skill|Method|
|---|---|
|Fast exam|Block method|
|Deep concept|Binary|
|Network design|VLSM|
|Daily admin|CIDR|

---

Below are the **most important commands you can use on your device to check subnet-related information**, grouped by operating system, with explanations and examples.

---

# ✅ 1. Linux (Ubuntu, Fedora, Arch, etc.)

### 🔹 1. Check IP Address & Subnet Mask

```bash
ip addr show
```

or

```bash
ip a
```

Example output:

```
inet 192.168.1.25/24
```

➡ `/24` = subnet mask

---

### 🔹 2. Show Only Active Interfaces

```bash
ip link show
```

---

### 🔹 3. Show Routing Table (Gateway & Subnet)

```bash
ip route
```

Example:

```
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 scope link
```

➡ Shows your subnet: `192.168.1.0/24`

---

### 🔹 4. Detailed Network Info (Legacy)

```bash
ifconfig
```

⚠ (May not be installed by default)

Install:

```bash
sudo apt install net-tools
```

---

### 🔹 5. Check DNS + Network Info

```bash
nmcli dev show
```

---

### 🔹 6. Test Subnet Connectivity

```bash
ping 192.168.1.1
```

---

### 🔹 7. Scan Devices in Subnet

```bash
nmap -sn 192.168.1.0/24
```

Find all active hosts.

---

# ✅ 2. Windows (CMD / PowerShell)

### 🔹 1. Full Network Info

```cmd
ipconfig /all
```

Example:

```
IPv4 Address . . : 192.168.1.50
Subnet Mask . . : 255.255.255.0
```

---

### 🔹 2. Routing Table

```cmd
route print
```

---

### 🔹 3. Show Interfaces

```cmd
netsh interface ip show config
```

---

### 🔹 4. ARP Table (Local Devices)

```cmd
arp -a
```

---

### 🔹 5. Test Local Subnet

```cmd
ping 192.168.1.1
```

---

# ✅ 3. macOS

### 🔹 1. Check IP & Mask

```bash
ifconfig
```

or

```bash
ipconfig getifaddr en0
```

---

### 🔹 2. Routing Table

```bash
netstat -rn
```

---

### 🔹 3. WiFi Info

```bash
airport -I
```

---

# ✅ 4. Find Subnet from Your IP (Manually)

If your IP is:

```
192.168.10.45/27
```

Then:

|Item|Value|
|---|---|
|Mask|255.255.255.224|
|Block|32|
|Network|192.168.10.32|
|Broadcast|192.168.10.63|

---

# ✅ 5. Cisco / Network Devices (Bonus)

### 🔹 Show Interface IP

```bash
show ip interface brief
```

---

### 🔹 Show Routing

```bash
show ip route
```

---

### 🔹 Show ARP

```bash
show arp
```

---

# ✅ 6. Real-World Workflow (Admin Use)

When checking subnet issues:

### Step 1

Check your IP:

```bash
ip a
```

### Step 2

Check route:

```bash
ip route
```

### Step 3

Ping gateway:

```bash
ping <gateway>
```

### Step 4

Scan subnet:

```bash
nmap -sn <network>
```

### Step 5

Trace route:

```bash
traceroute 8.8.8.8
```

---

# ✅ 7. Quick Command Summary

|Purpose|Linux|Windows|
|---|---|---|
|IP Info|ip a|ipconfig|
|Routes|ip route|route print|
|ARP|ip neigh|arp -a|
|Scan|nmap|nmap|
|Test|ping|ping|

---

# ✅ 8. Pro Tip (Subnet Troubleshooting)

If devices can't communicate:

Check:

✔ Same subnet?  
✔ Same mask?  
✔ Same gateway?  
✔ Firewall blocking?

Example check:

```bash
ip route get 192.168.1.50
```

Shows which interface is used.

---

If you want, I can next give you:

✅ Subnet Troubleshooting Scenarios  
✅ Lab Setup (VirtualBox + Practice)  
✅ Packet Tracer Labs  
✅ Advanced Routing/Subnet Design

Just tell me 👍