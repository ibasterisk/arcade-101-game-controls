[🇸🇰 Slovensky](README.md) | [🇬🇧 English](README_EN.md)

# Arcade-101 – Game Controls

Konfigurácie ovládania hier pre arkádový automat
Waveshare Arcade-101-1P s Raspberry Pi 3 a Batocera Linux.

## Účel repozitára

Tento repozitár slúži na zálohovanie a obnovenie
vlastných nastavení ovládania hier cez RetroArch
a emulátor DOSBox Pure.

Obsahuje iba konfiguračné súbory.
Neobsahuje ROM hry, BIOS súbory ani heslá.

## Podporované hry

| Hra | Systém | Konfigurácia |
| --- | --- | --- |
| Commander Keen 1 | MS-DOS | Spoločný profil DOSBox Pure |
| Commander Keen 4 | MS-DOS | padto.keys a vlastný remap |
| Wolfenstein 3D | MS-DOS | Vlastný remap |
| Heretic | MS-DOS | padto.keys a vlastné remapy |
| Dyna Blaster | MS-DOS | Vlastný remap |
| Duke Nukem 1 | MS-DOS | Vlastný remap DukeNukem1.pc.rmp |
| Duke Nukem 2 | MS-DOS | Spoločný profil DOSBox Pure |
| Duke Nukem 3D | MS-DOS | Funkčné ovládanie |
| DOOM 1 Shareware | PrBoom | Predvolené ovládanie |
| DOOM 2: Hell on Earth | PrBoom | Predvolené ovládanie |

## Commander Keen 4

Overené ovládanie arkádového automatu:

- Joystick – pohyb postavy
- Modré tlačidlo – skok
- Žlté tlačidlo – streľba
- Zelené tlačidlo – POGO odrážadlo
- Biele tlačidlo – pauza

Ovládanie bolo otestované aj po opätovnom spustení hry.

## Štruktúra repozitára

- retroarch/DOSBox-pure/ – profily ovládania RetroArchu
- dos/CommanderKeen4.pc/padto.keys – ovládanie Commander Keen 4
- dos/Heretic.pc/padto.keys – ovládanie Heretic

## Umiestnenie konfigurácií na Batocere

RetroArch remapy:

/userdata/system/configs/retroarch/config/remaps/DOSBox-pure/

Konfigurácia Commander Keen 4:

/userdata/roms/dos/CommanderKeen4.pc/padto.keys

Konfigurácia Heretic:

/userdata/roms/dos/Heretic.pc/padto.keys

## Obnova ovládania

1. Zálohovať aktuálne konfigurácie na Batocere.
2. Skopírovať potrebné súbory do príslušných adresárov.
3. Reštartovať príslušnú hru.
4. Overiť ovládanie joystickom a tlačidlami.

Poznámka: Niektoré DOS hry sa spúšťajú cez dosbox.bat.
RetroArch preto môže používať spoločný profil dosbox.rmp.
Pred obnovou odporúčame skontrolovať, ktorý remap hra načítava.

## Hardvér

- Waveshare Arcade-101-1P
- Raspberry Pi 3 Model B
- GPIO joystick a arkádové tlačidlá
- Batocera Linux 43.1
- DOSBox Pure / RetroArch

## Poznámka

Konfigurácie sú určené pre konkrétne zapojenie
ovládacích prvkov tohto arkádového automatu.

Pri inom zapojení GPIO tlačidiel môže byť potrebné
mapovanie upraviť.

## Predvolené nastavenia Arcade-101

Repozitár obsahuje aj konfiguráciu základného ovládania
a zvuku arkádového automatu.

### Ovládanie hlavnej ponuky Batocery

Súbor:

`batocera/emulationstation/gpio-controller.xml`

Obsahuje mapovanie zariadenia GPIO Custom Controller 1:

- joystick a navigácia v hlavnej ponuke
- farebné arkádové tlačidlá
- tlačidlo START a SELECT
- tlačidlo HOTKEY

Ide o výpis jednej sekcie z pôvodného `es_input.cfg`.
Pri obnove je potrebné vložiť túto sekciu do existujúceho
súboru `/userdata/system/configs/emulationstation/es_input.cfg`.
Nenahrádzajte ním celý súbor.

### Predvolené nastavenie zvuku

Súbor:

`batocera/arcade-settings.conf`

