# Clover device manifest

Local manifest for building The Clover Project Android 17 on Xiaomi merlinx and lancelot. Device and common trees use `clo`; the kernel uses `17.0`, and vendor, MediaTek, and Xiaomi dependencies use `lineage-24.0`.

Run these commands from your Clover source directory:

```bash
repo init -u https://github.com/The-Clover-Project/manifest.git -b 17 --git-lfs
mkdir -p .repo/local_manifests
curl -fsSL https://raw.githubusercontent.com/MrShockWAVEog/manifest/clo/manifest.xml -o .repo/local_manifests/xiaomi_mt6768.xml
repo sync -c --force-sync --optimized-fetch --no-tags --no-clone-bundle --prune -j$(nproc --all)
source build/envsetup.sh
lunch clover_merlinx-cp2a-userdebug
mka clover -j$(nproc --all)
```

For lancelot, use `lunch clover_lancelot-cp2a-userdebug`.

Clover includes Google apps by default. For a vanilla build, set `WITH_GMS=false` before lunch.
