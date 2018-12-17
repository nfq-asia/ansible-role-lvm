# ansible-lvm
Create lvm with ansible

## Description
Ansible create lvm automaticaly by command

```
$ansible-playbook -i hosts lvm.yml

```

#Note
We can change information in /vars/main.yml like vg_name, lv_name, mountpoint_name,... Please check it before running command
