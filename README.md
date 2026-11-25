PixelOS (Android 17) kernel build for Redmi Note 10 Pro (`sweet`) with BakaSU, SuSFS, and NoMount.

### Install

Flash the latest zip from [Releases](../../releases) via recovery (TWRP / OrangeFox). No wipes needed.

Manager APK: [BakaSU](https://github.com/Baka-SU/BakaSU/releases) (use the BakaSU manager matching the built driver).

### Notes

- **Base:** Linux 4.14.357 ([`PixelOS-Devices/android_kernel_xiaomi_sm6150:seventeen`](https://github.com/PixelOS-Devices/android_kernel_xiaomi_sm6150/tree/seventeen))
- **Toolchain:** ZyCromerZ Clang 17.0.0 + Greenforce bare-metal GCC (arm64/arm)
- **Root:** BakaSU (`main`, SUSFS inline hook mode)
- **Stealth:** SuSFS `kernel-4.14` backport (`simonpunk/susfs4ksu`)
- **Module Injection:** NoMount (`maxsteeel/nomount`, `CONFIG_NOMOUNT=y`)
- **AnyKernel3:** Uses `split_boot; flash_boot;` — untouched stock OEM ramdisk & DTB (prevents Android 17 SELinux / splash panics).
- **Hook patches:** SuSFS inline hook patches from [NonGKI_Kernel_Build_2nd](https://github.com/JackA1ltman/NonGKI_Kernel_Build_2nd).
- **Device scope:** Redmi Note 10 Pro (`sweet`) on PixelOS only.
- **Release details:** Generated from the upstream kernel commit and the BakaSU, SuSFS, NoMount, kernel, and compiler versions detected during each build. Releases contain the flashable ZIP only.