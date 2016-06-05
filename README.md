# ansible-role-postfix

This role configures postfix.

## Requirements

None.

## Role Variables

variable                    | required | default                                       | choice        | comment
--------------------------- | -------- | --------------------------------------------- | ------------- | -------------------
postfix_myhostname          | no       | {{ ansible_hostname }}                        |               |
postfix_mydomain            | no       | {{ ('.').join(ansible_fqdn.split('.')[1:]) }} |               |
postfix_myorigin            | no       | $mydomain                                     |               |
postfix_inet_interfaces     | no       | localhost                                     |               |
postfix_inet_protocols      | no       | ipv4                                          | all,ipv4,ipv6 |
postfix_mydestination       | no       | $myhostname, localhost.$mydomain, localhost   |               |
postfix_mynetworks          | no       | 127.0.0.0/8                                   |               |
postfix_alias_maps          | no       | hash:/etc/aliases                             |               |
postfix_alias_database      | no       | hash:/etc/aliases                             |               |
postfix_recipient_delimiter | no       | +                                             |               |
postfix_mailbox_size_limit  | no       | 51200000                                      |               |
postfix_option              | no       |                                               |               | the oether parameters can be defined with key&value.

## Dependencies

None.

## Example Playbook

```yml
- hosts: servers
  roles:
    - postfix
```

*Inside `vars/main.yml`*:  
Variables must be defined by list.
```yml
postfix_inet_interfaces: 192.168.1.1
postfix_mynetworks: 127.0.0.0/8 192.168.1.0/24 192.168.2.0/24
postfix_option:
  relayhost: [mail.tamandu.com]:587
```

## License

MIT

## Author Information
