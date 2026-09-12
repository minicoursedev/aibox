# AIBox

**English** | [繁體中文](README.zh-TW.md)

AIBox uses a physical device's lights to signal when an AI response ends or an approval is requested. Shake or sound events let the desktop app open the corresponding conversation.

## Repositories

| Repository | Responsibility |
|---|---|
| [aibox-mac](https://github.com/minicoursedev/aibox-mac) | macOS menu bar app, notifications, SSH connection management, and BLE |
| [aibox-firmware](https://github.com/minicoursedev/aibox-firmware) | XIAO nRF52840 Sense firmware, LEDs, and sensors |
| [aibox-remote](https://github.com/minicoursedev/aibox-remote) | Python scripts for installing and forwarding remote notifications |
| [aibox-spec](https://github.com/minicoursedev/aibox-spec) | Shared specifications, protocols, and validation records |

A Windows app has not been created yet. This repository is the integration entry point and pins each component to a specific commit using Git submodules.

## Clone the complete workspace

All components are public repositories. Clone over HTTPS without configuring a GitHub SSH key.

```sh
git clone --recurse-submodules https://github.com/minicoursedev/aibox.git
cd aibox
```

After updating an existing checkout, run:

```sh
git submodule update --init --recursive
```

## Development and validation

```sh
cd aibox-mac
swift test
zsh scripts/build-app.sh
```

From the workspace root, run the remote tests with `python3 aibox-remote/tests/test_notify.py` and the firmware host tests with `bash aibox-firmware/tests/run.sh`.

The Mac repository also references `aibox-remote` as a submodule at `Sources/AIBoxCore/Remote`, so it can be cloned and built independently. After changing the remote scripts, update both the Mac submodule and this entry point to the same commit.

Commit and push changes in each component repository first, then commit the updated submodule references here. An entry point commit records a set of component versions; it does not establish that the complete hardware workflow has been verified. See aibox-spec for physical device validation records.

## Releases

Source code is currently available; no version tags or GitHub Releases have been created yet. Components may publish app or firmware releases independently in the future, with compatible versions and download links recorded here.
