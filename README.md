UO Outlands AppImage is a Linux AppImage that downloads GE Proton and the official Ultima Online Outlands launcher from https://uooutlands.com on first run. It keeps the runtime, launcher, logs, and compatibility data in one user directory so the install is easier to remove and easier to inspect when something fails.

## Why

This project exists because Outlands is a Windows game client and the Linux setup steps are otherwise manual. The AppImage puts the download, Proton setup, launch path, and release packaging behind one file and one build command.

## How

On first run the AppImage checks that the machine is x86_64, checks that the data directory is writable, checks that enough disk space is available, and prevents a second copy from touching the same data directory at the same time. It then downloads GE Proton and the official Outlands launcher, checks that the Proton archive is a real tarball, checks that the launcher looks like a Windows executable, creates a dedicated compatdata directory, applies the needed Wine override, and starts the launcher.

Later runs reuse the same data directory and go straight to launch. Downloads are written to temporary files first and only moved into place after the download completes. Each release also ships with a sha256 file so the downloaded AppImage can be checked before it is run.

The default data directory is shown below.

```text
~/.local/share/uooutlands/
```

You can move that data somewhere else by setting `UOOUTLANDS_DATA_DIR` before launch.

```bash
UOOUTLANDS_DATA_DIR=/path/to/uooutlands ./UO-Outlands-x86_64.AppImage
```

## Install

<details open>
<summary>Automatic</summary>

Get the latest `UO-Outlands-x86_64.AppImage` and the matching `UO-Outlands-x86_64.AppImage.sha256` from Releases. Check the download first.

```bash
sha256sum -c UO-Outlands-x86_64.AppImage.sha256
```

Make the AppImage executable if your browser cleared that bit and run it.

```bash
chmod +x UO-Outlands-x86_64.AppImage
./UO-Outlands-x86_64.AppImage
```

</details>

<details>
<summary>Manual</summary>

Clone the repository and run the build script.

```bash
git clone https://github.com/Hezkore/uo-outlands.git
cd uo-outlands
./build.sh
```

The host system needs `tar`. The build uses the bundled `zenity` runtime when possible and falls back to terminal output when no GUI dialog can be shown.

</details>

