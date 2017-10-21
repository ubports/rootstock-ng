# Rootstock-NG

Rootstock-NG is a pair of scripts to help you build and install an Ubuntu Touch rootfs.

## rootstock-touch-install

rootstock-touch-install assists with installing an Ubuntu Touch rootfs on a device. 

### Usage

Before using rootstock-touch-install, flash your hybris-boot.img to your device using `fastboot`. Then, boot into recovery.

In most cases, the following usage will install Ubuntu Touch to your device successfully. If it does not, continue on to Options.

```
rootstock-touch-install <path to rootfs tarball> <path to android system.img>
```

A rootfs tarball (`.tar.gz` in this case) can be obtained from (The UBports cdimage server)[http://cdimage.ubports.com/rootfs/]. Simply pick the version and architecture (if applicable) that suits.

The Android system.img is located in `out/target/product/[model]/` in your Halium repository. It can be built using `make systemimage` as well. Please see [the Halium documentation](https://docs.halium.org) to learn more about building Halium.

### Options

#### -b|--busybox `<path to Busybox binary>`

Pushes a custom Busybox or Toybox binary to the device. This is later used when extracting the rootfs tarball. Use it when you're running into strange errors, such as `killed: out of memory` during the "unpacking rootfs tarball to system-image" step.

In a Halium tree, you can commonly find a Busybox binary in `out/target/product/[model]/utilities/`. You can find a Toybox binary in `out/target/product/[model]/system/bin/`.

#### -c|--custom

Install a customization tarball (commonly `custom.tar.xz`) on the device after extraction. Customization tarballs allow distributors to add packages or files to an Ubuntu Touch installation that are not included in the base rootfs by default, without rebuilding the whole rootfs.

#### -k|--keep-userdata

Set this option if you would like to keep your apps and data between installs. Without it, `/data/user-data` is deleted during installation of the Ubuntu Touch system.

For debugging purposes, it is recommended to keep this option unset. Keeping data from previous (possibly buggy) installs could cause unexpected behavior of Unity, apps, or the system in general.

#### -w|--wipe-file

Rewrites a file inside of the system image with ' ' (one space character).
