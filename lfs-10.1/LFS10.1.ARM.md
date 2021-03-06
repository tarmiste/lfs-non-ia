
## Notes regarding building LFS 10.1 on the ARM:

armv5: not supported

armv6: built with LFS 10.1 RC1.   Very slow build on RPI zero but did complete.

armv7: built with LFS 10.1 final.   vim build failed but may be operator error.

aarch64 does not build expect.   This can be fixed by finding and 
replacing config.guess and config.sub in the expect source tree
with the most recent versions.  This is not part of the book patch and
must be done manually.

the "gold" build in binutils chap06 requires a huge amount of time
on low RAM machines (due to swapping).  gold is not required for the base LFS
build (some BLFS packages need it)   Disabling gold in the binutils
configure step saves a lot of time.  


### Jhalfs

No changed to jhalfs needed for arm/aarch64.   Some prior versions of
jhalfs required LFS_TGT to be manually adjusted but that change no
longer seems to be needed.


### Book patch

The LFS book changes needed to build LFS 10.1 on the ARM can 
be found in lfs-book patch file in the subdirectory "patches".  The 
book patch can be applied to the LFS book to create a new version 
that can be used to build LFS for the ARM/aarch64.

(The book patch also includes changes for PowerPC architectures)

To apply the LFS book patch, extract a copy of the LFS10.1 book from
the svn repository and then apply the patch at the top of the book:

Then run jhalfs and point it at the patched book as it's 'working copy'


## Additional ARM packages

Beyond the changes found in the book patch, additional steps need to be
taken to complete a build for ARM.   

1) uboot_tools may be needed to build some ARM kernels.
2) There is a plethora of bootloaders and kernels for the various
   arm boards.   Additional packages may be needed to support your
   particular board.
 

## BLFS:

BLFS 10.1 packages seem to build on ARM without modification but this 
author has only tried a small set of them.

