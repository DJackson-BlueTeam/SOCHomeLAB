
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

## Phase 2: The pfSense Installer Process
Start the pfSense Virtual Machine

**1. Welcome Screen**
   - Select Install and press `Enter` on `ok`

**2. WAN Interface Assignment**
   - Select em0 (this matches the first VirtaulBoz Adapter). Press `Enter` on `ok`

**3. LAN Interace Assignment**
   - Select em1 (this matches the internal network adapter). Press `Enter` on `ok`

**4. Interface Confirmation**
   - The Screen will show `WAN -> em0` and `LAN -> em1`. Select Continue and press Enter

**5. Installation Options (File System)**
   - Select >>Continue (Process with the installation) and press `Enter` on `Ok`. Keep the defaults (ZFS and GPT)

**6. Package installation**
   - Select `Yes` this is normal, The installer is downloading the core system files from the internet. Do not interrupt this process.   

## Phase 3: Post-Installation
1. Reboot
   - Once the installation finishes, the system will ask to reboot.

2. Remove The ISO: CRUCIAL STEP
   - WHile the VM is rebooting (or after you shut it down). go back to `Settings > Storage` and remove  the `netgate-installer` ISO. If you don't, the VM will keep starting the installer.

3. Initial CLI Screen
   - After rebooting, you will see a text menu of `pfSense`. It will display your WAN IP (from your router) and your LAN IP (usually defaults to `xxx.xxx.x.x`)
4. Accessing The GuI
   - to finish the setup, you must open the web browser on another VM that is also connected to the Internal Network (intnet) and go to (`https//xxx.xxx.x.x`)
        - Default Username: admin
        - Default Password pfsense (Highly Recommened to Change Password. It will prompt you to do it will configuring through Wizard)
    
## Phase 4: Initial Console Setup
**1. VLANS**
   - When asked "Should VLANs be set up now?", type `n` and press Enter.
**2. Interface Assignment**
   - If prompted again, assign `em0` to `WAN` and `em1` to LAN. Type `y` to proceed.
   
**3. Configure LAN IP (Option 2**)
   - Select Option 2 (Set Interface(s) IP Address).
   - Select 2 for LAN
   - Configure via DHCP? `n`
   - Enter new LAN IPv4: `xxx.xxx.x.x`
   - Subnet bit count: `24`
   - Enable DHCP Server on LAN? `y`
   - Range: `xxx.xxx.x.10` to `xxx.xxx.x.100`
   - Revert to HTTP? `n` (stay on HTTPS)
  
## Phase 5: Windows Malware VM (Flare-VM) Configuration
**1. Network Setting**
   - Shut Down the Windows VM
   - Go to `Setting > Network`.
   - Set `Adapter 1` to `Internal Network`
   - Name musst be exactly `intnet` (to match `pfSense`)

**2. Verify Connection**
   - Start up Windows VM
   - Open Command Prompt and type `ipconfig /renew`
   - You Should see an IPv4 address like `xxx.xxx.x.10` and a Default Gateway of `xxx.xxx.x.1`
