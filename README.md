# ROLE dginhoux.mount



## DESCRIPTION

This role configure linux mounts and generate `/etc/fstab`. <br />
Mountpoints are created if necessary. <br /><br />

Two mode are possibles by toggle between ansible module "ansible.posix.mount" and "ansible.builtin.template"<br />
* mount : can return error and not populate fstab file for some reasons (busy dev...)
* template : generate file and try a shell "mount -a"


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
- name: Playbook
  hosts: all
  roles:
    - name: Start role dginhoux.mount
      ansible.builtin.include_role:
        name: dginhoux.mount
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml`


#### EXAMPLES VARIABLES


```yaml
###### NOTES FOR OPERATE MODE
#### toggle between ansible module "ansible.posix.mount" and "ansible.builtin.template"
#### mount    : can return error and not populate fstab file for some reasons (busy dev...)
####            an option is added to purge fstab content if necessary
#### template : generate file and try a shell "mount -a"

# mount_operate_mode: template
mount_operate_mode: mount
mount_operate_mode_mount_purge: true
mount_operate_mode_template_mount_a: true


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

mount_list_host: []
mount_list_group: []
```

NOTE : Theses 3 lists `mount_list`, `mount_list_group` and `mount_list_host` are merged. <br />
You can use the `_host` and `_group` lists to specify per host and/or per group content.


#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

`NOT USED BY THIS ROLE`


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
