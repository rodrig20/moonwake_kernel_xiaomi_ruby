# MoonWake

Redmi Note 12 pro 5G (ruby) kernel specify for powersave

## Features

- KernelSU patch (Can build with sukisu, ksun or ksu type root)
- SusFS patch
- BBR3 implemented
- Sync with [linux-cip](https://git.kernel.org/pub/scm/linux/kernel/git/cip/linux-cip.git/), google [kernel/common](https://android.googlesource.com/kernel/common) and [xiaomi-mediatek-devs/android_kernel_xiaomi_mt6877](https://github.com/xiaomi-mediatek-devs/android_kernel_xiaomi_mt6877) repo
- Enable some twaek for powersave but keep the performance
- ln8000 fast charge driver enabled
- Updated wireguard module
- Use google clang 19 (r530567)
- **Custom modification**: USB gadget reconfiguration to allow using the device as HID and MSD for ISO booting

## About this adaptation

This is an adaptation of the original [DPR-MoonWake/moonwake_kernel_xiaomi_ruby](https://github.com/DPR-MoonWake/moonwake_kernel_xiaomi_ruby) kernel with additional functionality to support using the device as a HID (Human Interface Device) and MSD (Mass Storage Device) for booting ISO images. The USB gadget reconfiguration feature allows properly unregistering the current gadget before setting up a new configuration, enabling flexible USB device mode switching.

## Compile guide

### Option 1: Compile and go (This way to compile my kernel directly from my source)

1. Fork [rodrig20/KernelAction_moonwake_kernel_xiaomi_ruby](https://github.com/rodrig20/KernelAction_moonwake_kernel_xiaomi_ruby/) repo
2. Enable action build in Actions tab
3. Click on `Build MoonWake Kernel`
4. Click on `Run workflow`
5. With `Choose a config type` option, choose it as `release`
6. With `Path to a specific config JSON file (optional). Leave blank to use all configs.`, type `moonwake.json`
7. Click `Run workflow` green button and wait
8. Download, extract the build and flash!

If you don't know how to flash, [read the original project's excellent wiki!](https://github.com/DPR-MoonWake/moonwake_kernel_xiaomi_ruby/wiki) For additional help, join Android development communities for assistance with the flashing process.

### Option 2: Kernel Player (For advanced user that build android kernel before)

Since you (Kernel Player) know how to build, pack AK3 and flash it, I just have some notes for you
- Compile it with only google `clang-r530567 (19)`, `clang-r498229b (17.0.4)` or `clang-r487747c (17.0.2)`. Clang 18, 20, 21 or older have some issues with ln8000 driver with make CN and IN variant can't boot
- To add a feature config (eg: vendor/kernelsu.config), please check `arch/arm64/configs/vendor`, see what config you want to add and then use `make $your_args_here vendor/example.config` after using `make $your_args_here ruby_defconfig`
