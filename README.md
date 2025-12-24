# **Automated Enterprise Network** <br/>
This network is designed to ensure continuous connectivity between the branch office (NYC) and central office (SF) with built-in redundancy and failover mechanisms to maintain uninterrupted operations for critical workloads. <br/>
##

**Figure 3.1: Overall Network Topology**

<img width="1432" height="766" alt="image" src="https://github.com/user-attachments/assets/f5cd5db9-f2e8-4e77-aee7-8aa87bcef6ca" />


**Figure 3.2: Critical VLANS on Dedicated Access Switches (VLAN 10/20/30)**

<img width="821" height="363" alt="image" src="https://github.com/user-attachments/assets/8315a2a8-d197-4406-a6d9-900dc7adf254" />


**Figure 3.3: User & Guest VLANs on Shared Access Switch (VLAN 100/200/300)**

<img width="596" height="759" alt="image" src="https://github.com/user-attachments/assets/f442313f-fb84-4dd1-b653-d7a98a606441" />

##

**High Availability and Edge Intelligence** <br/>
- Multi-Protocol Routing: Integrated eBGP for robust WAN/Edge peering and OSPF for internal link-state routing ensuring high-speed convergence.
- Gateway Redundancy: Primary and secondary Layer 3 switches utilizing HSRP for transparent sub-second failover.
- Resilient Switching: Optimized STP (Spanning Tree) configuration to ensure a loop-free, fault-tolerant topology. 
- Intelligent NAT: Scalable Network Address Translation (NAT) for seamless branch-to-headquarters communication. <br/>

**Optimized Traffic Segmentation** <br/> 
- VLAN 10 (Core): Critical infrastructure backbone and core services.
- VLAN 20 (Management): Dedicated out-of-band management for administrative tasks and automation traffic.
- VLAN 30 (Compute): High-bandwidth segment dedicated to intensive AI workloads and data processing.
- VLAN 99 (Native): Implemented a dedicated Native VLAN for all trunk links to mitigate VLAN Hopping and Double-Tagging exploits.
- VLAN 100 (R&D): Isolated environment for research and development traffic.
- VLAN 200 (Employee): Secure internal corporate access.
- VLAN 300 (Guest): Sandboxed segment for external and wireless device connectivity. 
- VLAN 999 (Blackhole): All unused ports are administratively disabled and assigned to a non-routed "Blackhole" VLAN to prevent unauthorized physical access. <br/>

**Infrastructure as Code (Iac) & Automation** <br/>
- Ansible Orchestration: Full lifecycle management of network devices via Ansible Playbooks.
- Dynamic Templating: Advanced Jinja2 templates used to generate vendor-agnostic configurations from centralized YAML data models.
- Standardized Deployment: Automated configuration pushes ensure 100% consistency across the fabric, eliminating manual CLI errors. <br/>

**Advanced Security & Management** <br/>
- Management Plane Protection: Restricted SSH access via VTY Access Control Lists (ACLs), ensuring only authorized automation nodes (VLAN 20) can modify device state.
- Port-Level Security: Hardware-level port security to prevent MAC spoofing and unauthorized physical access.
- Secure Credentialing: All sensitive variables (secrets, enable passwords) are fully encrypted using Ansible Vault. <br/>

**Future-Proof Design** <br/>
- Distributed Architecture: Built for horizontal scaling, allowing for the addition of new research teams or compute clusters without re-addressing the core.
- Zero-Trust Foundation: Rigid VLAN isolation and security policies provide the framework for a secure, scalable enterprise network. <br/>

##

```bash
Enterprise-Network/
├── CiscoIOS/          → Backups of current running-configs
├── data/              → Host devices YAML data configurations
├── inventory/         → Ansible inventory and host_vars (encrypted ansible vault)
├── logs/              → Per-device and run logs
├── outputs/           → Timestamped rendered configurations
├── playbooks/         → Deployment playbook
├── templates/         → Modular Jinja2 templates
```

# Setup

## Clone and Enter
```bash
git clone git@github.com:m3lcy/Enterprise-Network.git
cd Enterprise-Network
```

## (Optional) Create a Python virtual environment
```bash
python3 -m venv venv && source venv/bin/activate  
pip install ansible ansible-pylibssh
```

# Usage
(Use **cisco** as Vault Pass)
## Preview/Dry-run 
```bash
ansible-playbook playbooks/deploy_config.yaml -l l3-sw-01 --diff --check --ask-vault-pass
```

## Commit/Apply
```bash
ansible-playbook playbooks/deploy_config.yaml -l l3-sw-01  -e "deploy_mode=commit" --diff  --ask-vault-pass
```

**TechStack** <br/>
**Ansible**, **Jinja2**, **YAML**, **OSPF**, **BGP**, **IP ROUTING**, **DHCP**, **VLANS**, **HSRP**, **NAT**, **Port Security**, **ACLs**, **STP**, **SSH**
