# Based on the file created for Arch Linux by:
# Tobias Powalowski <tpowa@archlinux.org>
# Thomas Baechler <thomas@archlinux.org>
#
# This PKGBUILD is based on Manjaro Linux team work especially by:
# Maintainer: Philip Müller (x86_64) <philm@manjaro.org>
# Maintainer: Jonathon Fernyhough (i686) <jonathon@manjaro.org>
# Contributor: Helmut Stult <helmut[at]manjaro[dot]org>
#
# Made by Rocky Prabowo <rocky@lazycats.id>

### BUILD OPTIONS
# Optionally select a sub architecture by number if building in a clean chroot
# Leaving this entry blank will require user interaction during the build
# which will cause a failure to build if using makechrootpkg. Note that the
# generic (default) option is 30.
#
#  1. AMD Opteron/Athlon64/Hammer/K8 (MK8)
#  2. AMD Opteron/Athlon64/Hammer/K8 with SSE3 (MK8SSE3)
#  3. AMD 61xx/7x50/PhenomX3/X4/II/K10 (MK10)
#  4. AMD Barcelona (MBARCELONA)
#  5. AMD Bobcat (MBOBCAT)
#  6. AMD Jaguar (MJAGUAR)
#  7. AMD Bulldozer (MBULLDOZER)
#  8. AMD Piledriver (MPILEDRIVER)
#  9. AMD Steamroller (MSTEAMROLLER)
#  10. AMD Excavator (MEXCAVATOR)
#  11. AMD Zen (MZEN)
#  12. AMD Zen 2 (MZEN2)
#  13. Intel P4 / older Netburst based Xeon (MPSC)
#  14. Intel Atom (MATOM)
#  15. Intel Core 2 (MCORE2)
#  16. Intel Nehalem (MNEHALEM)
#  17. Intel Westmere (MWESTMERE)
#  18. Intel Silvermont (MSILVERMONT)
#  19. Intel Goldmont (MGOLDMONT)
#  20. Intel Goldmont Plus (MGOLDMONTPLUS)
#  21. Intel Sandy Bridge (MSANDYBRIDGE)
#  22. Intel Ivy Bridge (MIVYBRIDGE)
#  23. Intel Haswell (MHASWELL)
#  24. Intel Broadwell (MBROADWELL)
#  25. Intel Skylake (MSKYLAKE)
#  26. Intel Skylake X (MSKYLAKEX)
#  27. Intel Cannon Lake (MCANNONLAKE)
#  28. Intel Ice Lake (MICELAKE)
#  29. Intel Cascade Lake (MCASCADELAKE)
#  30. Generic-x86-64 (GENERIC_CPU)
#  31. Native optimizations autodetected by GCC (MNATIVE)
_subarch=31

# Set these variables below to "y" enable them

# Tweak kernel options prior to a build nconfig
_makenconfig='n'

# Compile ONLY used modules to VASTLY reduce the number of modules built
# and the build time.
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: https://aur.archlinux.org/packages/modprobed-db
# This PKGBUILD read the database kept if it exists
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed-db
_localmodcfg='n'

# Use the current kernel's .config file
#
# Enabling this option will use the .config of the RUNNING kernel rather than
# the ARCH defaults. Useful when the package gets updated and you already went
# through the trouble of customizing your config options.  NOT recommended when
# a new kernel is released, but again, convenient for package bumps.
_use_current='n'

# Unlock additional CPU optimizations for gcc
_enable_gcc_more_v='y'

# Enable ccache-friendly build
_ccache_friendly='y'

# Include AUFS support. Manjaro includes this to their kernel by default
_enable_aufs='n'

# Enable bootsplash support. Manjaro includes this to their kernel by default
_enable_bootsplash='n'

# Enable PCI overrides for missing acs capabilities
_enable_pci_acs_override='y'

# Use prebaked Manjaro kernel configurations.
_use_manjaro_configs='n'

##! IMPORTANT: Do no edit anything below this line unless you know what you're .

_major=5.6
_minor=6
_rel=1
_kernelname='clear'
_basekernel=${_major}
_basever=${_major/./}
_srcname=linux-${_major}
_clr=${_major}.4-938
_aufs='20200302'
_gcc_more_v='20191217'

