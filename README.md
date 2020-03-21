# tumbumer.user

Manage user accounts.

## Requirements

None.

## Role Variables

var | description
---|---
tumbumer_user_is_home_dir_private | if `yes` then newly created users will have a mask of 0700 for their home directories
tumbumer_user_list | a list with `name` keys and structure as well as an [official Ansible user module](https://docs.ansible.com/ansible/user_module.html). Supported keys are: `state`, `remove`, `password`, `update_password`, `comment`, `shell`, `system`, `createhome`, `home`, `group`, `groups`
tumbumer_user_force_change_password_list | list of users who must be forced to change the password at the first login

### Additional optionally vars

var | description
---|---
tumbumer_user_list.{{ name }}.ssh_public_key | User public key. Multiple keys can be specified in a single key string value by separating them by newlines.
tumbumer_user_list.{{ name }}.bashrc | Additional lines for the user `~/.bashrc`

## Dependencies

None.

## Example Playbook
```yaml
---
- hosts: all
  vars:
  - tumbumer_user_is_home_dir_private: yes
  - tumbumer_user_force_change_password_list:
    - test
  - tumbumer_user_list:
    - name: test
      comment: Test user
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
      ssh_public_key: "-----BEGIN OPENSSH PRIVATE KEY-----..."
      bashrc: |
        umask 0077
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
