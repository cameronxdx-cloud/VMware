
## Firewalling and Load Balancing Overview

In this module, we're going to talk about **network services**.  
Specifically, we will cover:
- **Firewalling**
- **Load Balancing**
- **DHCP**
- **NAT** (Network Address Translation)

We'll also dive deeper into the **Edge architecture**:
- Differences between **bare metal** and **VM form factors**.
- **Performance differences** between the two.

---

### NSX-T Firewall Types
There are two types of firewalls in NSX-T:

- **Distributed Firewall (DFW)**:
  - Runs on all NSX-T nodes.
  - Secures **east-west traffic** between segments.
  - Enables **micro-segmentation** at the firewall level.
  - Follows the compute workload, no matter which host it migrates to.

- **Gateway Firewall**:
  - Runs on a **services router** on the **Edge nodes**.
  - Can operate on either the **Tier-0** or **Tier-1** gateway.
  - Secures **north-south traffic** into and out of the NSX-T environment.
  - Provides broader network protection across multiple networks.
  - **Fixed** to the NSX-T Edge (does not migrate with workloads).

> **Note:**  
> NSX-T firewalling will be covered in much more detail in the upcoming module on **Security Architecture**.  
> This overview is to provide a reference for all NSX-T services in one place.

---

### Load Balancing with NSX-T

Key points:
- **Load balancing basics** remain the same across different vendors.
- In NSX-T:
  - Load balancing instance runs **only on a Tier-1 router**.
  - The Tier-1 router is closest to subnets providing services.
  - Supports **rapid scaling** of services based on load or defined parameters.
  
Example use case:
- A script detects increased network load for web
-  It spins up five or six new instances in a Docker host.
- The load balancer automatically expands to use these new Docker instances.

At its core:
- Load balancing **abstracts the services** that are provided to end users into a **virtual server**, backed by a **pool of multiple servers** serving that particular instance.

---

### Load Balancer Components

- **Virtual Server**:
  - Represents the service (e.g., a web service) with a **virtual IP address** on the Tier-1 gateway.
  - Clients connect to the virtual IP address, which then distributes traffic to the backend pool.

- **Server Pool**:
  - Backend servers serving the requested service.
  - Traffic is directed to pool members based on policies.
  - Policies may **stick sessions** to a specific member (session persistence) or distribute connections statelessly.

- **Health Checks**:
  - Load balancers **perform system checks** against pool members.
  - Health checks can include:
    - Simple TCP or UDP port checks,
    - Pings,
    - Advanced HTTP requests and parsing returned data.
  - If a server fails a health check (e.g., no ping response or HTTP failure):
    - The load balancer removes the unhealthy server from the pool.
    - New or existing sessions are redirected to healthy servers.

