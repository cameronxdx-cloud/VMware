## Overview
Before putting a newly installed NSX-T system into production, it must be **verified**. Verification can be performed through:
- **Web UI**
- **Command-Line Interface (CLI)**

---

## Web UI Verification

### Steps:
1. Navigate to the **System** tab → Click on **Appliances**.
2. Under **NSX Manager**, check the **Management Cluster status**:
   - Status should be **green and stable**.
   - If not, further investigation is required.

### View Detailed Status:
- Click **View Details** to access:
  - **NSX Manager Appliance info**:
    - CPU, Memory, and Storage usage
  - **List of services** and their statuses:
    - All services should be **UP**
    - **Repository Sync** should show **Success**

---

## CLI Verification

### Accessing NSX CLI:
- SSH into any **NSX Manager**
  - OR open a **direct console** from ESXi/KVM host
- **Login using the `admin` account** (not `root`)

### Key Commands:
- `get cluster status`
  - Displays the **overall management cluster status**
  - Shows role status: `CONTROLLER`, `MANAGER`, and `DATASTORE` per node
- `get services`
  - Lists all NSX services and their current state
- `start service <service-name>`
  - Starts a specific service (e.g., `start service snmp`)

### Notes:
- The following services may not be running by default:
  - `liagent`
  - `migration-coordinator`
  - `snmp`
- These do **not require intervention** unless explicitly needed.

---

## Summary
- Use both **Web UI** and **CLI** to verify NSX-T readiness before production.
- Focus on cluster health, service status, and sync validation.
- CLI provides deeper insights and control for troubleshooting.