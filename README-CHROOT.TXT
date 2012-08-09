It is possible to build inside a chroot on any distribution. This requires root
privileges, either a x86 system or and amd64 multilib system and a few
utilities. The procedure is simple:

   1. Make a chroot:

	mkdir /mnt/gentoo
	wget ftp://gentoo.osuosl.org/pub/gentoo/releases/x86/current-stage3/*.tar.bz2 -O - | tar -jx -C /mnt/gentoo
	mount -t proc none /mnt/gentoo/proc
	mount -t devtmpfs devfs /mnt/gentoo/dev	
	mount -t devpts devpts /mnt/gentoo/dev/pts
	chroot /mnt/gentoo /bin/bash
	export PS1="(chroot) ${PS1}"
	emerge =sys-devel/make-3.81-r2 dev-util/gperf dev-vcs/git sys-devel/bison sys-devel/flex

	Note: It is possible to substitute an amd64 Gentoo tarball. If you do, you must also `emerge app-emulation/emul-linux-x86-baselibs`.

   2. Extract sources to /media/ASUSWRT/asuswrt
	mkdir -p /media/ASUSWRT
	git clone git://github.com/RMerl/asuswrt-merlin.git /media/ASUSWRT/asuswrt

   3. Configure the environment
   	export PATH="${PATH}:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-linux/bin:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-uclibc/bin"
	cd /media/ASUSWRT/asuswrt/release/src-rt

   4. build firmware, ex, rt-n66u
	make rt-n66u

If you reboot your system, you will need to do the following:

   1. Reinitialize the chroot 
	mount -t proc none /mnt/gentoo/proc
	mount -t devtmpfs devfs /mnt/gentoo/dev	
	mount -t devpts devpts /mnt/gentoo/dev/pts
	chroot /mnt/gentoo /bin/bash
	export PS1="(chroot) ${PS1}"

   2. Configure the environment
   	export PATH="${PATH}:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-linux/bin:/media/ASUSWRT/asuswrt/tools/brcm/hndtools-mipsel-uclibc/bin"
	cd /media/ASUSWRT/asuswrt/release/src-rt

   3. build firmware, ex, rt-n66u
	make rt-n66u