pkgbase=linux-manjaro-clear
pkgname=('linux-manjaro-clear' 'linux-manjaro-clear-headers')
pkgver=${_major}.${_minor}
pkgrel=$_rel
arch=('i686' 'x86_64')
url="https://github.com/clearlinux-pkgs/linux"
license=('GPL2')
makedepends=('bc' 'cpio' 'docbook-xsl' 'git' 'inetutils' 'kmod' 'libelf' 'xmlto')
options=('!strip')
source=(
	### [BASE] Main release
	"https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${_major}.tar.xz"
	"https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${_major}.tar.sign"
	### [END OF BASE]

	### [PATCH-0] Minor release and stable release patches queue (disabled by default)
	"https://cdn.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
	# "prepatch-${_basekernel}.patch"
	### [END OF PATCH-0]

	### [PATCH-1] Patched kernel config files from Manjaro
	'config'
	'config.x86_64'
	'config.aufs'
	### [END OF PATCH-1]

	### [PATCH-2] AUFS Patches
 	"aufs5.x-rcN-${_aufs}.patch"
        'aufs5-base.patch'
        'aufs5-kbuild.patch'
        'aufs5-loopback.patch'
        'aufs5-mmap.patch'
        'aufs5-standalone.patch'
        'tmpfs-idr.patch'
        'vfs-ino.patch'
	### [END OF PATCH-2]

	### [PATCH-3] Arch Linux Patches
	'0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-CLONE_NEWUSER.patch'
	### [END OF PATCH-3]

	### [PATCH-4] Manjaro Patches
	'0001-apparmor-patch-to-provide-compatibility-with-v2-net-rules.patch'
	'0002-apparmor-af_unix-mediation.patch'
	'0003-apparmor-fix-use-after-free-in-sk_peer_label.patch'
	'0004-apparmor-fix-apparmor-mediating-locking-non-fs-unix-sockets.patch'
	### [END OF PATCH-4]

	### [PATCH-5] clearlinux Patches
	# "clearlinux::git+https://github.com/clearlinux-pkgs/linux.git#tag=${_clr}"
	"clearlinux-${_clr}.tar.gz::https://codeload.github.com/clearlinux-pkgs/linux/tar.gz/${_clr}"
	### [END OF PATCH-5]

	### [PATCH-6] Patch source to unlock additional gcc CPU optimizations
	"enable_additional_cpu_optimizations-$_gcc_more_v.tar.gz::https://github.com/graysky2/kernel_gcc_patch/archive/$_gcc_more_v.tar.gz"
	### [END OF PATCH-6]

	### [PATCH-7] ACS Override patch
	'pci-enable-overrides-for-missing-acs-capabilities.patch::https://aur.archlinux.org/cgit/aur.git/plain/pci-enable-overrides-for-missing-acs-capabilities.patch?h=linux-clear'
	### [END OF PATCH-7]

	### [PATCH-8] Personal custom patches, you might not need this. Comment any patch that you don't need.
    # No additional patches needed at this moment
	### [END OF PATCH-8]

	### [PATCH-9] Bootsplash: Add bootsplash - http://lkml.iu.edu/hypermail/linux/kernel/1710.3/01542.html
	'0001-bootsplash.patch'
	'0002-bootsplash.patch'
	'0003-bootsplash.patch'
	'0004-bootsplash.patch'
	'0005-bootsplash.patch'
	'0006-bootsplash.patch'
	'0007-bootsplash.patch'
	'0008-bootsplash.patch'
	'0009-bootsplash.patch'
	'0010-bootsplash.patch'
	'0011-bootsplash.patch'
	'0012-bootsplash.patch'
	'0013-bootsplash.patch'
	### [END OF PATCH-9]
        )
