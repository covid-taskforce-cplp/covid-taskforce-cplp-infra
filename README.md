# covid-taskforce-cplp-infra

## Usage

Assuming you already have the [Requisites](#requisites) meet, this is how you
use:

### How to download this ansible-linux-ha-cluster to your machine

```bash
git clone https://github.com/fititnt/ansible-linux-ha-cluster.git .

# This will download https://github.com/fititnt/https://github.com/fititnt/ap-application-load-balancer
# on roles/ap-application-load-balancer
ansible-galaxy install -r requirements.yml --roles-path roles/
```

## Requisites

### Ansible

Follow the [https://docs.ansible.com: Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)

Windows users can [use Windows WSL (then could choose Ubuntu 18.04 LTS)](https://docs.microsoft.com/windows/wsl/install-win10).
Check this [Windows Frequently Asked Questions](https://docs.ansible.com/ansible/latest/user_guide/windows_faq.html)

**Tip: if is your first time with Ansible, this computer is likely to be own
computer and NOT the server where you want to install ALB**. One way to explain
Ansible would be _it converts YAML variables + tasks on commands to execute
(more often) on remote hosts that can be accessed over SSH_.
