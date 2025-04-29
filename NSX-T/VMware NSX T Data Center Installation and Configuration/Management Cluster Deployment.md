# NSX-T Management Cluster Deployment and Verification (Demo Summary)

## Overview
This walkthrough covers:
- Installing the **first NSX-T Manager** step-by-step
- **Adding vCenter Server** as a compute manager
- **Deploying additional NSX-T Managers** to complete the management cluster
- **Validating** installation before proceeding to advanced configuration

---

## Platform Consideration
- NSX-T Managers can be deployed on:
  - **VMware vSphere** (preferred in most real-world deployments)
  - **Linux KVM**

---

## NSX-T Manager Installation on VMware vSphere

### Prerequisites:
- **NSX-T 3.2 OVA template** downloaded
- **vSphere 7 Update 3** with 3 ESXi hosts
- **vCenter Server** accessible

### Deployment Steps:
1. **Deploy OVF Template**:
   - Right-click on the cluster > Deploy OVF Template
   - Select **Local File**, then upload `nsx-unified-appliance` OVA
2. **Name & Folder Selection**:
   - Name: `nsxtmgr01`
   - Folder: Custom folder (e.g., `NSX-T`)
3. **Select Compute Resource**:
   - Choose ESXi host or cluster with DRS enabled
4. **Review Details**:
   - Ensure **300 GB free space** if using thick provisioning
   - Snapshot functionality is disabled by default
5. **Choose Appliance Size**:
   - Options: Extra Small, Small, Medium, Large
   - **All managers must have the same size**
   - Demo: `Small` size selected
6. **Select Storage**:
   - Example: vSAN (thin provisioning enforced by default)
7. **Network Configuration**:
   - Choose **management port group** for vNIC
8. **Customize Template Settings**:
   - Configure:
     - Passwords for `admin`, `root`, `GRUB`
     - GRUB password & timeout (mandatory in NSX-T 3.2+)
     - (Optional) Enable `audit` account by setting password
     - Hostname
     - Appliance Role:
       - NSX Manager (selected)
       - NSX Cloud Service Manager
       - NSX Global Manager
     - IP Settings:
       - Static IP, subnet mask, gateway
       - DNS, domain name, NTP
     - Enable SSH (recommended for CLI access)
     - Do **not** modify internal VMware section
9. **Review & Finish**:
   - Click **Finish** to begin deployment

---

## Post-Deployment

### Initial Boot:
- Takes **~20–30 minutes**
- After boot:
  - Power on the VM
  - Login via FQDN using `admin` account
  - Accept **End User License Agreement**
  - UI defaults to **dark mode** (toggleable)

### Web UI Dashboard:
- Displays system summary
- **Next steps** shown:
  - Add **vCenter Server** as a compute manager
  - Deploy **2 additional NSX Managers** for high availability

---

## Key Notes:
- All NSX-T Managers must be **same size**
- Avoid snapshots due to in-memory database
- **GRUB password & timeout required** for root password recovery
- **Enable SSH** for operational CLI access, but not for root (security best practice)
- Time sync and DNS are **critical** for NSX functionality

---

## Next Steps (Covered in Future Demos):
- Register vCenter Server in NSX-T as a **Compute Manager**
- Deploy the **second and third NSX Managers**
- Finalize and **verify management cluster setup**