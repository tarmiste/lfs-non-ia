

## General notes about building LFS on PowerPC machines:

   In this, the term "PowerPC" normally refers to the Apple G3, G4 and
G5 PowerPC machines.   Other PowerPC based machines exist but
this document and repository is primarily focused on the Apple
PowerPC machines.   

   Normally the LFS_TGT value as set in Chapter 3 can be left as
is for building LFS on the PowerPC.  LFS_TGT would likely need
changes if building for some of the other variants of the PPC
architecture (e.g. the e500v2) but for building LFS on an 
Apple PowerPC machine, LFS_TGT does not need to be modified.

   Normally, the PowerPC kernel can be built from the standard linux
kernel version as is specified in the LFS book.   There are a number
of non Apple PowerPC boards that are also supported in the standard
kernel code.   However, building LFS on the various embedded 
PowerPC devices will likely require a hunt for the needed kernel source
for that particular machine..

   The yaboot bootloader is typically needed on Apple PowerPC 
machines.   Building yaboot from source is very problematic and it is 
easier to simply obtain an already existing yaboot binary package and
use it instead.   The yaboot binary tarball within this repository was 
created by repackaging Debians yaboot binary package into a simple tarball.

   U-boot is a bootloader commonly used in non-Apple PPC machines.  
In this case, the u-boot tools will be needed and have to be built 
and installed prior to building the kernel.

   The Apple PowerPC machines use a different partitioning scheme
than IA machines.   Several additional tools (e.g. mac-fdisk, hfsutils,
etc ) will need to be built.

   
