# JoyCtl Android

JoyCtl Android is an on-device Android implementation based on [hexwander/joyctl](https://github.com/hexwander/joyctl). While the original desktop version controls rooted Xiaomi devices via PC-side ADB, this project reads and writes directly to the Joyose cloud control database on the device using `su`.

## Features

- **Bottom Navigation**: Switch between Device, Cloud, Rules, and Logs tabs with ripple touch effects; clicking buttons no longer disables the entire page.
- **Symmetric Device Layout**: Modeled after the PC version with Pull/Push and Freeze/Restore actions, plus status refresh at the bottom.
- **Device Info Badges**: Clear badge indicators for Model, Codename, OS Version, Root Status, and Cloud Control Status.
- **Smart Cloud Fetching**: Prioritizes pulling configs matching the local Joyose version; if unavailable, it probes for compatible configs based on your device model.
- **PC-Style Rule Cards**: Displays title, description, and game selection. Supports multi-selection; rules are only written after tapping "Modify". "All Games" only alters game entries already present in your Joyose config.
- **Relax Thermal Throttling for All Games**: Supports custom temperature thresholds and multi-game selection; values are converted to Joyose PID format before writing (e.g., `47` → `47:48`), modifying only existing PID policy groups.
- **Feature Detection & Sync**: Synchronizes FPS lock, thermal PID, migt prime core baselines, and package name changes. The Logs page displays step-by-step success/failure details with one-tap copy.
- **Baseline Comparison**: Automatically fetches unmodified cloud configs matching your local Joyose version as a baseline after pulling or importing configs; saving rules will not alter the baseline.
- **Card-Based Rule List**: Displays module type and index. Tap to switch between cards; alerts will notify you of unsaved changes.
- **Comprehensive Cloud Pulling**: Loads both `booster_config` and `common_config` simultaneously (for rules with `status=1` containing valid data).
- **Collapsible Guides**: Help and documentation are neatly tucked under an ⓘ icon at the top right of each panel.
- **Database Management**: Directly reads and writes `teg_config.db` under `com.xiaomi.joyose`.
- **Safety First**: Automatically creates a `.joyctl.bak` backup before pushing, with post-push readback verification.
- **Freeze/Restore Joyose MCC**: Toggle cloud control on/off via `persist.sys.sc_allow_conn=0/1`.
- **Restore Official Joyose (Emergency Recovery)**: Clears data for Joyose and related system apps, re-enables cloud control broadcast receivers, and triggers a boot completed broadcast.

## Prerequisites

- Xiaomi / Redmi / POCO devices.
- Root access (`su` must be accessible to third-party apps via Magisk, KernelSU, or APatch).
- Modifying system cloud control configurations may impact thermal behavior, battery life, and system stability. **Always make a backup beforehand.**

## Build

Release APKs are built, signed, and published automatically via GitHub Actions whenever a version tag matching `v*` is pushed.

## Credits & Acknowledgments

- **Original Android Port**: [308532806/joyctl-android](https://github.com/308532806/joyctl-android) by [@308532806](https://github.com/308532806)
- **Original Desktop Tool**: [hexwander/joyctl](https://github.com/hexwander/joyctl) by [@hexwander](https://github.com/hexwander)
