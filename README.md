# Community Package Groups

<p align="center">
  <img src="https://img.shields.io/badge/Arch-Linux-1793D1.svg?logo=arch-linux" alt="Arch Linux"/>
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License"/>
</p>

This repository contains package group definitions for the Community Manjaro repositories. These groups allow users to install multiple related packages with a single command.

## What are Package Groups?

Package groups in Arch/Manjaro allow you to define collections of packages that can be installed together. When users install a group (e.g., `pacman -S comm-hyprland`), all packages within that group will be installed automatically.

Unlike meta-packages, groups don't require creating empty packages - they are simply definitions in the repository database.

## Repository Structure

```
/
├── groups/
│   ├── testing/  # Package groups for testing repository
│   │   ├── comm-i3wm.group
│   │   ├── comm-hyprland.group
│   │   ├── comm-openbox.group
│   │   └── ...
│   └── stable/   # Package groups for stable repository
│       ├── comm-i3wm.group
│       ├── comm-hyprland.group
│       ├── comm-openbox.group
│       └── ...
└── README.md
```

## Group File Format

Each `.group` file defines a single package group. The format is:

```
@group-name
package1
package2
package3
...
```

### Examples:

#### `groups/testing/comm-i3wm.group`:
```
@comm-i3wm
i3-wm
i3status
i3blocks
dmenu
picom
nitrogen
rofi
dunst
xfce4-terminal
```

#### `groups/testing/comm-hyprland.group`:
```
@comm-hyprland
hyprland
waybar
wofi
wlogout
swappy
slurp
grim
kitty
polkit-kde-agent
```

#### `groups/testing/comm-openbox.group`:
```
@comm-openbox
openbox
obconf
obmenu-generator
tint2
pcmanfm
nitrogen
rofi
volumeicon
network-manager-applet
```

## How to Add or Modify Groups

1. Fork this repository
2. Create/modify the appropriate `.group` file in the correct directory (`groups/testing/` or `groups/stable/`)
3. Submit a pull request with your changes
4. Once merged, the groups will be automatically updated in the repository database during the next package build

### Guidelines for Group Files:

- Group names should be prefixed with `comm-` (e.g., `comm-hyprland`)
- Group files should be named after the group (e.g., `comm-hyprland.group`)
- One group per file
- Only include packages that are related and likely to be installed together
- Check that all packages in the group exist in the repository

## Integration with CI/CD

This repository is automatically pulled during the package build process in our CI/CD pipeline. When a package is built and the repository database is updated, the package groups defined here are included in the database.

No manual synchronization is required - just maintain the group definitions in this repository.

## Testing Groups Locally

To test a group locally, you can use the `--group` option with `repo-add`:

```bash
repo-add --group /path/to/your-group.group your_repo.db.tar.gz *.pkg.tar.zst
```
