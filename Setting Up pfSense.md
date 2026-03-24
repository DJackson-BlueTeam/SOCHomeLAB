
# What is pfSense


pfSense is a full operating system that is built on FreeBSD "Berkeley Software Distribution"; which is a robust, Unix-Like open-source OS known for its stability, security, and advanced networking capabilities.

- pfSense intergrates the FreeBSD kernel with Packet Filter (pf) firewall engine, providing a powerful platform for routing, firewalling, VPN, and network services.
- This allows pfSense to act as a dedicated network appliance OS, whether installed on a physical hardware or deployed as a virtual machine.

Key OS Characteristics
---
**Base System**
- FreeBSD (64-bit), oddering a secure and stable foundation.

**Firewall Engine**
- Packet Filter (pf) for stateful inspection and rule processing.

**Management Interface**
- Web-Based GUI for configuration and monitoring.

**Service Daemons** 
- Built-in support for DHCP, DNS, TCP, NTP, and more.

Packet System
- Extendable via packages like snort, Suricata, and OpenVPN

Deployement (Virtual Machines)
---
Runs on hypervisors like VirtualBox, VMware, KVM, or in cloud environments (AWS, AZURE) with pfSense Plus.

# Full Step-by-Step Procedure: Installing pfSense on Oracle VirtualBox
---
## Phase 1: VirtualBox VM Configuration
**1. Create the Virtual Machine**
   - Name: `pfSene Soc Lab` (or whatever name is desirable)
   - Type: `BSD`
   - Version: `FreeBSD (64-bit)`
  
**2. System Settings**
  - RAM: Set to 2048 MB (2GB) (RECOMMENEDED)
  - Processors: 2 CPUs
  - Features: Keep "PAE/NX" and "Shared Clipboard/Drag-and-Drop" Disabled for security isolation.

**3. Display Settings**
  - Video Memory: 16MB (pfSense is texted based)
  - Graphics Controller: VMSVGA
  - 3D Acceleration: Disabled

**4. Storage Settings**
  - Controller IDE: Attach the netgate-installer-v1.1.1-RELEASED.iso (or most current version)
  - Hard Disk: Ensure the `.vdi` file is created (recommened size is 8GB or more)

**5. Network Settings**
  - Adapter 1 (WAN): Enable and set to Bridge Adapter (Select your Wi-fi/Ethernet card) or NAT (this is the door to your internet)
  - Adapter 2 (LAN): Switched to the `Expert` tab, Enable the adapter, and set to Internal Network (name it `intnet`). This is the door to the private lab.
