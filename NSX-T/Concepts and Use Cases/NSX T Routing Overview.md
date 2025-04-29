
##🧭 Navigation
- Go to the **Networking tab** in **NSX-T Manager**.
- Under **Connectivity**, you’ll find:
  - **Tier-0 Gateways**
  - **Tier-1 Gateways**
  - **Segments**

---

## 🧱 Segments
- Essentially VLANs created within NSX-T.

---

## 🛣️ Tier-0 Gateway
- Connects NSX-T to the **physical external network**.
- Configuration includes:
  - Interfaces
  - Routing options

### 🔌 Interfaces
- 4 external and service interfaces shown.
- 2 interfaces per edge node.
- Uplink Segments:
  - Used for VLAN tagging to define network locations.
  - Both uplinks from each edge VM can go into the same router.
  - Can also connect to multiple routers (e.g., 5-10 upstream routers).

---

## 🌐 BGP Configuration
- Under **BGP settings**:
  - Local BGP configuration (Local AS)
  - 2 BGP neighbors (on VLANs `2712` and `2711`)
  - Both edge nodes use IPs to connect to upstream BGP neighbors.
- Interface is more user-friendly than traditional CLI (e.g., Cisco), but:
  - GUI has **limited BGP configuration depth**.

### 🧠 Note:
- BGP is configured.
- **OSPF is also supported** in **NSX-T version 3.1 and newer**.

---

## 🔁 Route Redistribution
- One redistribution statement configured.
- Redistributes:
  - NAT IPs
  - Connected interfaces
  - Segments
  - Advertised Tier-1 Subnets

### ⚠️ Important:
- Route redistribution must be **enabled**.
- Without it, routing will function internally but **not advertise subnets** connected to virtual switches.

---

## 🧩 Tier-0 ↔ Tier-1 Relationship
- **Tier-0 Gateway**:
  - Connects to **physical network**.
- **Tier-1 Gateway**:
  - Connects to **Tier-0**.
  - Used for:
    - Multitenancy
    - Automation/scripting
    - Security segmentation

### 🔗 Tier-1 Gateway Details
- Example: `t1-gw`
- The **Router Link**:
  - Automatically configured by NSX-T.
  - Auto-assigns IPs (IPv4 & IPv6).
  - No manual configuration required.

---

## 📝 Final Notes
- NSX-T virtual routers (Tier-0 & Tier-1) offer **robust BGP/OSPF implementations**.
- Functionality is **comparable to traditional hardware routers**.

