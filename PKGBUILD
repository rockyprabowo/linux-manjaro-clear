# Based on the file created for Arch Linux by:
# Tobias Powalowski <tpowa@archlinux.org>
# Thomas Baechler <thomas@archlinux.org>
# This PKGBUILD is based on Manjaro Linux team work especially by:
# Maintainer: Philip Müller (x86_64) <philm@manjaro.org>
# Maintainer: Jonathon Fernyhough (i686) <jonathon@manjaro.org>
# Contributor: Helmut Stult <helmut[at]manjaro[dot]org>

# Maintainer: Rocky Prabowo <rocky@lazycats.id>

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

_major=5.3
_minor=10
_basekernel=${_major}
_basever=${_major/./}
_srcname=linux-${_major}
#_clr=${_major}.${_minor}-859
_clr=5.3.9-863
_aufs=20190923
_gcc_more_v='20190822'
_enable_gcc_more_v='y'
_makenconfig=

pkgbase=linux-manjaro-clear
pkgname=('linux-manjaro-clear' 'linux-manjaro-clear-headers')
_kernelname='clear'
pkgver=${_major}.${_minor}
pkgrel=1
arch=('i686' 'x86_64')
url="http://www.kernel.org/"
license=('GPL2')
makedepends=('bc' 'cpio' 'docbook-xsl' 'git' 'inetutils' 'kmod' 'libelf' 'xmlto')
options=('!strip')
source=(
        # [BASE] Main release
        "https://www.kernel.org/pub/linux/kernel/v5.x/linux-${_basekernel}.tar.xz"
        # [END OF BASE]
        # [PATCH-0] Minor release and stable release queue (disabled by default)
        "https://www.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
        #"prepatch-${_basekernel}.patch"
        # [END OF PATCH-0]

        # [PATCH-1] Patched kernel config files
        'config.x86_64' 'config' 'config.aufs' 'config.new'
        # [END OF PATCH-1]

        # [PATCH-2] AUFS Patches
        "aufs5.3-${_aufs}.patch"
        'aufs5-base.patch'
        'aufs5-kbuild.patch'
        'aufs5-loopback.patch'
        'aufs5-mmap.patch'
        'aufs5-standalone.patch'
        'tmpfs-idr.patch'
        'vfs-ino.patch'
        # [END OF PATCH-2]

        # [PATCH-3] Arch Linux Patches
        '0001-ZEN-Add-sysctl-and-CONFIG-to-disallow-unprivileged-CLONE_NEWUSER.patch' # disable USER_NS for non-root users by default
        '0002-bluetooth-fix-assumptions-on-the-return-value-of-hidp_send_message.patch'
        # [END OF PATCH-3]

        # [PATCH-4] Manjaro Patches

        # [PATCH-4.1] add patches for snapd (https://gitlab.com/apparmor/apparmor-kernel/tree/5.2-outoftree)
        '0001-apparmor-patch-to-provide-compatibility-with-v2-net-rules.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/6408dbde30855bb9a2af44c9053ba2329db57c7f.patch'
        '0002-apparmor-af_unix-mediation.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/7a291673471aa583694ee760aa33e5a3f5ae9a9e.patch'
        '0003-apparmor-fix-use-after-free-in-sk_peer_label.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/9ae046ed7b54b01078e33227fa266282c41f981d.patch'
        '0004-apparmor-fix-apparmor-mediating-locking-non-fs-unix-sockets.patch::https://gitlab.com/apparmor/apparmor-kernel/commit/b6a5dfbaa728854457570bf72b693a89550cc1f8.patch'
        # [END OF PATCH-4.1]

        # [PATCH-4.2] fix dell xps 13 2-in-1 issue (https://lkml.org/lkml/2019/10/16/1230)
        '0001-v5-xps13-sparc64-implement-ioremap_uc.patch'
        '0002-v5-xps13-lib-devres-add-a-helper-function-for-ioremap_uc.patch'
        '0003-v5-xps13-mfd-intel-lpss-use-devm_ioremap_uc-for-MMIO.patch'
        '0004-v5-xps13-docs-driver-model-add-devm_ioremap_uc.patch'
        # [END OF PATCH-4.2]

        # [PATCH-4.3] TODO: remove when AMD properly fixes it! INFO: this is a hack and won't be upstreamed (https://forum.level1techs.com/t/145666/86 https://forum.manjaro.org/t/107820/11)
        '0001-nonupstream-navi10-vfio-reset.patch'
        # [END OF PATCH-4.3]

        # [PATCH-4.4] https://bugzilla.kernel.org/show_bug.cgi?id=204957
        '0001-drm-amdgpu-Add-DC-feature-mask-to-disable-fractional-pwm.patch'
        # [END OF PATCH-4.4]

        # [END OF PATCH-4]

        # [PATCH-5] clearlinux Patches
        # "clearlinux::git+https://github.com/clearlinux-pkgs/linux.git#tag=${_clr}"
        "clearlinux-${_clr}.tar.gz::https://codeload.github.com/clearlinux-pkgs/linux/tar.gz/${_clr}"
        # [END OF PATCH-5]

        # [PATCH-6] Patch source to unlock additional gcc CPU optimizations
        "enable_additional_cpu_optimizations-$_gcc_more_v.tar.gz::https://github.com/graysky2/kernel_gcc_patch/archive/$_gcc_more_v.tar.gz"
        # [END OF PATCH-6]

        # [PATCH-7] ACS Override patch
        'add-acs-overrides.patch::https://aur.archlinux.org/cgit/aur.git/plain/add-acs-overrides.patch?h=linux-vfio'
        # [END OF PATCH-7]

        # [PATCH-8] Personal custom patches, you might not need this. Comment any patch that you don't need.

        # [PATCH-8.1] Fix for NVMe IOMMU errors during fstrim/discard: https://bugzilla.kernel.org/show_bug.cgi?id=202665
        'kernel-5.3-nvme-discard-align-to-page-size.patch'
        # [END OF PATCH-8.1]

        # [END OF PATCH-8]

        # [PATCH-9] Bootsplash: Add bootsplash - http://lkml.iu.edu/hypermail/linux/kernel/1710.3/01542.html
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
        # [END OF PATCH-9]

        )
