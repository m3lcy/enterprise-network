# **Automated Enterprise Network** <br/>
This network is designed to ensure continuous connectivity between the branch office (NYC) and central office (SF) with built-in redundancy and failover mechanisms to maintain uninterrupted operations for critical workloads. <br/>
##

**Figure 3.11: Main Topology**

![image](https://github.com/user-attachments/assets/29e34b99-1105-413d-b282-71f13fa60433)


**Figure 3.12: VLAN Segmentation - High Performance Computing VLANs**

![image](https://github.com/user-attachments/assets/f2408ec4-0ca7-4c90-9eff-c22db12c8574)


**Figure 3.13: VLAN Segmentation - General Access VLANs**

![image](https://github.com/user-attachments/assets/6fe4f79a-0f5d-4777-b47a-89dee45562ee)

##

**High Availability and Redundancy** <br/>
- WAN connectivity with NAT ensures seamless branch to central communication, even during network disruptions.
- Primary and secondary Layer 3 switches with HSRP provide automatic failover.
- Spanning Tree Protocol (STP) ensures loop-free fault tolerant connectivity. 
- Dynamic routing protocols (OSPF, RIP) allow the network to adapt to changes and maintain resilient routing. <br/>

**Optimized Traffic Segmentation** <br/> 
- Core VLAN (10): Essential network functions.
- Management VLAN (20): Administrative tasks and monitoring.
- Compute VLAN (30): Prioritized AI workloads with QoS for low-latency and high bandwidth data processing.
- R&D (100): Supports research and development traffic.
- Employee (200): Provides internal employee network access.
- Guest (300): Supports external and wireless device connectivity. <br/>
  **Port security restricts unauthorized device access, ensuring secure segmentation.** <br/>

**Automation & Templates** <br/>
- Ansible is used to automate configurations for various protocols and routing.
- Jinja2 templates dynamically generate device configurations, reducing manual effort and ensuring consistency.
- Automated logging and configuration deployment allow the network to be managed efficiently while preventing errors from manual configuration. <br/>

**Security & Management** <br/>
- ACLs, SSH, VTP, NAT, Port Security etc. are used to enforce security and external access. <br/>
- All sensitive credentials (device passwords, enable secret etc.) are encrypted using **Ansible Vault**.

**Future-Proof Design** <br/>
- VLAN segmentation, distributed routing, loop-prevention, and security policies enable scalable growth.
- Supports evolving workloads and additional research teams without performance compromise. <br/>

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

## Clone and Setup
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

## Preview/Dry-run 
```bash
ansible-playbook playbooks/deploy_config.yaml -i inventory/hosts.yaml --check --diff --limit l3-sw-01 --ask-vault-pass
```

## Commit/Apply
```bash
ansible-playbook playbooks/deploy_config.yaml -i inventory/hosts.yaml --extra-vars "deploy_mode=commit" --diff --limit l3-sw-01 --ask-vault-pass
```

**TechStack** <br/>
**Ansible**, **Jinja2**, **YAML**, **OSPF**, **DHCP**, **QOS**, **VLANS**, **HSRP**, **NAT**, **Port Security**, **RIP**, **ACLs**, **STP**, **VTP**, **SSH**