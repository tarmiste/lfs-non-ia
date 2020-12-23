
# The lfs 10.0 book patch now nominally works for ppc32 and ppc64.   Haven't done much testing with it yet.

On some ppc linux systems (e.g. ubuntu 16) the version of the file utility is too old and the first build 
of file will fail due to it.   The LFS book does not indicate any specific version requirements for file but
apparently there is one.   Building and installing a current version of file on the host system fixes it.

libffi on ppc32 bit is suspicious.  It requires a patch and compiles with it but may require further 
patches to work properly.   If libffi is a crucial package, it may be prudent to back the version down
to 3.2.1.

# The ARM architecture probably won't be supported in this release.   Some of the needed changes are
present in the patch but are fully there.   Hopefully arm support will be back again in lfs 10.1.
