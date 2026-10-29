# Maintainer: Gyöngyösi Gábor <gabor at gshoots dot hu>
# Contributor: Philip Müller <philm[at]manjaro[dot]org>
# Contributor: Thomas Baechler <thomas@archlinux.org>
# Contributor: Jerry Xiao <aur@mail.jerryxiao.cc>
# Contributor: Giancarlo Razzolini <grazzolini@archlinux.org>
#
# Átírva: Debian 340xx/main patch-sorozat használatára (89 patch).
# A patchek a series.resolved sorrendjében, a kernel/ könyvtárban,
# mpatch-csel kerülnek alkalmazásra. Manjaro-specifikus patchek
# (0001-0029) eltávolítva. A patchek a PKGBUILD mellett, laposan
# (nincs debian-patches alkönyvtár).
#
# =============================================================================
#  NVIDIA 340xx – Debian patch-sorozat mpatch-csel
#  For Manjaro-awesome-respin
# =============================================================================
#
#  ┌─────────────────────────────────────────────────────────────────────────┐
#  │  MPATCH – HORDOZHATÓ KÉZIKÖNYV A PKGBUILD-BEN                          │
#  │  (Ha elfelejted, itt minden megtalálható. Nem kell GitHub-ot nyitni.)  │
#  └─────────────────────────────────────────────────────────────────────────┘
#
#  MI ÉS MIÉRT
#  -----------
#  Az mpatch egy fuzzy patchelő. Nem sorszám és nem bájt-pontos kontextus
#  alapján illeszt, hanem hasonlósági algoritmussal keresi a patch helyét.
#  Ez akkor hasznos, ha egy Debian patch egy kicsit elavult a forráshoz
#  képest, DE a változtatás lényege még stimmel.
#
#  KOCKÁZAT
#  --------
#  A fuzzy matching rossz helyre is illeszthet. Ezért:
#    - build-hez MINDIG használj --atomic-ot (minden-vagy-semmi)
#    - a --fuzz-factor-t csak indokolt esetben lazítsd
#    - ha egy patch elhasal: először debug, csak utána lazítás
#
#  ---------------------------------------------------------------------------
#  BEVEZETŐ FORMÁTUMOK (amit az mpatch automatikusan felismer)
#  ---------------------------------------------------------------------------
#   1. Unified Diff          – ez a Debian patchek formátuma (--- a/ +++ b/)
#   2. Markdown diff blokk   – ```diff ... ``` (LLM kimenet)
#   3. Aider Search/Replace  – <<<<<<< SEARCH ... ======= ... >>>>>>> REPLACE
#   4. Conflict Markers      – <<<< ==== >>>> (nincs benne fájlútvonal!)
#
#  A Debian patcheink az 1-es típusba esnek. A 4-es típus CLI-ből
#  csak egy "patch_target" nevű fájlt tud patchelni – nekünk nem jó.
#
#  ---------------------------------------------------------------------------
#  FORMÁTUM-LIMITÁCIÓK (ezeket az mpatch NEM tudja alkalmazni)
#  ---------------------------------------------------------------------------
#  Ha a patch az alábbiak bármelyikét tartalmazza, az mpatch NEM
#  próbálkozik fuzzy-val, hanem azonnal leáll (exit 1, semmit nem ír):
#
#    - Git rename/copy:    "rename from" / "copy from"
#    - Git binary patch:   "GIT binary patch"
#    - Symlink / submodule mód (bármi, ami nem 100644 / 100755)
#    - Context diff:       "diff -c"  → regeneráld "diff -u"-val
#
#  ⚠ EZ NEM FUZZ-PROBLÉMA. Ha egy patch elbukik, ELŐSZÖR ezt kell
#  kizárni, mielőtt a fuzz-factort lazítanád. Ha ezek közül van benne,
#  a --fuzz-factor 0.3 sem segít – a patchet ki kell venni, vagy
#  kézzel át kell írni.
#
#  ---------------------------------------------------------------------------
#  PARANCSONKÉNTI OPCIÓK (mind a PKGBUILD _mpatch_opts tömbben)
#  ---------------------------------------------------------------------------
#
#  --fuzz-factor N            Hasonlósági küszöb, 0.0 – 1.0
#     0.0   = fuzzy KIKAPCSOLVA. Az egzakt és a trailing-whitespace-t
#             toleráló match továbbra is működik. NEM bájt-pontos, és
#             NEM viselkedik úgy, mint a GNU patch. Preview: --dry-run.
#     0.5   = laza (kockázatos, csak debug célra)
#     0.7   = DEFAULT (a tool ajánlott értéke)
#     0.9   = nagyon szigorú (kevés eltűréssel)
#     1.0   = gyakorlatilag csak tökéletes egyezés
#
#     MIKOR MELYIK?
#       - Build-hez: 0.7 (default) vagy 0.9 (ha van idő debugolni)
#       - Ha egy patch elhasal 0.7-en: ELŐSZÖR a FORMÁTUM-LIMITÁCIÓK
#         szekciót kell kizárni (fent), csak utána lazíts 0.5-re.
#         Ha 0.5-ön sikerül, a patch elavult → FRISSÍTENI KELL,
#         nem lazítani.
#       - Ha 0.5 sem elég: a patch kontextusa túlságosan eltér,
#         valószínűleg upstream már beolvasztotta → a patchet ki kell venni
#
#  -a / --atomic / --all-or-nothing   (a kettő UGYANAZ)
#     Minden-vagy-semmi. Ha bármely hunk elhasal, egy fájl sem íródik.
#     Build-hez KÖTELEZŐ. Kikapcsolva részleges írás lehetséges, ami
#     csendben elrontja a forrásfát.
#
#     FONTOS: az atomic és a fuzz-factor ORTOGONÁLIS. Az atomic a
#     write-szemantikát szabályozza, a fuzz a match-szemantikát.
#     Az atomic-ot NEM kell a fuzz-hoz igazítani.
#
#     HATÓKÖR: egy mpatch híváson belül garantál atomitást. A while
#     ciklusban minden patch külön hívás → ha a 40. elhasal, az első
#     39 már lemezre íródott. Ez a mi esetünkben OK, mert a prepare()
#     elején úgyis rm -rf "${_pkg}"-vel tiszta lappal indulunk.
#
#  -R                          Patch megfordítása (add ↔ remove).
#                              Build-hez nem kell, de ha egy patch-et
#                              vissza akarsz fejteni (mit is csinál
#                              pontosan), akkor hasznos.
#
#  --dry-run                   Csak előnézet, nem ír fájlt.
#                              Debug workflow 1. lépése: mit tenne?
#
#  -c / --clipboard            Vágólapról olvas. Ilyenkor az INPUT_FILE
#                              elhagyható: `mpatch -c ./src` is működik.
#                              Build-hez nem kell.
#
#  -                           stdin-ről olvas. Pipe esetén a '-' is
#                              elhagyható: `git diff | mpatch ./src`.
#                              Build-hez nem kell (fájlból olvasunk).
#
#  -v / --verbose              Ismételhető, szintenként:
#                                -v     info (mit csinál épp)
#                                -vv    debug
#                                -vvv   trace
#                                -vvvv  trace + debug-riport fájl
#                              Siker esetén az mpatch ALAPBÓL SEMMIT
#                              nem ír ki. Ha a build logban látni akarod
#                              a patchek előrehaladását, tegyél -v-t a
#                              _mpatch_opts-ba.
#
#  -h / --help                 Súgó.
#
#  ---------------------------------------------------------------------------
#  EXIT KÓDOK ÉS KIMENET (a _mpatch_apply logikája erre épül)
#  ---------------------------------------------------------------------------
#
#    Siker (minden hunk alkalmazva)     → exit 0, semmit nem ír ki
#    Hiba (bármely hunk elbukik)        → exit 1, kiírja a legközelebbi
#                                          találatot + hasonlóságot
#    Nincs patch a bemenetben           → warning + exit 0  ⚠ CSAPDA
#
#  ⚠ A "nincs patch → exit 0" csapda: ha egy Debian patch véletlenül
#  üres, vagy csak kommenteket tartalmaz, az mpatch NÉMÁN átengedi,
#  és a build később, érthetetlen módon hasal el. A _mpatch_apply
#  ezt nem tudja kiszűrni – ha gyanús egy patch, nézd meg a tartalmát.
#
#  ⚠ --atomic NÉLKÜL a sikeres hunok lemezre íródnak akkor is, ha
#  más hunok elbuknak → részleges, csendben elrontott forrásfa.
#  Ezért van --atomic kötelezően a _mpatch_opts-ban.
#
#  ---------------------------------------------------------------------------
#  DEBUG WORKFLOW – HA EGY PATCH ELHASAL
#  ---------------------------------------------------------------------------
#
#  1. LÉPÉS – Nézd meg a hibaüzenetet
#     Az mpatch kiírja, melyik fájlt és melyik hunkot nem tudta alkalmazni.
#     A prepare() automatikusan -vvvv-vel újrafuttatja a hibás patchet,
#     és a debug-riportot a ${srcdir}/mpatch-debug/-be másolja.
#
#  2. LÉPÉS – Kizártad a FORMÁTUM-LIMITÁCIÓT?
#     Nézd meg a patch tartalmát:
#       grep -E 'rename from|copy from|GIT binary patch|^diff -c ' <patch>
#     Ha bármelyik találat van: a fuzz nem segít, a patchet ki kell
#     venni vagy kézzel át kell írni. Csak ha üres a találat, menj
#     tovább a 3. lépésre. (Ez a leggyakrabban elfelejtett ellenőrzés.)
#
#  3. LÉPÉS – Nézd meg a debug-riportot
#     mpatch-debug-report-<timestamp>.md a ${srcdir}/mpatch-debug/-ben.
#     Tartalmazza:
#       - az eredeti patch-et
#       - a célfájl érintett részeit
#       - inline word-level diffet a nem illeszkedő hunkról
#       - a legközelebbi hasonló fájlútvonalakat (ha a fájl nem található)
#
#  4. LÉPÉS – Próbáld lazítani a fuzz-factort
#     Szerkeszd a PKGBUILD-ben a _mpatch_opts-ot:
#       --fuzz-factor 0.5
#     Futtasd újra: makepkg -f
#     Ha sikerül: a patch elavult, jegyezd fel, és később frissítsd.
#     Ha nem sikerül: 5. lépés.
#
#  5. LÉPÉS – Reverse-engineer
#     Nézd meg, mit csinál a patch eredetileg:
#       mpatch -R --dry-run <patch> kernel/
#     Ez megmutatja, mit venne ki a forrásból.
#     Nézd meg a Debian upstream git history-t:
#       https://salsa.debian.org/nvidia-team/nvidia-graphics-drivers
#     Keress rá a patch nevére, nézd meg az eredeti commitot.
#
#  6. LÉPÉS – Kihagyás vagy frissítés
#     Ha a patch már upstream-ben van: vedd ki a series.resolved-ból.
#     Ha a patch elavult: frissítsd a Debian salsa repóból.
#     Ha muszáj: írj saját patchet a különbségre.
#
#  ---------------------------------------------------------------------------
#  TESZTELÉSI TIPP
#  ---------------------------------------------------------------------------
#  Egyetlen patch tesztelése a teljes sorozat helyett:
#     cd ${srcdir}/NVIDIA-Linux-x86_64-340.108-no-compat32/kernel
#     mpatch --dry-run --fuzz-factor 0.7 ${srcdir}/<patch> .
#  Ez megmutatja, mit tenne, anélkül hogy bármit írna.
#
# =============================================================================

