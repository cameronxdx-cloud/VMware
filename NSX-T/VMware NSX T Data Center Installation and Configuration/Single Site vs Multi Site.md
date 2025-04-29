## Single-Site Deployment

### Overview:
- A **straightforward setup** when all infrastructure is within a single physical site.

### Key Guidelines:
- **NSX-T Managers** should be installed in the **management cluster**, which typically hosts:
  - vCenter Server
  - Other management components
- **Production workloads** should run in **separate compute clusters**.

### Best Practice:
- **Create a DRS Anti-Affinity Rule** to ensure:
  - NSX-T Managers do **not reside on the same ESXi host**.
  - Improves availability and fault tolerance.

---

## Multi-Site Deployment

### Stretched Cluster Scenario:
- Applies when the **NSX-T environment spans multiple physical sites**.

#### Requirements:
- **< 10 ms network latency** between sites
- **No network congestion**

#### Recommended Manager Placement (Two Sites):
- **2 Managers** in the **preferred site**
- **1 Manager** in the **secondary site**

#### Critical Consideration:
- **NSX-T management plane requires at least 2 Managers online**.
  - If both Managers in the preferred site go down, the management plane becomes non-operational.
  - Recovery options:
    - **vSphere HA**
    - **Manual restart**

#### Scaling to 3 or More Sites:
- Same network criteria apply.
- **Distribute NSX-T Managers across all sites** while maintaining:
  - < 10 ms latency
  - No congestion

---

## Management Access: VIP vs Load Balancer

### Virtual IP (VIP) Access Method:
- Assign **3 IPs to the Managers** + **1 VIP**, all from the **same subnet**.
- Commonly configured using the **management VLAN**.

#### Example:
- Managers: `192.168.51.241`, `.242`, `.243`
- VIP: `192.168.51.240`
- Subnet: `192.168.51.0/24`

#### Prerequisite:
- **Management VLAN must be stretched across sites**

### Alternative: External Load Balancer
- Use this when **IP addresses cannot be assigned from the same subnet**.

#### Benefits:
1. Assign Manager IPs from **different subnets**.
2. **Load-balance sessions** across multiple NSX-T Managers.

---

## Summary

| Scenario        | Recommendation                                     |
| --------------- | -------------------------------------------------- |
| Single-Site     | Managers in management cluster + DRS anti-affinity |
| Multi-Site (2)  | 2 Managers in primary, 1 in secondary              |
| Multi-Site (3+) | Distribute Managers evenly with <10 ms latency     |
| VLAN Available  | Use VIP with IPs from same subnet                  |
| No VLAN Stretch | Use external load balancer                         |