# VantomKernel — PixelOS for Redmi Note 10 Pro (`sweet`)

VantomKernel is a Linux 4.14 kernel build for the Redmi Note 10 Pro (`sweet`) running PixelOS `seventeen`. It combines the PixelOS device kernel with BakaSU root management, a kernel-side SUSFS backport, and built-in NoMount support.

This build is device and ROM specific. The installer checks for the `sweet` codename. Do not flash it on another device or treat it as a generic kernel for other ROMs.

## Features

### BakaSU root management

[BakaSU](https://github.com/Baka-SU/BakaSU) provides kernel-based root access, per-app access profiles, and a module system based on metamodules. The kernel is built in SUSFS inline-hook mode for this non-GKI 4.14 device.

After flashing, install a [BakaSU Manager](https://github.com/Baka-SU/BakaSU/releases) compatible with the BakaSU driver included in the build. Root access and module management are controlled from the manager.

### SUSFS kernel features

This kernel includes a SUSFS kernel-4.14 backport and inline hooks adapted from [NonGKI_Kernel_Build_2nd](https://github.com/JackA1ltman/NonGKI_Kernel_Build_2nd). The enabled kernel options provide interfaces for:

- Hiding configured paths and mounts from selected process views.
- Automatically registering selected KernelSU/BakaSU and bind mounts for SUSFS handling.
- Returning configured file metadata through kstat spoofing.
- Spoofing the reported kernel name and `/proc/cmdline` contents.
- Hiding selected mapped files from process map interfaces.
- Redirecting selected file opens and hiding BakaSU/SUSFS symbols from kallsyms.

These are kernel capabilities, not a guarantee that every application or integrity check will be bypassed. Results depend on the manager, its SUSFS configuration, the ROM, and the detection method used by an application.

### NoMount VFS redirection

[NoMount](https://github.com/maxsteeel/nomount) is compiled into the kernel. It provides VFS-level path redirection and virtual file injection without creating conventional mounts for those redirections.

The flashable kernel ZIP contains the kernel, not the NoMount userspace package. To use NoMount, install its [matching metamodule](https://github.com/maxsteeel/nomount/releases) through BakaSU Manager and follow NoMount's setup instructions. Check the NoMount version listed in the kernel release notes and use compatible userspace components. Module behavior can vary; verify essential modules after installation.

### Kernel configuration

The build enables BBR congestion control with `sch_fq`, sets the kernel tick rate to 300 Hz, and enables jump labels and power-efficient workqueues by default. These are compile-time settings; they do not promise a specific battery-life or performance improvement on every workload.

## Compatibility

| Item | Target |
| --- | --- |
| Device | Xiaomi Redmi Note 10 Pro, codename `sweet` |
| ROM | PixelOS `seventeen` |
| Kernel base | PixelOS `android_kernel_xiaomi_sm6150`, Linux 4.14 |
| Root implementation | BakaSU, SUSFS inline-hook mode |
| NoMount | Built-in kernel subsystem; install its userspace metamodule separately |

The build is not tested or maintained here for MIUI/HyperOS, other Android releases, or other devices. A shared chipset or similar device name does not establish compatibility.

## Download and install

1. Download the latest ZIP from [Releases](../../releases), or download the ZIP artifact from a successful GitHub Actions run.
2. Confirm the device is a Redmi Note 10 Pro with codename `sweet` and is running the intended PixelOS build.
3. Keep a copy of the current boot image so you can restore it if the new kernel does not boot.
4. Flash the ZIP from a compatible custom recovery and reboot.
5. Install the compatible BakaSU Manager, then verify root access. Install the NoMount metamodule separately if you intend to use NoMount.

The AnyKernel3 installer checks the device codename, splits the existing boot image, replaces the kernel image, and flashes the boot partition. It does not install a ROM, vendor image, recovery, or BakaSU Manager.

If the device fails to boot, restore the saved boot image using recovery or fastboot before troubleshooting modules. For module-related boot issues, use the manager's module controls or recovery procedures documented by that module's maintainer.

## Releases

Each release contains one flashable kernel ZIP. The release notes identify the PixelOS kernel commit and report the kernel release string, BakaSU version, SUSFS version, NoMount version, and Clang/LLVM revision when available. The ZIP filename includes the build time in Jakarta time:

```text
PixelOS-sweet-BakaSU-SuSFS-NoMount-YYYYMMDD_HHMM.zip
```

## Project links

- [PixelOS kernel source](https://github.com/PixelOS-Devices/android_kernel_xiaomi_sm6150)
- [BakaSU and Manager releases](https://github.com/Baka-SU/BakaSU)
- [NonGKI SUSFS patches and inline hooks](https://github.com/JackA1ltman/NonGKI_Kernel_Build_2nd)
- [NoMount and its metamodule](https://github.com/maxsteeel/nomount)
- [ZyCromerZ Clang](https://github.com/ZyCromerZ/Clang)