pkgbase=nvidia-340xx-utils
pkgname=('nvidia-340xx-utils' 'opencl-nvidia-340xx' 'nvidia-340xx-dkms' 'mhwd-nvidia-340xx')
pkgver=340.108
pkgrel=1
arch=('x86_64')
url="https://www.nvidia.com/"
license=('custom')
options=('!strip')
makedepends=('mpatch-git')
_pkg="NVIDIA-Linux-x86_64-${pkgver}-no-compat32"

# =============================================================================
# MPATCH KONFIGURÁCIÓ – ITT ÁLLÍTS, ITT DEBUGOLJ
# =============================================================================
#
# Az AKTÍV opciók. A kommentelt sorok alternatívák – csak a # jelet kell
# levenni / visszatenni. A sorrend nem számít.
#
_mpatch_opts=(
    --atomic                # minden-vagy-semmi (build-hez kötelező)
#    --fuzz-factor 0.7       # default hasonlósági küszöb
    # --fuzz-factor 0.9     # szigorúbb: kevesebb eltűrés, több bukás
#    --fuzz-factor 0.3     # lazább: csak debug célra!
    # --fuzz-factor 0.0     # fuzzy kikapcsolva (egzakt + trailing-ws match)
    # --dry-run             # ne írjon, csak mutassa mit tenne
    # -v                    # info szint (siker esetén is ír valamit)
    # -vvvv                 # debug riport hiba esetén (a prepare() auto hívja)
    # -R                    # patch megfordítása (reverse-engineer)
    # -c                    # vágólapról olvas (build-hez nem kell)
    # -                     # stdin-ről olvas (build-hez nem kell)
)

