# Maintainer: Gyöngyösi Gábor <gabor at gshoots dot hu>
# Contributor: Philip Müller <philm[at]manjaro[dot]org>
# Contributor: Thomas Baechler <thomas@archlinux.org>
# Contributor: Jerry Xiao <aur@mail.jerryxiao.cc>
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>

pkgbase=nvidia-340xx-utils
pkgname=('nvidia-340xx-utils' 'opencl-nvidia-340xx' 'nvidia-340xx-dkms' 'mhwd-nvidia-340xx')
pkgver=340.108
pkgrel=4
arch=('x86_64')
url="https://www.nvidia.com/"
license=('custom')
options=('!strip')
_pkg="NVIDIA-Linux-x86_64-${pkgver}-no-compat32"

source=(
    "https://us.download.nvidia.com/XFree86/Linux-x86_64/${pkgver}/${_pkg}.run"
    "mhwd-nvidia"
    "nvidia-340xx-utils.install"
    "nvidia-utils.sysusers"
    "nvidia-340xx.rules"
    "10-nvidia.conf.in"
    "10-nvidia-modules.conf.in"
    "nvidia-340xx-lib-switch"
    "nvidia-340xx-lib-switch.service"
    "nv-gnu17-fms-extensions-1.patch"
    "nv-drm-fop-flags.patch"
    "nv-no-per-vma-lock-on-x86.patch"
    "nv-screen-info.patch"
    "nv-vma-lock-offset.patch"
    "nv-is-vma-write-locked-args.patch"
    "nv-gnu17-fms-extensions-2.patch"
    # Sorozat patchek: 0001-0075 (a series.in sorrendje szerint)
    "0001-bashisms.patch"
    "0002-backport-error-on-unknown-conftests.patch"
    "0003-unregister-procfs-on-failure.patch"
    "0004-kmem-cache-create-usercopy.patch"
    "0005-buildfix-kernel-4.11.patch"
    "0006-buildfix-kernel-5.2.patch"
    "0007-fix-build-for-kernel-5.5.patch"
    "0008-backport-drm-available-361.16.patch"
    "0009-backport-drm-driver-legacy-dev-list.patch"
    "0010-backport-drm-gem-object-get-418.30.patch"
    "0011-backport-nv-ioremap-nocache-440.64.patch"
    "0012-backport-nv-proc-ops-t-440.82.patch"
    "0013-backport-nv-timeval-440.82.patch"
    "0014-backport-drm-legacy-pci-init.patch"
    "0015-backport-asm-pgtable-types-390.138.patch"
    "0016-backport-linux-ioctl32-450.51.patch"
    "0017-backport-nv-vmalloc-450.57.patch"
    "0018-work-around-mmap-sem-lock-rename.patch"
    "0019-backport-get-user-pages-remote-455.23.0.patch"
    "0020-backport-vga-tryget-455.23.04.patch"
    "0021-backport-drm-driver-gem-free-object.patch"
    "0022-backport-drm-prime-pages-to-sg-device-arg.patch"
    "0023-check-for-drm-pci-init.patch"
    "0024-import-drm-legacy-pci-init-exit-5.9.1.patch"
    "0025-add-static-nv-prefix-to-drm-legacy-bits.patch"
    "0026-backport-asm-kmap-types-460.32.03.patch"
    "0027-backport-drm-driver-gem-prime-callbacks.patch"
    "0028-skip-list-operations-legacy-dev-list.patch"
    "0029-backport-set-current-state-470.63.01.patch"
    "0030-backport-drm-device-has-pdev-470.63.01.patch"
    "0031-check-member-agp-in-struct-drm-device.patch"
    "0032-backport-stdarg-470.82.00.patch"
    "0033-backport-pde-data-470.103.01.patch"
    "0034-backport-pci-dma-470.129.06.patch"
    "0035-backport-acpi-bus-get-device-470.129.06.patch"
    "0036-backport-acpi-390.157.patch"
    "0037-backport-acpi-op-remove-470.182.03.patch"
    "0038-backport-vm-area-struct-const-vm-flags.patch"
    "0039-backport-get-user-pages-418.30.patch"
    "0040-backport-get-user-pages-520.56.06.patch"
    "0041-backport-get-user-pages-525.53.patch"
    "0042-backport-get-user-pages-535.86.05.patch"
    "0043-backport-asm-page-470.223.02.patch"
    "0044-backport-drm-gem-prime-handle-to-fd.patch"
    "0045-refuse-load-legacy-module-if-ibt-enabled.patch"
    "0046-backport-nv-get-kern-phys-address-555.4.patch"
    "0047-build-without-wsign-compare.patch"
    "0048-backport-cmd-symlink-550.142.patch"
    "0049-fix-more-warnings.patch"
    "0050-backport-build-cflags-525.85.05.patch"
    "0051-backport-conftest-comment-515.48.07.patch"
    "0052-backport-conftest-comment-525.53.patch"
    "0053-backport-conftest-comment-545.23.06.patch"
    "0054-backport-drm-driver-has-date-570.124.04.patch"
    "0055-backport-ccflags-y-570.153.02.patch"
    "0056-backport-nv-timer-delete-sync-570.153.0.patch"
    "0057-backport-nv-vma-start-write-570.169.patch"
    "0058-disable-objtool-usage.patch"
    "0059-backport-drm-print-570.211.01.patch"
    "0060-backport-nv-in-hardirq-580.119.02.patch"
    "0061-backport-vma-flags-set-word-580.126.09.patch"
    "0062-separate-makefile-kbuild.patch"
    "0063-kernel-uname.patch"
    "0064-use-kbuild-compiler.patch"
    "0065-use-kbuild-flags.patch"
    "0066-build-sanity-checks.patch"
    "0067-conftest-verbose.patch"
    "0068-conftest-via-kbuild.patch"
    "0069-not-silent.patch"
    "0070-disable-cc-version-check.patch"
    "0071-avoid-ld-gold.patch"
    "0072-conftest-include-guard.patch"
    "0073-ignore-xen-on-arm.patch"
    "0074-arm-outer-sync.patch"
    "0075-armhf-on-arm64-kernel.patch"
    # Tools scriptek
    "get_configured340.sh"
    "get_defined340.sh"
    "split_conftest340.sh"
    "collect_tests340.sh"
    # Kiegészítő források
    "https://download.nvidia.com/XFree86/nvidia-settings/nvidia-settings-${pkgver}.tar.bz2"
    "https://download.nvidia.com/XFree86/nvidia-xconfig/nvidia-xconfig-${pkgver}.tar.bz2"
    "https://download.nvidia.com/XFree86/nvidia-modprobe/nvidia-modprobe-${pkgver}.tar.bz2"
)

