# Win11 Update Block Notes

Short reference notes on how to stop Windows 11 feature update prompts (like 24H2) using the command line. Created as a quick guide for future setup, troubleshooting, or reinstall scenarios.

## Overview

Sometimes Windows repeatedly prompts for a major feature update even when you’re not ready to upgrade. This guide explains a simple registry-based method to stay on your current Windows 11 release while still receiving regular security updates.

This approach is especially useful on Windows Home editions where Group Policy Editor is not available.

## Method: Block Feature Update via Registry

### 1. Open Command Prompt as Administrator

* Open Start Menu
* Type `cmd`
* Right-click Command Prompt
* Select **Run as administrator**

### 2. Set Target Windows Version

Run:

```
reg add HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate /v TargetReleaseVersion /t REG_DWORD /d 1 /f
```

Then:

```
reg add HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate /v TargetReleaseVersionInfo /t REG_SZ /d 23H2 /f
```

Replace `23H2` with whatever Windows version you want to remain on.

### 3. Restart the Computer

This applies the policy and should stop feature update prompts.

## Reverting the Change

If you decide to upgrade later:

```
reg delete HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate /f
```

Restart afterward to restore normal update behavior.

## Notes

* This blocks major feature updates only.
* Security updates should continue normally.
* Useful if hardware constraints (like EFI partition size) prevent upgrading immediately.
* Always keep backups before modifying system policies or partitions.

## Author

**Purva Patel**
