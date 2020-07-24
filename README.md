# ansible-youtrack

Installs Jetbrains youtrack server as systemd-managed docker container.

## System requirements

* Docker
* Systemd

## Role requirements

* python-docker package

## What does this role

* Pull docker image
* Create volume paths for docker container
* Setup systemd unit file
* Start/Restart service

## Role parameters

### Main config

| Variable      | Type | Mandatory? | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| youtrack_image_version | version number | yes |       | The youtrack docker image version (see [Youtrack@Docker Hub](https://hub.docker.com/r/jetbrains/youtrack/tags)) |
| youtrack_data_volume   | absolute path  | yes |       | The data directory path    |
| youtrack_config_volume | absolute path  | yes |       | The config directory path  |
| youtrack_logs_volume   | absolute path  | yes |       | The log directory path     |
| youtrack_backups_volume | absolute path | yes |       | The backups directory path |
| youtrack_port           | number        | yes |       | The server listen port     |
| youtrack_interface      | network address | no | 0.0.0.0 | The docker container bound network |

## Usage

### Requirements

```yaml
- name: install-youtrack
  src: https://github.com/borisskert/ansible-youtrack.git
  scm: git
```

### Playbook

```yaml
- hosts: test_machine
  become: yes

  roles:
    - role: ansible-youtrack
      youtrack_image_version: 2020.3.888
      youtrack_port: 8080
      youtrack_interface: 0.0.0.0
      youtrack_data_volume: /srv/youtrack/data
      youtrack_config_volume: /srv/youtrack/config
      youtrack_logs_volume: /srv/youtrack/logs
      youtrack_backups_volume: /srv/youtrack/backups
```

## Testing

Requirements:

* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox](https://www.virtualbox.org/)
* [Ansible](https://docs.ansible.com/)
* [Molecule](https://molecule.readthedocs.io/en/latest/index.html)
* [yamllint](https://yamllint.readthedocs.io/en/stable/#)
* [ansible-lint](https://docs.ansible.com/ansible-lint/)
* [Docker](https://docs.docker.com/)

### Run within docker

```shell script
molecule test
```

### Run within Vagrant

```shell script
 molecule test --scenario-name vagrant --parallel
```

I recommend to use [pyenv](https://github.com/pyenv/pyenv) for local testing.
Within the Github Actions pipeline I use [my own molecule Docker image](https://github.com/borisskert/docker-molecule).

## License

MIT

## Author Information

* [borisskert](https://github.com/borisskert)
