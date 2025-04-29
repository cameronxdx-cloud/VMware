## Overview
- NSX-T consists of **three integrated software planes**:
  - **Management Plane**
  - **Control Plane**
  - **Data Plane**

---

## 1. Management Plane
- Serves as the **single-entry point** for NSX-T configuration.
- Accessed via:
  - Web UI
  - REST API
- Stores configuration in an **in-memory database** called **CorfuDB**.
  - Transactions are written in short transaction-like files.
  - Queries are served from memory for performance and scalability.
- **Do not take snapshots** of NSX Manager appliances:
  - Risk of database corruption.
  - Snapshots are **auto-disabled since NSX-T 3.0.1**.
- Manages:
  - Integration with **vCenter Server**
  - Integration with **vRealize Automation**
- Works in an **active-passive** mode via a **Virtual IP (VIP)**:
  - One Manager becomes the owner of the VIP and handles all traffic.

---

## 2. Control Plane
- Responsible for **translating configurations** into **stateless instructions**.
- Pushes these instructions to:
  - Data Plane
  - Forwarding engines
- Divided into:
  - **Central Control Plane (CCP)** – resides on NSX Manager nodes
  - **Local Control Plane (LCP)** – resides on transport nodes (e.g., ESXi, Edge)
- Works in **active-active** mode.
  - Uses **control plane sharding** for scalability:
    - Each transport node is assigned to a single NSX Manager.
    - Load is distributed between Managers.

---

## 3. Data Plane
- Responsible for **actual data forwarding** based on control plane rules.
- Includes:
  - **ESXi hosts**
  - **KVM hosts**
  - **NSX Edge nodes**
  - **Bare metal servers**
  - **Public cloud environments** (Azure, AWS)
- Components are called **Transport Nodes**.
- Also handles:
  - **Topology change detection**
  - **Stat collection and reporting** back to management and control planes
- Communicates over:
  - **TCP ports 1234 and 1235**

---

## 4. NSX-T Manager
- Critical component that hosts both:
  - Management Plane
  - Control Plane (since NSX-T 2.4)
- **Management Cluster** setup in production:
  - Typically deploy **3 NSX Managers**
  - Use a **Virtual IP** for cluster access
- Enables:
  - High availability
  - Scalability
  - Integration with cloud management tools

---

## 5. Edge Nodes (Preview)
- Act as **gateways** for traffic entering or leaving NSX-T environments.
- Will be covered in more detail later.

---

## Summary
- NSX-T uses a **modular, distributed architecture** for scalability and resiliency.
- Management Plane = Configuration entry point
- Control Plane = Logic and state distribution
- Data Plane = Traffic forwarding and telemetry