sha256sums=('995d44fef587ff5284497a47a95d71adbee0c13020d615e940ac928f180f5b77'
            '9513f636c27d6ac06a3dd41f7761d2cf4fe8f1c91bb177fce3f333dd2b072713'
            '5bd726ef9e28ea0f62013eb63b9cf00fb2de01fbb07d6f8427a82d3d22b4fc79'
            'd8d1caa5d72c71c6430c2a0d9ce1a674787e9272ccce28b9d5898ca24e60a167'
            '19b61cce21c440bf86bde883ce8384dc1032ff30ca6785f03a02cfa0de425fbf'
            '9225323fe0ed6d2e4c46d5b3287810d6cc82cc771b20bdf929fed352905c6baf'
            'ce536db11dcd4a28a6de914e5f4d07f431051296aeda257d6ab8722e0fe6940d'
            '9922eae6a32dff82eb0390087d2129f399b4c4d0263f70db9044531c58b7c151'
            '95cf1c5c674e7fdba6be6b708f3835d8e9e947f5de241a0a38fd3296a03342d7'
            'b7b252ef8bc831562d4e7b3b25b6e4d835e64648a06cafab876309607751c360'
            '37a4353f35fcacabadc8d0f409df6e73aec3ee5e76a2d4f731ff3ccfec7dacc2'
            '4e93b2b952c6aff19f4f41118230348213099122d35f7141fe4bd6233b226a19'
            '4f26432b5f143bb66117609bd9dbd3e73928c30bacc680c383907639266f59fd'
            '4d28c74b0ce7185bb7c701aff8e8e1ab27a704f80a5ec0823a1ddb35a58d6d73'
            '7e36067badf65a46b36cf0f741f3cc2f7123c13111286cb247a6e851aeedba9d'
            '2c49b0379b5081bf06ea79d20bf33a66bdbdbc447bbfc82752c4c3705dd22f2c'
            '53db3bbf450dbacc6257194002535c5f8a6e6359d4c4fde5ec29603b2e085eb5'
            '36b5094922db3c925aa370ecc6fbd2d36980ff7147f64fadf81ac401503f5f1d'
            'c981dc01af43d9849d332596fb2cf20725c25d52843309348967d6a691b84318'
            '5e5280a5425e6f93efdacb2c51757799caf3ee62a5539de0dbaa79858f5171ac'
            'c7ed049ff0e594c8a7624474a34e8126ba60e36f1276a6c86c108b993d798350'
            'e40155ff823709d4d1914126a30bb0c900a5bb4d06cdc4e493da19d51325a8f2'
            'a052691c7546a1c8a2560a4008c4299ed5a61aab13d665b0502c6e8c0ab43c4e'
            '05d24dfd238cec1fd56dd48c974dedba61ea799196c732ad79a149e8981c5e4d'
            '32c03d606e6fab66d793f14b0079738e4e0e49a15da9202c5c36cf5dd09f209f'
            '97eff24adfbe52e84cd4654166055e6428730ed1c7fc92f23464b804d704e9d2'
            '86046d3172db427393f7ce239156d81cf200c9538d7216a8417d65347d8b1df0'
            '38072af5bf86a5eb02c6442708d44ea9a1c08cd54f3aaad7c3c8ae1d305bdfd7'
            'a666526244461d7aa1d70e848e9a48abfeafb7a4276815e009d4526004357b7d'
            'f3aa16f33ec5dbc06cc4cfd4a7061f34b72eaefb9371de5c5262b8f5fc6c696a'
            '8a41ca402f1f63091068fa30b9d6bc94b409b8301371e0d15e7d919eac76c508'
            '6f750552b854712a010e80e4e7a13a3fcc3a6eee0936a5fb033a6e608ca18b64'
            '6cddbf41336ec3623765751c9c55de293c097ec7bc4d3ade8e8212ba839a0489'
            'ff56050a3af591e87544641d362db32697274fcc273e119de1c588552528c5e0'
            'e6214b451bbda0aceec67eba014007b03a17743c58673988ec3cbf65637fc066'
            '3f3fbdddc245f27d21cef11501a9a24f211375f5b239f2c62c4f986584a8ae48'
            'ef8e0cc932aa1ee54ab6cf4d3658487cc633393e762a890427e1b871fafbefae'
            '881a9e649e9d74fe9ea3d62aa465c007bb4ced23f7bf06e1b29551fc2ee9345d'
            '8d175bab568463e2e75aaeddbbc01a8b556cf1731cffe24355b2334193bce8ec'
            '2d26f6c3f3ba3b8ef7cb768e50c775aef33c082a38d4a1a230aa1a4205ea5984'
            '397dcfa0c9ff9339916204d59c3441da7177cc47a9037e6168c4829324391025'
            '374838fc5197c0bbb1c448a5965dc106b182d970c329568a9d1c9b220e6efcb6'
            'ed16aacb499493d53b1f62d995cf6a25aef21bb0ee451188ae08fc595f9f2383'
            'e4fa7e850a76811212b0044bd899d69a8f8471f16887bb7c4cac502bd0572872'
            'de1aa4e6d3c387d3c5f20ee9ace2ea8ca15d8fdf50bf33d7e664f73f504ecce7'
            '3c162f7bfd38f8e772703b6eaf975eb969c1df4b3ce5147e762914ca9eef9356'
            'df6e105030db178fd2e68d76bcba74edff92fb92fb3c0e695d46afaffda3a6bb'
            '1dcee21fa0391f735e176aa268ade7942d5474878098ee1ade81f62fef3d2c37'
            '72aba65dbdd7309d9139da4f74a727cf078dc4aeba9bbe05e8fa98638dc83bce'
            '89461e5dc40205e520653845d7a06e4acf86ac2fdb2bd2361f0694bfe90f3c18'
            '326593b6f853a7b201fa39afa020d476d34adda99d89e5a01c3813da93d91d60'
            '2049d9104fb5e9165b56634d81f9dbf9e6ba0829d793abd75879d092fb79ddf2'
            '14da3aa5a8d87f0bc763ad94da8506413894863e5519974634d16d86b995c47a'
            'a89d1f02c5d6f153fc1bf5f9a6e361ec7740a745135df2f6dbad8ebd03eb233c'
            'b51abc1699ed55b2d98fcf98797f2d02601b417053b33cba4cc366b6b969b399'
            'ca2d1860af489791a40db17aff996ee77c193ba76894ff5b6a9604321ef976d9'
            '15f27a296bedda4e029a445941e766f3eee1119f2e6975234885b627d730743d'
            'ae4e805d42a228cf371a5d06ff32226d4bde5da78d8502d6331739a851ecde40'
            '62711c3208d4a9f88579ef340421722f1e184ef6c691ef50914fead1a5ffd41d'
            '72e9e7dfce14b0c3a356e80f622aeef9a7a07dfd8d839c58975b2aa377826c8e'
            'fa165f694ce8eb33ba2ed516228aba3568910d2e3183dbb6664103bd122e075e'
            'f2cd6b6f0e31320b73f8dea32df57b3001a0cadb0447b650677436ab6694d5fb'
            '0de4fdc8864e61488be6837ed9801b9fbbb05136a2e0213fdcfc9815f1d3e463'
            'ff8275c06f5e04ed094bef34ed8ce85d547c96294b3187bc9a7308faa339626d'
            '58f83d92a0bf65c281b4d413427534f98b4e43005d1cfc07c1a4ca508eab43ec'
            'd6ae0267f125927ec3fce2a7a749ec2c0c9d17ef0946a085912e9df9695c4f2c'
            'd66a8914e8d2ec500b748321c2d76bc5387dde9a89f8047fab3ce0371d1488aa'
            '4213eeb3bd0319d8ddb3d854ef0d4e973a7d826684b60cc57660e229cb9cbb6b'
            '7a2208146ad8c434724c490f782fc1737b0efcd0d01807b05da24eeed0f2606c'
            'e50b2d02b6955ba6dac57d48e239eb520deb00aaf03962813f61f5945a3950dd'
            'a2fd203800d2cac8374c2a522b58fc78174c99af1b6ecff73973085800586d33'
            'a9c4ee59cb27929d56b6b07b6440b5f31a7e7b5ef5447ae438f44065a13ad205'
            '95d06b6420db0935839627a9f4f1d092e6fa02ade0016945ae88484d088f2a7b'
            '53b37c1101dd9be2d126fd246af262a5305bd450257d22095e7c0baa469af03a'
            '2b889de6c89511cd7639c95a94a51c517eca0fddce152cc467b16a5ab8d73d43'
            '6fba0317d66c41052c41d2d9af7d85a88ae04fc323e84c34a44bcc4e1311489a'
            '47e822a296c449f0dc5e2e8d20709682c2c91a84f388d67d14dd5a5d5250e7a3'
            'd8f962fa0df9073f59bf4e090cb1ca01a2a6dcb99b6b4e9fdd52d71508551101'
            'eed94bb582fcdbb00a7d8fd9cc10824e6b75c6ba4650d70c97ab5252669876d9'
            'a01750010af1aa81dd4e9cb765bc805b60283cf19014bf90325deb776d4c9e54'
            '1e3e683bf1fb2009e9b1f1b453554575f2a77fb88f0595f66a4d3568817c5909'
            '37fb53681c82181059d3e8ae7a7940a3f0963ca0809f073670d0b8edcf212b10'
            '89ead0ee685666c40c3e8a027fbc11bde145a28271b73d8ca8aa81b2a2859cc4'
            'a5f7c23c16cb1cb2c07c5f4652b1ba8679ca9470c978e235e41a4b239de49d94'
            'f97b0362393aa1265309e4d618040f8fe2a706f55dfaa5adc3e381c3fb40ce8c'
            'a2c32ee9194d3bcf2eb6f734d93bbabe14d47a55d999135cd118383280aca307'
            '80e49700c9bed6b8172819e05f25bb7afe0cd9388c9ae908b24db6c9b83a16bf'
            '9af8b70497acf6c2ecd18bcdf62674f2e83e15a499eaa7d03d571ed754b26117'
            '7026a7bf9221096af816f70cd6ddd9eadf2740429018d1d1db395fc85d1daf54'
            '68876071bc948fddeb668f4561ab26943d04e00205c7385e0e9a15f4853c22e1'
            '5e8cde32a6670e065686988b5b1491c04e20daff1207157ef152fee06488c76d'
            'a7e4cdb5be58e264fd573d7c644ef489622e4c96eaa1146ffd88b9749f76454d'
            '409d99382de32e046c8873b5299c46bae4603cf8d93ebf1c264e70c4c84b2896'
            '82f4a68306491ba6bd37b9ca9c54cc3936bbde687708ce967a87a45b3f7a316e'
            'bed35a4026d9dd766890da0be8d7e225c3bed4ba31fae6569ce83e1284c5bb38'
            'd03c7f1d46be76191a2406ac347a5e309760b83b0302b3322126aed2e425e147'
            'cfb14c2f39fb9c09808878ae149ddfad3385f64a95ccab7335bef0c4b1864f53'
            'd07561b66a7648f270f4990f3794f90585dc1ae68423c1ec12e6344a74bb249f')

