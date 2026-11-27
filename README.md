# Harvest Index — 2026-11-27 01:11:30 

## TL;DR

- **State:** ❗1 failed · 🔍0 suspicious · ⚠9 warnings · ✅0 clean · 🚫0 not-built
- **Action needed (4):**
    - 7 builds · 28 hits · `warning: Please avoid flushing system-wide workqueues. [-Wattribute-warning]`
    - 3 builds · 3 hits · `warning: '__fbdev_warning' defined but not used [-Wunused-variable]`
    - 3 builds · 3 hits · `warning: 'nv_fbdev_failure_detected' defined but not used [-Wunused-variable]`
    - … and 1 more (see `## 🔁 Cross-build warning signatures`)
- **Informational:** 4 build-system signature(s) — no driver fix needed

## Overview

- **Diag root:** `/build/sources`
- **Harvest:**   `/build/harvest`
- **Branches:**  340xx
- **Builds:** 10 — ❗1 failed, 🔍0 suspicious, ⚠9 warn, ✅0 clean, 🚫0 not-built
- **Warning signatures:** 8 total — 4 actionable across multiple builds, 4 informational, 0 unique to one build
- **Suspicious signatures:** 2  ·  **integrity issues:** 0 builds  ·  **integrity notes:** 0 builds

## Legend

| Symbol | Status | Meaning |
|:------:|--------|---------|
| ❗ | failed     | make.log contains real errors — **blocker** |
| 🔍 | suspicious | no errors, but suspicious lines or integrity issues |
| ⚠  | warnings   | built, no errors, non-noise warnings to review |
| ✅ | clean      | built, no errors, only known noise |
| 🚫 | not-built  | no make.log at all |
| 🧪 | utils      | userspace utils failure, mpatch debug archived |

Per-build detail lives in the harvest tree, one directory per kernel: `00-header.txt`, `01-errors.txt`, `02-warnings.txt`, `03-noise.txt`, `04-suspicious.txt`, `summary.txt`.

The raw `make.log` is also archived in every build directory as `make.log.zst` (or `.gz` / plain).

## Status table

| # | Branch | Variant | Kernel | Driver | Status | Err | Clean (uniq/total) | Susp | Noise | Integ |
|---|--------|---------|--------|--------|:------:|----:|-------------------:|-----:|------:|:-----:|
| 1 | 340xx | normal | 6.1.192-2-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 2 | 340xx | normal | 6.12.117-1-MANJARO | 340.108 | ⚠ warnings | 0 | 3 / 6 | 0 | 1 |  |
| 3 | 340xx | normal | 6.18.63-3-MANJARO | 340.108 | ⚠ warnings | 0 | 4 / 7 | 0 | 0 |  |
| 4 | 340xx | normal | 6.6.162-2-MANJARO | 340.108 | ⚠ warnings | 0 | 3 / 6 | 0 | 1 |  |
| 5 | 340xx | normal | 7.3.4-3-MANJARO | 340.108 | ⚠ warnings | 0 | 6 / 9 | 0 | 0 |  |
| 6 | 340xx | normal | 7.4.0-rc2-3-MANJARO | 340.108 | ⚠ warnings | 0 | 6 / 9 | 0 | 0 |  |
| 7 | 340xx | normal | linux-next-nvidia-340xx | — | ❗ failed | 12 | 2 / 2 | 3 | 0 |  |
| 8 | 340xx | rt | 6.1.190-2-rt70-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 9 | 340xx | rt | 6.12.116-1-rt22-MANJARO | 340.108 | ⚠ warnings | 0 | 3 / 6 | 0 | 1 |  |
| 10 | 340xx | rt | 6.6.159-2-rt82-MANJARO | 340.108 | ⚠ warnings | 0 | 3 / 6 | 0 | 1 |  |

## ❗ Failures — fix these first

Full error list in each build's `01-errors.txt`. Excerpt below.

### 340xx / normal / linux-next-nvidia-340xx — ?  (12 errors)

Path: `340xx/normal/linux-next-nvidia-340xx`

