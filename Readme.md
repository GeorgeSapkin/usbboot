# USB boot code

This is the USB MSD boot code which should work on the Raspberry Pi model A, Compute Module, Compute
module 3 and Raspberry Pi Zero.

This version of rpiboot has been modified to work from directories which contain the booting
firmware.  There is a default directory msd/ which contains bootcode.bin and start.elf to turn
the Raspberry Pi device into a USB Mass Storage Device (MSD).

## Building on Debian-based distributions

```bash
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
sudo apt-get install libusb-1.0-0-dev
make
sudo ./rpiboot
```

## Building using Docker

Since binaries from different OSes aren't compatible with `libusb` from other
OSes you need to build `rpiboot` for your specific OS.

### For CentOS/RHEL

```bash
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
make docker-centos
sudo ./rpiboot-centos
```

### For Debian

```bash
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
make docker-debian
sudo ./rpiboot-debian
```

### For Fedora

```bash
git clone --depth=1 https://github.com/raspberrypi/usbboot
cd usbboot
make docker-fedora
sudo ./rpiboot-fedora
```

## Running your own (not MSD) build

If you would like to boot the Raspberry Pi with a standard build you just need to copy the FAT partition
files into a subdirectory (it must have at the minimum bootcode.bin and start.elf).  If you take a
standard firmware release then this will at the very least boot the linux kernel which will then stop
(and possibly crash!) when it looks for a filesystem.  To provide a filesystem there are many options,
you can build an initramfs into the kernel, add an initramfs to the boot directory or provide some
other interface to the filesystem.

```bash
sudo ./rpiboot -d boot
```

This will serve the boot directory to the Raspberry Pi Device.
