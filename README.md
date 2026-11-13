# TI-58 / TI-59 / TI-58C ROM dumps

This repository holds the ROM contents of the Texas Instruments TI-58, TI-59
and TI-58C programmable calculators and of their Solid State Software
modules, plus annotated disassemblies of the two calculator ROMs.

The dumps were read from the chips by the
[Datamath Calculator Museum](https://www.datamath.org/) in 2023, with its
TMS0500 ROM recorder. Every file starts with the recorder's header. The
header names the chip that was read (`DUT`), its banks, the calculator or
module it came from, and the month of the recording.

## Calculator ROM

Both calculators use three ROM chips each: two chips with 2.5 K words of
13-bit code plus a constant ROM, and one chip with 1 K words of code. The
TI-58 and the TI-59 share one ROM; the TI-58C has a revised ROM.

### TI-58 / TI-59 ([`dumps/ti59/`](dumps/ti59))

Read from a TI-59, ATA1979, SN#7112198.

| File | Chip | Banks | Contents |
|---|---|---|---|
| `TMC0582.txt` | TMC0582NL IB7910 | 0, 1, 2FH | First 2.5 K words of code |
| `TMC0583.txt` | TMC0583NL DBS7910 | 2SH, 3, 4 | Second 2.5 K words of code |
| `TMC0571B.txt` | TMC0571NL BP7849 (D0571B) | 5 | Additional 1 K words of code |
| `TMC0582-CONST-K.txt` | TMC0582NL IB7910 | – | Constant ROM of the TMC0582 |
| `TMC0583-CONST-K.txt` | TMC0583NL DBS7910 | – | Constant ROM of the TMC0583 |

### TI-58C ([`dumps/ti58c/`](dumps/ti58c))

Read from a TI-58C, ATA2980, SN#8171106.

| File | Chip | Banks | Contents |
|---|---|---|---|
| `CD2400.txt` | TMC0580NL CD2400 | 0, 1, 2FH | First 2.5 K words of code |
| `CD2401.txt` | TMC0580NL CD2401 | 2SH, 3, 4 | Second 2.5 K words of code |
| `TMC0573.txt` | TMC0573NL P8018K (W0573) | 5 | Additional 1 K words of code |
| `CD2400-CONST-K.txt` | TMC0580NL CD2400 | – | Constant ROM of the CD2400 |
| `CD2401-CONST-K.txt` | TMC0580NL CD2401 | – | Constant ROM of the CD2401 |

### Constant ROM

Each 2.5 K chip also holds a constant ROM of 32 × 16 BCD digits. The
`-CONST-K` files list it twice: once as numbers (`CONSTANT ROM (NUMBER)`) and
once spelled out as keycodes (`CONSTANT ROM (KEY CODE)`). Part of it is
keycode programs that the ROM runs for built-in functions (Σ+, x̄, P→R, D.MS,
Op 11–15); [`disasm/TI59-keycode-programs.asm`](disasm/TI59-keycode-programs.asm)
lists them.

## Solid State Software modules ([`dumps/modules/`](dumps/modules))

| File | Chip | Module | Recorded |
|---|---|---|---|
| `TMC0541.txt` | TMC0541NL ASP7749 | Master Library -1- | June 2023 |
| `TMC0542.txt` | TMC0542NL BSP7901 | Applied Statistics -2- | August 2023 |
| `TMC0543.txt` | TMC0543NL SP7731 | Investment -3- | June 2023 |
| `TMC0544.txt` | TMC0544NL ASP7849 | Surveying -4- | June 2023 |
| `TMC0545.txt` | TMC0545NL SP7727 | Marine Navigation -5- | June 2023 |
| `TMC0546.txt` | TMC0546NL SA7723 | Aviation -6- | September 2023 |
| `TMC0547.txt` | TMC0547NL SP7740 | Leisure Library -7- | June 2023 |
| `TMC0548.txt` | TMC0548NL BSA7812 | Securities Analysis -8- | September 2023 |
| `TMC0549.txt` | TMC0549NL ASA7832 | Business Decisions -9- | June 2023 |
| `TMC0550.txt` | TMC0550NL SP7927 | Math/Utilities -10- | June 2023 |
| `TMC0551.txt` | TMC0551NL SP7936 | EE Library -11- | September 2023 |
| `TMC0554.txt` | TMC0554NL SP7914 | Agriculture -12- | June 2023 |
| `TMC0555.txt` | TMC0555NL ASP8009 | RPN Simulator -13- | June 2023 |
| `TMC0553.txt` | TMC0553NL ASP8040 | Structural Engineering Rev. A | September 2023 |

## Module files ([`modules/`](modules))

One file per Solid State Software module, `modules/<ID>.rom.yaml`, in the
Calc-U Solid State ROM module format (`format: solid-state-rom-module`,
`format-version: 1`). Each file holds the module's name and description, its
ROM bytes and the pre-printed cue card of each library program. The emulator
reads these files; the dumps above stay as the source.

They were made once from the dumps in `dumps/modules/` (the bytes are
identical) and from the cue cards of Calc-U-59 2.3.0
(`roms/solid-state/cuecards.txt`). A library program that had no cue card
there gets a stand-in card: the module's description as its title and its
ID as its `id`. Only ML and LE have pre-printed cue cards so far. The title
printed in the dump of RE and SE differs from the module's `title`, and is
kept in `notes`.

| File | Chip | Module |
|---|---|---|
| `ML.rom.yaml` | TMC0541 | Master Library |
| `ST.rom.yaml` | TMC0542 | Applied Statistics |
| `RE.rom.yaml` | TMC0543 | Investment |
| `SY.rom.yaml` | TMC0544 | Surveying |
| `NG.rom.yaml` | TMC0545 | Marine Navigation |
| `AV.rom.yaml` | TMC0546 | Aviation |
| `LE.rom.yaml` | TMC0547 | Leisure Library |
| `SA.rom.yaml` | TMC0548 | Securities Analysis |
| `BD.rom.yaml` | TMC0549 | Business Decisions |
| `MU.rom.yaml` | TMC0550 | Math/Utilities |
| `EE.rom.yaml` | TMC0551 | EE Library |
| `SE.rom.yaml` | TMC0553 | Structural Engineering |
| `AG.rom.yaml` | TMC0554 | Agriculture |
| `RP.rom.yaml` | TMC0555 | RPN Simulator |

## Disassemblies ([`disasm/`](disasm))

Annotated disassemblies of both calculator ROMs and narrative guides to how
they work; see [`disasm/README.md`](disasm/README.md).

## File format

The dumps are text. After the header and a line of dashes, each line holds
an address and 16 words in hex:

```
0000: 0A01 0A0A 00B9 03DC 01D8 0A48 1002 0121 0A0F 0101 032C 1809 0A02 01D7 1ECE 0A77
```

Calculator code words are 13 bits wide. Module ROMs hold keycode programs
(bytes).

## Verification

MD5 checksums of the files:

```
c1cb6d40e063aae1ba7b851b11b1c18a  dumps/ti59/TMC0582.txt
2341a8e484c31ff24a16e70c14c1b3a3  dumps/ti59/TMC0583.txt
599050d2b1c1900e64b56c089338d32e  dumps/ti59/TMC0571B.txt
bf4fb6005177ffdec8f8ceee7e7e16d6  dumps/ti59/TMC0582-CONST-K.txt
81724f14b2827410650f032ef352b1aa  dumps/ti59/TMC0583-CONST-K.txt
638c4d0c8359e00cf1f600884f43b789  dumps/ti58c/CD2400.txt
3b0ec122cd34b214477780fd405ffdd8  dumps/ti58c/CD2401.txt
6c0cb7db542f3b74a28613ff4ed14bce  dumps/ti58c/TMC0573.txt
dbaee54fe0f478c7659d17bff4b790d4  dumps/ti58c/CD2400-CONST-K.txt
ac81d5b45c736a0f45c3835f0d977b87  dumps/ti58c/CD2401-CONST-K.txt
bbca8e7dc631849cf3f7770d1efa7aa7  dumps/modules/TMC0541.txt
99b1b41f4361ec2900f990002529193f  dumps/modules/TMC0542.txt
eb3a8d6a66996b471ee19c2a10458aad  dumps/modules/TMC0543.txt
64cd0fbe5adc5820c58a7e1262df521b  dumps/modules/TMC0544.txt
1f50c8b671f9f4aa1bfebe8ed8007002  dumps/modules/TMC0545.txt
0509ff2657edb063fbc666ffb8997d51  dumps/modules/TMC0546.txt
f3ac4e66fce6624bd2f4b0faee0db422  dumps/modules/TMC0547.txt
a3b802d1d70d38c8bd9de8e72b54a9fe  dumps/modules/TMC0548.txt
c30fe59d97f268f50756c15d223ef6a9  dumps/modules/TMC0549.txt
78e46b957573c63c05be0b2fa93f7ded  dumps/modules/TMC0550.txt
5f1d46e22657e3c432b8ec97a9b2f9ae  dumps/modules/TMC0551.txt
080546debf5326fe83eb4334923570e1  dumps/modules/TMC0553.txt
40832575c1464fbf23e3893495b165a4  dumps/modules/TMC0554.txt
86c670fb71d51d36c58f6846b25d025b  dumps/modules/TMC0555.txt
ab6db47478041bb1bd1b50b3114b8949  modules/ML.rom.yaml
6e7e4045c9e31720dba5fbee0ace248a  modules/ST.rom.yaml
6ea276ed76b4b67df59141d73708e6ec  modules/RE.rom.yaml
d87b45b1f0fc6963db7dc3e537eeaf05  modules/SY.rom.yaml
889d6f5c516afd62f7bd7680cecf47ed  modules/NG.rom.yaml
84823786f1b065a74ba7b36319c05ba4  modules/AV.rom.yaml
f67efb0d1b10c46266d9a32891c9aa6c  modules/LE.rom.yaml
f26fd2f1cbe52ec93387c76fe26122e6  modules/SA.rom.yaml
4ee8f14c5ce0f088cff3ea3f0c149f76  modules/BD.rom.yaml
81403a7ed013e53c0334a156a7ca8c0e  modules/MU.rom.yaml
63fdc4324deb68025c9e98af817a91fc  modules/EE.rom.yaml
ea082fed55d93610d95f16cf2577f1e1  modules/SE.rom.yaml
4903315a721f4ff41e60b40abbaeb284  modules/AG.rom.yaml
d62d3ea22600d0df8f24a6355ee0ea95  modules/RP.rom.yaml
```

## Users

[Calc-U-59](https://github.com/tinue/Calc-U-59), an emulator of the TI-58,
TI-59 and TI-58C, downloads the calculator dumps and the module files when it
is built.
