## Build LFS for ARM, PPC and (maybe other) non-IA machines

10Jan2019 WIP

### Synopsis:

This repository contains materials such as notes, patches, build logs
scriptlets and similar items that may be useful in building 
Linux From Scratch (LFS) and Beyond LFS (BLFS) on CPU architectures 
other than x86 and x86_64 (aka IA).   

Information in this repository has originated from various sources.
Any derivative material in this repository retains the original
authors Copyright and is used in this repository under the license 
terms associated with the original work.  All original information 
in this repository is Copyrighted by the author Tom Armistead and
is provided in this repository under the terms of the
Creative Commons license.

The contents of this repository is distributed in the hope that it will 
be useful, but without any warranty; without even the implied 
warranty of merchantability.

THERE IS NO WARRANTY FOR THESE MATERIALS, TO THE EXTENT PERMITTED BY
APPLICABLE LAW. EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT
HOLDERS AND/OR OTHER PARTIES PROVIDE THE PROGRAM AS IS WITHOUT
WARRANTY OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A
PARTICULAR PURPOSE. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF
THE PROGRAM IS WITH YOU. SHOULD THE PROGRAM PROVE DEFECTIVE, YOU ASSUME
THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.


### Description:


The LFS book specifically targets building an LFS system only 
for x86/x86_64 based machines.  Although many of the instructions in the
LFS also work in building LFS on a non x86/64 machine, there are a 
number of changes in the book instructions that are needed to 
accomplish an LFS build on other CPU architectures.   The purpose of 
this respository is to document those changes in the hope that 
it may be useful to developers who wish to build LFS/BLFS on non 
x86/64 architectures.

Materials in this repository are most often tested with the sysvinit
version of the LFS book.  Periodically they have been tried with the
systemd version of the book and also seem to work for systemd builds 
but if you want to stay on the road most traveled the sysvinit version is it.

Materials in this repository won't work with the multi-lib variant
of the LFS.   Only supports pure 64 or pure 32 bit builds.

If you are using this repository to build LFS and run into difficulties
building LFS on non x86/64 machines, please DO NOT ask questions on the
LFS website.   By intention, the LFS book specifically targets only
x86/64 so any questions or problems building on other architectures are not
appropriate for the main LFS site.  If you run into problems, file
an issue in this repository or work through the issue yourself.  

If you are specifically interested in LFS for RaspberryPI, you may
find pilfs (http://intestinate.com/pilfs/ ) to be useful.   Pilfs provides
tarballs, scripts and such that make it very easy to run LFS on your
Pi board.   This repository provides information that is more general
in nature regarding building LFS on nonIA boards and doesn't provide 
tarballs or turnkey solutions like those which can be found in pilfs.


### Repository structure: 

This repository consists of a main level which contains this README
and other information which may be of general use in building LFS
and subdirectories which coorespond to a specific LFS releases and
contain information specific to that particular release.  

Currently there are six subdirectories: lfs90, lfs84 to lfs81 and lfs79,
cooresponding to LFS releases 9.0 to 7.9.
All materials herein should be considered as WIP but have been used 
to build an LFS system for some of ppc64, ppc32, ARM32 and ARM64 (aarch64).

Due to lack of machines to test on, building LFS on MIPs and other
architectures beside ppc and arm is not part of this repository.  
Building on some ppc variants such as E500 machines is also an unknown.

The contents of each lfs subdirectory varies a bit but will contain at least 
a LFS book patch (lfs-book.patch) in the 'patches' subdirectory.  The LFS book
patch is the main thing.   It modifies the LFS book such that the instructions
in it will work for additional architectures besides Intel.   Each directory
also may contain notes, jhalfs patches, source code bits and pieces, build logs, kernel
config files and other information specific to building that release 
on various architectures.  

This repository contents would typically be used (with jhalfs
for the build tool) as follows:

1) Obtain a local copy of the LFS book (in XML format) using subversion or
   otherwise.
2) Find the LFS book patch in the patches subdirectory and apply it
   to the local copy of the LFS book.
2a) If doing a "cut and paste" build, render the patched book into human 
   easily readable form (skip the jhalfs stuff) and build from it.

3) Obtain a copy of jhalfs using subversion and make any changes 
   needed.  The patches subdirectory may contain jhalfs patch(s) 
   that will help with this step.
3a) Arch specific custom configs can be added to the jhalfs build if 
   desired.
4) Initiate the build of LFS using jhalfs pointed at the local
   (working) copy of the patched LFS book.
5) Copy any extra LFS package patches from the patches directory to
   the sources directory of the LFS build area.
