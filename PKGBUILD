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

# Tweak kernel options prior to a build via nconfig
_makenconfig=

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

# Compile ONLY used modules to VASTLY reduce the number of modules built
# and the build time.
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: https://aur.archlinux.org/packages/modprobed-db
# This PKGBUILD read the database kept if it exists
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed-db
_localmodcfg=

# Use the current kernel's .config file
#
# Enabling this option will use the .config of the RUNNING kernel rather than
# the ARCH defaults. Useful when the package gets updated and you already went
# through the trouble of customizing your config options.  NOT recommended when
# a new kernel is released, but again, convenient for package bumps.
_use_current='y'

# Unlock additional CPU optimizations for gcc
_enable_gcc_more_v='y'

# Include wireguard into the kernel
_enable_wireguard='n'

##! IMPORTANT: Do no edit below this line unless you know what you're doing

_major=5.5
_minor=8
_basekernel=${_major}
_basever=${_major/./}
_srcname=linux-${_major}
_clr=${_major}.8-917
_aufs=20200203
_gcc_more_v='20191217'

pkgbase=linux-manjaro-clear
pkgname=('linux-manjaro-clear' 'linux-manjaro-clear-headers')
_kernelname='clear'
pkgver=${_major}.${_minor}
pkgrel=1
arch=('i686' 'x86_64')
url="https://github.com/clearlinux-pkgs/linux"
_wrg_snap='0.0.20200215'
license=('GPL2')
makedepends=('bc' 'cpio' 'docbook-xsl' 'git' 'inetutils' 'kmod' 'libelf' 'xmlto')
options=('!strip')
source=(
        ### [BASE] Main release
        "https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${_major}.tar.xz"
        "https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${_major}.tar.sign"
        "https://git.zx2c4.com/wireguard-linux-compat/snapshot/wireguard-linux-compat-${_wrg_snap}.tar.xz"
        ### [END OF BASE]

        ### [PATCH-0] Minor release and stable release patches queue (disabled by default)
        "https://cdn.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
        # "prepatch-${_basekernel}.patch"
        ### [END OF PATCH-0]

        ### [PATCH-1] Patched kernel config files
        # 'config.x86_64' 'config' 'config.new'
        'config.aufs'
        ### [END OF PATCH-1]

        ### [PATCH-2] AUFS Patches
        "aufs${_major}-${_aufs}.patch"
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
        '0002-iwlwifi-pcie-restore-support-for-Killer-Qu-C0-NICs.patch'
        ##! DISABLED: This patch has been incorporated into Linux 5.5.1
        # '0003-btrfs-send-fix-emission-of-invalid-clone-operations-within-the-same-file.patch'
        ##! DISABLED: Patched by clearlinux
        # '0004-iwlwifi-mvm-Do-not-require-PHY_SKU-NVM-section-for-3168-devices.patch'
        '0006-drm-remove-PageReserved-manipulation-from-drm_pci_alloc.patch'
        '0008-drm-i915-serialise-i915_active_acquire()with__active_retire().patch'
        '0009-drm-i915-gem-take-runtime-pm-wakeref-prior-to-unbinding.patch'
        '0010-drm-i915-gem-avoid-parking-the-vma-as-we-unbind.patch'
        '0011-drm-i915-gem-try-to-flush-pending-unbind-events.patch'
        '0012-drm-i915-gem-reinitialise-the-local-list-before-repeating.patch'
        '0013-drm-i915-add-a-simple-is-bound-check-before-unbinding.patch'
        '0014-drm-i915-introduce-a-vma.kref.patch'
        ### [END OF PATCH-3]

        ### [PATCH-4] Manjaro Patches
        ### [PATCH-4.1] add patches for snapd (https://gitlab.com/apparmor/apparmor-kernel/tree/5.2-outoftree)
        '0001-apparmor-patch-to-provide-compatibility-with-v2-net-rules.patch'
        '0002-apparmor-af_unix-mediation.patch'
        '0003-apparmor-fix-use-after-free-in-sk_peer_label.patch'
        '0004-apparmor-fix-apparmor-mediating-locking-non-fs-unix-sockets.patch'
        ### [END OF PATCH-4.1]
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
        ##! No additional patches needed ATM.
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

        ### [PATCH-10] Steam fsync patches
        'futex-wait-multiple-5.2.1.patch::https://aur.archlinux.org/cgit/aur.git/plain/futex-wait-multiple-5.2.1.patch?h=linux-fsync'
        ### [END OF PATCH-10]

        )
