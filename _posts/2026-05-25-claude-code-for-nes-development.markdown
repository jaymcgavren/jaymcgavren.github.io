---
layout: post
title: 'Claude Code for NES Development'
tags: []
type: post
published: true
---

Claude Code is converting all our jobs into a boring code review trudge. But we may as well have some fun with it too. Luis Montes has been doing some [cool work](https://www.youtube.com/watch?v=cFZA3R0bPls) in retrogaming using LLMs, and he mentioned he'd been able to generate some simple homebrew demos for 8 and 16-bit consoles using Claude.

I've long wanted to try writing homebrew, but have never had the time. I don't know assembly language, and the low-level style of programming required can be a pain. But it turns out LLMs have all but eliminated the barriers to entry. In this post I'll walk through how I used Claude Code to generate my first Nintendo Entertainment System ROM!

![A NES emulator window showing a running ROM. It's a solid blue screen with the text "HELLO NES" at the center.](/assets/images/2026-05-22-claude-code-for-nes-development/hello_nes.png){: width="250" }

<!--more-->

```
$ pwd
/Users/jay/work/hellones
$ claude
[Claude Code v2.1.144, Sonnet 4.6 model, Claude Pro plan]

❯ I'm on MacOS Sequoia. I want you to write a simple program that I can run using a Nintendo Entertainment System emulator. What tools should I install for you to use?

⏺ For NES development on macOS, you'll need:

1. cc65 — the standard toolchain for 6502 assembly (includes the ca65 assembler and ld65 linker). Install via Homebrew:

brew install cc65

2. Mesen2 — the best NES emulator for macOS with accurate emulation and a built-in debugger. Download the macOS build from its
GitHub releases page (search "Mesen2 releases").
3. make — for build automation. Comes with Xcode Command Line Tools, which you likely already have. Verify with:

make --version

That's the full stack. Once those are in place, I can write a simple NES ROM (a classic "hello world" equivalent — e.g., a screen with a colored background and a sprite) along with a Makefile to assemble and link it into a .nes file you can open directly in Mesen2.
```

Sure _sounds_ easy! I opened a separate shell and installed cc65 following Claude's directions:

```
$ brew install cc65
=> Fetching downloads for: cc65
✔︎ Bottle Manifest cc65 (2.19)   Downloaded   14.1KB/ 14.1KB
✔︎ Bottle cc65 (2.19)            Downloaded    9.2MB/  9.2MB
==> Pouring cc65--2.19.arm64_sequoia.bottle.tar.gz
==> Caveats
Library files have been installed to:
  /opt/homebrew/Cellar/cc65/2.19/share/cc65
==> Summary
🍺  /opt/homebrew/Cellar/cc65/2.19: 482 files, 32.6MB
```

I did a Google search for "Mesen2 releases" as it directed. [https://github.com/SourMesen/Mesen2/releases](https://github.com/SourMesen/Mesen2/releases) was the top result.

At the top of the Mesen 2.1.1 description, it says:

> Requirements

> For the macOS and Linux builds, SDL2 must be manually installed first.

I could've asked Claude about that, but I already knew what SDL2 was: a graphics and audio library, frequently used by game developers. I also knew that Homebrew could install it for me. I checked to make sure there was an `sdl2` formula:

```
% brew info sdl2
==> sdl2 ↑: 2.32.8 → stable 2.32.10 (bottled), HEAD
Low-level access to audio, keyboard, mouse, joystick, and graphics
https://www.libsdl.org/
Installed (on request)
From: https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/s/sdl2.rb
License: Zlib
==> Installed Kegs and Versions
sdl2 ↑ 2.32.8 → 2.32.10 (94 files, 6.7MB) [Linked]
```

And it turned out that I already had it installed. (If I hadn't, `brew install sdl2` would have taken care of that.)

And lastly, I needed to verify `make` was already installed. `make` is a very old, very common build tool often used with compilers. Any Mac or Linux system will probably have it by default, and it's not hard to get for Windows either. To verify I had it, I just copy-pasted the command Claude gave me:

```
% make --version
GNU Make 3.81
Copyright (C) 2006  Free Software Foundation, Inc.
[...]
```

There it is!

I switched back to my Claude session and let it know I was ready.

```
❯ I have those installed, go ahead

⏺ I'll write three files: the 6502 assembly source, a linker config, and a Makefile.
```

Let's look at the files it generated.

## hello.s

At 4 kilobytes, `hello.s` is the largest and most important. It contains the "Hello NES" program. [Note: I asked Claude to go back and annotate each function with a comment on what it does.]

```
PPUCTRL   = $2000
PPUMASK   = $2001
PPUSTATUS = $2002
PPUSCROLL = $2005
PPUADDR   = $2006
PPUDATA   = $2007
APU_FC    = $4017

.segment "HEADER"
    .byte $4E, $45, $53, $1A    ; "NES" + EOF
    .byte 2                     ; 2 x 16KB PRG banks
    .byte 1                     ; 1 x 8KB CHR bank
    .byte $00                   ; mapper 0, horizontal mirroring
    .byte $00, $00, $00, $00, $00, $00, $00, $00, $00

.segment "CODE"

; reset: program entry point. The NES jumps here at power-on.
; We silence interrupts and the audio chip, set up the stack,
; and wait for the graphics chip (PPU) to finish booting
; before doing anything visible.
reset:
    sei
    cld
    ldx #$40
    stx APU_FC          ; disable APU frame IRQ
    ldx #$FF
    txs                 ; stack = $01FF
    inx                 ; X = 0
    stx PPUCTRL         ; disable NMI
    stx PPUMASK         ; disable rendering
    stx $4015           ; disable APU channels
    stx $4010           ; disable DMC IRQ

; vblank1: wait for the first vblank. "Vblank" is the brief
; pause between drawn frames; bit 7 of PPUSTATUS is set
; during it. The PPU needs two vblanks after power-on before
; it's safe to talk to.
vblank1:
    bit PPUSTATUS
    bpl vblank1

    lda #$00
    tax
; clrmem: zero out all 2KB of NES RAM ($0000-$07FF). The 6502's
; X register only counts 0-255, so we unroll across 8 pages
; of 256 bytes each, hitting one byte per page per iteration.
clrmem:
    sta $0000, x
    sta $0100, x
    sta $0200, x
    sta $0300, x
    sta $0400, x
    sta $0500, x
    sta $0600, x
    sta $0700, x
    inx
    bne clrmem

; vblank2: wait for the second vblank — the PPU is now ready.
vblank2:
    bit PPUSTATUS
    bpl vblank2

    ; palloop: copy 32 palette bytes into PPU memory at $3F00.
    ; The PPU has its own separate memory; we aim at an address
    ; by writing PPUADDR twice (high byte, then low), then stream
    ; bytes through PPUDATA. (Palette: dark blue bg, white text.)
    lda PPUSTATUS
    lda #$3F
    sta PPUADDR
    lda #$00
    sta PPUADDR
    ldx #0
palloop:
    lda paldata, x
    sta PPUDATA
    inx
    cpx #32
    bne palloop

    ; ntloop: fill the nametable with blank tiles. The nametable
    ; at PPU address $2000 is a 32x30 grid telling the PPU which
    ; tile to draw at each on-screen position. 960 tiles + 64
    ; attribute bytes = 1024 total, so we loop 4 x 256 times.
    lda PPUSTATUS
    lda #$20
    sta PPUADDR
    lda #$00
    sta PPUADDR
    lda #$00
    ldx #0
    ldy #4
ntloop:
    sta PPUDATA
    inx
    bne ntloop
    dey
    bne ntloop

    ; textloop: write the tile indices that spell "HELLO NES"
    ; into the nametable. Each byte is a tile number; the PPU
    ; looks it up in our CHR data to draw the actual pixels.
    ; Address $21AB = $2000 + row 13 * 32 + column 11.
    ; The loop stops when it hits the $FF sentinel byte.
    lda PPUSTATUS
    lda #$21
    sta PPUADDR
    lda #$AB
    sta PPUADDR
    ldx #0
textloop:
    lda tiles_hello, x
    cmp #$FF
    beq textdone
    sta PPUDATA
    inx
    jmp textloop
textdone:

    lda PPUSTATUS
    lda #$00
    sta PPUSCROLL
    sta PPUSCROLL

    lda #%00001010      ; show background
    sta PPUMASK
    lda #%10000000      ; enable NMI, BG from pattern table 0
    sta PPUCTRL

; mainloop: setup is done; the PPU now draws each frame on its
; own from the data we loaded. The CPU has nothing more to do,
; so spin here forever.
mainloop:
    jmp mainloop

; nmi: fires once per frame (60 Hz) when vblank begins. We
; enabled it via PPUCTRL but have nothing to do, so just return.
nmi:
    rti

; irq: would fire from the audio chip or cartridge mapper. Unused here.
irq:
    rti

paldata:
    ; 4 BG palettes: universal bg = $01 (dark blue), color 3 = $30 (white)
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30
    ; 4 sprite palettes (unused but required)
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30
    .byte $01, $00, $00, $30

; H=1 E=2 L=3 O=4 space=0 N=5 S=6, $FF = end sentinel
tiles_hello:
    .byte 1, 2, 3, 3, 4, 0, 5, 2, 6, $FF

.segment "VECTORS"
    .word nmi
    .word reset
    .word irq

; ---------------------------------------------------------------
; CHR-ROM: pattern table 0 — one tile per character
; Each tile = 8 bytes plane0 + 8 bytes plane1
; Both planes identical → every foreground pixel = palette color 3
; ---------------------------------------------------------------
.segment "CHARS"

; Tile 0: blank
.byte $00,$00,$00,$00,$00,$00,$00,$00
.byte $00,$00,$00,$00,$00,$00,$00,$00

; Tile 1: H   ##..##..  ##..##..  ######..  ##..##..  (x3)
.byte $CC,$CC,$FC,$CC,$CC,$CC,$00,$00
.byte $CC,$CC,$FC,$CC,$CC,$CC,$00,$00

; Tile 2: E   ######..  ##......  #####...  ##......  ##......  ######..
.byte $FC,$C0,$C0,$F8,$C0,$C0,$FC,$00
.byte $FC,$C0,$C0,$F8,$C0,$C0,$FC,$00

; Tile 3: L   ##......  (x5)  ######..
.byte $C0,$C0,$C0,$C0,$C0,$FC,$00,$00
.byte $C0,$C0,$C0,$C0,$C0,$FC,$00,$00

; Tile 4: O   .####...  ##..##..  (x4)  .####...
.byte $78,$CC,$CC,$CC,$CC,$78,$00,$00
.byte $78,$CC,$CC,$CC,$CC,$78,$00,$00

; Tile 5: N   ##..##..  ###.##..  ######..  ##.###..  ##..##..  (x2)
.byte $CC,$EC,$FC,$DC,$CC,$CC,$00,$00
.byte $CC,$EC,$FC,$DC,$CC,$CC,$00,$00

; Tile 6: S   .####...  ##..##..  ##......  .####...  ....##..  ##..##..  .####...
.byte $78,$CC,$C0,$78,$0C,$CC,$78,$00
.byte $78,$CC,$C0,$78,$0C,$CC,$78,$00
```

That's the whole program. We're expecting to see "HELLO NES" on the screen when it runs.

The remaining files are just configuration for converting this assembly code into a runnable ROM.

# nes.cfg

This file is the configuration file for ld65 (the ca65 toolchain's linker). It specifies how to lay out the final NES ROM.

```
# Linker configuration for ld65 — defines how to build the final .nes ROM file.

MEMORY {
    # RAM regions — not written to output file, used only for symbol/variable allocation.
    ZP:   file="",  start=$0000, size=$0100, type=rw;  # Zero page: 256 bytes of fast-access RAM
    RAM:  file="",  start=$0200, size=$0600, type=rw;  # General RAM ($0200-$07FF; $0100-$01FF is the stack)

    # ROM regions — written sequentially to the output file to form the .nes binary.
    HDR:  file=%O,  start=$0000, size=$0010, fill=yes, fillval=$00;  # 16-byte iNES header
    PRG:  file=%O,  start=$8000, size=$8000, fill=yes, fillval=$FF;  # 32KB PRG ROM (CPU $8000-$FFFF)
    CHR:  file=%O,  start=$0000, size=$2000, fill=yes, fillval=$00;  # 8KB CHR ROM (PPU pattern tables)
}

SEGMENTS {
    # RAM segments (variables — no output bytes generated).
    ZEROPAGE: load=ZP,  type=zp;   # Zero-page variables
    BSS:      load=RAM, type=bss;  # General uninitialized variables

    # ROM segments (written to the output file).
    HEADER:   load=HDR, type=ro;              # iNES header data
    CODE:     load=PRG, type=ro, start=$8000; # Executable code, fixed at $8000
    RODATA:   load=PRG, type=ro;              # Read-only data (follows CODE)
    VECTORS:  load=PRG, type=ro, start=$FFFA; # Interrupt vectors: NMI, Reset, IRQ (last 6 bytes of PRG)
    CHARS:    load=CHR, type=ro;              # Tile graphics (pattern table data)
}
```

## Makefile

As I mentioned, `make` is a build tool. It's not a compiler itself but it launches compilers and other tools to "make" executable programs. When `make` is run, it looks for a plain-text file called `Makefile` in the current directory and runs the commands it specifies to build all the "targets" (usually files) needed for the finished program.

I was given a `Makefile` that looks like this (comments added):

```
# Output ROM name (without extension).
TARGET = hello

# Default target — builds the .nes ROM.
all: $(TARGET).nes

# Link the assembled object file into a .nes ROM using the nes.cfg memory layout.
# Depends on the source and linker config so make rebuilds when either changes.
$(TARGET).nes: $(TARGET).s nes.cfg
	ca65 $(TARGET).s -o $(TARGET).o   # Assemble source to object file
	ld65 -C nes.cfg $(TARGET).o -o $(TARGET).nes  # Link object into .nes ROM

# Remove generated files to force a full rebuild next time.
clean:
	rm -f $(TARGET).o $(TARGET).nes

# Declare targets that don't correspond to real files.
.PHONY: all clean
```

## Building and running

With the files created, Claude didn't stop; it charged right ahead to build the ROM. It ran `make`, which in turn ran `ca65` (the assembler) and `ld65` (the linker) as specified in the `Makefile`:

```
⏺ Now let's build it:

⏺ Bash(make 2>&1)
  ⎿  ca65 hello.s -o hello.o
     ld65 -C nes.cfg hello.o -o hello.nes

⏺ That built cleanly. Open hello.nes in Mesen2 and you should see "HELLO NES" in
  white text on a dark blue background.
```

Claude announced "That built cleanly." And there in my working folder was a shiny new `hello.nes` ROM. I opened it in the Mesen emulator as directed. And saw my "HELLO NES" greeting!

![A NES emulator window showing a running ROM. It's a solid blue screen with the text "HELLO NES" at the center.](/assets/images/2026-05-22-claude-code-for-nes-development/hello_nes.png){: width="250" }

I don't have a means to test it on an actual NES console at the moment, but presumably it could be loaded onto a flash cart and run on original hardware. Meanwhile, it should work on almost any NES emulator out there.

"HELLO NES" demonstrates the basics of building a ROM from source code. The next step, of course, will be making actual games! I'm very confident Claude will be able to help me (and you) out there, too. That will take more than one blog post to cover, though. Until then!
