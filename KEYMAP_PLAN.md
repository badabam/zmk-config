# Piantor Pro BT — Keymap Redesign Plan

## Hardware

- **Board**: Piantor Pro BT (split ergonomic, nRF52840 + Bluetooth)
- **Layout**: 42 keys — 3 rows × 6 columns per half + 3 thumb keys per half
- **File to edit**: `config/piantor_pro_bt.keymap`

---

## Current Layout (baseline)

### Layer 0 — QWERTY (default)

```
┌───────┬───┬───┬───┬───┬───┐   ┌───┬───┬───┬───┬───┬───────┐
│  TAB  │ Q │ W │ E │ R │ T │   │ Y │ U │ I │ O │ P │ BSPC  │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│ LCTRL │ A │ S │ D │ F │ G │   │ H │ J │ K │ L │ ; │  '    │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│ LSHFT │ Z │ X │ C │ V │ B │   │ N │ M │ , │ . │ / │  ESC  │
└───────┴───┴───┴───┴───┴───┘   └───┴───┴───┴───┴───┴───────┘
                  ┌────┬────┬─────┐ ┌─────┬─────┬──────┐
                  │GUI │LWR │ SPC │ │ ENT │ RSE │ RALT │
                  └────┴────┴─────┘ └─────┴─────┴──────┘
```

### Layer 1 — NUMBER (hold LWR)

```
┌───────┬────┬────┬────┬────┬──────┐   ┌────┬────┬────┬─────┬───┬───────┐
│  TAB  │ 1  │ 2  │ 3  │ 4  │  5   │   │ 6  │ 7  │ 8  │  9  │ 0 │ BSPC  │
├───────┼────┼────┼────┼────┼──────┤   ├────┼────┼────┼─────┼───┼───────┤
│ LCTRL │BT1 │BT2 │BT3 │BT4 │ BT5  │   │ ← │ ↓  │ ↑  │  →  │   │       │
├───────┼────┼────┼────┼────┼──────┤   ├────┼────┼────┼─────┼───┼───────┤
│ LSHFT │BTCL│RGB │RST │BOOT│UNLCK │   │    │    │    │     │   │       │
└───────┴────┴────┴────┴────┴──────┘   └────┴────┴────┴─────┴───┴───────┘
                    ┌────┬──────┬─────┐ ┌─────┬──────┬──────┐
                    │GUI │(held)│ SPC │ │ GUI │      │ SPC  │
                    └────┴──────┴─────┘ └─────┴──────┴──────┘
```

### Layer 2 — SYMBOL (hold RSE)

```
┌───────┬───┬───┬───┬───┬───┐   ┌───┬───┬───┬───┬───┬───────┐
│  TAB  │ ! │ @ │ # │ $ │ % │   │ ^ │ & │ * │ ( │ ) │ BSPC  │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│ LCTRL │   │   │   │   │   │   │ - │ = │ [ │ ] │ \ │   `   │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│ LSHFT │   │   │   │   │   │   │ _ │ + │ { │ } │ | │   ~   │
└───────┴───┴───┴───┴───┴───┘   └───┴───┴───┴───┴───┴───────┘
                  ┌────┬──────┬─────┐ ┌─────┬──────┬──────┐
                  │GUI │      │ SPC │ │ ENT │(held)│ RALT │
                  └────┴──────┴─────┘ └─────┴──────┴──────┘
```

### Layers 3–8 — EXTRA 1–6

All keys are `&trans` (transparent / unused).

---

## Proposed Changes

> **Fill this in step by step together.**

### Layer 0 — QWERTY

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layer 1 — NUMBER

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layer 2 — SYMBOL

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layer 3 — EXTRA 1 (rename?)

Proposed name: _TBD_

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layer 4 — EXTRA 2 (rename?)

Proposed name: _TBD_

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layer 5 — EXTRA 3 (rename?)

Proposed name: _TBD_

| Key position | Current | Proposed | Reason |
|---|---|---|---|
| _to be defined_ | | | |

### Layers 6–8 — EXTRA 4–6

_Keep empty / repurpose — TBD_

---

## ZMK Cheat Sheet (common bindings)

| Binding | Meaning |
|---|---|
| `&kp X` | Key press |
| `&mo N` | Momentary layer N (hold) |
| `&lt N X` | Layer-tap: hold = layer N, tap = key X |
| `&mt MOD X` | Mod-tap: hold = modifier, tap = key X |
| `&tog N` | Toggle layer N |
| `&to N` | Switch to layer N permanently |
| `&trans` | Transparent (fall through to layer below) |
| `&none` | Blocked (do nothing) |
| `&bt BT_SEL N` | Select Bluetooth profile N (0–4) |
| `&bt BT_CLR` | Clear current BT pairing |
| `&rgb_ug RGB_TOG` | Toggle RGB underglow |
| `&sys_reset` | Soft reset |
| `&bootloader` | Enter bootloader (for flashing) |

---

## Implementation Order

1. Finalise this plan (layer by layer, step by step)
2. Edit `config/piantor_pro_bt.keymap`
3. Commit & push → GitHub Actions will build firmware
4. Flash and test

---

## Open Questions

- [ ] Keep QWERTY on layer 0, or switch to Colemak / Dvorak / other?
- [ ] What should the extra layers be used for? (Nav, F-keys, Numpad, Mouse, macOS shortcuts, …)
- [ ] Any home-row mods (`&mt`) desired?
- [ ] Combos or tap-dances needed?
- [ ] Layer-tap (`&lt`) on thumb keys instead of plain `&mo`?
