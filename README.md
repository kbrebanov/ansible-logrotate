logrotate
=========

[![Ansible Role](https://img.shields.io/ansible/role/5887.svg)](https://galaxy.ansible.com/list#/roles/5887)

Installs and configures logrotate

Requirements
------------

This role requires Ansible 1.9 or higher.

Role Variables
--------------

| Name                   | Default                                                                                             | Description                              |
|:-----------------------|:----------------------------------------------------------------------------------------------------|:-----------------------------------------|
| logrotate_options      | [ 'weekly', 'su root syslog', 'rotate 4', 'create' ]                                                | List of default options                  |
| logrotate_wtmp         | { logs: ['/var/log/wtmp'], options: ['missingok', 'monthly', 'create 0664 root utmp', 'rotate 1'] } | Logrotate options for wtmp               |
| logrotate_btmp         | { logs: ['/var/log/btmp'], options: ['missingok', 'monthly', 'create 0660 root utmp', 'rotate 1'] } | Logrotate options for btmp               |
| logrotate_applications | []                                                                                                  | Logrotate options for other applications |


Dependencies
------------

None

Example Playbook
----------------

Install logrotate
```
- hosts: all
  roles:
    - kbrebanov.logrotate
```

Install logrotate and configure rotation for ufw
```
- hosts: all
  vars:
    logrotate_applications:
      - name: ufw
        definitions:
          - logs:
              - /var/log/ufw.log
            options:
              - rotate 4
              - weekly
              - missingok
              - notifempty
              - compress
              - delaycompress
              - sharedscripts
            postrotate:
              - invoke-rc.d rsyslog reload >/dev/null 2>&1 || true
  roles:
    - kbrebanov.logrotate
```

Install logrotate and configure rotation for apt
```
- hosts: all
  vars:
    logrotate_applications:
      - name: apt
        definitions:
          - logs:
              - /var/log/apt/term.log
            options:
              - rotate 12
              - monthly
              - compress
              - missingok
              - notifempty
          - logs:
              - /var/log/apt/history.log
            options:
              - rotate 12
              - monthly
              - compress
              - missingok
              - notifempty
  roles:
    - kbrebanov.logrotate
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
