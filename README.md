# Ansible-lvm
Create lvm with ansible

## Description
Ansible create lvm automaticaly by command.

**Default vars:**
 * disk: /dev/xvdf
 * vgname: data-vg
 * lvname: data-lv
 * filesystem: ext4
 * mount_point: /data

```
$ansible-playbook -i hosts main.yml

```