Obsahuje:

- zvukové zariadenie WM8960
- hlasitosť 65 %
- zapnutú hudbu v hlavnej ponuke
- nastavenia ukončovania emulátorov

Tieto riadky patria do:

`/userdata/system/batocera.conf`

Pred ich pridaním je potrebné zazálohovať existujúci súbor
a skontrolovať prípadné duplicitné nastavenia.

### Ukončovanie hier

Na Arcade-101 používame kombináciu:

**HOTKEY + zelené tlačidlo**

Nastavenie bolo overené pre RetroArch a vybrané systémy,
najmä MS-DOS a Nintendo NES.

### Bezpečnosť

Repozitár neobsahuje ROM hry, heslá ani celý súbor
`batocera.conf`.

Pred obnovením konfigurácie odporúčame vytvoriť zálohu
pôvodných nastavení.

## Duke Nukem – trilógia

Na Arcade-101 boli otestované tieto hry:

| Hra | Systém | Stav |
| --- | --- | --- |
| Duke Nukem 1 | MS-DOS | Funkčné vlastné ovládanie |
| Duke Nukem 2 | MS-DOS | Funkčné predvolené ovládanie DOSBox Pure |
| Duke Nukem 3D | MS-DOS | Hrateľné |

### Duke Nukem 1 – ovládanie

Overené ovládanie GPIO joysticku a arkádových tlačidiel:

| Ovládací prvok | Funkcia | Kláves |
| --- | --- | --- |
| Joystick doľava | Pohyb doľava | D |
| Joystick doprava | Pohyb doprava | G |
| Joystick hore | Otváranie dverí | R |
| Modré tlačidlo | Streľba | Numpad 4 |
| Žlté tlačidlo | Skok | Numpad 5 |

Funkčná konfigurácia:

`retroarch/DOSBox-pure/DukeNukem1.pc.rmp`

Na Batocere sa nachádza v adresári:

`/userdata/system/configs/retroarch/config/remaps/DOSBox-pure/`

Dôležité: pri testovaní sa ukázalo, že súbor
`DukeNukem1.rmp` sa nenačítaval podľa očakávania.
Po vytvorení súboru `DukeNukem1.pc.rmp` sa ovládanie
vrátane otvárania dverí úspešne obnovilo aj po novom
spustení hry.

Pri obnove odporúčame použiť práve tento súbor.

### Duke Nukem 2

Hra používa spoločné mapovanie DOSBox Pure:

`retroarch/DOSBox-pure/dosbox.rmp`

Nie je potrebný samostatný herný remap.

### Duke Nukem 3D

Hra bola úspešne spustená a otestovaná na Raspberry Pi 3
prostredníctvom DOSBox Pure.

Samostatné mapovanie ovládania zatiaľ nebolo uložené
v tomto repozitári.

## DOOM 1 a DOOM 2

Obe hry boli otestované na Arcade-101 s jadrom PrBoom.

| Hra | Systém | Stav |
| --- | --- | --- |
| DOOM 1 Shareware | PrBoom | Funkčné |
| DOOM 2: Hell on Earth | PrBoom | Funkčné |

Pri oboch hrách bolo overené:

- pohyb pomocou GPIO joysticku
- streľba
- otváranie dverí

Nebolo potrebné vytvárať samostatné mapovanie ovládania.
Obe hry používajú existujúce nastavenie RetroArchu.

Repozitár neobsahuje herné WAD súbory.

## Aktivácia GPIO ovládača

Na Waveshare Arcade-101-1P používame vlastné mapovanie
GPIO pinov pre joystick a arkádové tlačidlá.

Konfigurácia v súbore `/userdata/system/batocera.conf`:

    controllers.gpio.enabled=1
    controllers.gpio.args="map=5 gpio=16,5,27,12,6,4,22,23,24,25,26,17,-1"

Tieto hodnoty aktivujú GPIO ovládač a definujú použité
GPIO piny na Raspberry Pi 3 Model B.

Konfigurácia je zálohovaná v repozitári v súbore:

`batocera/arcade-settings.conf`

**Upozornenie:** Nastavenie platí pre konkrétne zapojenie
Arcade-101. Pri inom zapojení môže byť potrebná úprava GPIO pinov.

Po obnove konfigurácie reštartujte Batoceru a overte
funkčnosť joysticku a tlačidiel.
