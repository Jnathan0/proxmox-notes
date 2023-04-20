# SATA Drive passthrough from mainboard controller 

This doc contains notes for passing through attached SATA drives from a controller integrated with a mainboard.
Typical applications include passing drives to a VM for software RAID. 
Passing SATA drives through a PCI controller is much easier and the whole controller can be passed instead of using this method.

### List drives on host system
```bash
lsblk -o +MODEL,SERIAL
```

### Get device by-id from /dev
```bash
ls /dev/disk/by-id | grep <DISK SERIAL NUMBER>
```

### Use `qm` command to set drive to be attached to vm by id
```bash
qm set <VM ID> -scsi<SCSI DRIVE NUMBER> /dev/disk/by-id/$(ls /dev/disk/by-id | grep <DISK SERIAL NUMBER>)
```
Once completed verify in the GUI that the harddrives are attached to the proper vm
