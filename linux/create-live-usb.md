# Make a bootable live usb

## Listing drives

```Shell
sudo fdisk -l
```

## Create Bootable usb

```Shell
sudo dd bs=4M if=/path/to/linux.iso of=/dev/sdX && sync
```

or with progress indicator

```Shell
sudo dd bs=4M if=/path/to/linux.iso of=/dev/sdX status=progress && sync
```