sha256sums=('e342b04a2aa63808ea0ef1baab28fc520bd031ef8cf93d9ee4a31d4058fcb622'
            'SKIP'
            '669e3bebb988e7f1124e6687e384304ed70139ea4a869bd4159c3df27c3d9082'
            'bfe52746bfc04114627b6f1e0dd94bc05dd94abe8f6dbee770f78d6116e315e8'
            'c4c1e6dc98efba3d0af1a70a28fdeaf84ce1bfc61713c2d7159403bbab59b233'
            'b44d81446d8b53d5637287c30ae3eb64cae0078c3fbc45fcf1081dd6699818b5'
            'ef60c4afbae6270748bca1661d054815ea83f84ac3962fa316cd1b6abea506a4'
            '294d00163a5c68fee26f0adb52ccc309b1d1ae69ed7fe65fdabf29d425798ee4'
            '8e3b0a3c7c9b62d29dc711885ef00578a65f1d0315f31e1d9f438aac1ced02d6'
            '562752375ec67ece529eadf3f003193a371a875bdf6ed842ea8afde0e2e5618f'
            '023a61cdf160ca98dc9a0222c1e82c98a1cc09ddfe2c04020a3c30a9b568107e'
            'eb1aaa49b9d5cdf35985a0803129b39145f81a4f1499f6e7f2afd8d31017b694'
            '1c69ed79eeef0c0dcf68ce3086a0e372260d2fed94c93c7711e0682b2bcaae39'
            '29adcb9fac02b77f93ec36c2003ae930cc0a6ee1884d002c280480b5e8f22261'
            '7685d526bbdbfa795986591a70071c960ff572f56d3501774861728a9df8664c'
            '98202b8ad70d02d86603294bae967874fa7b18704b5c7b867568b0fd33a08921'
            '5cbbf3db9ea3205e9b89fe3049bea6dd626181db0cb0dc461e4cf5a400c68dd6'
            'c7dbec875d0c1d6782c037a1dcefff2e5bdb5fc9dffac1beea07dd8c1bdef1d7'
            '77746aea71ffb06c685e7769b49c78e29af9b2e28209cd245e95d9cbb0dba3c9'
            '6d909aeebc1379e02aaa52a3b4984acf6a06b8a6b9f6e118f1b251883d411986'
            '7a4a209de815f4bae49c7c577c0584c77257e3953ac4324d2aa425859ba657f5'
            '4127910703ed934224941114c2a4e0bcc5b4841f46d04063ed7b20870a51baa0'
            'a504f6cf84094e08eaa3cc5b28440261797bf4f06f04993ee46a20628ff2b53c'
            'e096b127a5208f56d368d2cb938933454d7200d70c86b763aa22c38e0ddb8717'
            '8c1c880f2caa9c7ae43281a35410203887ea8eae750fe8d360d0c8bf80fcc6e0'
            '1144d51e5eb980fceeec16004f3645ed04a60fac9e0c7cf88a15c5c1e7a4b89e'
            'dd4b69def2efacf4a6c442202ad5cb93d492c03886d7c61de87696e5a83e2846'
            '028b07f0c954f70ca37237b62e04103e81f7c658bb8bd65d7d3c2ace301297dc'
            'c8b0cb231659d33c3cfaed4b1f8d7c8305ab170bdd4c77fce85270d7b6a68000'
            '8dbb5ab3cb99e48d97d4e2f2e3df5d0de66f3721b4f7fd94a708089f53245c77'
            'a7aefeacf22c600fafd9e040a985a913643095db7272c296b77a0a651c6a140a'
            'e9f22cbb542591087d2d66dc6dc912b1434330ba3cd13d2df741d869a2c31e89'
            '27471eee564ca3149dd271b0817719b5565a9594dc4d884fe3dc51a5f03832bc'
            '60e295601e4fb33d9bf65f198c54c7eb07c0d1e91e2ad1e0dd6cd6e142cb266d'
            '035ea4b2a7621054f4560471f45336b981538a40172d8f17285910d4e0e0b3ef')

_source_use_git_apply=(
	'0013-bootsplash.patch'
)

_source_skip_auto_patch=()

_source_acs_override_patches=(
	'pci-enable-overrides-for-missing-acs-capabilities.patch'
)

_source_aufs_patches=(
	'config.aufs'
	"aufs5.x-rcN-${_aufs}.patch"
        'aufs5-base.patch'
        'aufs5-kbuild.patch'
        'aufs5-loopback.patch'
        'aufs5-mmap.patch'
        'aufs5-standalone.patch'
        'tmpfs-idr.patch'
        'vfs-ino.patch'
)

