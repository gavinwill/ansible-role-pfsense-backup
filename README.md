Role Name
=========

This role is designed to interact with a pfsense firewall to create and download a local backup of the firewalls configuration. This runs locally to interact with pfsense via the webinterface. Currently it is limited to downloading just the basic configuration and does not include RRD Data or SSH keys as of writing.


Role Variables
--------------

| Name          | Description   | Default               |
| ------------- | ------------- | ----------------------|
| pfsense_hostname  | Hostname or IP of Fireall      |   |
| pfsense_username  | Username to login to pfsense   |   |
| pfsense_password  | password to login to pfsense   |   |
| pfsense_backup_page  | url for backup page in web interface  | `diag_backup.php`  |
| pfsense_backup_directory  | Local Backup Directory to save pfsense configr  |  |
| pfsense_backup_filename  | Filename of the saved file  | `'{{ pfsense_backup_directory }}/{{ pfsense_hostname }}-{{ ansible_date_time.iso8601 }}.xml'`  |
| pfsense_https  | If using HTTPS to connect to firewall | `true`  |
| pfsense_validate_certificates | Check for valid certificates  | `true` |
| pfsense_backup_no_log  | Hide output from ansible logs  | `true` |



Example Playbook
----------------

```
- hosts: 'localhost'
  connection: local 
  vars: 
    - pfsense_hostname: 'pfsense.example.com'
    - pfsense_username: 'pfbackup'
    - pfsense_password: 'redactedpassword'
    - pfsense_backup_directory: '/backups'
  roles:
    - role: ansible-role-pfsense-backup
```

License
-------

MIT

Author Information
------------------

Gavin Will - https://github.com/gavinwill
