[![No Maintenance Intended](http://unmaintained.tech/badge.svg)](http://unmaintained.tech/)

logrotate
=========

[![Build Status](https://travis-ci.org/kbrebanov/ansible-logrotate.svg?branch=master)](https://travis-ci.org/kbrebanov/ansible-logrotate)

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
```yaml
- hosts: all
  roles:
    - kbrebanov.logrotate
```

Install logrotate and configure rotation for ufw
```yaml
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
```yaml
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
