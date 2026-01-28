---
name: ohos-one-stop-build
description: One-stop workflow to build a HarmonyOS module, install the HAP, launch the app, clear logs, and fetch fresh logs from hilog. Use this skill whenever asked to compile/build/run/install/start/logs for an OHOS app or module.
license: Internal use only
allowed-tools: [Bash]
---

created by vanicliu @ 2026-01-19 15:38:17

## When to use this skill
Use this skill for:
- One-command build/install/run on HarmonyOS
- Reproducing IDE "Run" behavior via CLI
- Clearing and fetching hilog after install/run
- Standardizing hvigorw + hdc workflows

## How to use this skill

1) **Confirm or set configuration**
   - PROJECT_ROOT
   - HVIGORW
   - HDC
   - MODULE / PRODUCT
   - BUNDLE / ABILITY
   - HAP_PATH
   - LOG_TAG / LOG_LINES

2) **Auto-detect tools if not set** (preferred)
   - Use `command -v` first
   - Fall back to known default paths
   - Report the final resolved paths
   - If multiple candidates exist, pick the first valid executable

3) **Run the core workflow** (in order)
```
$HVIGORW assembleHap -p product=$PRODUCT -p module=$MODULE --daemon
$HDC shell hilog -r
$HDC install -r "$HAP_PATH"
$HDC shell aa force-stop $BUNDLE
$HDC shell aa start -a $ABILITY -b $BUNDLE
$HDC shell hilog -v time -T $LOG_TAG -z $LOG_LINES
```

4) **Report results**
   - Build success or error
   - Install result
   - Start result
   - Latest logs (tail)

## Configuration (defaults used in this repo)
- PROJECT_ROOT: /Users/vanicliu/Projects/HMProjects/FileComparator
- HVIGORW: /Users/vanicliu/Projects/ohos-build/command-line-tools-6.0.1/bin/hvigorw
- HDC: /Users/vanicliu/Library/OpenHarmony/Sdk/20/toolchains/hdc
- MODULE: entry
- PRODUCT: default
- BUNDLE: com.example.filecomparator
- ABILITY: EntryAbility
- HAP_PATH: entry/build/default/outputs/default/entry-default-unsigned.hap
- LOG_TAG: FileComparatorTag
- LOG_LINES: 500

## Examples
- examples/one-stop-run.md
- examples/auto-detect.md
- examples/naming.md

## Optional variants
- Build only:
```
$HVIGORW assembleHap -p product=$PRODUCT -p module=$MODULE --daemon
```

- Install only:
```
$HDC install -r "$HAP_PATH"
```

- Start only (no reinstall):
```
$HDC shell aa force-stop $BUNDLE
$HDC shell aa start -a $ABILITY -b $BUNDLE
```

- Fetch logs without tag filter:
```
$HDC shell hilog -v time -z $LOG_LINES
```

## Troubleshooting
- hvigorw not found: verify HVIGORW path or add to PATH
- hdc not found: verify HDC path or add to PATH
- No device: check `hdc list targets`
- HAP missing: verify HAP_PATH after build
- Signing warning: expected for unsigned debug HAP; configure signing if needed

## Keywords
ohos, harmonyos, hvigorw, hdc, assembleHap, install, run, start, hilog, logs
