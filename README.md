# Realme Q5 GKI Kernel Builder

GitHub Actions workflow for building GKI kernel for Realme Q5 (oscar) with KernelSU support.

## Features

- ✅ Automatic kernel compilation using AOSP Clang
- ✅ KernelSU integration for root access
- ✅ Support for LTO modes (thin/full/none)
- ✅ AnyKernel3 packaging for easy flashing
- ✅ Automated release creation
- ✅ Support for Realme Q5 (oscar) - SM6375

## Device Information

| Property | Value |
|----------|-------|
| Device | Realme Q5 |
| Codename | oscar |
| SoC | Qualcomm SM6375 (Snapdragon 695) |
| Architecture | arm64 |
| Kernel Version | 5.10 (Android 12) |
| GKI Version | android12-5.10 |

## Usage

### 1. Fork this repository

### 2. Enable GitHub Actions

Go to your repository's Actions tab and enable workflows.

### 3. Run the workflow

1. Go to **Actions** tab
2. Select **Build Realme Q5 GKI Kernel**
3. Click **Run workflow**
4. Configure options:
   - **kernel_branch**: Kernel source branch (default: master)
   - **enable_kernelsu**: Enable KernelSU root (default: true)
   - **enable_susfs**: Enable SUSFS (default: false)
   - **lto_mode**: LTO optimization mode (default: thin)
5. Click **Run workflow**

### 4. Download the kernel

After the build completes:
- Go to **Releases** to download the AnyKernel3 zip
- Or check **Actions** → **Artifacts** for the build output

## Flashing Instructions

### Method 1: AnyKernel3 (Recommended)

1. Download the AnyKernel3 zip from Releases
2. Reboot to recovery
3. Flash the zip using `adb sideload`:
   ```bash
   adb sideload RealmeQ5-GKI-Kernel-*.zip
   ```

### Method 2: Fastboot

1. Extract boot.img from the zip
2. Reboot to fastboot:
   ```bash
   adb reboot bootloader
   ```
3. Flash boot image:
   ```bash
   fastboot flash boot_a boot.img
   fastboot flash boot_b boot.img
   fastboot reboot
   ```

## KernelSU Manager

After flashing the kernel, install the KernelSU Manager APK to manage root access:
- Download from: https://github.com/tiann/KernelSU/releases

## Build Configuration

### LTO Modes

- **thin**: Faster compilation, smaller binary (default)
- **full**: Better optimization, larger binary
- **none**: Disable LTO

### KernelSU Options

- **enable_kernelsu**: Adds KernelSU support for root management
- **enable_susfs**: Adds SUSFS support for systemless modifications

## Troubleshooting

### Build fails

1. Check the build logs in Actions
2. Common issues:
   - Insufficient disk space
   - Missing dependencies
   - Kernel source compatibility issues

### Bootloop after flashing

1. Flash stock boot.img
2. Try different LTO mode
3. Check if KernelSU is compatible with your ROM

## Credits

- [Realme Kernel Source](https://github.com/realme-kernel-opensource)
- [KernelSU](https://github.com/tiann/KernelSU)
- [AnyKernel3](https://github.com/osm0sis/AnyKernel3)
- [AOSP](https://source.android.com)

## License

This project is licensed under the GPL v2 License.
