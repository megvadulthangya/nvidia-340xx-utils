# Harvest Index — 2026-11-27 01:07:23 

## TL;DR

- **State:** ❗0 failed · 🔍0 suspicious · ⚠10 warnings · ✅0 clean · 🚫0 not-built
- **Action needed:** none — no actionable cross-build warnings
- **Informational:** 4 build-system signature(s) — no driver fix needed

## Overview

- **Diag root:** `/build/sources`
- **Harvest:**   `/build/harvest`
- **Branches:**  340xx
- **Builds:** 10 — ❗0 failed, 🔍0 suspicious, ⚠10 warn, ✅0 clean, 🚫0 not-built
- **Warning signatures:** 4 total — 0 actionable across multiple builds, 4 informational, 0 unique to one build
- **Suspicious signatures:** 0  ·  **integrity issues:** 0 builds  ·  **integrity notes:** 0 builds

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
| 2 | 340xx | normal | 6.12.117-1-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 3 | 340xx | normal | 6.18.63-3-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 0 |  |
| 4 | 340xx | normal | 6.6.162-2-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 5 | 340xx | normal | 7.3.4-3-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 0 |  |
| 6 | 340xx | normal | 7.4.0-rc2-3-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 0 |  |
| 7 | 340xx | normal | 7.4.0-rc4-next-20261124-1-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 0 |  |
| 8 | 340xx | rt | 6.1.190-2-rt70-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 9 | 340xx | rt | 6.12.116-1-rt22-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |
| 10 | 340xx | rt | 6.6.159-2-rt82-MANJARO | 340.108 | ⚠ warnings | 0 | 2 / 2 | 0 | 1 |  |

## 🔁 Cross-build warning signatures

Warnings appearing in **more than one build**. Fixing the top signature fixes the most builds at once.

### 🎯 Actionable (driver source)

_None._

### ⚙️ Informational (build system / Makefile)

| # | Builds | Hits | Signature | Branches |
|---|-------:|-----:|-----------|----------|
| 1 | 6 | 6 | `warning: ignoring old recipe for target '<path>'` | 340xx/normal, 340xx/rt |
| 2 | 6 | 6 | `warning: overriding recipe for target '<path>'` | 340xx/normal, 340xx/rt |
| 3 | 4 | 4 | `warning: ignoring old recipe for target 'Module.symvers'` | 340xx/normal |
| 4 | 4 | 4 | `warning: overriding recipe for target 'Module.symvers'` | 340xx/normal |

## 🧩 Unique to one build

Warnings in exactly **one** build. Usually kernel- or config-specific.

_No unique-to-one-build warnings._

---
_End of index. Per-build detail files live in the harvest tree._
