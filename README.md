# Ansible Role LVM

## Description
Prepare a block EBS device and create volume group, logical volume, filesystem and fstab entry. This role is necessary for instances that store services' data on separated EBS for persistence.

## Prerequisites
* An EC2 instance running Ubuntu 18.04 minimal having EBS other than the root devices attached.

## Required variables

A configuration block like this is required:

```yaml
        lvm_config:
          pvs:
            - /dev/nvme1n1
          vgs:
            test_vg:
              pvs:
                - /dev/nvme1n1
          lvs:
            - name: test_lv
              vg: test_vg
              size: "+100%FREE"
        filesystems_config:
          data:
            dev: /dev/test_vg/test_lv
            type: ext4
            opts: ''
        mounts_config:
          data:
            dev: /dev/test_vg/test_lv
            fstype: ext4
            opts: 'noatime,nodiratime'
            mountpoint: /var/test_lv
            dump: '0'
            passno: '2'
            state: mounted
```

### `lvm_config`:
- `pvs`: a list of devices to be used as the physical volumes
- `vgs`: one or more volume group and its component `pvs`, in a list
- `lvs`: a list of one or more logical volume:
  - `name`: name of the logical volume
  - `vg`: the volume group that this volume resides in
  - `size`: Size of the volume, following [lvcreate](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/logical_volume_manager_administration/lv) syntax.

### `filesystems_config`:
- `dev`: device path pointing to the logical volume
- `type`: filesystem type. **Note**: The role will not manage dependency of filesystems type (i.e. playbooks need to install mkfs packages on their own)
- `opts`: `mkfs` additional options

### `mount_config`:
Configs that correspond to an `/etc/fstab` entry

## Defaults
n/a

## Optional variables
n/a

## Tags
* `install`: Create the set `EBS > VG > LV > filesystem`

## Notes
n/a
