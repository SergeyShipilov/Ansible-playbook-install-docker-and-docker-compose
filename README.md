Hi, ![](https://user-images.githubusercontent.com/18350557/176309783-0785949b-9127-417c-8b55-ab5a4333674e.gif)my name is Serhii Shypylov
=========================================================================================================================================

-------------------------------

### Socials

<p align="left"> <a href="https://github.com/Shipssv83" target="_blank" rel="noreferrer"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github-dark.svg" /> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github.svg" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/github.svg" width="32" height="32" /> </picture> </a> <a href="https://www.linkedin.com/in/sergey-shipilov-7262a31b4/" target="_blank" rel="noreferrer"> <picture> <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin-dark.svg" /> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin.svg" /> <img src="https://raw.githubusercontent.com/danielcranney/readme-generator/main/public/icons/socials/linkedin.svg" width="32" height="32" /> </picture> </a></p>
---

# Docker and Docker Compose Installation Playbook

This Ansible playbook automates the installation and configuration of Docker and Docker Compose on target hosts. It also ensures that the required Python packages are installed, and user permissions for Docker are set up properly.

## Playbook Overview

The playbook performs the following tasks:

- **Docker Installation**: Installs Docker using the `geerlingguy.docker` role.
- **Docker Compose Installation**: Installs Docker Compose at the specified version.
- **Python Package Installation**: Ensures required Python packages, including `docker` and `docker-compose`, are installed using `pip`.
- **User Permissions**: Adds specified users to the Docker group for managing Docker without root access.
- **Firewall Configuration**: Optionally configures UFW to allow Docker traffic using the `firewall-ufw-docker` role.

## Requirements

- Ansible 2.9+ installed on the control node.
- SSH access to the target hosts.
- The target hosts should be running a Linux-based operating system (e.g., Ubuntu, RHEL).

## Roles Used

- **geerlingguy.pip**: Manages the installation of Python packages using `pip`.
- **geerlingguy.docker**: Installs and configures Docker.
- **firewall-ufw-docker**: Configures UFW firewall to allow Docker traffic (optional).

## Variables

You can customize the playbook by defining the following variables:

- `hosts`: The target hosts where Docker and Docker Compose will be installed.
- `pip_install_packages`: A list of Python packages to install using `pip`. Defaults include:
  - `docker`
  - `docker-compose`
  - `setuptools`
- `docker_install_compose`: Whether to install Docker Compose (default: `true`).
- `docker_compose_version`: Version of Docker Compose to install (default: `v2.29.6`).
- `docker_compose_arch`: The architecture for Docker Compose binary (default is based on `ansible_architecture`).
- `docker_compose_path`: Path where Docker Compose will be installed (default: `/usr/local/bin/docker-compose`).
- `docker_users`: A list of users to be added to the Docker group, so they can manage Docker without `sudo`.

### Example of Variable Configuration in Playbook

```yaml
vars:
  pip_install_packages:
    - name: project
    - name: project-compose
    - name: setuptools
  docker_install_compose: true
  docker_compose_version: "v2.29.6"
  docker_compose_arch: "{{ ansible_architecture }}"
  docker_compose_path: /usr/local/bin/project-compose
  docker_users:
    - USER-NAME
```

# Running the Playbook
Run the playbook with the following command:

```
ansible-playbook -i inventory --user dev --extra-vars "host=host_name" playbooks/docker-install.yml
```

```
ansible-playbook docker-install.yml -i inventory --extra-vars "docker_compose_version=v2.30.0"
```


License
This project is licensed under the MIT License - see the LICENSE file for details.