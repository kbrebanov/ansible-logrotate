logrotate
=========

Installs and configures logrotate

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

| Name               | Default | Description                                                          |
|--------------------|---------|----------------------------------------------------------------------|
| logrotate_interval | weekly  | Interval of log rotation (daily, weekly, monthly or yearly)          |
| logrotate_rotate   | 4       | Number of times log files are rotated before being removed or mailed |
| logrotate_create   | true    | Create new log files after rotation                                  |
| logrotate_compress | false   | Compress log files after rotation                                    |

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

Install logrotate and compress log files
```
- hosts: all
  vars:
    logrotate_compress: true
  roles:
    - kbrebanov.logrotate
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