_source_bootsplash_patches=(
	'0001-bootsplash.patch'
	'0002-bootsplash.patch'
	'0003-bootsplash.patch'
	'0004-bootsplash.patch'
	'0005-bootsplash.patch'
	'0006-bootsplash.patch'
	'0007-bootsplash.patch'
	'0008-bootsplash.patch'
	'0009-bootsplash.patch'
	'0010-bootsplash.patch'
	'0011-bootsplash.patch'
	'0012-bootsplash.patch'
	'0013-bootsplash.patch'
)

validpgpkeys=(
  'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
  '647F28654894E3BD457199BE38DBBDC86092693E'  # Greg Kroah-Hartman
)

_bootstrap() {
	if [ "$_ccache_friendly" = "y" ] ; then
		export KBUILD_BUILD_HOST=manjaro
		export KBUILD_BUILD_USER=build
		export KBUILD_BUILD_TIMESTAMP="Thu, 01 Jan 1970 00:00:00 +0000"
	else
		export KBUILD_BUILD_HOST=$HOST
		export KBUILD_BUILD_USER=$USER
		export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"
	fi
	[ "$_enable_aufs" = "y" ] || _source_skip_auto_patch+=("${_source_aufs_patches[@]}")
	[ "$_enable_bootsplash" = "y" ] || _source_skip_auto_patch+=("${_source_bootsplash_patches[@]}")
	[ "$_enable_pci_acs_override" = "y" ] || _source_skip_auto_patch+=("${_source_acs_override_patches[@]}")
}

