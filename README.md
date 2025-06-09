
# rkhunter

**Author**: Marcin Dołęgowski (<marcin.dolegowski@debian.org.pl>)  
**Namespace**: `citizennone`  
**License**: MIT  
**Minimum Ansible Version**: 2.9

## Description

Lightweight Ansible role for installing and configuring Rootkit Hunter (RKHunter) on Debian, RedHat, and CentOS/Fedora-based systems.  
Tested on Debian and CentOS using Molecule. Ideal for minimal servers, labs, and DevOps environments.

The role **enables unhide** for Debian systems but **skips unhide installation** on RedHat-based systems by default.  
⚠️ **Note**: RKHunter may require additional tools such as `net-tools`, `iproute2`, etc. Installing them is beyond the scope of this role, as different organizations may manage them differently. 
If you want to install them automatically, set:

```yaml
rkhunter_install_utils: true
```
in `defaults/main.yml`.

## Features

- RKHunter installation
- Logrotate configuration for RKHunter logs
- Periodic RKHunter update and scan configuration

## Role Variables

See `defaults/main.yml` for a full variable list.

Key variables:

```yaml
rkhunter_email: your@email.com
rkhunter_cron:
  update_timer: "* * * * *"
  check_timer: "* * * * *"
```

## Requirements

- Debian-based system (tested on Debian 12 and 11)
- RedHat-based system (tested on CentOS 8)
- Ansible >= 2.9
- Python >= 3.6 on the target system
- Sendmail or any other system mail agent configured

## Example Playbook

```yaml
- name: Install RKHunter
  hosts: all
  become: true
  roles:
    - citizennone.rkhunter
```

## Molecule Support

This role includes a Molecule scenario with the Docker driver for local testing:

```bash
cd roles/rkhunter
molecule test
```
or

```bash
cd roles/rkhunter
molecule converge
```

## License

MIT License

## Disclaimer

This Ansible role is provided in good faith and is intended to assist with rootkit detection on Debian or RedHat-based systems.  
It is **your responsibility** to test the role in a staging environment before deploying it in production.  
The author is **not responsible** for any data loss, access lockouts, service disruption, or any other damage caused by the use or misuse of this role.

**Use at your own risk.**

---

Happy hardening!