```
216: nv.c:935:9: error: implicit declaration of function ‘rdmsr’; did you mean ‘rdmsrq’? [-Wimplicit-function-declaration]
227: make[4]: *** [/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/scripts/Makefile.build:321: nv.o] Error 1
229: make[3]: *** [/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/Makefile:2252: .] Error 2
230: make[2]: *** [/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/Makefile:248: __sub-make] Error 2
232: make[1]: *** [Makefile:248: __sub-make] Error 2
234: make: *** [Makefile:225: nvidia.ko] Error 2
255: make[5]: *** No rule to make target 'Makefile'.  Stop.
256: make[4]: *** [/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/Makefile:2252: .] Error 2
257: make[3]: *** [/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/Makefile:248: __sub-make] Error 2
259: make[2]: *** [Makefile:248: __sub-make] Error 2
261: make[1]: *** [Makefile:225: nvidia.ko] Error 2
263: make: *** [Makefile:226: ../Module.symvers] Error 2
```

## 🔍 Suspicious signatures

Lines that are **not** errors and **not** warnings, but contain keywords that often indicate real problems (missing files, permissions, OOM, crashes, missing deps).

| # | Builds | Hits | Signature | Branches |
|---|-------:|-----:|-----------|----------|
| 1 | 1 | 2 | `mkdir: cannot create directory '.tmp_NNN': Permission denied` | 340xx/normal |
| 2 | 1 | 1 | `/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/scripts/Makefile.build:38: Makefile: No such file or directory` | 340xx/normal |

<details><summary>Context excerpts (first few hits per signature)</summary>

**`mkdir: cannot create directory '.tmp_NNN': Permission denied`**

```
[340xx/normal/linux-next-nvidia-340xx] 250: mkdir: cannot create directory ‘.tmp_20382’: Permission denied
[340xx/normal/linux-next-nvidia-340xx] 251: mkdir: cannot create directory ‘.tmp_20385’: Permission denied
[340xx/normal/linux-next-nvidia-340xx] 254: /usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/scripts/Makefile.build:38: Makefile: No such file or directory
```

**`/usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/scripts/Makefile.build:38: Makefile: No such file or directory`**

```
[340xx/normal/linux-next-nvidia-340xx] 250: mkdir: cannot create directory ‘.tmp_20382’: Permission denied
[340xx/normal/linux-next-nvidia-340xx] 251: mkdir: cannot create directory ‘.tmp_20385’: Permission denied
[340xx/normal/linux-next-nvidia-340xx] 254: /usr/lib/modules/7.4.0-rc4-next-20261124-1-MANJARO/build/scripts/Makefile.build:38: Makefile: No such file or directory
```

</details>

## 🔁 Cross-build warning signatures

Warnings appearing in **more than one build**. Fixing the top signature fixes the most builds at once.

### 🎯 Actionable (driver source)

| # | Builds | Hits | Signature | Branches |
|---|-------:|-----:|-----------|----------|
| 1 | 7 | 28 | `warning: Please avoid flushing system-wide workqueues. [-Wattribute-warning]` | 340xx/normal, 340xx/rt |
| 2 | 3 | 3 | `warning: '__fbdev_warning' defined but not used [-Wunused-variable]` | 340xx/normal |
| 3 | 3 | 3 | `warning: 'nv_fbdev_failure_detected' defined but not used [-Wunused-variable]` | 340xx/normal |
| 4 | 3 | 3 | `warning: ignoring return value of 'refcount_sub_and_test' declared with attribute 'warn_unused_result' [-Wunused-result]` | 340xx/normal |

### ⚙️ Informational (build system / Makefile)

| # | Builds | Hits | Signature | Branches |
|---|-------:|-----:|-----------|----------|
| 1 | 6 | 6 | `warning: ignoring old recipe for target '<path>'` | 340xx/normal, 340xx/rt |
| 2 | 6 | 6 | `warning: overriding recipe for target '<path>'` | 340xx/normal, 340xx/rt |
| 3 | 3 | 3 | `warning: ignoring old recipe for target 'Module.symvers'` | 340xx/normal |
| 4 | 3 | 3 | `warning: overriding recipe for target 'Module.symvers'` | 340xx/normal |

## 🧩 Unique to one build

Warnings in exactly **one** build. Usually kernel- or config-specific.

_No unique-to-one-build warnings._

---
_End of index. Per-build detail files live in the harvest tree._
