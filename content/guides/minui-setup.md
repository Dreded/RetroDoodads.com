---
title: "Setting up MinUI"
date: 2025-06-14
descripion: "Learn how to setup minui for a handheld retro doodad Like the TrimUI Brick."
tags: ["guides", "sd card", "Custom OS"]
---
## Setting Up MinUI on Your Device (TrimUI, etc.)

### 1. Format Your SD Card

#### On Windows (Using Rufus)

Use **Rufus** to format your microSD card:

* Download Rufus: [https://rufus.ie/](https://rufus.ie/)
* Insert your microSD card
* In Rufus:
  * Select the SD card under *Device*
  * Under Boot Selection change it to "Non Bootable"
  * Choose *FAT32* as the file system
  * Uncheck "Create Extended Label and icon Files"
  * (OPTIONAL) Put in a Volume Label of "MinUI"
  * Leave other options at default and click **Start**

#### On Linux (Using `mkfs`)

Open a terminal and run:

```bash
sudo umount /dev/sdX*
sudo mkfs.vfat -F 32 -n MinUI /dev/sdX
```

Replace `/dev/sdX` with the actual device name of your SD card (e.g., `/dev/sdb`). You can identify it using:

```bash
lsblk
```

#### On macOS (Using `diskutil`)

Open a terminal and run:

```bash
diskutil list
diskutil eraseDisk FAT32 MinUI MBRFormat /dev/diskN
```

Replace `/dev/diskN` with your SD card’s identifier (e.g., `/dev/disk2`). You can find it using:

```bash
diskutil list
```

> ⚠️ Be extremely careful when selecting disk devices to avoid wiping the wrong drive.


> ⚠️ It's highly recommended to use quality microSD cards like **Samsung**. Even some **SanDisk** cards are incompatible with certain Chinese handhelds like the R36S. Avoid using the generic black-label SD card included with your device.

### 2. Download MinUI

Head to the official GitHub page:

* Download both the **Base** and **Extras** from the latest release:

  * [https://github.com/shauninman/MinUI/releases](https://github.com/shauninman/MinUI/releases)

Unsure if your device is supported? Check the main page here: [https://github.com/shauninman/MinUI](https://github.com/shauninman/MinUI)

### 3. Prepare the SD Card

Unzip the **Base** package using your preferred tool (7-Zip, Windows Explorer, etc.). Copy the following contents to the **root of your SD card**:

* `Bios`
* `Roms`
* `Saves`
* `MinUI.zip`
* The folder matching your device (e.g., `trimui` for TrimUI Brick)

Your SD card should now resemble:

```
.
├── Bios
│   ├── FC
│   ├── GB
│   ├── GBA
│   ├── GBC
│   ├── MD
│   ├── PS
│   └── SFC
├── MinUI.zip
├── Roms
│   ├── Game Boy (GB)
│   ├── Game Boy Advance (GBA)
│   ├── Game Boy Color (GBC)
│   ├── Nintendo Entertainment System (FC)
│   ├── Sega Genesis (MD)
│   ├── Sony PlayStation (PS)
│   └── Super Nintendo Entertainment System (SFC)
├── Saves
│   ├── FC
│   ├── GB
│   ├── GBA
│   ├── GBC
│   ├── MD
│   ├── PS
│   └── SFC
└── trimui
    └── app
        ├── MainUI
        ├── keymon
        ├── main.sh
        └── runtrimui.sh
```

### 4. Install the Extras

Unzip the **Extras** package and copy all its contents to the SD card. If prompted, allow files to **merge/overwrite**.

Optionally, you can delete unused folders from `Tools` and `Emu` to free up \~100MB. For example, keep only the folder for your device, since im using the TrimUI Brick... (you may want to keep these to make it so this SD works in any system that MinUI supports)

```
Tools/
├── trimuismart    ✅
├── gkdpixel       ❌
├── miyoomini      ❌
├── rg35xx         ❌
...etc
```

### 5. Add ROMs

You’ll need to dump your own game backups. Ahem, Google and Reddit may be helpful (search: "rom megathread" or "Tiny Best Set").

* Empty folders will not appear in the UI.
* Any folder ending in `.disabled` will be hidden.
* Only the **emulator code in parentheses** matters, so:

  * `Game Boy (GB)` = `MyCoolROMs (GB)` = `GameBoyUS (GB)` — all will show as "Game Boy" in the frontend.

This gives you the flexibility to organize folders by region, version, etc.

### 6. Add BIOS Files

BIOS files are copyrighted and must be sourced legally (search: "Retro BIOSes System.dat"). Example layout:

```
Bios/
├── FC/     → disksys.rom            # Famicom Disk System
├── GB/     → gb_bios.bin            # Game Boy
├── GBA/    → gba_bios.bin           # Game Boy Advance
├── MGBA/   → gba_bios.bin           # Game Boy Advance MGBA Emulator
├── GBC/    → gbc_bios.bin           # Game Boy Color
├── NGPC/   → ngpc_bios.bin          # Neo Geo Pocket Color
├── MD/
│   ├── bios_CD_E.bin                # Sega CD (Europe)
│   ├── bios_CD_J.bin                # Sega CD (Japan)
│   └── bios_CD_U.bin                # Sega CD (USA)
├── PKM/    → bios.min               # Pokémon Mini
├── PCE/    → syscard3.pce           # TurboGrafx-CD
├── PS/     → psxonpsp660.bin        # PlayStation
├── SGB/    → sgb_bios.bin           # Super Game Boy

ROMs/neogeo/ → neogeo.zip            # Neo Geo BIOS

Emus/tg3040/PICO.pak/PICO8_Wrapper/bin/
├── pico8.dat
└── pico8_64                          # Pico-8 (licensed version only)
```

#### Optional BIOSes

```
Bios/
├── GG/   → gg.rom        # Game Gear BIOS (optional)
├── SMS/  → smsbios.bin   # Sega Master System (optional)
├── SFC/  → [empty]       # Super Famicom — no BIOS needed
├── VB/   → [empty]       # Virtual Boy
```

---

## Optional: Collections

To create a custom collection (like a Mario-themed one):

1. Make a folder named `Collections` in the root of the SD card.
```
SDCard/
├── Collections/
│   └── Mario.txt
```

2. Inside it, create a text file like `Mario.txt` listing the paths to the games:
```
/Roms/Game Boy (GB)/Super Mario Land (USA).gb
/Roms/Game Boy (GB)/Super Mario Land 2 - 6 Golden Coins (USA, Europe).gb
/Roms/Game Boy Color (GBC)/Mario Golf (USA).gbc
/Roms/Game Boy Color (GBC)/Mario Tennis (USA).gbc
/Roms/Game Boy Advance (GBA)/Super Mario Advance (USA).gba
/Roms/Game Boy Advance (GBA)/Super Mario Advance 2 - Super Mario World (USA).gba
/Roms/Game Boy Advance (GBA)/Super Mario Advance 4 - Super Mario Bros. 3 (USA).gba
/Roms/Nintendo Entertainment System (FC)/Super Mario Bros. (World).nes
/Roms/Nintendo Entertainment System (FC)/Super Mario Bros. 2 (USA).nes
/Roms/Nintendo Entertainment System (FC)/Super Mario Bros. 3 (USA).nes
/Roms/Super Nintendo Entertainment System (SFC)/Super Mario World (USA).sfc
/Roms/Super Nintendo Entertainment System (SFC)/Super Mario All-Stars + Super Mario World (USA).sfc
/Roms/Sega Game Gear (GG)/Super Mario Bros. (Homebrew Demo).gg
/Roms/TurboGrafx-16 (PCE)/Super Mario World (Bootleg).pce
/Roms/Sony PlayStation (PS)/Mario's Game Gallery (USA).chd
/Roms/Virtual Boy (VB)/Mario's Tennis (USA).vb
```
## (Optional) Add Custom Pak Files

To expand MinUI’s emulator support, grab community-made PAK files from:

* https://github.com/tenlevels/PakUI

These include extras like **FBNEO** for arcade titles and dont forget the added Bios's needed for any Paks you add.

## Done
Eject the SD card(properly), insert it into your device, power it on, wait for MinUI to fully install, it will power off if inactive for 30second so power on and enjoy.


## TrimUI Usage Notes
1. The slide Switch on the side is a mute switch slide up if you have no sound
2. Adjust brightness by holding menu(3 dots) and VOL +/-
3. Save/Load/Quit are all in the menu accessed by hitting the Menu Button (3 dots)
3. Hold the power button mid game to have a save state created and power off completely (no battery drain)
4. Tap power for sleep, if its inactive for more than a few minutes it will power off and if in the middle of a game make a save state.
5. When browsing the Game list press X on a game to load directly into a save state previously made with save+quit.

### Setup your shortcuts...
When running a game hit the menu button(3 dots) and go to Options > SHortcuts and setup the htokeys you weant to use for that core. My suggestion for GBA for example is.
- Save State = Menu+R1
- Load State = Menu+L1
- Reset = L3
- Save + Quit = R3
- Toggle FF = Menu+R2
- Hold FF = R2

Then when done hit B(back) and Save Changes > Save for Console(or game)