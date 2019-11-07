# Based on the file created for Arch Linux by:
# Tobias Powalowski <tpowa@archlinux.org>
# Thomas Baechler <thomas@archlinux.org>
# This PKGBUILD is based on Manjaro Linux team work especially by:
# Maintainer: Philip Müller (x86_64) <philm@manjaro.org>
# Maintainer: Jonathon Fernyhough (i686) <jonathon@manjaro.org>
# Contributor: Helmut Stult <helmut[at]manjaro[dot]org>

# Maintainer: Rocky Prabowo <rocky@lazycats.id>

_major=5.3
_minor=8
_basekernel=${_major}
_basever=${_major/./}
_srcname=linux-${_major}
_clr=${_major}.${_minor}-859
_aufs=20190923
_gcc_more_v='20190822'
_enable_gcc_more_v='y'
_makenconfig=

pkgbase=linux-manjaro-clear
pkgname=('linux-manjaro-clear' 'linux-manjaro-clear-headers')
_kernelname=MANJARO-clear
pkgver=${_major}.${_minor}
pkgrel=4
arch=('i686' 'x86_64')
url="http://www.kernel.org/"
license=('GPL2')
makedepends=('bc' 'cpio' 'git' 'inetutils' 'kmod' 'libelf' 'xmlto')
options=('!strip')
source=("https://www.kernel.org/pub/linux/kernel/v5.x/linux-${_basekernel}.tar.xz"
        "https://www.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
        # the main kernel config files
        'config.x86_64' 'config' 'config.aufs' 'config.new'
        "${pkgbase}.preset" # standard config files for mkinitcpio ramdisk
        '60-linux.hook'     # pacman hook for depmod
        '90-linux.hook'     # pacman hook for initramfs regeneration
        "aufs5.3-${_aufs}.patch"
        'aufs5-base.patch'
        'aufs5-kbuild.patch'
        'aufs5-loopback.patch'
        'aufs5-mmap.patch'
        'aufs5-standalone.patch'
        'tmpfs-idr.patch'
        'vfs-ino.patch'
        # ARCH Patches
        '0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-CLONE_NEWUSER.patch'
        '0002-bluetooth-fix-assumptions-on-the-return-value-of-hidp_send_message.patch'
        # MANJARO Patches
        '0001-apparmor-patch-to-provide-compatibility-with-v2-net-rules.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/6408dbde30855bb9a2af44c9053ba2329db57c7f.patch'
        '0002-apparmor-af_unix-mediation.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/7a291673471aa583694ee760aa33e5a3f5ae9a9e.patch'
        '0003-apparmor-fix-use-after-free-in-sk_peer_label.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/9ae046ed7b54b01078e33227fa266282c41f981d.patch'
        '0004-apparmor-fix-apparmor-mediating-locking-non-fs-unix-sockets.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/b6a5dfbaa728854457570bf72b693a89550cc1f8.patch'
        '0001-v5-xps13-sparc64-implement-ioremap_uc.patch'
        '0002-v5-xps13-lib-devres-add-a-helper-function-for-ioremap_uc.patch'
        '0003-v5-xps13-mfd-intel-lpss-use-devm_ioremap_uc-for-MMIO.patch'
        '0004-v5-xps13-docs-driver-model-add-devm_ioremap_uc.patch'
        '0001-nonupstream-navi10-vfio-reset.patch'
        # clearlinux Patches
        "enable_additional_cpu_optimizations-$_gcc_more_v.tar.gz::https://github.com/graysky2/kernel_gcc_patch/archive/$_gcc_more_v.tar.gz"
        # "clearlinux::git+https://github.com/clearlinux-pkgs/linux.git#tag=${_clr}"
        "clearlinux-${_clr}.tar.gz::https://codeload.github.com/clearlinux-pkgs/linux/tar.gz/${_clr}"
        'add-acs-overrides.patch::https://aur.archlinux.org/cgit/aur.git/plain/add-acs-overrides.patch?h=linux-vfio'
        #"prepatch-${_basekernel}.patch"
        # My Patches
        "kernel-5.3-nvme-discard-align-to-page-size.patch"
        '0001-drm-amdgpu-Add-DC-feature-mask-to-disable-fractional-pwm.patch'
        # Bootsplash
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
sha256sums=('78f3c397513cf4ff0f96aa7d09a921d003e08fa97c09e0bb71d88211b40567b2'
            '7225bd200069c7dd4fbae5cfe1c24f4f73939ea5bd213e20ac62771bdc9e7578'
            '2cd4aed40dea452ce36e6a61dcf62d3147ff2c845ac5a56c440e83fd09d9fb8e'
            'f5903377d29fc538af98077b81982efdc091a8c628cb85566e88e1b5018f12bf'
            'b44d81446d8b53d5637287c30ae3eb64cae0078c3fbc45fcf1081dd6699818b5'
            'e2e641b2afd9310766caff0947e60cba36f2a0a349206e65a37b841bd6315c38'
            'd3ec6e33a6377714b4b92c37f358a2fe1cc3eab95c7d7211cd5ee5e19ca1c5ab'
            'ae2e95db94ef7176207c690224169594d49445e04249d2499e9d2fbc117a0b21'
            'b97c4b7ef01d90de5b5ad3359e6a36c8a2fdcb82c65e70ec8d00533a33d29f1d'
            'fb57bd74a20ca03559fcd3e5418069e9449ccc8629cc6c6812dca468c9d9f797'
            'da26a3800b23a0342b58badf72f708c5e40cf256a7dcc6851fdcab2073888ebf'
            'f6d43c68f35c5fafbb93b6ac13fe9e7fdabf7b134f8c08ebb4a7ec4b4e7d7fb3'
            '30a44c836859156b8724c92c6bcb9eaba4cf891ce13147c7bf8433b5bc29177e'
            'd73cfe15d67ff1bc77d9e9343486c3a34cbb8dc293e7ec3eb33297e171b84804'
            '3f53f56f6c883876c9ceff2af3abeb73e5a06cdfc3773b72be95c218ce9f8113'
            '55dc8df3a3d3e248eb93f5878f567428f77acb72f6243934bd6980cfede3b6ca'
            'e2d75e11a2c220e5d3a450bb226e7e19d62a871764da5f76034fbc135fe6c749'
            '7685d526bbdbfa795986591a70071c960ff572f56d3501774861728a9df8664c'
            '24259dbc5e452a7ace71308d070e96c5e3944a5c457931cfe4e0fb501ad188f0'
            '4b4146786e68af3bd49e9fabdbc92232e51cb2da179ba8037287b96d8addd17c'
            'ac2cff4d3b04dde98bafc67e1a898fa8628f3bacba08531ce473edc43ddcccff'
            '749ac28edc2cd2ac3a4406becc13327a1ece3445196ca41cbfca460454fa01bf'
            'e55e88fe22256f079f5ac7b015c2d510912cae6f48a27a0f768b8f5f6acfc11b'
            'f196cf64384cc4c35f9b82615bd62aca538653fa1e8d2ee82cd021697daa27b2'
            '62539558ec5b5f87f1740f5e4e84a3740528afb8bec6335d2de721a3c8b93531'
            '267a28e932095238604e4e23062d142fa1e2836b629190e673614159968dbec7'
            'e82c72cd391261e79ae25330848877c451b4fa60cabed9c16898983eab269c89'
            '7a2758f86dd1339f0f1801de2dbea059b55bf3648e240878b11e6d6890d3089c'
            '8c11086809864b5cef7d079f930bd40da8d0869c091965fa62e95de9a0fe13b5'
            '5f5b2b84c7ce24b40f5ea91c5e5fd4eb02a0f08613d39b040167343acc80277f'
            'dbf4ac4b873ce6972e63b78d74ddba18f2701716163bb7f4b4fe5e909346a6e1'
            'd3d5e11d78ba5652281714deb12aefe725852b18552ef710d244844a38af0373'
            '5b38d1666d51f8863117ec1d107d3f1c68a57e2b2ab44da1a7da10cbfc7f8ef3'
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

# Optionally select a sub architecture by number if building in a clean chroot
# Leaving this entry blank will require user interaction during the build
# which will cause a failure to build if using makechrootpkg. Note that the
# generic (default) option is 30.
#
# Note - the march=native option is unavailable by this method, use the nconfig
# and manually select it.
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

export KBUILD_BUILD_HOST=$HOST
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
  cd "${srcdir}/linux-${_basekernel}"

  # add upstream patch
  patch -p1 -i "${srcdir}/patch-${pkgver}"

  # add latest fixes from stable queue, if needed
  # http://git.kernel.org/?p=linux/kernel/git/stable/stable-queue.git
  # enable only if you have "gen-stable-queue-patch.sh" executed before
  #patch -Np1 -i "${srcdir}/prepatch-${_basekernel}.patch"

  # disable USER_NS for non-root users by default
  patch -Np1 -i ../0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-CLONE_NEWUSER.patch
  patch -Np1 -i ../0002-bluetooth-fix-assumptions-on-the-return-value-of-hidp_send_message.patch

  # add patches for snapd
  # https://gitlab.com/apparmor/apparmor-kernel/tree/5.2-outoftree
  patch -Np1 -i "${srcdir}/0001-apparmor-patch-to-provide-compatibility-with-v2-net-rules.patch"
  patch -Np1 -i "${srcdir}/0002-apparmor-af_unix-mediation.patch"
  patch -Np1 -i "${srcdir}/0003-apparmor-fix-use-after-free-in-sk_peer_label.patch"
  patch -Np1 -i "${srcdir}/0004-apparmor-fix-apparmor-mediating-locking-non-fs-unix-sockets.patch"

  # fix dell xps 13 2-in-1 issue
  # https://lkml.org/lkml/2019/10/16/1230
  patch -Np1 -i "${srcdir}/0001-v5-xps13-sparc64-implement-ioremap_uc.patch"
  patch -Np1 -i "${srcdir}/0002-v5-xps13-lib-devres-add-a-helper-function-for-ioremap_uc.patch"
  patch -Np1 -i "${srcdir}/0003-v5-xps13-mfd-intel-lpss-use-devm_ioremap_uc-for-MMIO.patch"
  patch -Np1 -i "${srcdir}/0004-v5-xps13-docs-driver-model-add-devm_ioremap_uc.patch"

  # https://bugzilla.kernel.org/show_bug.cgi?id=204957
  patch -Np1 -i "${srcdir}/0001-drm-amdgpu-Add-DC-feature-mask-to-disable-fractional-pwm.patch"

  # TODO: remove when AMD properly fixes it!
  # INFO: this is a hack and won't be upstreamed
  # https://forum.level1techs.com/t/145666/86
  # https://forum.manjaro.org/t/107820/11
  patch -Np1 -i "${srcdir}/0001-nonupstream-navi10-vfio-reset.patch"

  # Add bootsplash - http://lkml.iu.edu/hypermail/linux/kernel/1710.3/01542.html
  patch -Np1 -i "${srcdir}/0001-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0002-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0003-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0004-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0005-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0006-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0007-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0008-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0009-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0010-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0011-bootsplash.patch"
  patch -Np1 -i "${srcdir}/0012-bootsplash.patch"
  # use git-apply to add binary files
  git apply -p1 < "${srcdir}/0013-bootsplash.patch"

  # add aufs5 support
  patch -Np1 -i "${srcdir}/aufs5.3-${_aufs}.patch"
  patch -Np1 -i "${srcdir}/aufs5-base.patch"
  patch -Np1 -i "${srcdir}/aufs5-kbuild.patch"
  patch -Np1 -i "${srcdir}/aufs5-loopback.patch"
  patch -Np1 -i "${srcdir}/aufs5-mmap.patch"
  patch -Np1 -i "${srcdir}/aufs5-standalone.patch"
  patch -Np1 -i "${srcdir}/tmpfs-idr.patch"
  patch -Np1 -i "${srcdir}/vfs-ino.patch"

  # Custom patches, you might not need this. Comment patches that you don't need.
  # Fix for NVMe IOMMU errors when fstrim/discard is executed: https://bugzilla.kernel.org/show_bug.cgi?id=202665
  patch -Np1 -i "${srcdir}/kernel-5.3-nvme-discard-align-to-page-size.patch"

  ### Add Clearlinux patches
  for i in $(grep '^Patch' ${srcdir}/linux-${_clr}/linux.spec | grep -Ev '^Patch0123|^Patch0130|^Patch0073' | sed -n 's/.*: //p'); do
    msg2 "Applying patch ${i}..."
    patch -Np1 -i "${srcdir}/linux-${_clr}/${i}"
  done

  ### Setting config
  msg2 "Setting config..."
  # cp -Tf ${srcdir}/linux-${_clr}/config ${srcdir}/config.clear

  # if [ "${CARCH}" = "x86_64" ]; then
  #   cat "${srcdir}/config.x86_64" > ./.config
  # else
  #   cat "${srcdir}/config" > ./.config
  # fi

  # scripts/kconfig/merge_config.sh -m "${srcdir}/config.x86_64" "${srcdir}/config.clear"
  cat "${srcdir}/config.new" > ./.config
  read -p "Paused. Press any key to continue"
  cat "${srcdir}/config.aufs" >> ./.config

  if [ "${_kernelname}" != "" ]; then
    sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"-${_kernelname}\"|g" ./.config
    sed -i "s|CONFIG_LOCALVERSION_AUTO=.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
  fi


  ### Enable extra stuff from arch kernel
  msg2 "Enable extra stuff from arch kernel..."

  scripts/config --undefine MODULE_SIG_FORCE \
                  --enable DELL_SMBIOS_SMM \

  # Scheduler features
  scripts/config --undefine RT_GROUP_SCHED

  # Networking support
  scripts/config --enable NETFILTER_INGRESS \
                  --module NET_SCH_CAKE

  # Queueing/Scheduling
  scripts/config --module NET_SCH_CAKE

  # PATA SFF controllers with BMDMA
  scripts/config --module PATA_JMICRON

  # Power management and ACPI options
  scripts/config --enable ACPI_REV_OVERRIDE_POSSIBLE \
                  --enable HIBERNATION

  # Console display driver support
  scripts/config --enable FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER

  # Security options
  scripts/config --enable SECURITY_TOMOYO \
                  --enable SECURITY_APPARMOR \
                  --enable SECURITY_YAMA \

  # AMD and KVM stuff
  scripts/config --enable HAVE_KVM \
                --enable KVM \
                --enable KVM_AMD \
                --enable DRM_AMD_DC_DCN2_0 \
                --enable AMD_IOMMU \
                --enable AMD_IOMMU_V2 \
                --module GPIO_AMD_FCH \
                --module NTB_AMD \
                --enable MICROCODE_AMD \

  # Disable full refcount check
  # This will hide the warning from Nvidia proprietary drivers.
  # Comment the line below to keep the clearlinux default config.
  scripts/config --undefine REFCOUNT_FULL

  # ACPI Table Upgrade
  # Comment this if you don't need DSDT patching capability.
  scripts/config --enable ACPI_TABLE_UPGRADE

  make olddefconfig

  ### Patch source to unlock additional gcc CPU optimizations
  # https://github.com/graysky2/kernel_gcc_patch
  if [ "${_enable_gcc_more_v}" = "y" ]; then
    msg2 "Applying enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v4.13+.patch ..."
    patch -Np1 -i "${srcdir}/kernel_gcc_patch-$_gcc_more_v/enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v4.13+.patch"
  fi

  ### Enable ACS override patch
  if [ "${_enable_acs_override}" = "y" ]; then
    msg2 "Enabling ACS override patch..."
    patch -Np1 -i "${srcdir}/add-acs-overrides.patch"
  fi

  ### Get kernel version
  if [ "${_enable_gcc_more_v}" = "y" ] || [ -n "${_subarch}" ]; then
    yes "$_subarch" | make oldconfig
  # else
  #   make prepare
  fi

  ### Optionally load needed modules for the make localmodconfig
  # See https://aur.archlinux.org/packages/modprobed-db
  if [ -n "$_localmodcfg" ]; then
    if [ -f $HOME/.config/modprobed.db ]; then
      msg2 "Running Steven Rostedt's make localmodconfig now"
      make LSMOD=$HOME/.config/modprobed.db localmodconfig
    else
      msg2 "No modprobed.db data found"
      exit
    fi
  fi

  ### Prepared version
  make -s kernelrelease > version
  msg2 "Prepared %s version %s" "$pkgbase" "$(<version)"

  ### do not run `make olddefconfig` as it sets default options
  # yes "" | make config >/dev/null

  # set patchlevel to 2
  # sed -ri "s|^(PATCHLEVEL =).*|\1 2|" Makefile

  # set extraversion to pkgrel
  sed -ri "s|^(EXTRAVERSION =).*|\1 -${_kernelname}-${pkgrel}|" Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh

  [[ -z "$_makenconfig" ]] || make nconfig

  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  #make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config

  # rewrite configuration
  yes "" | make config >/dev/null

  ### Save configuration for later reuse
  cp -Tf ./.config "${startdir}/config-${pkgver}-${pkgrel}-${_kernelname}"
}

build() {
  cd "${srcdir}/linux-${_basekernel}"

  # build!
  make ${MAKEFLAGS} LOCALVERSION= bzImage modules
}

package_linux-manjaro-clear() {
  pkgdesc="The ${pkgbase/linux/Linux} kernel and modules"
  depends=('coreutils' 'linux-firmware' 'kmod' 'mkinitcpio>=0.7')
  optdepends=('crda: to set the correct wireless channels of your country')
  provides=("linux-clear=${pkgver}")
  backup=("etc/mkinitcpio.d/${pkgbase}.preset")
  install=${pkgname}.install

  cd "${srcdir}/linux-${_basekernel}"

  KARCH=x86

  # get kernel version
  _kernver="$(make LOCALVERSION= kernelrelease)"

  mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
  make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}/usr" modules_install
  # cp arch/$KARCH/boot/bzImage "${pkgdir}/boot/vmlinuz-${_basekernel}-${CARCH}"
  cp arch/$KARCH/boot/bzImage "${pkgdir}/boot/vmlinuz-${_basekernel}-${_kernelname}-${CARCH}"

  # add kernel version
  if [ "${CARCH}" = "x86_64" ]; then
     echo "${pkgver}-${pkgrel}-${_kernelname} x64" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  else
     echo "${pkgver}-${pkgrel}-${_kernelname} x32" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  fi

  # make room for external modules
  local _extramodules="extramodules-${_basekernel}-${_kernelname:--MANJARO}"
  ln -s "../${_extramodules}" "${pkgdir}/usr/lib/modules/${_kernver}/extramodules"

  # add real version for building modules and running depmod from hook
  echo "${_kernver}" |
    install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules/${_extramodules}/version"

  # remove build and source links
  rm "${pkgdir}"/usr/lib/modules/${_kernver}/{source,build}

  # now we call depmod...
  depmod -b "${pkgdir}/usr" -F System.map "${_kernver}"

  # add vmlinux
  install -Dt "${pkgdir}/usr/lib/modules/${_kernver}/build" -m644 vmlinux

  # sed expression for following substitutions
  local _subst="
    s|%PKGBASE%|${pkgbase}|g
    s|%BASEKERNEL%|${_basekernel}|g
    s|%KERNELNAME%|${_kernelname}|g
    s|%ARCH%|${CARCH}|g
    s|%KERNVER%|${_kernver}|g
    s|%EXTRAMODULES%|${_extramodules}|g
  "

  # hack to allow specifying an initially nonexisting install file
  sed "${_subst}" "${startdir}/${install}" > "${startdir}/${install}.pkg"
  true && install=${install}.pkg

  # install mkinitcpio preset file
  sed "${_subst}" ${srcdir}/${pkgbase}.preset |
    install -Dm644 /dev/stdin "${pkgdir}/etc/mkinitcpio.d/${pkgbase}.preset"

  # install pacman hooks
  sed "${_subst}" ${srcdir}/60-linux.hook |
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/60-${pkgbase}.hook"
  sed "${_subst}" ${srcdir}/90-linux.hook |
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/90-${pkgbase}.hook"
}