prepare() {
	_bootstrap
	cd "${srcdir}/linux-${_basekernel}"

	### Add upstream patch
	patch -p1 -i "${srcdir}/patch-${pkgver}"

	### Add the latest fixes from stable queue, if needed
	### http://git.kernel.org/?p=linux/kernel/git/stable/stable-queue.git
	### Enable only if you have "gen-stable-queue-patch.sh" executed before
	# patch -Np1 -i "${srcdir}/prepatch-${_basekernel}.patch"

	### Kernel version setting
	if [ "${_kernelname}" != "" ] ; then
		# sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"-${_kernelname}\"|g" ./.config
		# sed -ri "s|(\#\s)?CONFIG_LOCALVERSION_AUTO.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
		msg2 "Setting version..."
		scripts/setlocalversion --save-scmversion
		echo "-$pkgrel" > localversion.10-pkgrel
		echo "-${_kernelname}" > localversion.20-pkgname
	fi

	### Set extraversion to pkgrel
	# sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

	### Add Clear Linux patches
	msg2 "Applying Clear Linux patches..."
	for i in $(grep '^Patch' ${srcdir}/linux-${_clr}/linux.spec |\
			grep -Ev '^Patch0123' | sed -n 's/.*: //p'); do
			echo "Applying patch ${i}..."
		patch -Np1 -i "$srcdir/linux-${_clr}/${i}"
	done

	### Automatic source patching routine
	local src
	for src in "${source[@]}"; do
		src="${src%%::*}"
		src="${src##*/}"
		[[ $src = *.patch ]] || continue

		### Skip auto patching on patches defined in _source_skip_auto_patch
		if [[ " ${_source_skip_auto_patch[@]} " =~ " ${src} " ]]; then
			msg2 "Skipping patch $src..."
			continue
		fi

		### Binary patching, needed for 0013-bootsplash.patch on PATCH-9
		if [[ " ${_source_use_git_apply[@]} " =~ " ${src} " ]]; then
			msg2 "Applying patch with binary files $src..."
			### Using git-apply to patch binary files
			git apply -p1 < "${srcdir}/$src"
			continue
		fi

		msg2 "Applying patch $src..."
		patch -Np1 < "${srcdir}/$src"
	done

	### Setting config
	msg2 "Setting config..."
	if [ "$_use_manjaro_configs" = "y" ] ; then
		[ "${CARCH}" = "x86_64" ] && cat "${srcdir}/config.x86_64" > ./.config || cat "${srcdir}/config" > ./.config
		cat $srcdir/linux-${_clr}/config >> ./.config
	else
		cp -Tf $srcdir/linux-${_clr}/config ./.config
	fi
	[ "$_enable_aufs" = "y" ] && cat "${srcdir}/config.aufs" >> ./.config

	### Enable extra stuff from Arch and Manjaro kernel
	msg2 "Enable extra stuff from Arch and Manjaro kernel..."

	### General setup
	scripts/config	--enable IKCONFIG \
			--enable-after IKCONFIG IKCONFIG_PROC \
			--undefine RT_GROUP_SCHED

	### Power management and ACPI options
	scripts/config	--enable ACPI_REV_OVERRIDE_POSSIBLE  \
			--enable ACPI_TABLE_UPGRADE

	### Enable loadable module support
	scripts/config	--undefine MODULE_SIG_FORCE \
			--enable MODULE_COMPRESS \
			--enable-after MODULE_COMPRESS MODULE_COMPRESS_XZ

	### Networking support
	scripts/config	--enable NETFILTER_INGRESS \
			--module NET_SCH_CAKE

	### Device Drivers
	scripts/config	--enable FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER \
			--enable DELL_SMBIOS_SMM \
			--module PATA_JMICRON \
			--enable SND_OSSEMUL \
			--module-after SND_OSSEMUL SND_MIXER_OSS \
			--module-after SND_MIXER_OSS SND_PCM_OSS \
			--enable-after SND_PCM_OSS SND_PCM_OSS_PLUGINS

	# Security options
        scripts/config --enable SECURITY_SELINUX \
                       --enable-after SECURITY_SELINUX SECURITY_SELINUX_BOOTPARAM \
                       --enable SECURITY_SMACK \
                       --enable-after SECURITY_SMACK SECURITY_SMACK_BRINGUP \
                       --enable-after SECURITY_SMACK_BRINGUP SECURITY_SMACK_NETFILTER \
                       --enable-after SECURITY_SMACK_NETFILTER SECURITY_SMACK_APPEND_SIGNALS \
                       --enable SECURITY_TOMOYO \
                       --enable SECURITY_APPARMOR \
                       --enable SECURITY_YAMA	
	
	### AMD and KVM stuff
	scripts/config	--enable HAVE_KVM \
			--module KVM \
			--module KVM_INTEL \
			--module KVM_AMD \
			--enable KVM_AMD_SEV \
			--enable DRM_AMD_DC_DCN2_0 \
			--enable AMD_IOMMU \
			--enable AMD_IOMMU_V2 \
			--module GPIO_AMD_FCH \
			--enable MICROCODE_AMD

	### Default Manjaro loglevel
	scripts/config	--set-val CONSOLE_LOGLEVEL_DEFAULT 4 \
			--set-val CONSOLE_LOGLEVEL_QUIET 1 \
			--set-val MESSAGE_LOGLEVEL_DEFAULT 7 \
			--undefine TTY_PRINTK

	### Disable GCC plugins for ccache-friendly build
	if [ "$_ccache_friendly" = "y" ] ; then
		scripts/config	--disable GCC_PLUGINS \
				--undefine GCC_PLUGIN_STRUCTLEAK \
				--undefine GCC_PLUGIN_STRUCTLEAK_BYREF_ALL
	fi
	
	## Library routines
	scripts/config --enable FONT_TER16x32

	make olddefconfig

	### Patch source to unlock additional gcc CPU optimizations
	### https://github.com/graysky2/kernel_gcc_patch
	if [ "${_enable_gcc_more_v}" = "y" ]; then
		echo "Applying enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v5.5+.patch ..."
		patch -Np1 -i "$srcdir/kernel_gcc_patch-$_gcc_more_v/enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v5.5+.patch"
	fi

	### Get kernel version
	if [ "${_enable_gcc_more_v}" = "y" ] || [ -n "${_subarch}" ]; then
		yes "$_subarch" | make oldconfig
	else
		make prepare
	fi

	### Prepared version
	make -s kernelrelease > version
	msg2 "Prepared %s version %s" "$pkgbase" "$(<version)"

	### Optionally load needed modules for the make localmodconfig
	# See https://aur.archlinux.org/packages/modprobed-db
	if [ "$_localmodcfg" = "y" ]; then
		if [ -f $HOME/.config/modprobed.db ]; then
		msg2 "Running Steven Rostedt's make localmodconfig now"
		make LSMOD=$HOME/.config/modprobed.db localmodconfig
		else
		msg2 "No modprobed.db data found"
		exit
		fi
	fi

	### Optionally use running kernel's config
    # code originally by nous; http://aur.archlinux.org/packages.php?ID=40191
    if [ "$_use_current" = "y" ]; then
        if [[ -s /proc/config.gz ]]; then
            echo "Extracting config from /proc/config.gz..."
            # modprobe configs
            zcat /proc/config.gz > ./.config
        else
            warning "Your kernel was not compiled with IKCONFIG_PROC!"
            warning "You cannot read the current config!"
            warning "Aborting!"
            exit
        fi
    fi

  # Don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh

  ### Configure the kernel. Replace the line below with one of your choice.
  # make menuconfig # CLI menu for configuration
  # make nconfig # new CLI menu for configuration
  # make xconfig # X-based configuration
  # make oldconfig # using old config from previous kernel version
  ### ... or manually edit .config

  ### Rewrite configuration
  yes "" | make config >/dev/null

  ### Run make nconfig if needed
  [ "$_makenconfig" = "y" ] && make nconfig

  ### Save configuration for later reuse
  cp -Tf ./.config "${startdir}/config-${pkgver}-${pkgrel}-${_kernelname}"
}

