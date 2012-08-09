
The GPL source is created for ASUS wireless router related products. Please visit the ASUS support site (http://support.asus.com) to get the latest GPL tarball.It has a lot in common with many wireless router open source projects, including Oleg/Tomato/DD-WRT/OpenWRT. Thanks the developers of those projects for making the source code available.

Set Up Environment

    1. Install required packages
	
	Install these packages on Fedora x86 (tested on Fedora 8/9 by Asus):

	libncurses5
	libncurses5-dev
	m4
	bison
	gawk
	flex
	libstdc++6-4.4-dev
	g++-4.4
	g++
	git
	gitk
	zlib1g-dev	
	
	Install these packages on Ubuntu 10.04 LTS 64-bit:

	bison
	flex
	g++
	g++-4.4
	g++-multilib
	gawk
	gcc-multilib
	gperf
	gitk
	lib32z1-dev
	libncurses5
	libncurses5-dev
	libstdc++6-4.4-dev
	libtool
	m4
	pkg-config
	zlib1g-dev

	Install these packages on Gentoo Linux x86:
	
	=sys-devel/make-3.81-r2
	dev-util/gperf
	dev-vcs/git
	sys-devel/bison
	sys-devel/flex

	Note: Those using Gentoo Linux amd64 can install app-emulation/emul-linux-x86-baselibs in addition to the above packages.

   2. Extract sources to /media/ASUSWRT/asuswrt
	mkdir -p /media/ASUSWRT
	cd /media/ASUSWRT
	git clone git://github.com/RMerl/asuswrt-merlin.git /media/ASUSWRT/asuswrt
 
   3. Configure the environment
   	export PATH="${PATH}:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-linux/bin:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-uclibc/bin"
	cd /media/ASUSWRT/asuswrt/release/src-rt

   4. build firmware, ex, rt-n66u
	make rt-n66u

Known Issues

	1. Linker failures occur when a mipsel-linux-uclibc toolchain built against a newer version of uclibc is installed on your system.

	2. The build system is incompatible with a parallel make. You must not use make's -j option.

	3. The build system depends on GNU Make 3.81. Using any other version will cause build failures.
	
	4. Attempting to build without gperf installed will generate empty .c files that are not removed by `make clean`. This causes all subsequent attempts to build to fail.