6) Once the jhalfs build of LFS is complete, chroot into the LFS build
   and build any extra tools needed for the architecture.   Build
   the kernel and bootloader as needed for the architecture.

Note that the book patch concentrates on changes to the build instructions
and not so much on the descriptive text.  If you are cut and pasting from 
the rendered book, be aware that the descriptive text may sometimes not 
exactly match the modified build instructions


### General notes about building LFS on nonIA boards:

   This section provides general information regarding building LFS
on non-IA CPUs.  Additional detailed information regarding building LFS for 
specific architectures and for specific LFS versions can be be found 
in other READMEs or documents.

1) LFS_TGT will likely need to be modified.

   The default LFT_TGT target variable value may not work properly for
nonIA architectures.  (Although the default LFS_TGT works ok for PowerMac 
builds).  It may need to be modified to a value that works for the 
architecture that you are building on.

   A mistake in the LFS_TGT setting will likely not be discovered
until some hours of time have been spent building packages.   So,
it is worth spending some time on getting this set properly before
starting the build.


2) Jhalfs may need to be modified.

   Note also that if building LFS with jhalfs, a modification may be
needed to the jhalfs code itself to set the LFS_TGT properly.   jhalfs
does not read and use the value of LFS_TGT from the book source but 
instead sets the LFS_TGT value in one of it's scripts.  So, if you have
to modify LFS_TGT for your target, you will also have to make an
adjustment to jhalfs.


3) SWAP space will likely be needed.

   Enabling SWAP space is crucial.   Many nonIA boards have 
limited amounts of RAM and the LFS build will not complete without
access to a SWAP partition.  Even with SWAP space, attempting to 
build LFS on a board with less than 256Meg of DRAM will not likely
succeed.

   Some boards primarly use SD cards or USB flash drives for storage.
If possible, use regular hard disk (or ssd) drives for the swap area 
and also for the LFS build area.  This will speed up the build up
a bit vs using usb flash drives or sd cards.

4) Be prepared for long build times.

   Patience is crucial.   The lower CPU speeds,small caches, and limited 
RAM of nonIA boards means that an LFS build will likely take some days.
(e.g. a build of LFS 8.1 with all final test suites enabled on a 
700Mhz ppc G3 required nearly 120 hours of compile time.)

   Using fast media (like an actual hard disk) for the LFS and swap
areas may help speed up the build on SD/flash based machines.

   It's best to patch (if needed) jhalfs to build for your machine and
let it take care of doing the long build.

5) The bulk of the needed changes will be in LFS Chapter 05.

   Typically, most of the changes needed to build LFS on nonIA board are 
in the building of the tool chain packages.  In particular, the
build of GCC pass1 and pass2 in Chapter 5 will almost certainly
require changes to work with non-IA CPUs.   But there will likely 
be other changes needed besides the tool chain.

   Note: The LFS patches sometimes don't work for non-IA boards.  e.g.
In the LFS8.3 the chap6 coreutils patch causes problems for PPC32 builds.

   Most BLFS packages seem to build ok as is on non-IA machines.  But
then again, only a small set of them have been built by this author.

   The blfs tool itself seems to function properly on PPC and ARM
systems without any changes needed.

6) Skip building Grub on non-IA boards.

   grub is specific to the IA boards and is not needed on nonIA
boards.   It does not likely need to be built for a non IA board.

7) Serial console may need to be enabled.

   Many nonIA boards have no graphics display and are accessed 
through serial console.   A change to /etc/inittab is required to 
enable login via serial console.

8) Non standard kernel and bootloader code may be needed.

   Appropriate kernels and bootloaders for the LFS build 
will have to be tracked down.   The kernel version listed in the LFS
book may not work for the board of interest.  The kernel code may 
need to be obtained from a non standard repository and/or may need 
to be patched.   Additional tools may need to be built in order 
to even build the kernel.  The same is true for whatever bootloader 
is needed.

   Finding working kernel source is often a challenge.   Googling
may find many possible sources  of a kernel for a particular board
and it's not clear which one(s) will work well.

   The kernel referenced in the LFS book can be used to build 
the kernel headers even if the kernel itself is built from another
source base.  (as long as it is a reasonably recent kernel version).

9) Make sure the clock is set accurately

   If the system clock is not set to a reasonably accurate value,
some packages will not build properly.   Clock setting is not 
typically a concern on most IA computers but many hobbyist type of
boards do not have a built in clock and expect the time to be 
set manually or via network.   An incorrect clock value can cause
build problems.


10) Next

   Materials that may be helpful for building specific LFS releases
may be found in the release subdirectories within this repository.
