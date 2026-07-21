# zabbix-lab
Zabbix monitoring lab deployed in Docker on Ubuntu.

## Architecture

- **Zabbix Server** — collects data from agents (port 10051)
- **Zabbix Web** — Nginx frontend (port 8080)
- **MySQL** — database for metrics
- **Zabbix Agent** — monitored host

## Quick Start

```bash
docker-compose up -d

Open: http://localhost:8080
    Login: Admin
    Password: zabbix

Monitoring Setup
    Host: Ubuntu
    Template: Linux by Zabbix agent
    Items: 73 (CPU, Memory, Disk, Network)
    Triggers: 35
    Custom trigger: CPU load over 75%

## Screenshots

<p align="center">
  <b>Host Availability</b><br>
  <img src="https://raw.githubusercontent.com/Ivan-qa-rgb/zabbix-lab/main/screenshots/hosts.png" width="800"><br>
  <i>ZBX status green, host Ubuntu online</i>
</p>

<p align="center">
  <b>CPU Utilization</b><br>
  <img src="https://raw.githubusercontent.com/Ivan-qa-rgb/zabbix-lab/main/screenshots/cpu.png" width="800"><br>
  <i>CPU load with custom trigger over 75%</i>
</p>

<p align="center">
  <b>Memory Utilization</b><br>
  <img src="https://raw.githubusercontent.com/Ivan-qa-rgb/zabbix-lab/main/screenshots/memory.png" width="800"><br>
  <i>Memory usage ~23%</i>
</p>

Tech Stack
    Zabbix 7.0
    Docker & Docker Compose
    MySQL 8.0
    Ubuntu 