create_links() {
    find "$pkgdir" -type f -name '*.so*' ! -path '*xorg/*' -print0 | while read -d $'\0' _lib; do
        _soname=$(dirname "${_lib}")/$(readelf -d "${_lib}" | grep -Po 'SONAME.*: \[\K[^]]*' || true)
        _base=$(echo ${_soname} | sed -r 's/(.*)\.so.*/\1.so/')
        [[ -e "${_soname}" ]] || ln -s $(basename "${_lib}") "${_soname}"
        [[ -e "${_base}" ]] || ln -s $(basename "${_soname}") "${_base}"
    done
}

prepare() {
    chmod +x "${srcdir}/get_configured340.sh" \
             "${srcdir}/get_defined340.sh" \
             "${srcdir}/split_conftest340.sh" \
             "${srcdir}/collect_tests340.sh"

    rm -rf "${_pkg}"
    sh "${_pkg}.run" --extract-only
    cd "${_pkg}"

    sed -i 's|/usr/libLIBDIRSUFFIX|/usr/lib|g' "${srcdir}/10-nvidia.conf.in"
    sed -i 's|/usr/libLIBDIRSUFFIX|/usr/lib|g' "${srcdir}/10-nvidia-modules.conf.in"

    cd kernel

    # 1. nv-gnu17-fms-extensions-1.patch
    patch -p2 < "${srcdir}/nv-gnu17-fms-extensions-1.patch"

    # 2. Első állapotmentés
    "${srcdir}/get_configured340.sh"
    mv got_configured340.txt got_configured340.orig
    "${srcdir}/get_defined340.sh"
    mv got_defined340.txt got_defined340.orig
    cp Makefile Makefile.orig
    cp conftest.sh conftest.orig
    cp uvm/Makefile uvm/Makefile.orig
    cp uvm/conftest.sh uvm/conftest.orig

    # 3. A sorozat patchek: 0001-0075, névsorrendben (a series.in pontosan így van számozva)
    for _p in "${srcdir}"/[0-9][0-9][0-9][0-9]-*.patch; do
        echo "Applying patch $(basename "$_p")"
        patch -p1 < "$_p" || true
    done

    # 4. Második állapotmentés
    "${srcdir}/get_configured340.sh"
    mv got_configured340.txt got_configured340.deb
    "${srcdir}/get_defined340.sh"
    mv got_defined340.txt got_defined340.deb
    cp Makefile Makefile.deb
    cp conftest.sh conftest.deb
    cp uvm/Makefile uvm/Makefile.deb
    cp uvm/conftest.sh uvm/conftest.deb

    # 5. Külön patchek a sorozaton kívül
    for _p in \
        nv-drm-fop-flags.patch \
        nv-no-per-vma-lock-on-x86.patch \
        nv-screen-info.patch \
        nv-vma-lock-offset.patch \
        nv-is-vma-write-locked-args.patch; do
        echo "Applying patch ${_p}"
        patch -p2 < "${srcdir}/${_p}" || true
    done

    # 6. Split és collect
    "${srcdir}/get_defined340.sh"
    "${srcdir}/split_conftest340.sh"
    "${srcdir}/collect_tests340.sh"
    mv conftest.new conftest.sh
    "${srcdir}/get_configured340.sh"
    chmod +x conftest.sh
    cp -f conftest.sh uvm
    mv Makefile.new Makefile
    mv uvm/Makefile.new uvm/Makefile

    # 7. nv-gnu17-fms-extensions-2.patch
    patch -p2 < "${srcdir}/nv-gnu17-fms-extensions-2.patch" || true

    # 8. Makefile módosítások
    sed -i "s|-DNDEBUG$|-DNDEBUG -Wno-error=return-type -Wno-error=implicit-function-declaration|" Makefile
    cd uvm
    sed -i "s|-O2$|-O2 -Wno-error=incompatible-pointer-types|" Makefile
    cd ..

    cd ../..
}