build() {
	cd "${srcdir}/linux-${_basekernel}"

	# build!
	# make ${MAKEFLAGS} LOCALVERSION= bzImage modules
	make ${MAKEFLAGS} bzImage modules
}

package_linux-manjaro-clear() {
	pkgdesc="The ${pkgbase/linux/Linux} kernel and modules"
	depends=('coreutils' 'kmod' 'initramfs')
	optdepends=('crda: to set the correct wireless channels of your country'
				'linux-firmware: firmware images needed for some devices'
				'modprobed-db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig')
	provides=("linux-clear=${pkgver}")
	provides+=(VIRTUALBOX-GUEST-MODULES WIREGUARD-MODULE)

	cd "${srcdir}/linux-${_basekernel}"

	KARCH=x86

	### Get kernel version
	#   _kernver="$(make LOCALVERSION= kernelrelease)"
	_kernver="$(make kernelrelease)"
	local _modulesdir="${pkgdir}/usr/lib/modules/${_kernver}"

	mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
	#   make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}/usr" modules_install
	make INSTALL_MOD_PATH="${pkgdir}/usr" modules_install

	### Systemd expects to find the kernel here to allow hibernation
	### https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
	#   install -Dm644 "$(make LOCALVERSION= -s image_name)" "${_modulesdir}/vmlinuz"
	install -Dm644 "$(make -s image_name)" "${_modulesdir}/vmlinuz"

	### Used by mkinitcpio to name the kernel
	echo "${pkgbase}" | install -Dm644 /dev/stdin "${_modulesdir}/pkgbase"
	echo "${_basekernel}-${_kernelname}-${CARCH}" | install -Dm644 /dev/stdin "${_modulesdir}/kernelbase"

	### Add kernel version
	if [ "${CARCH}" = "x86_64" ]; then
		echo "${pkgver}-${pkgrel}-${_kernelname} x64" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
	else
		echo "${pkgver}-${pkgrel}-${_kernelname} x32" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
	fi

	### Make room for external modules
	local _extramodules="extramodules-${_basekernel}-${_kernelname:--MANJARO}"
	ln -s "../${_extramodules}" "${_modulesdir}/extramodules"

	### Add real version for building modules and running depmod from hook
	echo "${_kernver}" |
		install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules/${_extramodules}/version"

	### Remove build and source links
	rm ${_modulesdir}/{source,build}

	### Run depmod
	depmod -b "${pkgdir}/usr" -F System.map "${_kernver}"

	### Add vmlinux
	install -Dt "${pkgdir}/usr/lib/modules/${_kernver}/build" -m644 vmlinux

	### Fix package files permissions
	msg2 "Fixing permissions..."
	chmod -Rc u=rwX,go=rX "${pkgdir}"
}

