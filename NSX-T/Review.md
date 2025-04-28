# VMware NSX-T Data Center: Concepts and Use Cases

---

## Module Review

Let's take a couple of minutes and review what we've covered in this module.

We started off with **logical routing**:
- Discussed the **tier‑0** versus the **tier‑1 router**.
  - **Tier‑0**: Connects the NSX environment to the rest of the network (**north‑south traffic**).
  - **Tier‑1**: Connects different segments together (**east‑west traffic**).

We also talked about:
- **Distributed Router** vs **Services Router**:
  - **Distributed Router**: Runs on multiple nodes simultaneously, handling traffic forwarding and routing protocol updates.
  - **Services Router**: Runs on a single node, handling things like **NAT**, **firewalling**, etc.

Then we discussed **logical switching** and the various switch types:
- **vSphere Standard Switch**: Included in any version of VMware.
- **vSphere Distributed Switch**: Extends the standard switch across multiple hosts for consistent naming.
- **N‑VDS**: Older version of the NSX virtual distributed switch.
- **VDS 7.0**: Allows convergence of the vCenter controlled distributed switch with the NSX controlled switch.

We also reviewed **port groups** vs **segments**:
- **Port Groups**: Controlled in vCenter Server, traffic passes directly to the physical network.
- **Segments**: Controlled within NSX; NSX acts as the default gateway, traffic stays within NSX, VLAN may not be advertised to the broader network.

---

