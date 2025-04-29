# NSX-T Routing – Tier-1 Gateway & Edge Node Exploration

## 🧱 Tier-1 Gateway Overview
- Configuration is **similar to Tier-0**, but with fewer options.
- No need to configure physical **interfaces** directly.

### 🔧 Edge Cluster Assignment
- Tier-1 Gateways run on an **Edge Cluster**.
- Operates in an **active-standby** model:
  - In a 2-node cluster: 1 active, 1 standby.
  - With more nodes, they would appear in the **allocated edges window**.

---

## 📣 Route Advertisement (Tier-1)
- Configurable via the **Edit > Route Advertisement** option.
- Options enabled:
  - **Advertise static routes**
  - **Advertise NAT IPs**
  - **Connected segments**
  - **Service ports**

---

## 🌐 Linked Segments
- Purpose of Tier-1 Gateway: **Connect segments to the overlay network**.
- Example linked segments:
  - `app-server-seg`
  - `web-server-seg`
- Each segment has a **gateway IP address**.
- If DHCP is configured, DHCP ranges would be visible here too.

---

## 🛠️ Edge Node CLI Inspection

### 🔐 Logging In
- Access one of the **Edge Nodes** as `admin`.
- Maximize terminal for clarity.

---

## 🔍 View Logical Routers
- Command: `get logical routers`
- Output:
  - **VRF 0**: Management
  - **VRF 1, 2, 4,**
