# Linux Infrastructure Automation & Monitoring lab 

## Overview
Production like homelab demonstrating Linux administration,
Docker, Ansible, monitoring and CI.

## Tech Stack
- Ubuntu Server
- Docker Compose
- osTicket
- MariaDB
- Ansible
- Zabbix
- GitHub Actions

## Features
- Automated Linux configuration with Ansible
- Containerized osTicket + MariaDB
- Zabbix host monitoring
- HTTP availability monitoring
- Docker container discovery
- Failure detection and recovery testing
- CI validation for YAML, Ansible and Docker Compose

## Deployment

The lab is deployed on an Ubuntu Server virtual machine running under KVM .
Application deployment is automated with Ansible and Docker Compose.

## Monitoring
Monitoring is implemented with Zabbix.

The Ubuntu host is monitored through Zabbix Agent 2.

Monitored metrics include:
- CPU usage
- Available memory
- Filesystem usage
- System uptime
- Network metrics
- Docker information

Docker containers are discovered automatically using the
`Docker by Zabbix agent 2` template.


## CI

GitHub Actions is used to validate infrastructure configuration on every push to the `main` branch and on pull requests.

The CI pipeline performs:

- YAML linting with `yamllint`
- Ansible syntax validation
- Docker Compose configuration validation

Workflow file:

.github/workflows/ci.yml

## Reproducibility Test

The full provisioning and application deployment were successfully validated on a clean Ubuntu VM using Ansible.

The playbooks:
- install Docker and Docker Compose;
- configure required system packages;
- create the application directory;
- transfer Docker Compose configuration;
- deploy the osTicket and MariaDB stack;
- start and verify the services without manual application setup.

Deployment command && Verification:

`docker compose ps | 
curl -I http://localhost:8080`

```bash
ansible-playbook \
  -i ansible/inventory.ini \
  ansible/setup.yml \
  --limit testvm

ansible-playbook \
  -i ansible/inventory.ini \
  ansible/deploy.yml \
  --limit testvm
## Future Improvements
- Automated database backups
- Backup restore testing
- HTTPS / reverse proxy
- Ansible roles``` 
