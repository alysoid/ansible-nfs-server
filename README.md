# [Catena](https://github.com/alysoid/catena) Ansible Role: nfs-server

Manage list of [NFS exports](https://man.archlinux.org/man/exports.5) via Ansible. Custom exports are placed in `/etc/exports.d/*.exports`, the global configuration file `/etc/nfs.conf` is untouched. For mounting check the [ansible-systemd-mount](https://github.com/alysoid/ansible-systemd-mount/) role.

## Role Variables

### `nfs_exports`

List of custom exports. They must be below the NFSv4 root directory. See `nfs_exports_root`.

```yaml
# Defaults
nfs_exports: []

# Example
nfs_exports:
  - name: Storage                     # Description
    path: /srv/nfs/storage            # Below NFS root
    options: 192.168.0.0/24(rw,async) # See man exports(5)
```

### `nfs_exports_root`

NFSv4 root directory (denoted by `fsid=0`). Other directories in `nfs_exports` must be below it.

```yaml
# Defaults
nfs_exports_root:
  - name: NFSv4 root
    path: /srv/nfs
    options: 192.168.0.0/24(rw,sync,crossmnt,fsid=0)
```
