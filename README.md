Ansible role common
=========

A role for managing common settings for typical server such as users, groups, sshd, sudoers, ntp, dns etc. Also manages user's dotfiles such as .bashrc or .vimrc and ssh keys.

Requirements
------------

None

Role Variables
--------------

#### `managed_users` (optional)

Add and configure users  (dict). For example:

```
managed_users:
  - username: user1
    state: present
    comment: "John Doe"
    group: staff
    uid: 1234
    groups:
      - "{{ admin_group }}"
    publickeys:
      - 'ssh-rsa xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
  - username: user2
    state: present
    comment: "Esko Mörkö
    group: staff
    uid: 1235
    groups:
      - "{{ admin_group }}"
    publickeys:
      - 'ssh-rsa xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
```

#### `managed_groups**` (optional)

Add and manage groups (dict). For example:

```
managed_groups:
  - groupname: staff
    state: present
    system: false
    gid: 10000
```

#### `dotfiles` (optional)
Creates dotfiles for users. For example:

```
dotfiles:
 - user: user1
   group: staff
   files:
   - name: bashrc
     content: |
        # Ansible managed
        # Source global definitions
        if [ -f /etc/bashrc ]; then
          . /etc/bashrc
        fi
        alias ls='ls -Fh --color=auto'
        alias ll='ls -lahF --color=auto'
   - name: vimrc
     content: |
        " Ansible managed
        set fo=tcq
        set nocompatible
        set modeline
        set bg=dark
        syntax on
        set hlsearch
        set t_Co=256
```

#### `dns_servers` (optional)
Manages dns servers (list). For example:

```
dns_servers:
 - 192.168.0.1
 - 8.8.8.8
 - 8.8.4.4
```

#### `dns_search_path` (optional)
Configures DNS search path. For example:

```
dns_search_path: mydomain.com
```

#### `allow_root_ssh` (optional)
Configure ssh root login (yes/no)

#### `timezone` (optional)
Timezone e.g. "Europe/Helsinki"

#### `ntp_servers` (optional)
used to configure ntp servers (list). For example:

```
ntp_servers:
- 192.168.0.1
- pool.ntp.org
```

#### `common_sudoers_files`(optional)
Allows adding custom sudoers files under /etc/sudoers.d directory. For example:

```
common_sudoers_files:
  - name: 10_zabbix
    content: |
      zabbix ALL=(ALL) NOPASSWD: /bin/find
```



Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - common

License
-------

Proprietary

Author Information
------------------

Tuomas Vallaskangas
