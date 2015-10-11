logrotate
=========

Installs and configures logrotate

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

<<<<<<< HEAD
| Name               | Default | Description                                                          |
|--------------------|---------|----------------------------------------------------------------------|
| logrotate_interval | weekly  | Interval of log rotation (daily, weekly, monthly or yearly)          |
| logrotate_rotate   | 4       | Number of times log files are rotated before being removed or mailed |
| logrotate_create   | true    | Create new log files after rotation                                  |
| logrotate_compress | false   | Compress log files after rotation                                    |
=======
None
>>>>>>> 19ea373d0b5a3ed3661eefd09460700adb0bf86b

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
<<<<<<< HEAD

Install logrotate and compress log files
```
- hosts: all
  vars:
    logrotate_compress: true
  roles:
    - kbrebanov.logrotate
```
=======
>>>>>>> 19ea373d0b5a3ed3661eefd09460700adb0bf86b

License
-------

BSD

Author Information
------------------

Kevin Brebanov
