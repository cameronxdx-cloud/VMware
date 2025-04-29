## Distributed Router 
- Runs on multiple nodes
- Allows for one-hop routing from switches
- Cannot host stateful services
## Service Router
- Runs on a single node (kernel)
- Runs NAT, firewall, etc

## Virtual Switching 
- VSS (vSphere Standard Switch)
- VDS (vSphere Distributed Switch)
- N-VDS(NSX-T Virtual Distributed Switch)
- VDS 7.0 (Allows for converged VDS)

## Transport Zones and Nodes
- Transport Zones limit which hosts can communicate with each other by limiting the visibility of logical switches 
- Limits the switches that trans port nodes can connect to
- Transport Nodes are simply hosts (ESXi, KVM, etc) that are configured to be a part of the NSX-T network.