sha256sums=('78f3c397513cf4ff0f96aa7d09a921d003e08fa97c09e0bb71d88211b40567b2'
            '4c0304c4ac05105881c7f50463a1485a71c0a5899830f07eac0321f32ae4eb4a'
            '41f6c4f0445ec055db9d441d2856675e7d2f32bdf2ed8fed407f69b45bbad22b'
            'f5903377d29fc538af98077b81982efdc091a8c628cb85566e88e1b5018f12bf'
            'b44d81446d8b53d5637287c30ae3eb64cae0078c3fbc45fcf1081dd6699818b5'
            'd7935017b09f20fc57b079a449da8c50d0e01fcb6c312ce479481c6d905b9b8e'
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
            '5b38d1666d51f8863117ec1d107d3f1c68a57e2b2ab44da1a7da10cbfc7f8ef3'
            '07466e74fc3280e8a1f7a1c81861c9a4a745367bfb8fe0befd15e7cb9b02af6d'
            '8c11086809864b5cef7d079f930bd40da8d0869c091965fa62e95de9a0fe13b5'
            'dbf4ac4b873ce6972e63b78d74ddba18f2701716163bb7f4b4fe5e909346a6e1'
            'd3d5e11d78ba5652281714deb12aefe725852b18552ef710d244844a38af0373'
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
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue

    # Binary patching, needed for 0013-bootsplash.patch on PATCH-9
    if [[ $src = 0013-bootsplash.patch ]]; then
      # use git-apply to add binary files
      git apply -p1 < "${srcdir}/0013-bootsplash.patch"
      continue
    fi

    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  ### Add Clearlinux patches
  for i in $(grep '^Patch' ${srcdir}/linux-${_clr}/linux.spec | grep -Ev '^Patch0123|^Patch0130|^Patch0073' | sed -n 's/.*: //p'); do
    msg2 "Applying patch ${i}..."
    patch -Np1 -i "${srcdir}/linux-${_clr}/${i}"
  done

  ### Setting config
  msg2 "Setting config..."
  cat "${srcdir}/config.new" > ./.config
  cat "${srcdir}/config.aufs" >> ./.config

  ### Enable extra stuff from Arch and Manjaro kernel
  msg2 "Enable extra stuff from Arch and Manjaro kernel..."

  # General setup
  scripts/config --undefine RT_GROUP_SCHED \
              --enable GCC_PLUGIN_STRUCTLEAK_BYREF_ALL

  # Power management and ACPI options
  scripts/config --enable ACPI_REV_OVERRIDE_POSSIBLE  \
                  --enable HIBERNATION

  # Enable loadable module support
  scripts/config --undefine MODULE_SIG_FORCE \
                  --enable MODULE_COMPRESS \
                  --enable-after MODULE_COMPRESS MODULE_COMPRESS_LZO

  # Networking support
  scripts/config --enable NETFILTER_INGRESS \
                  --module NET_SCH_CAKE

  # Device Drivers
  scripts/config --enable FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER \
                  --enable DELL_SMBIOS_SMM \
                  --module PATA_JMICRON \
                  --enable SND_OSSEMUL \
                  --module-after SND_OSSEMUL SND_MIXER_OSS \
                  --module-after SND_MIXER_OSS SND_PCM_OSS \
                  --enable-after SND_PCM_OSS SND_PCM_OSS_PLUGINS

  # Security options
  scripts/config --enable SECURITY_TOMOYO \
                  --enable SECURITY_APPARMOR \
                  --enable SECURITY_YAMA

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

  scripts/config --disable LOCALVERSION_AUTO

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
  else
    make prepare
  fi

  if [ "${_kernelname}" != "" ]; then
    # sed -i "s|CONFIG_LOCALVERSION=.*|CONFIG_LOCALVERSION=\"-${_kernelname}\"|g" ./.config
    # sed -ri "s|(\#\s)?CONFIG_LOCALVERSION_AUTO.*|CONFIG_LOCALVERSION_AUTO=n|" ./.config
      msg2 "Setting version..."
      scripts/setlocalversion --save-scmversion
      echo "-$pkgrel" > localversion.10-pkgrel
      echo "-${_kernelname}" > localversion.20-pkgname
  fi

  # set extraversion to pkgrel
  # sed -ri "s|^(EXTRAVERSION =).*|\1 -${pkgrel}|" Makefile

  ### Prepared version
  make -s kernelrelease > version
  msg2 "Prepared %s version %s" "$pkgbase" "$(<version)"

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

  # set patchlevel to 2
  # sed -ri "s|^(PATCHLEVEL =).*|\1 2|" Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh

  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  #make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config

  # rewrite configuration
  yes "" | make config >/dev/null

  ### Running make nconfig
  [[ -z "$_makenconfig" ]] || make nconfig

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
  depends=('coreutils' 'linux-firmware' 'kmod' 'mkinitcpio>=27')
  optdepends=('crda: to set the correct wireless channels of your country')
  provides=("linux-clear=${pkgver}")

  cd "${srcdir}/linux-${_basekernel}"

  KARCH=x86

  # get kernel version
  _kernver="$(make LOCALVERSION= kernelrelease)"
  local _modulesdir="${pkgdir}/usr/lib/modules/${_kernver}"

  mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
  make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}/usr" modules_install

  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make -s image_name)" "${_modulesdir}/vmlinuz"

  # Used by mkinitcpio to name the kernel
  echo "${pkgbase}" | install -Dm644 /dev/stdin "${_modulesdir}/pkgbase"
  echo "${_basekernel}-${_kernelname}-${CARCH}" | install -Dm644 /dev/stdin "${_modulesdir}/kernelbase"

  # add kernel version
  if [ "${CARCH}" = "x86_64" ]; then
     echo "${pkgver}-${pkgrel}-${_kernelname} x64" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  else
     echo "${pkgver}-${pkgrel}-${_kernelname} x32" > "${pkgdir}/boot/${pkgbase}-${CARCH}.kver"
  fi

  # make room for external modules
  local _extramodules="extramodules-${_basekernel}-${_kernelname:--MANJARO}"
  ln -s "../${_extramodules}" "${_modulesdir}/extramodules"

  # add real version for building modules and running depmod from hook
  echo "${_kernver}" |
    install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules/${_extramodules}/version"

  # remove build and source links
  rm ${_modulesdir}/{source,build}

  # now we call depmod...
  depmod -b "${pkgdir}/usr" -F System.map "${_kernver}"

  # add vmlinux
  install -Dt "${_modulesdir}/build" -m644 vmlinux
}

