defconfig file: cyanogenmod_m7_defconfig  (arm-eabi-4.8)

Download:
=========
If you are not already using an AOSP toolchain (included in an AOSP build tree), download the corresponding official android toolchain for the arm-eabi specified above for this device:
        
git clone https://github.com/SaberMod/android_prebuilts_gcc_linux-x86_arm_sabermod-arm-eabi-4.8 for 4.8.2

Build the kernel:
=================
set the following environment variables:

export TOP= [where you installed the toolchain or top of android AOSP code base]
export PATH=$TOP/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8/bin:$PATH (use corresponding arm-eabi bin path)
export ARCH=arm
export SUBARCH=arm
export CROSS_COMPILE=arm-eabi-

make [the defconfig file for this device above]
make clean  (for subsequent builds)
make -j4    (in this example 4 is the number of processors of your build machine)

Output Binary Files:
====================
After the build process is finished, there should be a file named "zImage" found in arch/arm/boot/
If you are building a rom with this kernel ZImage, copy it into your build's output folder and rename it to "kernel".

You will also need the following kernel modules. These will eventually be installed into /system/lib/modules on the device.

kernel modules:
./driver/*.ko

If you have already built and installed a boot.img with root access you can also install the modules directly into the device using "adb remount" and "apb push [file] system/lib/modules/" for each file listed above. After installing files set permissions with "adb shell chmod 0644 system/lib/modules/*" and "adb reboot"

For additional information:
=========================== 
http://htcdev.com
