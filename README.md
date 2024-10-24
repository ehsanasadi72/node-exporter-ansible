
---

### **Ansible Playbook Guide: Node Exporter Installation**


#### **Environment Variables**
In the `config/env.yml` file, the following variables are defined:

1. **`monitoring_ip`**: The IP address of the monitoring server, likely used to configure where Node Exporter sends metrics or from where it allows access.
   - Example: `192.168.5.22`
   
2. **`basic_auth_user`**: The username used for basic authentication when accessing the Node Exporter service.
   - Example: `user`
   
3. **`basic_auth_pass`**: The password used for basic authentication when accessing the Node Exporter service.
   - Example: `pass1234`

These variables will ensure that only authorized users can access the Node Exporter metrics, providing basic authentication.

### **Step 1: Create and Activate a Python Virtual Environment**

1. **Create a Python Virtual Environment**: 
```bash
python3 -m venv .venv
```
2. **Activate the Virtual Environment**:
```bash
source ansible_env/bin/activate
```
2. **Set Up the `requirements.txt File`**:
```bash
source ansible_env/bin/activate
```

### **Step 2: Run Your Ansible Playbooks**

#### **Playbook Tags**
- **`install-node-exporter-tls`**: Installs Node Exporter with TLS and basic authentication.
- **`install-node-exporter-non-tls`**: Installs Node Exporter without TLS but may still use basic authentication.
- **`delete-node-exporter`**: Uninstalls or removes Node Exporter from the target systems.

##### *1. Install Node Exporter with TLS*

```bash
ansible-playbook -l all -i src/inventory.ini src/play.yml --tags "install-node-exporter-tls" --extra-vars @./config/env.yml
```
##### **2. Install Node Exporter without TLS**
```bash
ansible-playbook -l all -i src/inventory.ini src/play.yml --tags "install-node-exporter-non-tls" --extra-vars @./config/env.yml
```
##### **3. Delete Node Exporter**
```bash
ansible-playbook -l all -i src/inventory.ini src/play.yml --tags "delete-node-exporter" --extra-vars @./config/env.yml
```
- This tag will stop and remove Node Exporter from the servers.
- **No specific environment variables** are needed other than inventory details.
