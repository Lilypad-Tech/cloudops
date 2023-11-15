# CloudOps: Lilypad Infrastructure Deployment Using Ansible

This guide provides instructions for deploying the Lilypad infrastructure on arbitrary Debian-based nodes using Ansible.

## Prerequisites

Ensure you have Ansible installed on your control machine and access to Debian-based target nodes.

## How to Use

### 1. Configure the Inventory File

- Specify the IP addresses of your target nodes.
- Set the ansible user for SSH connections.

Example Inventory File (`inventory`):

```ini
[lilypad]
192.0.2.1 ansible_user=ubuntu
```

### Prepare Environment Variable Files
- Place a `.env.network` file in the root directory, where network corresponds to the target blockchain network (e.g., sepolia, mumbai).
- Each `.env.network` file should contain the necessary environment variables for that specific network.

### 3. Configure the Deployment Playbook (deploy.yml)
- Update the network variable in the vars section of the playbook to match the target network. This variable determines which `.env.network`` file will be used.
- The playbook will automatically select and copy the appropriate .env file based on the specified network.

Example deploy.yml:

```ini
---
- name: Deploy Lilypad Infrastructure
  hosts: lilypad
  become: true

  vars:
    network: "mumbai"  # Set your target network here

  # ... (rest of the playbook)

```

### 4. Execute the Playbook
Run the Ansible playbook to start the deployment on the specified nodes.

```bash
ansible-playbook -i inventory deploy.yml
```

By following these steps, you can deploy the Lilypad infrastructure on your desired Debian-based nodes for different blockchain networks using Ansible. Ensure that each target environment has its corresponding .env.network file for a seamless deployment process.
