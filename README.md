# CraftGit

### Version control for Minecraft instances — and any folder.

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python\&logoColor=white)](https://www.python.org/)
[![pywebview](https://img.shields.io/badge/GUI-pywebview-2B2B2B)](https://pywebview.flowrl.com/)
[![Google Drive](https://img.shields.io/badge/Google%20Drive-optional-4285F4?logo=google-drive\&logoColor=white)](https://drive.google.com/)
[![Platform](https://img.shields.io/badge/Platform-Windows-0078D4?logo=windows\&logoColor=white)](https://www.microsoft.com/windows)
[![Status](https://img.shields.io/badge/Status-Pre--release-orange)](https://github.com/ProgramerPro-arch/CraftGit)

CraftGit is a local version-control and snapshot system designed primarily for Minecraft instances.

It allows you to create named snapshots, compare file changes, restore previous states, automatically create safety backups before restoration, and optionally upload snapshots to Google Drive.

CraftGit is currently in active development and is **not yet an official public release**.

---

## Features

* Named snapshots
* Snapshot restoration
* Automatic backup before restoration
* File change detection
* Detection of added files
* Detection of removed files
* SHA-256 file hashing
* Local snapshot storage
* Backup management
* Minecraft-specific file tracking
* Generic folder support
* Desktop GUI
* CLI/backend architecture
* Optional Google Drive integration
* Automatic Google Drive uploads
* Manual Google Drive uploads
* Configurable remote folder
* Persistent application settings
* Planned Windows `.exe` distribution

---

## How it works

CraftGit stores its repository data inside a hidden `.craftgit` directory in the selected folder.

Example:

```text
MyMinecraftInstance/
├── mods/
├── config/
├── resourcepacks/
├── shaderpacks/
├── datapacks/
├── options.txt
├── servers.dat
└── .craftgit/
    ├── snapshots/
    ├── backups/
    └── ...
```

CraftGit does not require the selected folder to be a Minecraft instance.

Any normal directory can be used as a repository.

---

## Snapshots

A snapshot is a point-in-time copy of the tracked files.

Example:

```text
Before Mod Update
After Mod Update
Working Configuration
Shader Test
Clean Instance
```

Snapshots can be:

* created
* listed
* restored
* deleted
* uploaded to Google Drive

Before restoring a snapshot, CraftGit creates a backup of the current state.

This makes it possible to return to the state that existed immediately before the restoration.

---

## File change detection

CraftGit calculates SHA-256 hashes for files and uses them to detect changes.

The status system can identify:

```text
Added
Removed
Modified
Unchanged
```

This allows changes between the current directory and the latest snapshot to be identified without relying only on timestamps.

---

## Minecraft support

CraftGit is designed with Minecraft instances in mind.

Common Minecraft paths can be tracked, including:

```text
mods/
config/
resourcepacks/
shaderpacks/
datapacks/
options.txt
servers.dat
```

The architecture also allows CraftGit to work with completely generic directories.

---

# Google Drive

Google Drive integration is optional.

It can be used to upload local snapshots as ZIP archives.

Example:

```text
Google Drive
└── CraftGit
    └── MyMinecraftInstance
        ├── snapshot-2026-09-18.zip
        ├── Before-Mod-Update.zip
        └── Clean-Instance.zip
```

## Auto Upload

CraftGit includes an **Auto Upload** configuration section.

Automatic uploading is **disabled by default**.

Connecting a Google account does **not** automatically enable uploads.

Default configuration:

```json
{
  "auto_upload": false,
  "upload_backups": false,
  "google_drive": {
    "enabled": false,
    "folder": "CraftGit"
  }
}
```

The user must explicitly enable:

```text
Automatically upload new snapshots
```

or:

```text
Automatically upload backups
```

Manual uploads remain available even when Auto Upload is disabled.

---

## Google Drive authentication

CraftGit uses Google OAuth 2.0.

The OAuth credentials are kept outside the source repository.

The local token is stored in:

```text
%USERPROFILE%\.craftgit\google_token.json
```

The OAuth client file should be stored locally as:

```text
credentials.json
```

`credentials.json` and OAuth tokens should **never be committed to Git**.

---

## Desktop GUI

CraftGit uses:

* HTML
* CSS
* JavaScript
* pywebview
* Python backend

The GUI is designed as a native-style desktop application while keeping the interface flexible and easy to develop.

Planned interface sections include:

```text
Dashboard
Snapshots
Changes
Auto Upload
Settings
```

---

## Project structure

A simplified project structure:

```text
CraftGit/
├── craftgit.py
├── repository.py
├── google_drive.py
├── requirements.txt
├── README.md
├── LICENSE
├── credentials.json
└── web/
    ├── index.html
    ├── style.css
    └── app.js
```

`credentials.json` is a local OAuth credential file and should not be committed.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/ProgramerPro-arch/CraftGit.git
cd CraftGit
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run CraftGit:

```bash
python craftgit.py
```

---

## Google Drive setup

Google Drive is optional.

To enable it:

1. Create a Google Cloud project.
2. Enable the Google Drive API.
3. Configure OAuth consent.
4. Create a Desktop OAuth client.
5. Download the credentials file.
6. Save it as:

```text
credentials.json
```

7. Start CraftGit.
8. Open **Auto Upload**.
9. Select **Connect Google Drive**.
10. Complete the Google OAuth flow.

Connecting the account alone does not enable automatic uploads.

---

## Command / backend operations

| Operation         | Description                                      |
| ----------------- | ------------------------------------------------ |
| `create snapshot` | Creates a new snapshot                           |
| `list snapshots`  | Lists local snapshots                            |
| `delete snapshot` | Removes a snapshot                               |
| `restore`         | Restores a snapshot                              |
| `list backups`    | Lists restoration backups                        |
| `status`          | Shows file changes                               |
| `upload snapshot` | Manually uploads a snapshot                      |
| `auto upload`     | Automatically uploads new snapshots when enabled |

---

## Data safety

CraftGit is designed to keep the local repository as the primary copy.

When a snapshot is created:

```text
Selected folder
      │
      ▼
Create local snapshot
      │
      ├── Auto Upload OFF
      │       └── Done
      │
      └── Auto Upload ON
              │
              ▼
        Google Drive upload
```

If Google Drive is unavailable, the local snapshot can still be created.

Cloud storage is an additional backup layer, not a replacement for the local repository.

---

# Roadmap

## Core

* [x] Snapshot creation
* [x] Snapshot restoration
* [x] SHA-256 hashing
* [x] Automatic pre-restore backups
* [x] Snapshot deletion
* [x] Backup management
* [x] File change detection
* [ ] Incremental snapshots
* [ ] Snapshot deduplication
* [ ] Improved restore transactions
* [ ] Repository integrity checking

## Minecraft

* [x] Minecraft-oriented file tracking
* [ ] Multiple Minecraft instances
* [ ] Configurable tracked paths
* [ ] Mod metadata
* [ ] Minecraft version detection
* [ ] Mod loader detection
* [ ] Launcher profile support
* [ ] Modpack integration

## Google Drive

* [x] OAuth authentication
* [x] Manual snapshot upload
* [x] Automatic snapshot upload
* [x] Configurable remote folder
* [x] Backup upload support
* [ ] Cloud snapshot browser
* [ ] Cloud restore
* [ ] Upload queue
* [ ] Upload retry system
* [ ] Cloud/local synchronization

## GUI

* [x] Desktop GUI
* [x] Snapshot browser
* [x] Change detection view
* [x] Auto Upload configuration
* [ ] Snapshot comparison viewer
* [ ] Snapshot details
* [ ] Search and filtering
* [ ] Settings page
* [ ] Themes
* [ ] Drag and drop
* [ ] Notifications
* [ ] Upload progress UI

## Distribution

* [ ] Windows `.exe`
* [ ] Portable version
* [ ] Windows installer
* [ ] Automatic updates
* [ ] First public release

---

# Project status

**Pre-release — active development**

CraftGit is currently being developed and tested.

There is currently no official public Windows `.exe` release.

The project structure, GUI and backend are still subject to change before the first public release.

---

# License

CraftGit is distributed under the:

**CraftGit Attribution & Commercial License v1.0**

The license permits non-commercial use, modification, forks, branches and redistribution subject to the attribution requirements.

Commercial use requires prior written permission from the copyright holder.

Copyright holder:

```text
Piotrekos69
```

See [`LICENSE`](LICENSE) for the complete terms.

> This is a custom license and is not intended to be an SPDX-standard open-source license.

---

# Author

**Piotrekos69**

CraftGit is developed as an independent project focused on practical version control for Minecraft instances and local game data.

---

# Repository

Source code:

https://github.com/ProgramerPro-arch/CraftGit

CraftGit is currently a development project and is not yet considered a stable public release.
