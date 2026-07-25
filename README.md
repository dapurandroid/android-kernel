# android-kernel 🔧

> A GitHub Actions CI pipeline that builds a KernelSU-patched kernel for the **Samsung Galaxy A04s (SM-A047F)** and packages it as a flashable AnyKernel3 ZIP.

![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-CI-blue?logo=githubactions)
![Device](https://img.shields.io/badge/device-Samsung%20A04s-orange)
![KernelSU](https://img.shields.io/badge/KernelSU-supported-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green)

## Features

- ⚙️ **Automated kernel compilation** using Clang 17 with full LLVM toolchain
- 🛡️ **KernelSU integration** — patches root support directly into the kernel
- 📦 **AnyKernel3 packaging** — produces a flashable ZIP ready for TWRP / OrangeFox
- 🚀 **Optional GitHub Release** — automatically publishes the ZIP as a tagged release
- 🔧 **Auto-patches Mali GPU Kconfig** — fixes Samsung Exynos `shell()` syntax errors at build time
- 📊 **Compile log upload on failure** — artifacts are saved for debugging failed builds

## Requirements

- A GitHub account with Actions enabled
- No local setup needed — everything runs on GitHub-hosted runners

## Usage

1. **Fork this repository** to your own GitHub account.
2. Go to the **Actions** tab and select **Build Kernel with KernelSU (Samsung A04s)**.
3. Click **Run workflow** and fill in the inputs:

| Input | Default | Description |
|---|---|---|
| `kernel_source` | `SavedByLight/android_kernel_samsung_a04s` | Kernel source repo URL |
| `kernel_branch` | `main` | Branch to build from |
| `kernelsu_tag` | `main` | KernelSU release tag, or `main` for latest |
| `create_release` | `false` | Set to `true` to publish a GitHub Release |

4. The workflow will compile the kernel, package it, and upload the ZIP as a build artifact.

## Flashing

1. Download the ZIP from the **Artifacts** section of the completed Actions run (or from **Releases** if you enabled it).
2. Boot your Samsung A04s into **TWRP** or **OrangeFox** recovery.
3. Flash the ZIP.
4. Reboot to system.
5. Install the [KernelSU Manager APK](https://github.com/tiann/KernelSU/releases) and open it — status should show **Working**.

## How It Works

1. Clones the specified kernel source at the given branch.
2. Fixes script permissions and patches the Mali GPU Kconfig for Samsung Exynos compatibility.
3. Downloads and integrates KernelSU via the official setup script.
4. Sets up Clang 17 from [ZyCromerZ/Clang](https://github.com/ZyCromerZ/Clang).
5. Configures the kernel using the A04s defconfig with KernelSU and overlay FS enabled.
6. Compiles with `make -j$(nproc)` using the full LLVM toolchain.
7. Collects DTBs and packages everything with AnyKernel3.
8. Optionally creates a GitHub Release with build metadata.

## Supported Devices

| Device | Codename | Model |
|---|---|---|
| Samsung Galaxy A04s | `a04s` | SM-A047F |

## License
 
MIT
