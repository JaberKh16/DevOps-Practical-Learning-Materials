Let’s create a **complete, structured guide for Classful IPv4 addressing**, including **concepts, formulas, network bits, host bits, broadcast, and usable hosts**. I’ll also include **easy formulas** for quick calculation.

---

# ✅ 1. What is Classful Addressing?

**Classful addressing** is the original IPv4 system that divides IP addresses into fixed **classes A, B, C, D, E**.

- IPv4 = 32 bits
    
- Divided into **Network bits** + **Host bits**
    
- Each class has **default subnet mask**
    

---

# ✅ 2. IP Classes, Network Bits, Host Bits

| Class | First Octet | Default Mask  | Network Bits | Host Bits | Usage             |
| ----- | ----------- | ------------- | ------------ | --------- | ----------------- |
| A     | 0–127       | 255.0.0.0     | 8            | 24        | Large orgs / ISPs |
| B     | 128–191     | 255.255.0.0   | 16           | 16        | Medium orgs       |
| C     | 192–223     | 255.255.255.0 | 24           | 8         | Small orgs        |
| D     | 224–239     | N/A           | N/A          | N/A       | Multicast         |
| E     | 240–255     | N/A           | N/A          | N/A       | Reserved          |

---

# ✅ 3. Formulas

### 3.1 Number of Hosts per Network

```
Hosts per network = 2^(Host bits) - 2
```

- Subtract 2 for **Network ID** and **Broadcast address**
    

---

### 3.2 Number of Networks per Class

```
Networks = 2^(Network bits reserved for class) 
```

- Example: Class A → Network bits = 7 (first bit fixed) → 2^7 = 128 networks
    

---

### 3.3 Broadcast Address

- All **host bits = 1**
    
- Formula (if Network Address known):
    

```
Broadcast = Network Address + (2^(Host bits) - 1)
```

---

### 3.4 Usable IP Range

```
Usable IPs = Network Address + 1  … Broadcast Address - 1
```

---

# ✅ 4. Default Masks and Host Formulas

|Class|Default Mask|Host Bits|Max Hosts Formula|Max Hosts Value|
|---|---|---|---|---|
|A|255.0.0.0|24|2^24 - 2|16,777,214|
|B|255.255.0.0|16|2^16 - 2|65,534|
|C|255.255.255.0|8|2^8 - 2|254|

---

# ✅ 5. Quick Examples

### Example 1: Class A

```
IP: 10.5.6.7
Class: A
Default mask: 255.0.0.0
Network bits: 8
Host bits: 24
```

- Network address = 10.0.0.0
    
- Broadcast address = 10.255.255.255
    
- Usable IP range = 10.0.0.1 – 10.255.255.254
    
- Hosts = 2^24 - 2 = 16,777,214
    

---

### Example 2: Class B

```
IP: 172.16.5.10
Class: B
Default mask: 255.255.0.0
Network bits: 16
Host bits: 16
```

- Network address = 172.16.0.0
    
- Broadcast address = 172.16.255.255
    
- Usable IP range = 172.16.0.1 – 172.16.255.254
    
- Hosts = 2^16 - 2 = 65,534
    

---

### Example 3: Class C

```
IP: 192.168.1.25
Class: C
Default mask: 255.255.255.0
Network bits: 24
Host bits: 8
```

- Network address = 192.168.1.0
    
- Broadcast address = 192.168.1.255
    
- Usable IP range = 192.168.1.1 – 192.168.1.254
    
- Hosts = 2^8 - 2 = 254
    

---

# ✅ 6. Steps to Calculate Network, Broadcast, Hosts (Classful)

1. **Identify Class** (use first octet)
    
2. **Find default subnet mask**
    
3. **Calculate Network address** (set host bits = 0)
    
4. **Calculate Broadcast address** (set host bits = 1)
    
5. **Usable IP range** = Network +1 … Broadcast -1
    
6. **Hosts** = 2^(host bits) - 2
    

---

# ✅ 7. Classful Addressing Quick Reference

|First Octet|Class|Mask|Hosts|Notes|
|---|---|---|---|---|
|1–126|A|/8|16M+|Big orgs|
|128–191|B|/16|65k|Medium orgs|
|192–223|C|/24|254|Small orgs|
|224–239|D|N/A|N/A|Multicast|
|240–255|E|N/A|N/A|Reserved|

---

If you want, I can make a **diagram showing Class A/B/C with network bits, host bits, broadcast, and usable IPs visually** — perfect for quick memory and exam revision.

Do you want me to create that visual diagram?