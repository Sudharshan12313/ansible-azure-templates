# Ansible Azure Infra Automation

This package contains **roles + playbooks + inventory** to manage:
- VM Patching
- NSG (Network Security Group)
- Application Gateway

---

## 🚀 Steps to Use

### 1. Unzip the package
```bash
unzip ansible-azure-infra.zip
cd ansible-azure-infra
```

### 2. Install required collections
```bash
ansible-galaxy collection install azure.azcollection ansible.windows
```

### 3. Update inventory
Edit `inventories/hosts.ini` with:
- Linux VM IPs + SSH key
- Windows VM IPs + WinRM credentials
- Keep `[localhost]` as is for Azure resources

### 4. Update variables
Modify variables in `playbooks/*.yml` (like `rg_name`, `location`, `backend_ip`).

### 5. Test connectivity
```bash
ansible -i inventories/hosts.ini linux -m ping
ansible -i inventories/hosts.ini windows -m win_ping
```

### 6. Run playbooks in check mode (dry run)
```bash
ansible-playbook -i inventories/hosts.ini playbooks/nsg.yml --check
ansible-playbook -i inventories/hosts.ini playbooks/appgw.yml --check
ansible-playbook -i inventories/hosts.ini playbooks/patching.yml --check
```

### 7. Apply changes (real run)
```bash
ansible-playbook -i inventories/hosts.ini playbooks/nsg.yml
ansible-playbook -i inventories/hosts.ini playbooks/appgw.yml
ansible-playbook -i inventories/hosts.ini playbooks/patching.yml
```

---

✅ Now you have a ready-to-use structure for Azure automation.