sha256sums=('a6fbd4ee903c128367892c2393ee0d9657b6ed3ea90016d4dc6f1f6da20b2330'
            'SKIP'
            '0def6f3608ec06f6dfc454aa5281a7c38b06ff27096cb341448d20602da4e923'
            'b3f900cc7ef8aec03a9c0ab1108d4abc6105d5874965df3ada275bf76f6a5a0d'
            'b44d81446d8b53d5637287c30ae3eb64cae0078c3fbc45fcf1081dd6699818b5'
            '2f7bf415269853fb807aafe850e723321e25a8250d2eaa8fa0a890af74d05ef0'
            '9fa21f968b39c773bd81a699344d5d804bee17e02689d34a279eedfc550314c9'
            '8d13ad211226851a090f27cef8d29a80b8776e40396a880e970d3649780b7964'
            'c02a56c85f93752538caaf303d5e55f642edfaac7111defb831e74b570b95750'
            '5dad02ae9c6df0e62c1030cde906863a5b0cfb4e67cadf37463ec180706aa693'
            '902c195313a52a84a40faad9e22c41ae0816a0ac58fbb1af71c6aeebfb2b438e'
            'c9796feddec29b332602bee218e8d3e5b629523b40314eeab078f415b96d1322'
            'c95cc6bc798978e29125c49ab613959c939ab7cf505142e968025373f4ffb9d5'
            '7685d526bbdbfa795986591a70071c960ff572f56d3501774861728a9df8664c'
            'fcb9e515bf0816db05446fd8ced7468756bea3cf01b060504bace41b2e7f5f74'
            'c39011b7aef8e3f06c5a2fb4e5a0ea4ee6c452eb26518d05fbb7889a40487892'
            '9653c9310468c38fce09d5c6450965359f453c9ec64d04b8647aad3759539d06'
            '6b8c563287b694efff91a65cff7fc3924e0468e6874b62dd5ace629e96c1394b'
            '2fac1c411f5c33405226b294081107ec1d0e24c52f02651c6e674b9b34f08431'
            '1e3ad73ede2a80e1052b7e66dcc2adec7f909038c77195c3ad59ad4e8f731f6c'
            '277596368b8fe02704e5291a1ad043adad279e98216eb78d2c4f38c4a047a63b'
            '6a9de6902bc97f201a5c32768e8a68a0e8f2639d2e1cfe86d8f01bc6fda1f221'
            'dc46801624696fb8df0e9e5aed0f66e55e48dd03a5dfe6b04281ba810c79ce70'
            '98202b8ad70d02d86603294bae967874fa7b18704b5c7b867568b0fd33a08921'
            '5cbbf3db9ea3205e9b89fe3049bea6dd626181db0cb0dc461e4cf5a400c68dd6'
            'c7dbec875d0c1d6782c037a1dcefff2e5bdb5fc9dffac1beea07dd8c1bdef1d7'
            '77746aea71ffb06c685e7769b49c78e29af9b2e28209cd245e95d9cbb0dba3c9'
            '1578cab807f56aeb6e769fcc587e749522f28f38b36c60f0014b27749c8225c9'
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
            '035ea4b2a7621054f4560471f45336b981538a40172d8f17285910d4e0e0b3ef'
            'b8a9225b4b5cbabac26398d11cc26566e4407d150dacb92f3411c9bb8cc23942')

_source_use_git_apply=(
  '0013-bootsplash.patch'
)

_source_skip_auto_patch=(
  'pci-enable-overrides-for-missing-acs-capabilities.patch'
)

validpgpkeys=(
  'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
  '647F28654894E3BD457199BE38DBBDC86092693E'  # Greg Kroah-Hartman
)


export KBUILD_BUILD_HOST=$HOST
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