package_opencl-nvidia-340xx() {
    pkgdesc="OpenCL implemention for NVIDIA"
    depends=('zlib')
    optdepends=('opencl-headers: headers necessary for OpenCL development')
    provides=("opencl-nvidia=${pkgver}" 'opencl-driver')
    conflicts=('opencl-nvidia')

    cd "${_pkg}"

    install -Dm644 nvidia.icd "${pkgdir}/etc/OpenCL/vendors/nvidia.icd"
    install -Dm755 "libnvidia-compiler.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-compiler.so.${pkgver}"
    install -Dm755 "libnvidia-opencl.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-opencl.so.${pkgver}"

    create_links

    mkdir -p "${pkgdir}/usr/share/licenses"
    ln -s nvidia "${pkgdir}/usr/share/licenses/opencl-nvidia"
}

package_nvidia-340xx-dkms() {
    pkgdesc="NVIDIA driver sources for linux, 340xx legacy branch"
    depends=('dkms' "nvidia-340xx-utils=${pkgver}")
    provides=('NVIDIA-MODULE' "nvidia-dkms=${pkgver}")
    conflicts=('nvidia-dkms')

    cd "${_pkg}"

    install -dm 755 "${pkgdir}"/usr/src
    cp -dr --no-preserve='ownership' kernel "${pkgdir}/usr/src/nvidia-${pkgver}"

    cat > "${pkgdir}/usr/src/nvidia-${pkgver}/dkms.conf" << EOF
PACKAGE_NAME="nvidia-340xx"
PACKAGE_VERSION="${pkgver}"
CLEAN="make clean"
BUILT_MODULE_NAME[0]="nvidia"
BUILT_MODULE_LOCATION[0]="kernel"
DEST_MODULE_LOCATION[0]="/kernel/drivers/video"
BUILT_MODULE_NAME[1]="nvidia-uvm"
BUILT_MODULE_LOCATION[1]="kernel/uvm"
DEST_MODULE_LOCATION[1]="/kernel/drivers/video"
MAKE[0]="make -j\$(nproc) module SYSSRC=/usr/lib/modules/\$kernelver/build KERNELRELEASE=\$kernelver IGNORE_CC_MISMATCH=1"
STRIP[0]="yes"
EOF

    install -Dt "${pkgdir}/usr/share/licenses/${pkgname}" -m644 "${srcdir}/${_pkg}/LICENSE"
}

