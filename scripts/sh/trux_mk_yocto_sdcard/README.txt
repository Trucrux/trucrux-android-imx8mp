How to use the Trucrux SD card creation script:
=================================================

This utility is provided on an "AS IS" basis.
This is the script we use to create our recovery SD card with Android images.
For machines with Android support, it is a part of a larger script we use to create our recovery SD card, which also includes Android.
It is a good example for using the output of the Yocto build to create a bootable SD card, and use it to flash the target NAND flash/eMMC.

Note:
Before running this script you need to bitbake fsl-image-gui.
Run below commands to create symbolic link from yocto to Android scripts
- Assuming your yocto and android is built under following paths
Yocto Base DIR : ~/trux-fsl-yocto
Android Base DIR : ~/trux_imx-android-11.0.0_1.0.0
$ export YOCTO_BSP_BUILD=/media/tru-ser-01/Storage1_seagate/Trucrux/imx8mq_trucrux/codesetup/Yocto/Dunfell
$ export ANDROID_BSP_BUILD=/media/tru-ser-01/Storage1_seagate/imx8/imx8mq/codesetup/Android/Android-11/android_build
$ ln -sf ${ANDROID_BSP_BUILD}/device/trucrux/scripts/sh/trux_mk_yocto_sdcard/trux-create-yocto-sdcard-with-android.sh \
 ${YOCTO_BSP_BUILD}/sources/meta-trucrux/scripts/trux_mk_yocto_sdcard/trux-create-yocto-sdcard-with-android.sh
$ ln -sf ${ANDROID_BSP_BUILD}/device/trucrux/scripts/sh/trux_mk_yocto_sdcard/trucrux_scripts/mx8_install_android.sh \
 ${YOCTO_BSP_BUILD}/sources/meta-trucrux/scripts/trux_mk_yocto_sdcard/trucrux_scripts/mx8_install_android.sh

$ cd ${YOCTO_BSP_BUILD}

For creating SDcard with only Yocto:
=================================
Usage:
sudo MACHINE=<imx6ul-trux|imx8mq-trux-q01|imx8mm-trux|imx8mp-trux> sources/meta-trucrux/scripts/trux_mk_yocto_sdcard/trux-create-yocto-sdcard.sh [options] /dev/sdX
(Change /dev/sdX to your device name)

options:
  -h            Display help message
  -s            Only show partition sizes to be written, without actually write them
  -a            Automatically set the rootfs partition size to fill the SD card
  -r            Select alternative rootfs for recovery images (default: build_x11/tmp/deploy/images/trux-som-mx6/fsl-image-gui-trux-som-mx6.*)

If you don't use the '-a' option, a default rootfs size of 3700MiB will be used.
The '-r' option allows you to create a bootable sdcard with an alternative image for the installation to NAND flash or eMMC.
Example: "-r tmp/deploy/images/trux-som-mx6/fsl-image-qt5-trux-som-mx6" -- selects the "Qt5 image with X11" recovery image


Once the script is done, use the SD card to boot, and then to flash your internal storage/s either use the icons,
or the following linux shell script:
install_yocto.sh

For creating SDcard with Yocto + Android:
=========================================
Usage:
sudo MACHINE=<imx8mq-trux-q01|imx8mm-trux|imx8mp-trux> sources/meta-trucrux/scripts/trux_mk_yocto_sdcard/trux-create-yocto-sdcard-with-android.sh [options] /dev/sdX
(Change /dev/sdX to your device name)

options:
  -h            Display help message
  -s            Only show partition sizes to be written, without actually write them
  -a            Automatically set the rootfs partition size to fill the SD card
  -r            Select alternative rootfs for recovery images (default: build_x11/tmp/deploy/images/trux-som-mx6/fsl-image-gui-trux-som-mx6.*)

If you don't use the '-a' option, a default rootfs size of 3700MiB will be used.
The '-r' option allows you to create a bootable sdcard with an alternative image for the installation to NAND flash or eMMC.
Example: "-r tmp/deploy/images/trux-som-mx6/fsl-image-qt5-trux-som-mx6" -- selects the "Qt5 image with X11" recovery image


Once the script is done, use the SD card to boot, and then to flash your internal storage/s either use the icons(imx6/imx7),
or the following linux shell script:
install_android.sh