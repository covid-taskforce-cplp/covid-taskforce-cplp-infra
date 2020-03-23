# covid-taskforce-cplp-infra
**This repository contain the main [Ansible](https://www.ansible.com/)
[Infrastructure-As-Code](https://en.wikipedia.org/wiki/Infrastructure_as_code)
from the [covid-taskforce-cplp organization](https://github.com/covid-taskforce-cplp).
The non-Ansible resources are on the [logbooks folder](logbooks/).**

## List of servers

**Check also: [Infra resources of covid-taskforce-cplp](https://github.com/orgs/covid-taskforce-cplp/projects/1)<sup>Organization Dashboard</sup>.**

### oswaldo-cruz.vps.etica.ai
> This is the "main" server for heavy workloads. Addtional servers may be added later.

- **DNS**: oswaldo-cruz.vps.etica.ai
- **IP**: 167.86.127.220 _(Please: use DNS and not IP on your applications, this may change!)_
- **RAM**: 8GB
- **Disk:**: 200GB SSD
- **Network:** 200Mbit/s _(UNLIMITED Traffic)_
- **Cost**: 4.99 EUR / month (via @fititnt)

### oswaldo-cruz.hom.vps.etica.ai
> This is the "homolog/testing server version of oswaldo-cruz.vps.etica.ai

- **DNS**: oswaldo-cruz.hom.vps.etica.ai
- **IP**: 167.86.127.225
- **RAM**: 8GB
- **Disk:**: 200GB SSD
- **Network:** 200Mbit/s _(UNLIMITED Traffic)_
- **Cost**: 4.99 EUR / month (via @fititnt)

### covid-chagas.vps.etica.ai
> Proxy server

- **DNS**: covid-chagas.vps.etica.ai
- **IP**: 191.252.103.250
- **RAM**: 512MB
- **Disk:**: 20GB SSD
- **Network:** ? (Note: maximum 1TB of data transfer without extra costs)
- **Cost**: 15,90 BRL / month (via @fititnt)

## Usage

Assuming you already have the [Requisites](#requisites) meet, have the
`.valt/secret` file with the same value of who created the valted passwords,
and the computer running Ansible already can ssh on the target servers, this is
a quickstart on
how to run.

### Production mode

#### Oswaldo

```bash
ansible-playbook -i inventories/oswaldo-prod/ --vault-password-file .valt/pass playbook.yml
```

#### Chagas

> Chagas server is not using Ansible at this moment.

### Homolog mode

#### Oswaldo

```bash
ansible-playbook -i inventories/oswaldo-homolog/ --vault-password-file .valt/pass playbook.yml
```

### About .valt/pass
Please read [.valt/README.md](README.md)

## Requisites

### Ansible

Follow the [https://docs.ansible.com: Installation Guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html)

Windows users can [use Windows WSL (then could choose Ubuntu 18.04 LTS)](https://docs.microsoft.com/windows/wsl/install-win10).
Check this [Windows Frequently Asked Questions](https://docs.ansible.com/ansible/latest/user_guide/windows_faq.html)
