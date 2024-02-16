# Overview

## Naming convension 


| Short | Long                   |
| ----- | ---------------------- |
| prx   | Proxmox                |
| db    | Database               |
| ns    | Nameserver/DNS         |
| srv   | Service                |
| home  | local DNS server entry |

## Network topography

![[homelab_overview | width=200%]]

## Services in the VMs

| server      | services                                          |
|:----------- | ------------------------------------------------- |
| srv-prod-1  | Portainer, Nginx Proxy Manager, VS Code Server    |
| srv-prod-2  | Home Assistant, Proxmox and Kubernetes Monitoring |
| srv-prod-3  | Ansible and Terraform                             |
| srv-prod-ah | Python API and Grafana                            |
| db-prod-1   | InfluxDB for srv-prod-db                          |
| srv-test-1  | K3s                                               |
| srv-demo-2  | Factorio game server                              |
