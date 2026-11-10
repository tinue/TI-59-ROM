# Disassemblies of the TI-59 and TI-58C ROMs

Both calculator ROMs in [`../dumps/`](../dumps) have a disassembly here,
6144 13-bit words each (addresses 0000–17FF).

| File | What it is |
|---|---|
| `TI59.asm`, `TI58C.asm` | Raw listings, one line per word, decoded with the TMC0501 instruction set. No labels, no comments. |
| `TI59-commented.asm`, `TI58C-commented.asm` | The same listings with routine headers and line comments. |
| `TI59-labels.asm`, `TI58C-labels.asm` | Label tables: the names of jump targets that the comments use, each tagged trace-confirmed, derived or speculative. |
| `TI59-keycode-programs.asm`, `TI58C-keycode-programs.asm` | The keycode programs stored in the constant ROM, as program steps. |
| `TI59-ROM-Guide.md` | How the TI-59 ROM works: control flow, key handling, the program interpreter, printer, card reader and more. |
| `TI58C-ROM-Guide.md` | How the TI-58C ROM differs from the TI-59 ROM: constant memory, bug fixes, enhancements, removed and moved code. |
| `fastmode.md` | The fast mode that runs ROM and module keycode programs. |
| `printerinterrupt.md` | The program step that stops the PC-100 printer while it prints. |

The TI-58 uses the TI-59 ROM.

## Origin

The files come from [Calc-U-59](https://github.com/tinue/Calc-U-59) and
are copies of its `rom/` directory. They were made there with the emulator
and its tools, which are not part of this repository:

- `tools/disasm.py` generates the raw listings; `tools/mnemonics.tsv` holds
  the mnemonics.
- `tools/annotate_rom.py` applies comment batches to the commented
  listings.
- `tools/headless/` traces the unmodified ROM; claims marked
  trace-confirmed were checked this way.

Paths in the files (`rom/…`, `tools/…`, `roms/calculator/…`,
`reference/…`) refer to the Calc-U-59 repository.
