# Piantor Pro BT — Keymap Redesign Plan

## Hardware

- **Board**: Piantor Pro BT (split ergonomic, nRF52840 + Bluetooth, **ANSI/US**)
- **Layout**: 42 keys — 3 rows × 6 columns per half + 3 thumb keys per half
- **Files**:
  - `config/piantor_pro_bt.keymap` (the keymap)
  - `config/piantor_pro_bt.conf` (Kconfig — mouse enabled here)
- **OS context**: macOS, typing on a **US QWERTY** layout. `CMD = LGUI`, `OPT = LALT`.

### Key position index (0-based, as ZMK numbers them)

```
 0  1  2  3  4  5      6  7  8  9 10 11
12 13 14 15 16 17     18 19 20 21 22 23
24 25 26 27 28 29     30 31 32 33 34 35
         36 37 38     39 40 41
```

---

## Layer Map

| # | Name | Reached by |
|---|---|---|
| 0 | BASE | default |
| 1 | SYMBOL | hold `MO 1` (left **inner** thumb) |
| 2 | NUMBER | hold `MO 2` (right **inner** thumb) |
| 3 | NAV | right **outer** thumb (`&mo NAV`), or tri-layer: hold `MO 1` + `MO 2` |
| 4 | MOUSE | hold ENTER thumb (`&lt 4 RET`, left **middle** thumb) |
| 5 | FN | hold SPACE thumb (`&lt 5 SPACE`, right **middle** thumb) — **reserved/empty** |

Thumb row (base): `GUI · ENT(L4) · MO1  ‖  MO2 · SPC(L5) · NAV`

---

## Layer 0 — BASE ✅

```
 ESC    Q       W       E       R       T            Y     U       I       O       P       BSPC
 TAB    A/SFT   S/CTL   D/ALT   F/GUI   G            H     J/GUI   K/ALT   L/CTL   ;/SFT   '
 SFT*   Z       X       C       V       B            N     M       ,       .       /       MEH
                GUI    ENT/L4   MO1                   MO2   SPC/L5   NAV
```

- **Home-row mods** (hold) — opposite-hand trigger only (`hold-trigger-key-positions`):
  - Left: `A`=Shift, `S`=Ctrl, `D`=Alt, `F`=Cmd(GUI)
  - Right: `J`=Cmd(GUI), `K`=Alt, `L`=Ctrl, `;`=Shift
  - Mods are side-appropriate (`LGUI/LALT/...` left, `RGUI/RALT/...` right).
- `SFT*` (outer-left pinky) = tap-dance: **tap = Shift, double-tap = Caps Word**.
- `MEH` = `LS(LC(LALT))`, `HYPER` = `LS(LC(LA(LGUI)))`.
- ENTER and SPACE are layer-taps (tap = key, hold = layer).

---

## Layer 1 — SYMBOL ✅ (hold MO 1)

```
  €     !     @     #     $     %             ^     &     *     _     ;     =
  §     `     ~     {     (     [             :    CMD   OPT   CTL   SFT    +
        <     >     }     )     ]             |     "     \           ?     -
```

- Outer-right column (top→bottom): `= + -`.
- `?` sits at the column where `/` lives on BASE.
- `CMD OPT CTL SFT` (right home row) are **sticky mods** (`&sk LGUI/LALT/LCTRL/LSHFT`).
- `€` = `LA(LS(N2))`, `§` = `LA(N6)` — **Mac US-layout** Option combos.
- Empty cells (`&trans`) at: outer-left rows 0/1 untouched? No — outer-left top two are `€`/`§`; bottom-left and the gap at row 2 / C10 are transparent.

---

## Layer 2 — NUMBER ✅ (hold MO 2)

```
 RGB                 PREV  NEXT  PLAY               7     8     9           =
       BRI-  BRI+   VOL-  VOL+  MUTE                4     5     6           +
 BTCLR BT1   BT2    BT3   BT4   STUD          0     1     2     3           -
```

- Right hand = **numpad**: `u i o`=7 8 9, `j k l`=4 5 6, `m , .`=1 2 3, `n`=0.
- `= + -` outer-right column (matches SYMBOL).
- Left hand:
  - `Q`=RGB toggle
  - `E/R` = prev/next track, `T` = play/pause, `G` = mute
  - `A/S` = brightness down/up, `D/F` = volume down/up
  - Bottom row: `BT_CLR`, `BT1–BT4` (`&bt BT_SEL 0–3`), `B` = `&studio_unlock`

---

## Layer 3 — NAV ✅ (MO1 + MO2 tri-layer)

```
                                              HOME  PGDN  PGUP  END
       SFT   CTL   ALT   CMD                  ←     ↓     ↑     →
                                              SOL   W←    W→    EOL
```

- Right hand: `hjkl` = arrows; `u/i` = PgDn/PgUp; `y/o` = Home/End.
- `n/.` = start/end of line (`Cmd+Left` / `Cmd+Right`); `m/,` = word left/right (`Opt+Left` / `Opt+Right`).
- Left home row = **plain hold mods** (`&kp LSHFT/LCTRL/LALT/LGUI`) for select-while-arrowing.
- Everything else transparent.

---

## Layer 4 — MOUSE ✅ (hold ENTER thumb)

```
       BOOT  RST
                   RCLK  LCLK              MS←   MS↓   MS↑   MS→
                                           SCL↓  SCL↑
```

- Right home row `hjkl` = mouse move (`&mmv MOVE_LEFT/DOWN/UP/RIGHT`).
- `n/m` = scroll down/up (`&msc SCRL_DOWN/UP`).
- `D` = right click (`&mkp RCLK`), `F` = left click (`&mkp LCLK`).
- `Q` = bootloader, `W` = sys reset (top row, left).
- Requires `CONFIG_ZMK_POINTING=y` (set in `.conf`).

---

## Layer 5 — FN ✅ (hold SPACE thumb)

Reserved — all `&trans` for now. Free to fill later.

---

## Global combos ✅

| Keys | Positions | Output |
|---|---|---|
| W + E | 2, 3 | ESC |
| X + C | 26, 27 | TAB |
| I + O | 8, 9 | BSPC |
| , + . | 32, 33 | ENTER |

(`timeout-ms = 50`.)

---

## Custom behaviors ✅

- `hml` / `hmr` — home-row-mod hold-taps (balanced flavor, `tapping-term 200`, `quick-tap 175`, `require-prior-idle 150`, opposite-hand `hold-trigger-key-positions`, `hold-trigger-on-release`).
- `td_shift` — tap-dance: Shift / Caps Word.
- `conditional_layers` — `if-layers <1 2> then-layer <3>`.

---

## Build / flash

1. Commit + push → GitHub Actions builds firmware (`.uf2`) automatically.
2. Download artifacts from the Actions run.
3. Flash each half (bootloader = double-tap reset, or BOOT key on NUMBER layer is **not** mapped — use physical reset).
4. Test, iterate.

## Status

All six layers + combos + behaviors implemented in `config/piantor_pro_bt.keymap`. ✅
