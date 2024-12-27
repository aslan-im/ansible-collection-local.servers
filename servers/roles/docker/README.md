# Docker Ansible Role
This Ansible role installs and configures Docker on Debian and RedHat-based systems.

## Requirements
Ensure that the target systems have network access to the Docker repositories.

## Role Variables
The following variables can be set to customize the role behavior:

### Shared Variables
- `docker_repo_url`: URL of the Docker repository (default: `https://download.docker.com/linux`)
- `docker_packages_to_install`: List of Docker packages to install (default: `['docker-ce', 'docker-ce-cli', 'containerd.io', 'docker-buildx-plugin', 'docker-compose-plugin']`)

### RedHat Specific Variables
- `docker_repo_rhel`: URL of the Docker repository for RedHat (default: `{{ docker_repo_url }}/rhel/docker-ce.repo`)
- `docker_yum_gpg_key`: URL of the Docker GPG key for RedHat (default: `{{ docker_repo_url }}/centos/gpg`)

### Debian Specific Variables
- `docker_repo_debian`: URL of the Docker repository for Debian (default: `{{ docker_repo_url }}/debian`)
- `debian_prerequisites`: List of prerequisite packages for Debian (default: `['ca-certificates', 'curl', 'apt-transport-https']`)
- `docker_apt_gpg_key`: URL of the Docker GPG key for Debian (default: `{{ docker_repo_url }}/{{ docker_apt_ansible_distribution | lower }}/gpg`)
- `docker_gpg_key_file_path`: Path to save the Docker GPG key (default: `/etc/apt/keyrings/docker.gpg`)
- `docker_apt_filename`: Filename for the Docker APT repository (default: `docker`)
- `docker_apt_arch`: Architecture for the Docker APT repository (default: determined based on `ansible_architecture`)
- `docker_apt_repository`: Docker APT repository configuration (default: `deb [arch={{ docker_apt_arch }} signed-by=/etc/apt/keyrings/docker.asc] {{ docker_repo_url }}/{{ docker_apt_ansible_distribution | lower }} {{ docker_distribution_release }} {{ docker_apt_release_channel }}`)

## Dependencies
None.

## Example Playbook
```yml
- hosts: all
  roles:
    - role: docker
```