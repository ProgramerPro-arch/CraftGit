<div align="center">

# CraftGit

**Version control for Minecraft instances.**

[![Python](https://img.shields.io/badge/Python-3.11%2B-blue?logo=python\&logoColor=white)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?logo=windows)](#requirements)
[![Status](https://img.shields.io/badge/Status-Pre--release-orange)](#project-status)
[![GUI](https://img.shields.io/badge/GUI-pywebview-blue)](#interface)
[![License](https://img.shields.io/badge/License-Custom-red)](#license)

</div>

---

## About

CraftGit is a local version control system designed specifically for Minecraft instances.

It creates snapshots of selected Minecraft files and directories, allowing changes to be reviewed and previous states to be restored without manually copying an entire instance.

CraftGit combines a Python backend with a desktop interface built using HTML, CSS, JavaScript, and pywebview.

The project is primarily designed for modded Minecraft instances.

---

## Features

* Named snapshots
* Snapshot restoration
* Automatic backup before restoration
* File change detection
* Detection of added and removed files
* SHA-256 hashing
* Local snapshot storage
* Minecraft-specific file tracking
* Desktop GUI
* CLI support
* Planned Windows `.exe` distribution

---

## Tracked Files

The default configuration tracks:

```text
mods/
config/
resourcepacks/
shaderpacks/
datapacks/

options.txt
servers.dat
```

Tracked paths will become configurable in a future version.

---

## Interface

CraftGit uses a web-based frontend displayed inside a native desktop window through **pywebview**.

### Frontend

```text
HTML
CSS
JavaScript
```

### Backend

```text
Python
```

The backend is responsible for filesystem operations, hashing, snapshot management, restoration, and application logic.

The frontend communicates with the Python backend through the application's local API.

### Screenshots

Screenshots will be added when the interface reaches a stable development state.

#### Dashboard

![CraftGit Dashboard](docs/screenshots/dashboard.png)

#### Snapshots

![CraftGit Snapshots](docs/screenshots/snapshots.png)

#### Changes

![CraftGit Changes](docs/screenshots/changes.png)

---

## Installation

### Public Release

CraftGit is currently **not publicly released**.

Official Windows `.exe` builds will be published through GitHub Releases when the project reaches its first stable release.

### From Source

Clone the repository:

```bash
git clone https://github.com/ProgramerPro-Arch/CraftGit.git
cd CraftGit
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run CraftGit:

```bash
python craftgit.py
```

The source structure and required dependencies may change during development.

---

## Requirements

### End Users

| Requirement         | Status                  |
| ------------------- | ----------------------- |
| Windows             | Planned                 |
| Standalone `.exe`   | Planned                 |
| Python installation | Not required for `.exe` |
| Internet connection | Not required            |

### Development

| Requirement | Version     |
| ----------- | ----------- |
| Python      | 3.11+       |
| pywebview   | Required    |
| Git         | Recommended |
---

## Commands

The graphical interface is intended to be the primary user interface.

The CLI is currently intended mainly for development and automation.

| Command              | Description              |
| -------------------- | ------------------------ |
| `init`               | Initialize CraftGit      |
| `snapshot <name>`    | Create a snapshot        |
| `list`               | List available snapshots |
| `status`             | Display detected changes |
| `restore <snapshot>` | Restore a snapshot       |

Example:

```bash
python craftgit.py snapshot "Before mod update"
```

---

## Storage

CraftGit stores its repository directly inside the Minecraft instance:

```text
.minecraft/
└── .craftgit/
    └── snapshots/
        ├── 2026-09-16-before-update/
        │   ├── manifest.json
        │   ├── mods/
        │   └── config/
        │
        └── 2026-09-16-stable/
            ├── manifest.json
            ├── mods/
            └── config/
```

Each snapshot contains a manifest describing the files included in that snapshot.

SHA-256 hashes are used to detect modifications and verify file state.

Before a snapshot is restored, CraftGit creates a backup of the current instance state.

---

## Workflow

A typical workflow:

```text
Create Snapshot
      │
      ▼
Modify Minecraft Instance
      │
      ▼
Check Changes
      │
      ├── No Issues
      │
      └── Something Changed
               │
               ▼
        Restore Snapshot
               │
               ▼
        Previous State
```

All snapshot data is stored locally.

CraftGit does not require a remote server or cloud storage for its core functionality.

---

## Project Structure

```text
CraftGit/
├── src/
│   ├── backend/
│   │   ├── snapshots/
│   │   ├── filesystem/
│   │   └── hashing/
│   │
│   └── gui/
│       ├── index.html
│       ├── css/
│       └── js/
│
├── docs/
│   └── screenshots/
│       ├── dashboard.png
│       ├── snapshots.png
│       └── changes.png
│
├── craftgit.py
├── requirements.txt
├── LICENSE
├── README.md
└── .gitignore
```

The project structure is subject to change during development.

---

## Roadmap

### Core

* [x] Basic snapshot creation
* [x] Snapshot restoration
* [x] SHA-256 hashing
* [x] Pre-restore backups
* [ ] Snapshot comparison
* [ ] Incremental snapshots
* [ ] Deduplicated storage
* [ ] Improved change detection
* [ ] Improved deleted-file handling

### Minecraft

* [ ] Multiple instance support
* [ ] Configurable tracked paths
* [ ] Mod metadata
* [ ] Mod version tracking
* [ ] Launcher detection
* [ ] Modpack support
* [ ] Instance profiles

### GUI

* [ ] Desktop interface
* [ ] Snapshot browser
* [ ] Change viewer
* [ ] Settings
* [ ] Dark / light themes
* [ ] Drag & drop
* [ ] Notifications

### Distribution

* [ ] Windows `.exe`
* [ ] Portable version
* [ ] Installer
* [ ] Automatic updates
* [ ] First public release

---

## Privacy

CraftGit is designed around local operation.

The core application does not require:

* an online account;
* cloud storage;
* uploading Minecraft files;
* a permanent internet connection.

Minecraft files and snapshots remain on the user's machine unless manually copied elsewhere.

---

## Project Status

**Pre-release — development**

CraftGit is currently under active development and is **not yet available as a public release**.

There are currently no official public `.exe` builds.

The following components may change before the first release:

* GUI
* snapshot format
* internal APIs
* CLI
* project structure
* configuration format
* storage format

The first official version will be published through GitHub Releases once development and testing are complete.

---

## License

CraftGit is distributed under the **CraftGit Attribution & Commercial License v1.0**.

Non-commercial use, modification, forks, branches, and redistribution are permitted according to the license terms.

**Commercial use requires prior permission from the copyright holder.**

Required author and project attribution must be preserved in derivative works.

See [`LICENSE`](LICENSE) for the complete license terms.

---

## Author

**Piotrekos69**

---

<div align="center">

CraftGit is an independent project.

Not affiliated with Mojang Studios, Microsoft, Modrinth, or CurseForge.

</div>
