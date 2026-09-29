# Maintainer: Gyöngyösi Gábor <gabor at gshoots dot hu>
# Contributor: Philip Müller <philm[at]manjaro[dot]org>
# Contributor: Thomas Baechler <thomas@archlinux.org>
# Contributor: Jerry Xiao <aur@mail.jerryxiao.cc>
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
#
# Átírva: Debian 340xx/main patch-sorozat használatára (81 patch).
# A patchek a series.resolved sorrendjében, a kernel/ könyvtárban
# kerülnek alkalmazásra. Manjaro-specifikus patchek (0001-0029) eltávolítva.
# A patchek a PKGBUILD mellett, laposan (nincs debian-patches alkönyvtár).

pkgbase=nvidia-340xx-utils
pkgname=('nvidia-340xx-utils' 'opencl-nvidia-340xx' 'nvidia-340xx-dkms' 'mhwd-nvidia-340xx')
pkgver=340.108
pkgrel=1
arch=('x86_64')
url="https://www.nvidia.com/"
license=('custom')
options=('!strip')
_pkg="NVIDIA-Linux-x86_64-${pkgver}-no-compat32"

# ---- Debian patch lista (a series.resolved-ból, sorrend kötelező) ----
_debian_patches=(
    'bashisms.patch'
    '0001-backport-error-on-unknown-conftests.patch'
    '0002-backport-error-on-unknown-conftests-uvm-part.patch'
    'unregister_procfs_on_failure.patch'
    'kmem_cache_create_usercopy.patch'
    'buildfix_kernel_4.11.patch'
    'buildfix_kernel_5.2.patch'
    '03-unfuck-for-5.5.x.patch'
    '0008-backport-drm_available-changes-from-361.16.patch'
    '0009-backport-drm_driver_has_legacy_dev_list-changes-from.patch'
    '0010-backport-drm_gem_object_get-changes-from-418.30.patch'
    '0011-backport-nv_ioremap_nocache-changes-from-440.64.patch'
    '0012-backport-nv_proc_ops_t-changes-from-440.82.patch'
    '0013-backport-nv_timeval-changes-from-440.82.patch'
    '0014-backport-nv_proc_ops_t-nv_timeval-changes-from-440.8.patch'
    '0015-drm_legacy_pci_init-was-moved-to-drm-drm_legacy.h.patch'
    '0016-backport-asm-pgtable_types.h-changes-from-390.138.patch'
    '0017-backport-linux-ioctl32.h-changes-from-450.51.patch'
    '0018-backport-nv_vmalloc-changes-from-450.57.patch'
    '0019-work-around-mmap_-sem-lock-rename.patch'
    '0020-work-around-mmap_-sem-lock-rename-uvm-part.patch'
    '0021-backport-get_user_pages_remote-changes-from-455.23.0.patch'
    '0022-backport-vga_tryget-changes-from-455.23.04.patch'
    '0023-backport-drm_driver_has_gem_free_object-changes-from.patch'
    '0024-backport-drm_prime_pages_to_sg_has_drm_device_arg-ch.patch'
    '0025-check-for-drm_pci_init.patch'
    '0026-import-drm_legacy_pci_init-exit-from-src-linux-5.9.1.patch'
    '0027-add-static-and-nv_-prefix-to-copied-drm-legacy-bits.patch'
    '0028-backport-asm-kmap_types.h-changes-from-460.32.03.patch'
    '0029-backport-drm_driver_has_gem_prime_callbacks-changes-.patch'
    '0030-skip-list-operations-if-drm_device.legacy_dev_list-i.patch'
    '0031-backport-set_current_state-changes-from-470.63.01.patch'
    '0032-backport-drm_device_has_pdev-changes-from-470.63.01.patch'
    '0033-check-for-member-agp-in-struct-drm_device.patch'
    '0034-backport-stdarg.h-changes-from-470.82.00.patch'
    '0035-backport-pde_data-changes-from-470.103.01.patch'
    '0036-backport-pci-dma-changes-from-470.129.06.patch'
    '0037-backport-acpi_bus_get_device-changes-from-470.129.06.patch'
    '0038-backport-acpi-changes-from-390.157.patch'
    '0039-backport-acpi_op_remove-changes-from-470.182.03.patch'
    '0040-backport-vm_area_struct_has_const_vm_flags-changes-f.patch'
    '0041-backport-get_user_pages-changes-from-418.30.patch'
    '0042-backport-get_user_pages-changes-from-520.56.06.patch'
    '0043-backport-get_user_pages-changes-from-525.53.patch'
    '0044-backport-get_user_pages-changes-from-535.86.05.patch'
    '0045-backport-asm-page.h-changes-from-470.223.02.patch'
    '0046-backport-drm_gem_prime_handle_to_fd-changes-from-470.patch'
    '0047-refuse-to-load-legacy-module-if-IBT-is-enabled.patch'
    '0048-backport-nv_get_kern_phys_address-changes-from-555.4.patch'
    '0051-build-without-Wsign-compare.patch'
    '0052-backport-cmd_symlink-changes-from-550.142.patch'
    '0053-fix-more-warnings.patch'
    '0054-fix-more-uvm-warnings.patch'
    '0060-backport-build_cflags-changes-from-525.85.05.patch'
    '0063-backport-conftest.sh-comment-changes-from-515.48.07.patch'
    '0063-backport-conftest.sh-comment-changes-from-525.53.patch'
    '0063-backport-conftest.sh-comment-changes-from-545.23.06.patch'
    '0064-backport-drm_driver_has_date-from-570.124.04.patch'
    '0065-backport-ccflags-y-changes-from-570.153.02.patch'
    '0066-backport-nv_timer_delete_sync-changes-from-570.153.0.patch'
    '0071-backport-nv_vma_start_write-changes-from-570.169.patch'
    '0072-disable-objtool-usage.patch'
    '0075-backport-drm_print.h-changes-from-570.211.01.patch'
    '0076-backport-nv_in_hardirq-changes-from-580.119.02.patch'
    '0077-backport-vma_flags_set_word-changes-from-580.126.09.patch'
    '0078-backport-vma_flags_set_word-changes-from-580.126.09-.patch'
    'separate-makefile-kbuild.patch'
    'KERNEL_UNAME.patch'
    'use-kbuild-compiler.patch'
    'use-kbuild-flags.patch'
    'build-sanity-checks.patch'
    'conftest-verbose.patch'
    'conftest-via-kbuild.patch'
    'not-silent.patch'
    'disable-cc_version_check.patch'
    'use-nv-kernel-ARCH.o_binary.patch'
    'avoid-ld.gold.patch'
    'conftest-include-guard.patch'
    'ignore_xen_on_arm.patch'
    'arm-outer-sync.patch'
    'armhf-on-arm64-kernel.patch'
    'kernel-6.18-workqueue-flush.patch'
    'kernel-7.0-screen_info.patch'
    'vma-lock-7.0-plus.patch'
    'kernel-7.3-acpi.patch'
    'cve-2022-34670-nv-h-IS-OFFSET.patch'
    'cve-2022-34674-vma-size.patch'
    'cve-2022-34670-nv-c-usage-count-overflow.patch'
)

