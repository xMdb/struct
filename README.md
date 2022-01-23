# Raspberry Pi/Ubuntu Server Ansible Playbook

This is my Ansible playbook that I use to automatically provision settings and applications on my Raspberry Pi 4 using Ubuntu Server 20.04.

Inspired by Wolfgang's [Infra](https://github.com/notthebee/infra). [Check out his channel](https://www.youtube.com/channel/UCsnGwSIHyoYN0kiINAGUKxg).

## Usage

For this you need a server running Ubuntu.

1. [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems).
2. Clone the repo.
```bash
git clone https://github.com/xMdb/structure
```
3. Edit the `hosts` file and adjust the variables.
4. Run the playbook.
```bash
ansible-playbook run.yml -K
```