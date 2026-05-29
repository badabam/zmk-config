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

## Layer Index

| # | Name | How to reach |
|---|---|---|
| 0 | QWERTY | default |
| 1 | _TBD_ | hold left inner thumb (MO 1) |
| 2 | _TBD_ | hold right inner thumb (MO 2) |
| 3 | _TBD_ | hold MO 1 + MO 2 simultaneously (tri-layer) |
| 4 | _TBD_ | hold left outer thumb (ENTER key) |
| 5 | _TBD_ | hold right inner thumb (SPACE key) |
| 6–8 | EXTRA 4–6 | _TBD_ |

---

## Proposed Changes

### Layer 0 — QWERTY ✅ decided

**New layout:**

```
┌───────┬───┬───┬───┬───┬───┐   ┌───┬───┬───┬───┬───┬───────┐
│  ESC  │ Q │ W │ E │ R │ T │   │ Y │ U │ I │ O │ P │ BSPC  │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│  TAB  │ A │ S │ D │ F │ G │   │ H │ J │ K │ L │ ; │   '   │
├───────┼───┼───┼───┼───┼───┤   ├───┼───┼───┼───┼───┼───────┤
│ SHIFT │ Z │ X │ C │ V │ B │   │ N │ M │ , │ . │ / │  MEH  │
└───────┴───┴───┴───┴───┴───┘   └───┴───┴───┴───┴───┴───────┘
           ┌─────┬──────┬────────────┐ ┌────────────┬──────┬─────────┐
           │ GUI │ MO 1 │  ENT / L4  │ │  SPC / L5  │ MO 2 │  HYPER  │
           └─────┴──────┴────────────┘ └────────────┴──────┴─────────┘
```

**Key details:**

| Key | ZMK binding | Notes |
|---|---|---|
| ESC (outer-L row 0) | `&kp ESC` | was TAB |
| TAB (outer-L row 1) | `&kp TAB` | was LCTRL |
| SHIFT (outer-L row 2) | `&td_shift` | tap = LSHFT, double-tap = CAPS_WORD |
| MEH (outer-R row 2) | `&kp LS(LC(LALT))` | was ESC |
| ENT / L4 (left outer thumb) | `&lt 4 RET` | tap = ENTER, hold = layer 4 |
| SPC / L5 (right inner thumb) | `&lt 5 SPACE` | tap = SPACE, hold = layer 5 |
| HYPER (right outer thumb) | `&kp LS(LC(LA(LGUI)))` | was RALT |
| MO 1 (left inner thumb) | `&mo 1` | unchanged |
| MO 2 (right inner thumb) | `&mo 2` | unchanged |
| GUI (left outer thumb) | `&kp LGUI` | unchanged |

**Combos (global — active on all layers):**

| Keys | Positions | Output |
|---|---|---|
| W + E | 2, 3 | ESC |
| X + C | 26, 27 | TAB |
| I + O | 8, 9 | BSPC |
| , + . | 32, 33 | ENTER |

**New ZMK behaviors needed:**

```c
// Tap-dance: tap = SHIFT, double-tap = Caps Word
td_shift: tap_dance_shift {
    compatible = "zmk,behavior-tap-dance";
    #binding-cells = <0>;
    tapping-term-ms = <200>;
    bindings = <&kp LSHFT>, <&caps_word>;
};

// Tri-layer: holding MO 1 + MO 2 activates layer 3
conditional_layers {
    compatible = "zmk,conditional-layers";
    tri_layer {
        if-layers = <1 2>;
        then-layer = <3>;
    };
};
```

---

### Layer 1 — _TBD_ (hold MO 1)

> **To be decided** — what goes here?

Common options: number row, F-keys, left-hand numbers + right-hand nav, …

---

### Layer 2 — _TBD_ (hold MO 2)

> **To be decided** — what goes here?

Common options: symbols, brackets/operators, …

---

### Layer 3 — _TBD_ (tri-layer: MO 1 + MO 2)

> **To be decided** — activated only when both MO 1 and MO 2 are held.

Common use: system/config (BT, RGB, reset, boot) — keep dangerous keys behind a two-hand chord.

---

### Layer 4 — _TBD_ (hold ENTER thumb)

> **To be decided** — what goes here?

---

### Layer 5 — _TBD_ (hold SPACE thumb)

> **To be decided** — what goes here?

---

### Layers 6–8 — EXTRA 4–6

_Keep empty for now, decide later._

---

## ZMK Cheat Sheet (common bindings)

| Binding | Meaning |
|---|---|
| `&kp X` | Key press |
| `&mo N` | Momentary layer N (hold) |
| `&lt N X` | Layer-tap: hold = layer N, tap = key X |
| `&mt MOD X` | Mod-tap: hold = modifier, tap = key X |
| `&td_NAME` | Tap-dance (custom behavior) |
| `&caps_word` | Caps Word (capitalises until non-alpha key) |
| `&tog N` | Toggle layer N |
| `&to N` | Switch to layer N permanently |
| `&trans` | Transparent (fall through to layer below) |
| `&none` | Blocked (do nothing) |
| `&bt BT_SEL N` | Select Bluetooth profile N (0–4) |
| `&bt BT_CLR` | Clear current BT pairing |
| `&rgb_ug RGB_TOG` | Toggle RGB underglow |
| `&sys_reset` | Soft reset |
| `&bootloader` | Enter bootloader (for flashing) |
| `LS(LC(LALT))` | MEH modifier chord |
| `LS(LC(LA(LGUI)))` | HYPER modifier chord |

---

## Implementation Order

1. ~~Layer 0~~ ✅ decided
2. Decide layers 1–5 (step by step)
3. Edit `config/piantor_pro_bt.keymap`
4. Commit & push → GitHub Actions will build firmware
5. Flash and test

---

## Open Questions

- [ ] Layer 1 purpose and contents?
- [ ] Layer 2 purpose and contents?
- [ ] Layer 3 purpose and contents (tri-layer)?
- [ ] Layer 4 purpose and contents (ENTER-hold)?
- [ ] Layer 5 purpose and contents (SPACE-hold)?