source=("https://us.download.nvidia.com/XFree86/Linux-x86_64/${pkgver}/${_pkg}.run"
        'mhwd-nvidia'
        'nvidia-340xx-utils.install'
        'nvidia-utils.sysusers'
        'nvidia-340xx.rules'
        'series.resolved'
        '20-nvidia.conf'
        "${_debian_patches[@]}"
)

sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

create_links() {
    find "$pkgdir" -type f -name '*.so*' ! -path '*xorg/*' -print0 | while read -d $'\0' _lib; do
        _soname=$(dirname "${_lib}")/$(readelf -d "${_lib}" | grep -Po 'SONAME.*: \[\K[^]]*' || true)
        _base=$(echo ${_soname} | sed -r 's/(.*)\.so.*/\1.so/')
        [[ -e "${_soname}" ]] || ln -s $(basename "${_lib}") "${_soname}"
        [[ -e "${_base}" ]] || ln -s $(basename "${_soname}") "${_base}"
    done
}

prepare() {
    rm -rf "${_pkg}"
    sh "${_pkg}.run" --extract-only

    cd "${_pkg}"

    cd kernel

    # -----------------------------------------------------------------------
    # 1. Debian patch-sorozat alkalmazása
    # -----------------------------------------------------------------------
    echo ">>> Debian patch-sorozat alkalmazása (kernel/ könyvtárban)..."

    if [ ! -f "${srcdir}/series.resolved" ]; then
        echo "!!! HIBA: hiányzik a series.resolved a PKGBUILD mellől"
        exit 1
    fi

    local _n=0
    local _total
    _total=$(grep -cve '^[[:space:]]*$' "${srcdir}/series.resolved")

    while IFS= read -r _patch || [ -n "$_patch" ]; do
        _patch="${_patch%$'\r'}"
        [ -z "${_patch//[[:space:]]/}" ] && continue
        _n=$((_n + 1))
        _patchfile="${srcdir}/${_patch}"

        if [ ! -f "$_patchfile" ]; then
            echo "!!! HIBA: hiányzó patch: $_patchfile"
            exit 1
        fi

        printf '[%3d/%d] %s\n' "$_n" "$_total" "$_patch"
        patch -Np1 --forward --no-backup-if-mismatch < "$_patchfile" \
            || { echo "!!! PATCH FAILED: $_patch"; exit 1; }
    done < "${srcdir}/series.resolved"

    echo ">>> Mind a $_n patch sikeresen alkalmazva."

    # -----------------------------------------------------------------------
    # 2. UVM conftest.sh lecserélése a patchelt fő conftest.sh másolatára.
    #
    # Az UVM saját, 2019-es conftest.sh-ja nem ismeri fel a modern kernel
    # API-kat (kmem_cache_create 5 argumentummal, kuid_t, task_struct.euid).
    # A Debian symlinket használ, de a DKMS belső másolásai miatt a symlink
    # nem érvényesül megbízhatóan. Ezért TÉNYLEGES MÁSOLATOT készítünk,
    # a patchek UTÁN, hogy a másolat már a patchelt tartalmat kapja.
    # -----------------------------------------------------------------------
    if [ -e uvm/conftest.sh ] && [ ! -L uvm/conftest.sh ]; then
        rm -f uvm/conftest.sh
    fi
    cp -f conftest.sh uvm/conftest.sh

    echo ">>> uvm/conftest.sh lecserélve a patchelt fő conftest.sh másolatára."
    echo ">>> 'NV_CONFTEST_H_' előfordulások száma:"
    echo "    $(grep -c 'NV_CONFTEST_H_' uvm/conftest.sh || echo 0)"

    # -----------------------------------------------------------------------
    # 3. Debian build-stamp blob-előkészítés.
    #
    # A Debian build-stamp a következőt csinálja:
    #     $(RM) build/kernel/nv-kernel.o
    #     cp -al NVIDIA-Linux-$a/kernel/nv-kernel.o \
    #              build/kernel/nv-kernel-$a.o_binary
    #
    # Vagyis az eredeti nv-kernel.o-t ELTÁVOLÍTJA, és csak az
    # arch-specifikus .o_binary marad. Ez azért kritikus, mert a
    # use-nv-kernel-ARCH.o_binary.patch az alábbi szabályt hozza létre:
    #
    #     $(obj)/$(CORE_OBJS): $(src)/$(CORE_OBJS-y)_binary
    #             $(call if_changed,symlink)
    #
    # Az if_changed csak akkor futtatja a receptet (és írja a
    # .nv-kernel.o.cmd-t), ha a cél NEM létezik, VAGY a prerequisite
    # újabb, VAGY a parancs eltér, VAGY FORCE van a prerequisite-ek
    # között. Ha a target (nv-kernel.o) már létezik és nem elavult,
    # a recept kimarad, és a .cmd fájl nem jön létre. A modpost
    # fázisban ez a következőt okozza:
    #     .nv-kernel.o.cmd: No such file or directory
    #     make[2]: *** [scripts/Makefile.modpost:127: .../Module.symvers] Error 1
    #
    # Ezért a Debian mintájára az eredeti nv-kernel.o-t ELTÁVOLÍTJUK
    # (mv-vel átnevezzük), így a DKMS build során a target hiányzik,
    # és a recept garantáltan lefut.
    # -----------------------------------------------------------------------
    if [ ! -f nv-kernel.o ]; then
        echo "!!! HIBA: hiányzik kernel/nv-kernel.o"
        exit 1
    fi
    mv -f nv-kernel.o nv-kernel-amd64.o_binary
    echo ">>> nv-kernel.o → nv-kernel-amd64.o_binary (átnevezve, Debian build-stamp szerint)"

    # -----------------------------------------------------------------------
    # 4. DKMS workaround: KERNELRELEASE semlegesítése a top-level make híváskor.
    #
    # A DKMS 3.x a top-level make híváskor beállítja a KERNELRELEASE-t:
    #   make -j2 KERNELRELEASE=6.x.y module KERNEL_UNAME=6.x.y
    #
    # A Debian patchelt nvidia-modules-common.mk a build logikát a
    # KERNELRELEASE alapján kettéválasztja. Ha M nincs beállítva (DKMS
    # top-level hívás), ürítjük a KERNELRELEASE-t, így a Makefile-szekció
    # (module, nvidia.ko, BUILD_MODULE_RULE) aktiválódik. A Kbuild belső
    # hívásakor M be van állítva, ott minden marad.
    # -----------------------------------------------------------------------
    {
        cat <<'EOF_HEADER'
# --- DKMS workaround: KERNELRELEASE semlegesítése a top-level híváskor ---
ifeq ($(M),)
  override KERNELRELEASE :=
endif
# --- end DKMS workaround ---
EOF_HEADER
        cat Makefile
    } > Makefile.new
    mv Makefile.new Makefile

    echo ">>> DKMS workaround hozzáadva a kernel/Makefile tetejére."

    # -----------------------------------------------------------------------
    # 5. DKMS dkms.conf előkészítése
    # -----------------------------------------------------------------------
    if ! grep -q "nvidia-uvm" dkms.conf; then
        cat uvm/dkms.conf.fragment >> dkms.conf
    fi
    sed -i "s/__JOBS/`nproc`/" dkms.conf
    sed -i -E 's/^([[:space:]]*)CLEAN/\1clean/' dkms.conf
    cd ..
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

    install -Dm755 nvidia_drv.so "${pkgdir}/usr/lib/xorg/modules/drivers/nvidia_drv.so"

    install -Dm755 "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so.${pkgver}"
    ln -s "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so.1"
    ln -s "libglx.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/xorg/libglx.so"

    install -Dm755 "libGL.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGL.so.${pkgver}"
    install -Dm755 "libEGL.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libEGL.so.${pkgver}"
    install -Dm755 "libGLESv1_CM.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGLESv1_CM.so.${pkgver}"
    install -Dm755 "libGLESv2.so.${pkgver}" "${pkgdir}/usr/lib/nvidia/libGLESv2.so.${pkgver}"

    install -Dm755 "libnvidia-glcore.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-glcore.so.${pkgver}"
    install -Dm755 "libnvidia-eglcore.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-eglcore.so.${pkgver}"
    install -Dm755 "libnvidia-glsi.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-glsi.so.${pkgver}"

    install -Dm755 "libnvidia-ifr.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-ifr.so.${pkgver}"
    install -Dm755 "libnvidia-fbc.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-fbc.so.${pkgver}"
    install -Dm755 "libnvidia-encode.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-encode.so.${pkgver}"
    install -Dm755 "libnvidia-cfg.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-cfg.so.${pkgver}"
    install -Dm755 "libnvidia-ml.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-ml.so.${pkgver}"

    install -Dm755 "libvdpau_nvidia.so.${pkgver}" "${pkgdir}/usr/lib/vdpau/libvdpau_nvidia.so.${pkgver}"

    install -Dm755 "tls/libnvidia-tls.so.${pkgver}" "${pkgdir}/usr/lib/libnvidia-tls.so.${pkgver}"

    install -Dm755 "libcuda.so.${pkgver}" "${pkgdir}/usr/lib/libcuda.so.${pkgver}"
    install -Dm755 "libnvcuvid.so.${pkgver}" "${pkgdir}/usr/lib/libnvcuvid.so.${pkgver}"

    install -Dm755 nvidia-debugdump "${pkgdir}/usr/bin/nvidia-debugdump"

    install -Dm755 nvidia-xconfig "${pkgdir}/usr/bin/nvidia-xconfig"
    install -Dm644 nvidia-xconfig.1.gz "${pkgdir}/usr/share/man/man1/nvidia-xconfig.1.gz"

    install -Dm444 pci.ids "${pkgdir}/usr/share/nvidia/pci.ids"
    install -Dm444 monitoring.conf "${pkgdir}/usr/share/nvidia/monitoring.conf"

    install -Dm755 nvidia-bug-report.sh "${pkgdir}/usr/bin/nvidia-bug-report.sh"

    install -Dm755 nvidia-smi "${pkgdir}/usr/bin/nvidia-smi"
    install -Dm644 nvidia-smi.1.gz "${pkgdir}/usr/share/man/man1/nvidia-smi.1.gz"

    install -Dm755 nvidia-cuda-mps-server "${pkgdir}/usr/bin/nvidia-cuda-mps-server"
    install -Dm644 nvidia-cuda-mps-control.1.gz "${pkgdir}/usr/share/man/man1/nvidia-cuda-mps-control.1.gz"

    install -Dm4755 nvidia-modprobe "${pkgdir}/usr/bin/nvidia-modprobe"

    install -Dm644 nvidia-application-profiles-${pkgver}-rc "${pkgdir}/usr/share/nvidia/nvidia-application-profiles-${pkgver}-rc"
    install -Dm644 nvidia-application-profiles-${pkgver}-key-documentation "${pkgdir}/usr/share/nvidia/nvidia-application-profiles-${pkgver}-key-documentation"

    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/nvidia/LICENSE"
    ln -s nvidia "${pkgdir}/usr/share/licenses/nvidia-utils"
    install -Dm644 README.txt "${pkgdir}/usr/share/doc/nvidia/README"
    install -Dm644 NVIDIA_Changelog "${pkgdir}/usr/share/doc/nvidia/NVIDIA_Changelog"
    ln -s nvidia "${pkgdir}/usr/share/doc/nvidia-utils"

    install -Dm644 "${srcdir}/20-nvidia.conf" "${pkgdir}/usr/share/X11/xorg.conf.d/20-nvidia-340xx.conf"

    install -Dm644 "${srcdir}/nvidia-340xx.rules" "${pkgdir}/usr/lib/udev/rules.d/60-nvidia-340xx.rules"
    install -Dm644 "${srcdir}/nvidia-utils.sysusers" "${pkgdir}/usr/lib/sysusers.d/nvidia-340xx-utils.conf"

    echo "blacklist nouveau" | install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modprobe.d/${pkgname}.conf"
    echo "nvidia-uvm" | install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules-load.d/${pkgname}.conf"

    create_links

    install -dm 755 "${pkgdir}"/etc/ld.so.conf.d
    echo -e '/usr/lib/nvidia/' > "${pkgdir}"/etc/ld.so.conf.d/00-nvidia.conf
}

package_mhwd-nvidia-340xx() {
    pkgdesc="MHWD module-ids for nvidia ${pkgver}"
    arch=('any')
    depends=('mhwd')

    install -d -m755 "${pkgdir}/var/lib/mhwd/ids/pci/"

    # A Debian build-stamp mintájára az eredeti nv-kernel.o-t a prepare()
    # átnevezte nv-kernel-amd64.o_binary-re. A blob tartalma azonos, így
    # az mhwd-nvidia script ugyanúgy ki tudja olvasni belőle a támogatott
    # PCI ID-kat.
    sh -e ${srcdir}/mhwd-nvidia \
        ${srcdir}/${_pkg}/README.txt \
        ${srcdir}/${_pkg}/kernel/nv-kernel-amd64.o_binary \
        > ${pkgdir}/var/lib/mhwd/ids/pci/nvidia-340xx.ids
}