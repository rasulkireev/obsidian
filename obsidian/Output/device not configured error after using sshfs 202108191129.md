---
status:
  - writing_idea
tags:
  - code
---

After mounting an external server via `sshfs` a folder that you mount can be "faulty". For example if you do `ls` on a folder where it is located you will be able to see it, but won't be able to `cd` into it. The error will be something like

```
... Device not configured ...
```

This means that you first have to unmount the filesystem you previously mounted. You can do that with:

```bash
sudo diskutil umount force /path/to/mount
```

than mount again via

```bash
sshfs username@ip-address:path/to/desired/mount/folder /path/to/desired/mount/location/locally
```

found answer on https://stackoverflow.com/questions/44110633/device-not-configured-after-sshfs-attempt