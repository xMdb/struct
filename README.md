# struct: Raspberry Pi/Ubuntu Server Ansible Playbooks

- [Raspberry Pi](https://github.com/xMdb/struct/tree/master/dnspi)
- [Nova NAS](https://github.com/xMdb/struct/tree/master/nova)

---

These are my two Ansible playbooks that I use to automatically provision settings and applications on my Raspberry Pi 4 using Ubuntu Server, as well as my main server, named Nova, also running Ubuntu Server.

[Ansible](https://www.ansible.com/) is an awesome tool by Red Hat that allows idempotent and reproducible configuration for one or many servers. It only takes one command to run through all the tasks.

Personally, I am learning this to be able to re-provision my Raspberry Pi and Nova server if anything goes wrong. I actually discovered Ansible just before I nuked my Pi's permission system (chown gone wrong). Therefore, I decided to configure everything via Ansible instead of sshing into the Pi and re-downloading all of my docker-compose files. Just run the playbook and it will do the rest.

I learned the very basics of Ansible (and that it exists) from [Wolfgang's Channel](https://www.youtube.com/channel/UCsnGwSIHyoYN0kiINAGUKxg). His [infra](https://github.com/notthebee/infra) playbook he uses to provision his Ubuntu NAS has been very handy. Most of the roles and tasks are from there. Kudos!

EDIT (Nov 2023): I still use Ansible to configure Nginx using templates! However, I use [Docker Compose](https://docs.docker.com/compose/) more frequently, and just backup the docker-compose.yml files. I find it way easier than integrating it with Ansible. If my servers ever go down, or I want to re-install for any reason, I can still use Ansible to help me recover with ease.

## Features

### General

- Installs/updates/upgrades packages, disables password SSH and sets custom hostname
- Installs zsh with oh-my-zsh and a custom Powerline10k theme, sets the default shell as zsh
- Installs and configures Docker (as well as docker-compose and the Ansible Docker module)

### Networking

- Installs and configures Nginx
    * I use Jinja templates to create a file for each service that points the port of the service to a custom URL, such as jellyfin.box. In PiHole, I use Local DNS to assign jellyfin.box to the correct IP, and Nginx routes it accordingly.
    * Each service is configured with an SSL cert, automatic re-writes to HTTPS, CORS and HTTS rules, and the required proxy headers for the service to function.

### Services

Installs and configures the following on the Raspberry Pi:

- [PiHole](https://github.com/pi-hole/pi-hole) (DNS filter)
- [Wireguard VPN](https://github.com/linuxserver/docker-wireguard) (access home network from anywhere)
    * Also fetches client QR codes and config files from the Docker container for use

Installs and configures the following on my Nova server:

- [hd-idle](https://github.com/adelolmo/hd-idle) (spins down disks when idle for a specified time)

Configures the Nginx reverse proxy on my Nova server for the following Docker containers:

- [Dashy](https://github.com/Lissy93/dashy) (home page for self-hosted services)
- [Deluge](https://github.com/linuxserver/docker-deluge) (torrent client)
- [Grafana](https://github.com/grafana/grafana/) (data visualisation)
- [Jellyfin](https://github.com/jellyfin/jellyfin) (free software media system)
- [Jellyseerr](https://github.com/Fallenbagel/jellyseerr) (media library request system for Jellyfin)
- [Librespeed](https://github.com/linuxserver/docker-librespeed) (local speedtests)
- [Photoprism](https://github.com/photoprism/photoprism) (self-hosted online photo browser)
- [Nextcloud](https://github.com/nextcloud/docker) (basically self-hosted MS365)
- [Prometheus](https://github.com/prometheus/prometheus) (data provider to Grafana)
- [Radarr](https://github.com/linuxserver/docker-radarr) (legally obtained Linux ISO collection manager)
- [Sonarr](https://github.com/linuxserver/docker-sonarr) (same as Radarr but for Linux ISO series)
- [Uptime Kuma](https://github.com/louislam/uptime-kuma) (self-hosted monitoring tool and status site)
- [Wakapi](https://github.com/muety/wakapi) (WakaTime-compatible coding statistics dashboard for developers)

## Usage

All you need is something running Ubuntu Server.

1. [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems).
2. Clone the repo.
```bash
git clone https://github.com/xMdb/structure
```
3. Edit the `hosts` file and adjust the variables so it can connect to your server using SSH.
4. Run the playbook.
```bash
ansible-playbook run.yml -K
```

For future runs, omit the -K, as passwordless sudo will be enabled.

For more information, please see the [Ansible docs](https://docs.ansible.com/).