package_linux-manjaro-clear-headers() {
	pkgdesc="Header files and scripts for building modules for ${pkgbase/linux/Linux} kernel"
	provides=("linux-clear-headers=$pkgver")

	cd "${srcdir}/linux-${_basekernel}"
	local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"
	msg2 "Installing headers and build files..."

	# install -Dt "${_builddir}" -m644 Makefile .config Module.symvers System.map localversion.* version vmlinux
	install -Dt "${_builddir}" -m644 Makefile .config Module.symvers
	install -Dt "${_builddir}/kernel" -m644 kernel/Makefile

	mkdir "${_builddir}/.tmp_versions"

	cp -t "${_builddir}" -a include scripts

	install -Dt "${_builddir}/arch/${KARCH}" -m644 "arch/${KARCH}/Makefile"
	install -Dt "${_builddir}/arch/${KARCH}/kernel" -m644 "arch/${KARCH}/kernel/asm-offsets.s"
	#install -Dt "${_builddir}/arch/${KARCH}/kernel" -m644 "arch/${KARCH}/kernel/macros.s"

	if [ "${CARCH}" = "i686" ]; then
		install -Dt "${_builddir}/arch/${KARCH}" -m644 "arch/${KARCH}/Makefile_32.cpu"
	fi

	cp -t "${_builddir}/arch/${KARCH}" -a "arch/${KARCH}/include"

	install -Dt "${_builddir}/drivers/md" -m644 drivers/md/*.h
	install -Dt "${_builddir}/net/mac80211" -m644 net/mac80211/*.h

	### http://bugs.archlinux.org/task/13146
	install -Dt "${_builddir}/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

	### http://bugs.archlinux.org/task/20402
	install -Dt "${_builddir}/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
	install -Dt "${_builddir}/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
	install -Dt "${_builddir}/drivers/media/tuners" -m644 drivers/media/tuners/*.h

	### Add xfs and shmem for aufs building
	mkdir -p "${_builddir}"/{fs/xfs,mm}

	msg2 "Installing KConfig files..."
	find . -name Kconfig\* -exec install -Dm644 {} "${_builddir}/{}" \;

	if [ "${CARCH}" = "x86_64" ]; then
		### Add objtool for external module building and enabled VALIDATION_STACK option
		install -Dt "${_builddir}/tools/objtool" tools/objtool/objtool
	fi

	### Remove unused architectures
	msg2 "Removing unneeded architectures..."
	local _arch
	for _arch in "${_builddir}"/arch/*/; do
		[[ ${_arch} == */${KARCH}/ ]] && continue
		rm -r "${_arch}"
	done

	### Remove the kernel documentations
	msg2 "Removing documentations..."
	rm -r "${_builddir}/Documentation"

	### Remove broken symlinks
	msg2 "Removing broken symlinks..."
	find -L "${_builddir}" -type l -printf 'Removing %P\n' -delete

	### Remove loose objects
	msg2 "Removing loose objects..."
	find "${_builddir}" -type f -name '*.o' -printf 'Removing %P\n' -delete

	### Strip build tools
	msg2 "Stripping build tools..."
	local _binary
	while read -rd '' _binary; do
		case "$(file -bi "${_binary}")" in
		application/x-sharedlib\;*)      # Libraries (.so)
			strip -v $STRIP_SHARED "${_binary}" ;;
		application/x-archive\;*)        # Libraries (.a)
			strip -v $STRIP_STATIC "${_binary}" ;;
		application/x-executable\;*)     # Binaries
			strip -v $STRIP_BINARIES "${_binary}" ;;
		application/x-pie-executable\;*) # Relocatable binaries
			strip -v $STRIP_SHARED "${_binary}" ;;
		*) continue ;;
		esac
	done < <(find "${_builddir}/scripts" -type f -perm -u+w -print0 2>/dev/null)

	### Symlink kernel headers to /usr/src
	msg2 "Adding symlink..."
	mkdir -p "${pkgdir}/usr/src"
	ln -sr "${_builddir}" "${pkgdir}/usr/src/$pkgbase"

	### Fix package files permissions
	msg2 "Fixing permissions..."
	chmod -Rc u=rwX,go=rX "$pkgdir"
}

