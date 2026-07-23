# 🚀 OnePlus ReSukiSU Kernel Builder

GitHub Actions workflow for building flashable **ReSukiSU GKI kernels** for supported OnePlus devices.

It syncs Android GKI sources, adds **ReSukiSU**, optionally applies **SUSFS**, and packages the result as an **AnyKernel3 ZIP**.

---

## 📱 Supported Devices

| Device | ID | Codename | SoC |
|---|---|---|---|
| OnePlus 15 | `oneplus15` | `Infinity` | `sm8850` |
| OnePlus 15T | `oneplus15t` | `Infinity` | `sm8850` |
| OnePlus 15R | `oneplus15r` | `Infinity` | `sm8845` |
| OnePlus Ace 6T | `ace6t` | `Infinity` | `sm8845` |

---

## ✨ Features

- ReSukiSU integration
- Optional SUSFS
- Optional Baseband Guard / ✨LSM Do not enable as it does not work with 6.12 kernels !✨
- Optional Netfilter + IPSet
- Optional BBR + ECN
- Optional BBRv3 backport (KMI-safe on android16-6.12)
- Net schedulers built in: `fq`, `fq_codel`, `cake`
- Optional Unicode bypass patch
- Flashable AnyKernel3 ZIP
- GitHub Release or artifact output
- Build logs, hashes, and summary

---

## 🚀 Quick Start

1. Fork this repo
2. Open **Actions**
3. Run the workflow
4. Select your device and options
5. Download the generated ZIP

---

## ⚙️ Key Options

| Option | Description |
|---|---|
| `DEVICE` | Device to build, or `all` |
| `KSU_META` | ReSukiSU source: `branch/tag/commit` |
| `SUSFS_META` | Empty = latest, `-1` = disabled, hash = pinned |
| `LSM` | Enable Baseband Guard | 
| `NETFILTER` | Enable Netfilter/IPSet |
| `BBR_ECN` | Enable BBR + ECN |
| `BBR3` | Backport BBRv3 (patches `net/tcp`, adds `CONFIG_TCP_CONG_BBR3`) |
| `CREATE_RELEASE` | Publish ZIP to GitHub Releases |

---

## 📦 Output

Naming: `AK3_ReSukiSU_<ksuver>_<SUSFS-ver|noSUSFS>_<device>_<kernel>[_LSM].zip`

Example ZIP:
`AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15_6.12.0.zip`

With LSM:
`AK3_ReSukiSU_43000_SUSFS-1.5.9_OnePlus15_6.12.0_LSM.zip`

SUSFS disabled:
`AK3_ReSukiSU_43000_noSUSFS_OnePlus15_6.12.0.zip`

> Building `DEVICE=all` compiles each **unique** kernel once — OnePlus 15 and 15T
> share `sm8850`/`android16-6.12-2025-06`, while 15R and Ace 6T share
> `sm8845`/`android16-6.12-2025-09` — so you get two ZIPs (`OnePlus15-15T`,
> `OnePlus15R-Ace6T`), each flashable on both of its devices.

---

## ⚠️ Notice

Use at your own risk. Keep a backup boot image and make sure fastboot/recovery access is available.

---

## 🙏 Credits

Thanks to the maintainers of Android GKI, ReSukiSU, SUSFS, AnyKernel3, Baseband Guard, and related community patches.