# Debug célú extra opciók, amiket a prepare() automatikusan fűz a
# hibás patchek újrafuttatásához. Ne módosítsd, hacsak nem tudod mit teszel.
_mpatch_debug_opts=(
    -vvvv
    --dry-run
)

# Ha 1-re állítod, a prepare() az ELSŐ hibás patchnél megáll, és
# részletes debug-riportot generál a ${srcdir}/mpatch-debug/-be.
# Ha 0-ra, akkor csak a hibát írja ki, debug nélkül.
_mpatch_debug_on_failure=1

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
    'fixup-warnings.patch'
)

source=("https://us.download.nvidia.com/XFree86/Linux-x86_64/${pkgver}/${_pkg}.run"
        'mhwd-nvidia'
        'nvidia-340xx-utils.install'
        'nvidia-utils.sysusers'
        'nvidia-340xx.rules'
        'series.resolved'
        '20-nvidia.conf'
        'nvidia-340xx-utils.conf'
        'nvidia-340xx-utils-modules-load.conf'
        "${_debian_patches[@]}"
)

# Hash-ek: mind SKIP (9 fix fájl + 89 Debian patch = 98 db), hogy a gyakran
# frissülő Debian patchek és helper fájlok ne okozzanak felesleges build-hibát.
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP'
            'SKIP' 'SKIP')

