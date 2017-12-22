# Make a bootable live usb

## Listing drives

```bash
sudo fdisk -l
```

## Create Bootable usb

```bash
sudo dd bs=4M if=/path/to/linux.iso of=/dev/sdX && sync
```

or with progress indicator

```bash
sudo dd bs=4M if=/path/to/linux.iso of=/dev/sdX status=progress && sync
```