package_linux-manjaro-clear-headers() {
  pkgdesc="Header files and scripts for building modules for ${pkgbase/linux/Linux} kernel"
  provides=("linux-clear-headers=$pkgver")

  cd "${srcdir}/linux-${_basekernel}"
  local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"

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

  # http://bugs.archlinux.org/task/13146
  install -Dt "${_builddir}/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # http://bugs.archlinux.org/task/20402
  install -Dt "${_builddir}/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "${_builddir}/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "${_builddir}/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  # add xfs and shmem for aufs building
  mkdir -p "${_builddir}"/{fs/xfs,mm}

  # copy in Kconfig files
  find . -name Kconfig\* -exec install -Dm644 {} "${_builddir}/{}" \;

  if [ "${CARCH}" = "x86_64" ]; then
    # add objtool for external module building and enabled VALIDATION_STACK option
    install -Dt "${_builddir}/tools/objtool" tools/objtool/objtool
  fi

  # remove unneeded architectures
  local _arch
  for _arch in "${_builddir}"/arch/*/; do
    [[ ${_arch} == */x86/ ]] && continue
    rm -r "${_arch}"
  done

  # remove files already in linux-docs package
  rm -r "${_builddir}/Documentation"

  # Fix permissions
  chmod -R u=rwX,go=rX "${_builddir}"

  # strip scripts directory
  local _binary _strip
  while read -rd '' _binary; do
    case "$(file -bi "${_binary}")" in
      *application/x-sharedlib*)  _strip="${STRIP_SHARED}"   ;; # Libraries (.so)
      *application/x-archive*)    _strip="${STRIP_STATIC}"   ;; # Libraries (.a)
      *application/x-executable*) _strip="${STRIP_BINARIES}" ;; # Binaries
      *) continue ;;
    esac
    /usr/bin/strip ${_strip} "${_binary}"
  done < <(find "${_builddir}/scripts" -type f -perm -u+w -print0 2>/dev/null)
}
