
## Notes regarding building LFS 10.1 on the PowerPC:

### Jhalfs

JHALFS does not require modifications to build LFS for MAC PPC type 
machines.   

### Book patch

The LFS book changes needed to build LFS 10.1 on the PowerPC can 
be found in lfs-book.patch file in the subdirectory "patches".  The 
book patch can be applied to the LFS book to create a new version 
that can be used to build LFS for the PowerPC.

(The book patch also includes changes for arm architectures)

To apply the LFS book patch, extract a copy of the LFS10.1 book from
the svn repository and then apply the patch at the top of the book:

Then run jhalfs and point it at the patched book as it's 'working copy'


## Additional PPC packages

Beyond the changes found in the book patch, additional steps need to be
taken to complete a build for PowerPC.   

1) Various additional packages are needed for Apple PowerPC machines. 
 
2) The yaboot bootloader needs to be installed (and later configured)

Custom config files may be found in the subdirectory custom_ppc_configs
that can be used to automatically build the needed additional packages.

To use the custom config files with jhalfs, copy them to the custom/config
subdirectory of jhalfs and enable the custom tools menu selection in 
jhalfs. 


## BLFS:

BLFS 10.1 packages generally seem to build on PPC without modification but 
this author has only tried a small set of them.

nss build is known to fail on ppc32.    This build failure goes away if the gcc
version is bumped down to 9.3.0 (and presumably earlier versions also.).   This
might be a gcc 10.x bug on ppc32.