prepare() {
  cd "${srcdir}/linux-${_basekernel}"

  ### Add upstream patch
  patch -p1 -i "${srcdir}/patch-${pkgver}"

  ### Add the latest fixes from stable queue, if needed
  ### http://git.kernel.org/?p=linux/kernel/git/stable/stable-queue.git
  ### Enable only if you have "gen-stable-queue-patch.sh" executed before
  # patch -Np1 -i "${srcdir}/prepatch-${_basekernel}.patch"

  ### Kernel version setting
  if [ "${_kernelname}" != "" ]; then
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
      grep -Ev '^Patch0123|^Patch1001' | sed -n 's/.*: //p'); do
      echo "Applying patch ${i}..."
    patch -Np1 -i "$srcdir/linux-${_clr}/${i}"
  done

  ### Link the WireGuard source directory into the kernel tree
  if [ "${_enable_wireguard}" = "y" ]; then
    msg2 "Adding the WireGuard source directory..."
    "${srcdir}/wireguard-linux-compat-${_wrg_snap}/kernel-tree-scripts/jury-rig.sh" ./
  fi

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
  # cat "${srcdir}/config.new" > ./.config
  cat "${srcdir}/config.aufs" >> ./.config

  cp -Tf $srcdir/linux-${_clr}/config ./.config

  ### Enable extra stuff from Arch and Manjaro kernel
  msg2 "Enable extra stuff from Arch and Manjaro kernel..."

  ### General setup
  scripts/config --undefine RT_GROUP_SCHED \
              --enable GCC_PLUGIN_STRUCTLEAK_BYREF_ALL

  ### Power management and ACPI options
  scripts/config --enable ACPI_REV_OVERRIDE_POSSIBLE  \
                  --enable HIBERNATION

  ### Enable loadable module support
  scripts/config --undefine MODULE_SIG_FORCE \
                  --enable MODULE_COMPRESS \
                  --enable-after MODULE_COMPRESS MODULE_COMPRESS_LZO

  ### Networking support
  scripts/config --enable NETFILTER_INGRESS \
                  --module NET_SCH_CAKE

  ### Device Drivers
  scripts/config --enable FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER \
                  --enable DELL_SMBIOS_SMM \
                  --module PATA_JMICRON \
                  --enable SND_OSSEMUL \
                  --module-after SND_OSSEMUL SND_MIXER_OSS \
                  --module-after SND_MIXER_OSS SND_PCM_OSS \
                  --enable-after SND_PCM_OSS SND_PCM_OSS_PLUGINS

  ### Security options
  scripts/config --enable SECURITY_TOMOYO \
                  --enable SECURITY_APPARMOR \
                  --enable SECURITY_YAMA

  ### AMD and KVM stuff
  scripts/config --enable HAVE_KVM \
                --enable KVM \
                --module KVM_AMD \
                --enable DRM_AMD_DC_DCN2_0 \
                --enable AMD_IOMMU \
                --enable AMD_IOMMU_V2 \
                --module GPIO_AMD_FCH \
                --enable MICROCODE_AMD \

  ### Disable full refcount check
  ### This config will hide the warning from Nvidia proprietary drivers.
  ### Comment the line below to keep the clearlinux default config.
  # scripts/config --undefine REFCOUNT_FULL

  ### ACPI Table Upgrade
  ### Comment this if you don't need ACPI table patching capability.
  scripts/config --enable ACPI_TABLE_UPGRADE

  make olddefconfig

  ### Patch source to unlock additional gcc CPU optimizations
  ### https://github.com/graysky2/kernel_gcc_patch
  if [ "${_enable_gcc_more_v}" = "y" ]; then
    echo "Applying enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v5.5+.patch ..."
    patch -Np1 -i "$srcdir/kernel_gcc_patch-$_gcc_more_v/enable_additional_cpu_optimizations_for_gcc_v9.1+_kernel_v5.5+.patch"
  fi


  ### Enable ACS override patch
  if [ "${_enable_acs_override}" = "y" ]; then
    msg2 "Enabling ACS override patch..."
    patch -Np1 -i "${srcdir}/pci-enable-overrides-for-missing-acs-capabilities.patch"
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

  # Set patchlevel to 2
  # sed -ri "s|^(PATCHLEVEL =).*|\1 2|" Makefile

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
  depends=('coreutils' 'kmod' 'initramfs')
  optdepends=('crda: to set the correct wireless channels of your country'
                'linux-firmware: firmware images needed for some devices'
                'modprobed-db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig')
  provides=("linux-clear=${pkgver}")

  if [ "${_enable_wireguard}" = "y" ]; then
    provides+=('WIREGUARD-MODULE')
  fi

  cd "${srcdir}/linux-${_basekernel}"

  KARCH=x86

  ### Get kernel version
  _kernver="$(make LOCALVERSION= kernelrelease)"
  local _modulesdir="${pkgdir}/usr/lib/modules/${_kernver}"

  mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
  make LOCALVERSION= INSTALL_MOD_PATH="${pkgdir}/usr" modules_install

  ### Systemd expects to find the kernel here to allow hibernation
  ### https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make LOCALVERSION= -s image_name)" "${_modulesdir}/vmlinuz"

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
    [[ ${_arch} == */x86/ ]] && continue
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

  ### Fix package files permissions
  msg2 "Fixing permissions..."
  chmod -R u=rwX,go=rX "${_builddir}"

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
}
