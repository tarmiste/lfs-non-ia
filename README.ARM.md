

## General notes about building LFS on ARM machines:

   The LFS_TGT value is different for ARM than it is for x86/PPC:

*-lfs--linux-gnueabi   works for armv5
*-lfs--linux-gnueabihf   works for armv6,armv7
*-lfs--linux-gnu   works for aarch64

   The various patches in this repository use the above LFT_TGT settings
but your own situation might require or benefit from a different setting.

   Few of the ARM boards are fully supported in the standard kernel
source.   It is likely that you will have to track down the proper
kernel source to use with your board.   

   Same with the bootloader for ARM boards.   U-boot seems to be 
a common (but not universal) bootloader for ARM boards but even so, 
the proper bootloader code may have to be obtained from somewhere other
than the standard u-boot repository.

    For now, a gcc patch is used for the armv6,7 and 8 builds
to enable hardware floating point.   The patches may be found in the
patches subdirectory and will have to be manually copied into the 
sources subdirectory during the LFS build.   (The arm gcc patches are
not included in the LFS book package list and so are not downloaded
as part of the wget list or jhalfs run).

    ARMv5 support may be dropped from GCC in release 9.0.  

