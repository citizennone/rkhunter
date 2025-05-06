# debian_hardening_lite

**Author**: Marcin Dołęgowski (<marcin.dolegowski@debian.org.pl>)  
**Namespace**: `citizennone`  
**License**: MIT  
**Minimum Ansible Version**: 2.9

## Description

Lightweight security hardening role for Debian-based systems.  
Includes tools like `rkhunter`, `unattended-upgrades`, basic `SSH` and `sudo` lockdown, log hygiene (`logrotate`), and minimal service exposure.  
Ideal for minimal servers, labs, and DevOps environments.

## Features

- RKHunter installation and periodic check configuration
- Fail2ban support
- Unattended Upgrades with safe defaults and exclusions
- SSH Hardening:
  - Optional creation of admin user with SSH key-based login
  - Optional disabling of root login
  - Custom port and allowed users/groups
- System Banner
- Extensive logrotate configuration for:
  - rkhunter, fail2ban, auth, unattended upgrades, syslogs
  - Apache, Nginx, MySQL, PostgreSQL, Redis, MongoDB, RabbitMQ, Kafka, Varnish, Zabbix, HAProxy
  - Conditional deployment based on detected packages
- Optional basic sysctl rules
- Optional disabling of unneeded services (like Avahi, CUPS, etc.)

## Role Variables

See `defaults/main.yml` for full variable list.

Key variables:

```yaml
ssh_key_auth_enabled: true
ssh_admin_user: admin
ssh_admin_key_path: ~/.ssh/id_rsa.pub
logrotate_enabled: true
fail2ban_enabled: false
rkhunter_enabled: true
...
```

## Requirements

- Debian-based system (tested on Debian 12 and 11)
- Ansible >= 2.9
- `ansible.posix` collection

Install via:

```bash
ansible-galaxy collection install ansible.posix
```

## Example Playbook

```yaml
- name: Harden Debian server
  hosts: all
  become: true
  roles:
    - citizennone.debian_hardening_lite
```

## Molecule Support

This role includes Molecule scenario with Docker driver for local testing:

```bash
cd roles/debian_hardening_lite
molecule test
```

## License

MIT License

## Disclaimer

This Ansible role is provided in good faith and intended for general-purpose hardening on Debian systems.  
It is your responsibility to test the role in a staging environment before applying to production.  
The author is **not responsible** for any potential data loss, access lockout, or service disruption caused by misuse or incorrect application of this role.

Use at your own risk.

---

Happy hardening!