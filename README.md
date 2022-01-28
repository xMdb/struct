# struct: Raspberry Pi/Ubuntu Server Ansible Playbook

This is my Ansible playbook that I use to automatically provision settings and applications on my Raspberry Pi 4 using Ubuntu Server 20.04.

Ansible is an awesome tool that allows idempotent and reproducible configuration for one or many servers. It only takes one command to run through all the tasks.

Personally I am learning this to be able to re-provision my Raspberry Pi if anything goes wrong. I actually discovered Ansible just before I nuked my Pi's permission system (chown gone wrong). Therefore, I decided to configure everything via Ansible instead of sshing into the Pi and re-downloading all of my docker-compose files. Just run the playbook and it will do the rest.

I learned the very basics of Ansible (and that it exists) from [Wolfgang's Channel](https://www.youtube.com/channel/UCsnGwSIHyoYN0kiINAGUKxg). His [Infra](https://github.com/notthebee/infra) playbook he uses to provision his Ubuntu NAS has been very handy. Most of the roles and tasks are from there. Kudos!

## Features

### General

- Installs/updates/upgrades packages, disables password SSH and sets custom hostname
- Installs zsh with oh-my-zsh and a custom Powerline10k theme, sets the default shell as zsh
- Installs and configures Docker (as well as docker-compose and the Ansible Docker module)

### Services

Installs and configures the following: 

- PiHole + Unbound (DNS filter)
- Firefly III (personal finance manager)
- Homer (self-hosted dashboard)

### Networking

- Configures all applications/services to use SWAG, which includes an Nginx reverse proxy, SSL, and fail2ban.

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