
## Notes regarding building LFS 8.4 on the PowerPC:

### Jhalfs

JHALFS does not require modifications to build LFS for MAC PPC type 
machines.   

### Book patch

The LFS book changes needed to build LFS 8.4 on the PowerPC can 
be found in book patch file in the subdirectory "patches".  The 
book patch can be applied to the LFS book to create a new version 
that can be used to build LFS for the PowerPC.

(The book patch also includes changes for arm architectures)

To apply the LFS book patch, extract a copy of the LFS8.4 book from
the svn repository and then apply the patch at the top of the book:

Then run jhalfs and point it at the patched book as it's 'working copy'


This book patch does the following:

1) The LFS book performs a number operations that are x86_64 (64 bit)
specific.  E.g. create a symlink for /tools/lib and /tools/lib64.   
The book patch makes these same changes for the G5 (ppc64) CPU.

2) In Chapter 5 both passes of GCC build require a change to the 
files that are modified under gcc/config .   The existing LFS book
only modified those files needed to build on the IA CPUs.
 
3) Various: (gcc-dumpmachine)/ is used instead of (uname -m)-pc-linux-gnu

4)  Grub is not needed and so grub is removed from Chapter 6.

5) In Chapter 6, "--enable-stack-protector=strong" is removed from 
the glibc configure step.    On PowerPC32 (only) this option may result
in segmentation violations after installation of glibc.    This failure
doesn't seem to happen when building for G5 or ARM boards.   The
book patch removes it for all architectures.    Add it back in if 
you need it enabled but you will probably run into problems that
you will have to fix.

6) The book patch disables the removal of various static libraries.
This change is not specifically needed for ARM or PPC but is done simply for 
the authors preference that they not be deleted.
   
7) The book patch adds a (disabled by default) serial console entry
to inittab.   Not usually needed on PowerMACs but is benign.

8) The book patch modifies the kernel build in Chapter as needed for
the PowerPC names.   It also enables stripping of kernel modules
to save space but this stripping change is not needed for ARM or PPC and  
is done simply for the authors preference.
   


## Additional PPC packages

Beyond the changes found in the book patch, additional steps need to be
taken to complete a build for PowerPC.   

1) Various additional packages are needed for Apple PowerPC machines. 
 
2) The yaboot bootloader needs to be installed (and later configured)

Custom config files can be found in the subdirectory custom_ppc_configs
that can be used to automatically build the needed additional packages.

To use the custom config files with jhalfs, copy them to the custom/config
subdirectory of jhalfs and enable the custom tools menu selection in 
jhalfs. 


## BLFS:

BLFS 8.4 packages generally seem to build on PPC without modification but 
this author has only tried a small set of them.