package_linux-manjaro-clear-headers() {
  pkgdesc="Header files and scripts for building modules for ${pkgbase/linux/Linux} kernel"
  provides=("linux-clear-headers=$pkgver")

  cd "${srcdir}/linux-${_basekernel}"
  local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"
  msg2 "Installing headers and build files..."

  install -Dt "${_builddir}" -m644 Makefile .config Module.symvers System.map \
    localversion.* version vmlinux
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

  msg2 "Installing KConfig files..."
  find . -name Kconfig\* -exec install -Dm644 {} "${_builddir}/{}" \;

  if [ "${CARCH}" = "x86_64" ]; then
    # add objtool for external module building and enabled VALIDATION_STACK option
    install -Dt "${_builddir}/tools/objtool" tools/objtool/objtool
  fi

  msg2 "Removing unneeded architectures..."
  local _arch
  for _arch in "${_builddir}"/arch/*/; do
    [[ ${_arch} == */x86/ ]] && continue
    rm -r "${_arch}"
  done

  msg2 "Removing documentation..."
  rm -r "${_builddir}/Documentation"

  msg2 "Removing broken symlinks..."
  find -L "${_builddir}" -type l -printf 'Removing %P\n' -delete

  msg2 "Removing loose objects..."
  find "${_builddir}" -type f -name '*.o' -printf 'Removing %P\n' -delete

  msg2 "Fixing permissions..."
  chmod -R u=rwX,go=rX "${_builddir}"

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

  msg2 "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "${_builddir}" "$pkgdir/usr/src/$pkgbase"
}
