[🇸🇰 Slovensky](README.md) | [🇬🇧 English](README_EN.md)

# Arcade-101 – Game Controls

Game control configurations for the Waveshare Arcade-101-1P arcade cabinet, powered by a Raspberry Pi 3 and Batocera Linux.

## Repository purpose

This repository backs up and helps restore custom game control configurations for RetroArch and the DOSBox Pure emulator.

It contains configuration files only. It does not include game ROMs, BIOS files, or passwords.

## Supported games

| Game | System | Configuration |
| --- | --- | --- |
| Commander Keen 1 | MS-DOS | Shared DOSBox Pure profile |
| Commander Keen 4 | MS-DOS | `padto.keys` and custom remap |
| Wolfenstein 3D | MS-DOS | Custom remap |
| Heretic | MS-DOS | `padto.keys` and custom remaps |
| Dyna Blaster | MS-DOS | Custom remap |
| Duke Nukem 1 | MS-DOS | Custom `DukeNukem1.pc.rmp` remap |
| Duke Nukem 2 | MS-DOS | Shared DOSBox Pure profile |
| Duke Nukem 3D | MS-DOS | Working controls |
| DOOM 1 Shareware | PrBoom | Default controls |
| DOOM 2: Hell on Earth | PrBoom | Default controls |

## Commander Keen 4

Verified arcade cabinet controls:

- Joystick – character movement
- Blue button – jump
- Yellow button – shoot
- Green button – POGO stick
- White button – pause

The controls were also tested after restarting the game.

## Repository structure

- `retroarch/DOSBox-pure/` – RetroArch control remap profiles
- `dos/CommanderKeen4.pc/padto.keys` – Commander Keen 4 controls
- `dos/Heretic.pc/padto.keys` – Heretic controls

## Configuration locations in Batocera

RetroArch remaps:

`/userdata/system/configs/retroarch/config/remaps/DOSBox-pure/`

Commander Keen 4 configuration:

`/userdata/roms/dos/CommanderKeen4.pc/padto.keys`

Heretic configuration:

`/userdata/roms/dos/Heretic.pc/padto.keys`

## Restoring controls

1. Back up the current configuration files on Batocera.
2. Copy the required files into their respective directories.
3. Restart the affected game.
4. Verify joystick and button operation.

Note: Some DOS games launch through `dosbox.bat`. RetroArch may therefore use the shared `dosbox.rmp` profile. Before restoring a configuration, check which remap the game actually loads.

## Hardware

- Waveshare Arcade-101-1P
- Raspberry Pi 3 Model B
- GPIO joystick and arcade buttons
- Batocera Linux 43.1
- DOSBox Pure / RetroArch

## Note

These configurations are intended for the specific wiring of this arcade cabinet's controls.

If the GPIO buttons are wired differently, the mapping may need to be adjusted.

## Default Arcade-101 settings

The repository also includes the arcade cabinet's basic controller and audio settings.

### Batocera main menu controls

File:

`batocera/emulationstation/gpio-controller.xml`

Contains the mapping for `GPIO Custom Controller 1`:

- Joystick and main menu navigation
- Colored arcade buttons
- START and SELECT buttons
- HOTKEY button

This is an extract containing a single section from the original `es_input.cfg`. To restore it, insert the section into the existing `/userdata/system/configs/emulationstation/es_input.cfg` file. **Do not replace the entire file with this snippet.**

### Default audio settings

File:

`batocera/arcade-settings.conf`

Contains:

- WM8960 audio device
- 65% volume
- Main menu background music enabled
- Emulator exit settings

These lines belong in:

`/userdata/system/batocera.conf`

Before adding them, back up the existing file and check for duplicate settings.

### Exiting games

On the Arcade-101, the following combination is used:

**HOTKEY + green button**

This has been verified with RetroArch and selected systems, especially MS-DOS and Nintendo NES.

### Security

The repository does not contain game ROMs, passwords, or the complete `batocera.conf` file.

Always back up the existing configuration before restoring settings.

## Duke Nukem trilogy

The following games have been tested on the Arcade-101:

| Game | System | Status |
| --- | --- | --- |
| Duke Nukem 1 | MS-DOS | Working custom controls |
| Duke Nukem 2 | MS-DOS | Working default DOSBox Pure controls |
| Duke Nukem 3D | MS-DOS | Playable |

### Duke Nukem 1 – controls

Verified GPIO joystick and arcade button mappings:

| Control | Action | Key |
| --- | --- | --- |
| Joystick left | Move left | D |
| Joystick right | Move right | G |
| Joystick up | Open doors | R |
| Blue button | Shoot | Numpad 4 |
| Yellow button | Jump | Numpad 5 |

Working configuration:

`retroarch/DOSBox-pure/DukeNukem1.pc.rmp`

In Batocera, it belongs in:

`/userdata/system/configs/retroarch/config/remaps/DOSBox-pure/`

Important: During testing, `DukeNukem1.rmp` did not load as expected. After creating `DukeNukem1.pc.rmp`, the controls—including door interaction—worked again after restarting the game.

Use `DukeNukem1.pc.rmp` when restoring the controls.

### Duke Nukem 2

The game uses the shared DOSBox Pure remap:

`retroarch/DOSBox-pure/dosbox.rmp`

No separate game-specific remap is required.

### Duke Nukem 3D

The game was successfully launched and tested on the Raspberry Pi 3 using DOSBox Pure.

A separate control remap for this game has not yet been saved in this repository.

## DOOM 1 and DOOM 2

Both games were tested on the Arcade-101 using the PrBoom core.

| Game | System | Status |
| --- | --- | --- |
| DOOM 1 Shareware | PrBoom | Working |
| DOOM 2: Hell on Earth | PrBoom | Working |

The following functions were verified in both games:

- Movement using the GPIO joystick
- Shooting
- Opening doors

No separate control remap was necessary. Both games use the existing RetroArch settings.

The repository does not include game WAD files.

## Enabling the GPIO controller

The Waveshare Arcade-101-1P uses a custom GPIO pin mapping for its joystick and arcade buttons.

Configuration in `/userdata/system/batocera.conf`:

```ini
controllers.gpio.enabled=1
controllers.gpio.args="map=5 gpio=16,5,27,12,6,4,22,23,24,25,26,17,-1"
```

These settings enable the GPIO controller and specify the GPIO pins used on the Raspberry Pi 3 Model B.

The configuration is also backed up in:

`batocera/arcade-settings.conf`

**Warning:** These settings are specific to this Arcade-101's wiring. Other button wiring may require different GPIO pin assignments.

After restoring these settings, reboot Batocera and verify that the joystick and buttons work correctly.
