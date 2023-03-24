# Role Name

This role is designed to interact with a pfsense firewall to create and download a local backup of the firewalls configuration. This runs locally to interact with pfsense via the webinterface. 

By default it will download all availible data and options for pfSense backups (ssh keys, rrd data, extra services data...). If a `pfsense_encrypted_password` is supplied it will encrypt the backup file with this password. It will need to be supplied if using the backup file to restore pfSense.

## Role Variables

| Name                          | Description                                    | Default                                                                                       |
| ----------------------------- | ---------------------------------------------- | --------------------------------------------------------------------------------------------- |
| pfsense_hostname              | Hostname or IP of Fireall                      |                                                                                               |
| pfsense_username              | Username to login to pfsense                   |                                                                                               |
| pfsense_password              | password to login to pfsense                   |                                                                                               |
| pfsense_backup_page           | url for backup page in web interface           | `diag_backup.php`                                                                             |
| pfsense_backup_directory      | Local Backup Directory to save pfsense configr |                                                                                               |
| pfsense_backup_filename       | Filename of the saved file                     | `'{{ pfsense_backup_directory }}/{{ pfsense_hostname }}-{{ ansible_date_time.iso8601 }}.xml'` |
| pfsense_https                 | If using HTTPS to connect to firewall          | `true`                                                                                        |
| pfsense_validate_certificates | Check for valid certificates                   | `true`                                                                                        |
| pfsense_backup_no_log         | Hide output from ansible logs                  | `true`                                                                                        |
| pfsense_backupssh         | Option to include the SSH keys for the firewall                | `true`                                                                                        |
| pfsense_backupdata         | Option to include extra data such as DHCP leases and captive portal databases                  | `true`                                                                                        |
| pfsense_donotbackuprrd         | Negate backup of the RRD files                | `false`                                                                                        |
| pfsense_encrypted_password         | Password to encrypt the backup file               | `true`                                                                                        |

## Example Playbook

```
- hosts: 'localhost'
  connection: local
  vars:
    - pfsense_hostname: 'pfsense.example.com'
    - pfsense_username: 'pfbackup'
    - pfsense_password: 'redactedpassword'
    - pfsense_backup_directory: '/backups'
    - pfsense_donotbackuprrd: true
    - pfsense_encrypted_password: 'hunter2'

  roles:
    - role: ansible-role-pfsense-backup
```

## License

MIT

## Author Information

Gavin Will - https://github.com/gavinwill
