# TWRP Device Tree for Motorola G62 5G (rhodei).

## Setup repo tool
Setup repo tool from here https://source.android.com/setup/develop#installing-repo

## Compile

Sync TWRP manifest:

```
repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
```

Make a directory named local_manifest under .repo, and create a new manifest file, for example local_manifests.xml
and then paste the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote name="github"
	fetch="https://github.com/" />

<project path="device/motorola/rhodei"
	name="abkdmn-ng/twrp_rhodei"
	remote="github"
	revision="main" />
</manifest>
```
You might need to pick few patches from gerrit.twrp.me to get some stuff working.

Sync the sources with

```
repo sync -j$(nproc --all)
```

To build, execute this command:

```
. build/envsetup.sh; lunch twrp_rhodei-eng; make bootimage
```

To test it:

```
# To temporarily boot it
fastboot boot out/target/product/rhodei/boot.img 

# To make twrp replace stock recovery temporarily boot twrp and navigate
to advanced menu and select Flash Current TWRP option.
```

## Device Full Specification
```
Type | Specs
---:|:---
CPU | Octa-core (2x2.2 GHz Kryo 660 Gold & 6x1.7 GHz Kryo 660 Silver)
CHIPSET | Qualcomm SM7325 ("Holi") Snapdragon 695 5G (6nm)
GPU | Adreno 619
Memory | 6/8 GB
Android Version | 13
Storage | 128 GB (UFS 2.1?)
Battery | 5000 mAh
Dimensions | 161.8 x 74 x 8.6 mm
Display | 1080 x 2400 pixels, 20:9 ratio (~405 ppi density)
Rear Camera | 50 MP, f/1.8 (wide), 1/2.76", 0.64µm, PDAF 8 MP, f/2.2, 118˚ (ultrawide), 1/4.0", 1.12µm 2 MP, f/2.4, (macro)
Front Camera | 16 MP, f/2.2, (wide), 1.0µm

```

## Copyright

```
#
# Copyright (C) 2022 The Android Open Source Project
#
# SPDX-License-Identifier: Apache-2.0
#
