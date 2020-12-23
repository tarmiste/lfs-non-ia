
## Notes regarding building LFS 8.4 on the ARM:

armv5: not tried yet.

armv6: not tried yet.

armv7: built without problems.

aarch64 does not build expect.   This can be fixed by finding and 
replacing config.guess and config.sub in the expect source tree
with the most recent versions.  This is not part of the book patch
yet.

the "gold" build in binutils chap06 requires a huge amount of time
on low RAM machines (due to swapping).  disabling gold in the binutils
configure step saves a lot of time.  


### Jhalfs

jhalfs LFS_TGT value must be modified for ARM.  Edit the LFS/master.sh
file and change LFS_TGT to:

..._gnueabi     for armv5
..._gnueabihf   for armv6,v7
..._gnu   for aarch64  (no change needed for aarch64...)

There is a jhalfs .patch file in patches that may be helpful in making
this change.  Check it visually though.


### Book patch

The LFS book changes needed to build LFS 8.4 on the ARM can 
be found in book patch file in the subdirectory "patches".  The 
book patch can be applied to the LFS book to create a new version 
that can be used to build LFS for the ARM.

(The book patch also includes changes for PowerPC architectures)

To apply the LFS book patch, extract a copy of the LFS8.4 book from
the svn repository and then apply the patch at the top of the book:

Then run jhalfs and point it at the patched book as it's 'working copy'


This book patch does the following:

1) Applies a patch to all gcc builds to enable hw floating point for
armv6 and v7.   armv5 does not have hw floating point.

2) In Chapter 5 both passes of GCC build require a change to the 
files that are modified under gcc/config .   The existing LFS book
only modified those files needed to build on the IA CPUs.
 
3) Various: (gcc-dumpmachine)/ is used instead of (uname -m)-pc-linux-gnu

4)  Grub is not needed and so grub is removed from Chapter 6.

5) In Chapter 6, "--enable-stack-protector=strong" is removed from 
the glibc configure step.    This is done for a powerpc bug but is benign
for ARM.

6) The book patch disables the removal of various static libraries.
This change is not specifically needed for ARM or ARM but is done simply for 
the authors preference that they not be deleted.
   
7) The book patch adds a (disabled by default) serial console entry
to inittab.   May not be needed but is benign if not.


## Additional ARM packages

Beyond the changes found in the book patch, additional steps need to be
taken to complete a build for ARM.   

1) uboot_tools may be needed to build ARM kernels.
 

## BLFS:

BLFS 8.4 packages seem to build on ARM without modification but this 
author has only tried a small set of them.

