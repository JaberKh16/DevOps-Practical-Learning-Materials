Below is a **clear, structured guide to Subnetting**, including **concepts, formulas, and worked examples**.

---

# ✅ 1. What is Subnetting?

**Subnetting** = Dividing a large network into smaller logical networks (subnets).

### Why Subnetting is Used

- Improves network performance
    
- Reduces broadcast traffic
    
- Improves security
    
- Efficient IP usage
    

---

# ✅ 2. IP Address Structure (IPv4)

IPv4 = **32 bits** → divided into:

```
Network Portion | Host Portion
```

Example:

```
192.168.1.10/24
```

- `/24` = Network bits
    
- Remaining = Host bits
    

---

# ✅ 3. CIDR Notation

- IETF(Internet Engineering Task Force) introduced CIDR in 1993 to replace the 
   IANA provided classfull addressing system to overcome the wasted IP's
- CIDR = Classless Inter-Domain Routing

Format:

```
IP / Prefix
```

Example:

```
192.168.1.0/24
```

Means:

- 24 bits = Network
    
- 8 bits = Host
    

---

# ✅ 4. Important Subnetting Formulas

### 1️⃣ Number of Subnets

```
Subnets = 2ⁿ
```

n = Borrowed bits

---

### 2️⃣ Number of Hosts per Subnet

```
Hosts = 2ʰ - 2
```

h = Host bits

(−2 for Network ID & Broadcast)

---

### 3️⃣ Block Size (Increment)

```
Block Size = 256 - Subnet Mask Value
```

(Used in last subnet octet)

---

# ✅ 5. Subnet Mask Table

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

# ✅ 6. Example 1: Basic Subnetting

### Problem:

Subnet:

```
192.168.1.0/26
```

### Step 1: Find Mask

```
/26 = 255.255.255.192
```

### Step 2: Block Size

```
256 - 192 = 64
```

### Step 3: Subnet Ranges

|Subnet|Network|First IP|Last IP|Broadcast|
|---|---|---|---|---|
|1|192.168.1.0|.1|.62|.63|
|2|192.168.1.64|.65|.126|.127|
|3|192.168.1.128|.129|.190|.191|
|4|192.168.1.192|.193|.254|.255|

### Step 4: Hosts

```
2⁶ - 2 = 62 hosts
```

---

# ✅ 7. Example 2: Subnet by Required Hosts

### Problem:

You need **50 hosts per subnet**.

### Step 1: Find Required Host Bits

Try values:

```
2⁵ - 2 = 30 ❌
2⁶ - 2 = 62 ✅
```

So:

```
Host bits = 6
```

### Step 2: Find Prefix

```
32 - 6 = 26
```

So:

```
/26
```

### Step 3: Subnet Mask

```
255.255.255.192
```

---

# ✅ 8. Example 3: Subnet by Required Subnets

### Problem:

You need **8 subnets** from:

```
192.168.10.0/24
```

### Step 1: Borrow Bits

```
2³ = 8
```

Borrow = 3 bits

### Step 2: New Prefix

```
24 + 3 = /27
```

### Step 3: New Mask

```
255.255.255.224
```

### Step 4: Hosts

```
2⁵ - 2 = 30
```

---

# ✅ 9. Example 4: Find Network Info

### Problem:

Find network details for:

```
IP: 10.0.5.17/20
```

### Step 1: Mask

```
/20 = 255.255.240.0
```

### Step 2: Block Size

```
256 - 240 = 16
```

### Step 3: Find Range

Subnets increase by 16:

```
0,16,32,48,...
```

IP = 5 → belongs to block 0–15

### Step 4: Results

```
Network   = 10.0.0.0
Broadcast = 10.0.15.255
Usable    = 10.0.0.1 – 10.0.15.254
```

---

# ✅ 10. VLSM (Variable Length Subnet Masking)

VLSM = Different subnet sizes in same network.

### Example:

Network:

```
192.168.1.0/24
```

Needs:

|Dept|Hosts|
|---|---|
|A|100|
|B|50|
|C|20|

### Step 1: Sort Descending

100 → 50 → 20

### Step 2: Allocate

|Dept|Needed|CIDR|Block|
|---|---|---|---|
|A|100|/25|128|
|B|50|/26|64|
|C|20|/27|32|

### Step 3: Assign

|Dept|Subnet|
|---|---|
|A|192.168.1.0/25|
|B|192.168.1.128/26|
|C|192.168.1.192/27|

---

# ✅ 11. Quick Subnetting Method (Exam Trick)

### Step 1: Find interesting octet

Where mask ≠ 255

Example:

```
255.255.192.0 → 3rd octet
```

### Step 2: Block Size

```
256 - 192 = 64
```

### Step 3: Jump

```
0,64,128,192
```

---

# ✅ 12. Key Summary

|Concept|Formula|
|---|---|
|Subnets|2ⁿ|
|Hosts|2ʰ − 2|
|Block|256 − mask|
|Prefix|32 − host bits|

---

If you want, I can next give you:

✅ Practice Questions  
✅ Subnetting Cheat Sheet  
✅ Binary Method  
✅ Exam-Speed Method (30 seconds)

Just tell me 👍