package_nvidia-340xx-utils() {
    pkgdesc="NVIDIA drivers utilities"
    depends=('xorg-server' 'mesa' 'mhwd')
    optdepends=('nvidia-340xx-settings: configuration tool'
                'xorg-server-devel: nvidia-xconfig'
                'opencl-nvidia-340xx: OpenCL support')
    conflicts=('nvidia-utils' 'nvidia-304xx-utils' 'nvidia-340xx-libgl')
    provides=('opengl-driver' 'nvidia-libgl' "nvidia-utils=${pkgver}" 'nvidia-340xx-libgl')
    replaces=('nvidia-340xx-libgl')
    install="${pkgname}.install"

    cd "${_pkg}"

    # X driver
    install -Dm755 nvidia_drv.so "${pkgdir}/usr/lib/xorg/modules/drivers/nvidia_drv.so"

    # GLX extension module for X
    install -dm 755 "${pkgdir}/usr/lib/nvidia/xorg"
    install -Dm755 "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so.${pkgver}"
    ln -s "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so.1"
    ln -s "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so"

    # OpenGL libraries
    install -Dm755 "libGL.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGL.so.${pkgver}"
    install -Dm755 "libEGL.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libEGL.so.${pkgver}"
    install -Dm755 "libGLESv1_CM.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGLESv1_CM.so.${pkgver}"
    install -Dm755 "libGLESv2.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGLESv2.so.${pkgver}"

    # OpenGL core library
    install -Dm755 "libnvidia-glcore.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-glcore.so.${pkgver}"
    install -Dm755 "libnvidia-eglcore.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-eglcore.so.${pkgver}"
    install -Dm755 "libnvidia-glsi.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-glsi.so.${pkgver}"

    # misc
    install -Dm755 "libnvidia-ifr.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-ifr.so.${pkgver}"
    install -Dm755 "libnvidia-fbc.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-fbc.so.${pkgver}"
    install -Dm755 "libnvidia-encode.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-encode.so.${pkgver}"
    install -Dm755 "libnvidia-cfg.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-cfg.so.${pkgver}"
    install -Dm755 "libnvidia-ml.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-ml.so.${pkgver}"

    # VDPAU
    install -Dm755 "libvdpau_nvidia.so.${pkgver}" "${pkgdir}/usr/lib/vdpau/libvdpau_nvidia.so.${pkgver}"

    # nvidia-tls library
    install -Dm755 "tls/libnvidia-tls.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-tls.so.${pkgver}"

    # CUDA
    install -Dm755 "libcuda.so.${pkgver}" "${pkgdir}/usr/lib/libcuda.so.${pkgver}"
    install -Dm755 "libnvcuvid.so.${pkgver}" "${pkgdir}/usr/lib/libnvcuvid.so.${pkgver}"

    # DEBUG
    install -Dm755 nvidia-debugdump "${pkgdir}/usr/bin/nvidia-debugdump"

    # nvidia-xconfig
    install -Dm755 nvidia-xconfig "${pkgdir}/usr/bin/nvidia-xconfig"
    install -Dm644 nvidia-xconfig.1.gz "${pkgdir}/usr/share/man/man1/nvidia-xconfig.1.gz"

    # gsync support
    install -Dm444 pci.ids "${pkgdir}/usr/share/nvidia/pci.ids"
    install -Dm444 monitoring.conf "${pkgdir}/usr/share/nvidia/monitoring.conf"

    # nvidia-bug-report
    install -Dm755 nvidia-bug-report.sh "${pkgdir}/usr/bin/nvidia-bug-report.sh"

    # nvidia-smi
    install -Dm755 nvidia-smi "${pkgdir}/usr/bin/nvidia-smi"
    install -Dm644 nvidia-smi.1.gz "${pkgdir}/usr/share/man/man1/nvidia-smi.1.gz"

    # nvidia-cuda-mps
    install -Dm755 nvidia-cuda-mps-server "${pkgdir}/usr/bin/nvidia-cuda-mps-server"
    install -Dm644 nvidia-cuda-mps-control.1.gz "${pkgdir}/usr/share/man/man1/nvidia-cuda-mps-control.1.gz"

    # nvidia-modprobe
    install -Dm4755 nvidia-modprobe "${pkgdir}/usr/bin/nvidia-modprobe"

    # application profiles
    install -Dm644 nvidia-application-profiles-${pkgver}-rc "${pkgdir}/usr/share/nvidia/nvidia-application-profiles-${pkgver}-rc"
    install -Dm644 nvidia-application-profiles-${pkgver}-key-documentation "${pkgdir}/usr/share/nvidia/nvidia-application-profiles-${pkgver}-key-documentation"

    # License, docs
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/nvidia/LICENSE"
    ln -s nvidia "${pkgdir}/usr/share/licenses/nvidia-utils"
    install -Dm644 README.txt "${pkgdir}/usr/share/doc/nvidia/README"
    install -Dm644 NVIDIA_Changelog "${pkgdir}/usr/share/doc/nvidia/NVIDIA_Changelog"
    ln -s nvidia "${pkgdir}/usr/share/doc/nvidia-utils"

    # Xorg configuration files
    install -Dm644 "${srcdir}/10-nvidia.conf.in" "${pkgdir}/usr/share/X11/xorg.conf.d/10-nvidia.conf"
    install -Dm644 "${srcdir}/10-nvidia-modules.conf.in" "${pkgdir}/usr/share/X11/xorg.conf.d/10-nvidia-modules.conf"

    # Udev rules és sysusers
    install -Dm644 "${srcdir}/nvidia-340xx.rules" "${pkgdir}/usr/lib/udev/rules.d/60-nvidia-340xx.rules"
    install -Dm644 "${srcdir}/nvidia-utils.sysusers" "${pkgdir}/usr/lib/sysusers.d/nvidia-340xx-utils.conf"

    # Blacklist nouveau és nvidia-uvm betöltés
    echo "blacklist nouveau" | install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modprobe.d/${pkgname}.conf"
    echo "nvidia-uvm" | install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules-load.d/${pkgname}.conf"

    # ld.so.conf.d
    install -dm 755 "${pkgdir}"/etc/ld.so.conf.d
    echo -e '/usr/lib/nvidia/' > "${pkgdir}"/etc/ld.so.conf.d/00-nvidia.conf

    # Váltó script és systemd service
    install -Dm755 "${srcdir}/nvidia-340xx-lib-switch" "${pkgdir}/usr/bin/nvidia-340xx-lib-switch"
    install -Dm644 "${srcdir}/nvidia-340xx-lib-switch.service" "${pkgdir}/usr/lib/systemd/system/nvidia-340xx-lib-switch.service"
}

package_mhwd-nvidia-340xx() {
    pkgdesc="MHWD module-ids for nvidia ${pkgver}"
    arch=('any')
    depends=('mhwd')

    install -d -m755 "${pkgdir}/var/lib/mhwd/ids/pci/"

    sh -e ${srcdir}/mhwd-nvidia \
        ${srcdir}/${_pkg}/README.txt \
        ${srcdir}/${_pkg}/kernel/nv-kernel.o \
        > ${pkgdir}/var/lib/mhwd/ids/pci/nvidia-340xx.ids
}