# =============================================================================
# SYMLINK GENERÁTOR – a .so SONAME-ekhez szükséges linkek létrehozása.
# Ezt a prepare() után minden package_* függvény meghívja.
# =============================================================================
create_links() {
    find "$pkgdir" -type f -name '*.so*' ! -path '*xorg/*' -print0 | while read -d $'\0' _lib; do
        _soname=$(dirname "${_lib}")/$(readelf -d "${_lib}" | grep -Po 'SONAME.*: \[\K[^]]*' || true)
        _base=$(echo ${_soname} | sed -r 's/(.*)\.so.*/\1.so/')
        [[ -e "${_soname}" ]] || ln -s $(basename "${_lib}") "${_soname}"
        [[ -e "${_base}" ]] || ln -s $(basename "${_soname}") "${_base}"
    done
}

# =============================================================================
# SEGÉDFÜGGVÉNYEK – mpatch wrapperek
# =============================================================================

# Az összes opció egy stringgé fűzése – így a prepare() tisztán hívhatja.
_mpatch_cmd() {
    printf '%s ' mpatch "${_mpatch_opts[@]}"
}

# Egy patch alkalmazása. Ha elhasal ÉS _mpatch_debug_on_failure=1,
# akkor automatikusan -vvvv --dry-run-nal újrafuttatja, és a debug
# riportot a ${srcdir}/mpatch-debug/-be másolja.
_mpatch_apply() {
    local _patchfile="$1"
    local _targetdir="$2"
    local _patchname
    _patchname=$(basename "$_patchfile")

    # 1. Alkalmazás – a VALÓDI exit kódot elmentjük, mielőtt bármi felülírná.
    mpatch "${_mpatch_opts[@]}" "$_patchfile" "$_targetdir"
    local _rc=$?

    # 2. Siker → korai visszatérés, debug nem kell.
    if [ "$_rc" -eq 0 ]; then
        return 0
    fi

    # 3. Bukás → hibaüzenet, majd debug riport (ha be van kapcsolva).
    echo "!!! mpatch FAILED (rc=$_rc): $_patchname" >&2

    if [ "${_mpatch_debug_on_failure}" = "1" ]; then
        local _dbgdir="${srcdir}/mpatch-debug"
        mkdir -p "$_dbgdir"
        echo ">>> Debug riport generálása: $_dbgdir/" >&2
        ( cd "$_targetdir" && mpatch "${_mpatch_debug_opts[@]}" \
            "$_patchfile" . ) > "$_dbgdir/${_patchname}.stdout" 2>&1 || true
        find "${_targetdir}" -maxdepth 1 -name 'mpatch-debug-report-*.md' \
            -exec mv {} "$_dbgdir/${_patchname}.report.md" \; 2>/dev/null || true
        echo ">>> Nézd meg: $_dbgdir/${_patchname}.report.md" >&2
        echo ">>> Ha elakadtál: olvasd el a PKGBUILD fejlécében a" >&2
        echo ">>> 'DEBUG WORKFLOW – HA EGY PATCH ELHASAL' részt." >&2
    fi

    # 4. A VALÓDI hibakóddal térünk vissza → a hívó `|| exit 1` lefut.
    return "$_rc"
}

