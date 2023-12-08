# ROLE dginhoux.mount



## DESCRIPTION

This role configure linux mounts and generate `/etc/fstab`.
Mountpoints are created if necessary.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

| Platform | Versions |
|----------|----------|
| Debian | all |
| EL | all |
| Fedora | all |
| Ubuntu | all |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.mount
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.mount dginhoux.mount
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.mount
      ansible.builtin.include_role:
        name: dginhoux.mount
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
mount_purge_fstab: true

mount_list:
  - target: /boot
    owner: root
    group: root
    mode: "0750"
    source: /dev/sda1
    boot: true
    fstype: ext2
    options:
      - defaults
      - noatime
    dump: 0
    pass: 0
    state: mounted

  - target: /
    owner: root
    group: root
    mode: "0750"
    source: /dev/mapper/vg0-lv--root
    boot: true
    fstype: xfs
    options:
      - defaults
      - noatime
    dump: 0
    pass: 0
    state: mounted

  - target: /home
    owner: root
    group: root
    mode: "0750"
    source: /dev/mapper/vg0-lv--home
    boot: true
    fstype: xfs
    options:
      - defaults
      - noatime
    dump: 0
    pass: 0
    state: mounted

  - target: none
    owner: root
    group: root
    mode: "0750"
    source: /dev/mapper/vg0-lv--swap
    boot: true
    fstype: swap
    options:
      - sw
    dump: 0
    pass: 0
    state: mounted
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
