# Intensive Networking Fundamentals Crash Course

##  Simple Analogy (Online Order)

Suppose you are ordering something from a website:

1. **Application Layer**  
   This is how you interact with the website using protocols like HTTP or DNS (you place the order).

2. **Transport Layer**  
   Decides how the data is sent:  
   - **TCP** = reliable delivery (like tracked courier)  
   - **UDP** = faster but no guarantee (like normal untracked delivery)  

3. **Internet Layer**  
   Determines the path using IP addresses and routing (like deciding which roads/cities the package travels through).

4. **Link Layer**  
   Handles the actual physical delivery over hardware (WiFi, Ethernet, MAC addresses), like the final delivery agent bringing the package to your door.

---

##  Real-World Flow (When You Open a Website)

- You type a URL → DNS resolves it (**Application Layer**)  
- A connection is established (TCP handshake) (**Transport Layer**)  
- Packets are routed across the internet using IP (**Internet Layer**)  
- Data is physically transmitted over networks (**Link Layer**)


---
##  IP Addressing + Subnetting (Just Enough)

### 1. Private IP Ranges
Used inside local networks (not routable on the internet):

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

---

### 2. CIDR Basics

CIDR notation (`/24`, `/25`, etc.) defines network size.

**Formula:**
Total IPs = 2^(32 - prefix)
Usable IPs = Total - 2


**Examples:**
- `/24` → 256 total → 254 usable  
- `/25` → 128 total → 126 usable  
- `/26` → 64 total → 62 usable  
- `/27` → 32 total → 30 usable  

---

### 3. Block Size (Most Important)
Block Size = 2^(32 - prefix)


Used to split networks into ranges:

| CIDR | Block Size | Ranges Example |
|------|-----------|---------------|
| /24  | 256       | 0–255         |
| /25  | 128       | 0–127, 128–255 |
| /26  | 64        | 0–63, 64–127, 128–191, 192–255 |
| /27  | 32        | 0–31, 32–63, 64–95, ... |

---

### 4. Network, Broadcast, Hosts

For any subnet:
- **Network address** = first IP  
- **Broadcast address** = last IP  
- **Usable hosts** = everything in between  

**Example: `192.168.1.0/24`**
- Network → `192.168.1.0`  
- Broadcast → `192.168.1.255`  
- Usable → `192.168.1.1 – 192.168.1.254`  

---

### 5. Quick Subnetting Method (Mental Trick)

1. Find block size  
2. Start from 0 and add block size  
3. Identify which range your IP falls into  
4. First = network, last = broadcast  

---

### 6. Example

**IP:** `10.0.5.77/27`

- Block size = 32  
- Ranges → `0–31`, `32–63`, `64–95`, ...  
- Subnet → `10.0.5.64/27`  
- Network → `10.0.5.64`  
- Broadcast → `10.0.5.95`  
- Usable → `10.0.5.65 – 10.0.5.94`  

---

### 7. Real System Commands

```bash
ip addr     # find your IP and subnet
ip route    # find default gateway