prepare() {
    rm -rf "${_pkg}"
    sh "${_pkg}.run" --extract-only

    cd "${_pkg}"

    cd kernel

    # -----------------------------------------------------------------------
    # 1. Debian patch-sorozat alkalmazása mpatch-csel (series.resolved sorrend)
    # -----------------------------------------------------------------------
    echo ">>> Debian patch-sorozat alkalmazása mpatch-csel (kernel/ könyvtárban)..."
    echo ">>> Opciók: ${_mpatch_opts[*]}"

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
        _mpatch_apply "$_patchfile" . \
            || { echo "!!! PATCH FAILED: $_patch"; exit 1; }
    done < "${srcdir}/series.resolved"

    echo ">>> Mind a $_n patch sikeresen alkalmazva (mpatch)."

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
    # PREEMPT_RT flag beégetése a DKMS make hívásaiba, hogy RT kernelen
# a DKMS automatikus újraépítés is átmenjen (nem csak a prebuilt csomag).
    sed -i 's|^MAKE\[0\]="make |MAKE\[0\]="IGNORE_PREEMPT_RT_PRESENCE=1 make |' dkms.conf
    sed -i 's|; make -C uvm |; IGNORE_PREEMPT_RT_PRESENCE=1 make -C uvm |' dkms.conf
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

    # -----------------------------------------------------------------------
    # modprobe.d: blacklist + softdep (fájlból, echo nélkül)
    # -----------------------------------------------------------------------
    install -Dm644 "${srcdir}/nvidia-340xx-utils.conf" \
        "${pkgdir}/usr/lib/modprobe.d/${pkgname}.conf"

    # -----------------------------------------------------------------------
    # modules-load.d: nvidia-uvm (fájlból, echo nélkül)
    # -----------------------------------------------------------------------
    install -Dm644 "${srcdir}/nvidia-340xx-utils-modules-load.conf" \
        "${pkgdir}/usr/lib/modules-load.d/${pkgname}.conf"

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