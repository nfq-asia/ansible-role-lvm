# Ansible-lvm
Create lvm with ansible

## Description
Ansible create lvm automaticaly by command.
We should define new disk device, volume group name, logical volume name, mount point file, file system type in file vars/main.yml

**Default vars:**
 * new_disk: /dev/sdb
 * vg_name: data-vg
 * lv_name: data-lv
 * filesystem: ext4
 * mount_point: /data


```
$ansible-playbook -i hosts lvm.yml

```

#Note
We can change information in /vars/main.yml like vg_name, lv_name, mountpoint_name,... Please check it before running command
