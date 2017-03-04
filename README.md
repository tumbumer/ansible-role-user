# tumbumer.user

Manage software.

## Requirements

None.

## Role Variables

`tumbumer_user_list` - a list with `name` keys and structure as well as an
[official Ansible user module](https://docs.ansible.com/ansible/user_module.html)

### Additional optionally vars

var | default | choices | description
---|---|---|---
tumbumer_user_list.{{ name }}.ssh_public_key_path | | | Relative path to the user public ssh key file
tumbumer_user_list.{{ name }}.bashrc | | | Additional lines for the user `~/.bashrc`

## Dependencies

None.

## Example Playbook
```yaml
---
- hosts: all
  vars:
  - tumbumer_user_list:
    - name: test
      state: present
      remove: no
      password: $6$/lTW6W7l$42C8ilXCEKRr3qLx10Wf3I.hCawAiqw95Vt/e6x6J8pzxszeooo3pd5ppwBW6VEWRKLTbMhChTVwEjmj1vVox.
      update_password: on_create
      shell: /bin/bash
      system: no
      createhome: yes
      home: /home/test
      group: test
      groups: ""
      ssh_public_key_path: host_files/_ssh/tumbumer.pub
      bashrc: |
        alias la='ls -lAh'
        if [ -f /usr/bin/screenfetch ]; then echo && /usr/bin/screenfetch -c ,2; fi
        df -h | grep ^/dev
        echo
        date
        echo
  roles:
  - tumbumer.user
```

## License

Apache-2.0

## Author Information

Denis Dvoretskov aka tumbumer <denis@tumbum.com>
