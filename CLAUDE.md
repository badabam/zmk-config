# CLAUDE.md — Piantor keymap project

This is a ZMK config repo. The active work is a **custom Piantor Pro BT keymap**.
Read `KEYMAP_PLAN.md` for the full, authoritative layer-by-layer design — this
file is the quick pickup summary.

## What's been done

- Branch: **`plan`** (PR #1, draft). All keymap work lives here.
- Implemented the full redesign in `config/piantor_pro_bt.keymap` (6 layers,
  home-row mods, tap-dance, tri-layer, combos, mouse).
- Enabled `CONFIG_ZMK_POINTING=y` in `config/piantor_pro_bt.conf` (mouse layer).

## Files that matter

| File | Purpose |
|---|---|
| `config/piantor_pro_bt.keymap` | **The keymap** — edit this |
| `config/piantor_pro_bt.conf` | Kconfig (mouse, BT, sleep, etc.) |
| `KEYMAP_PLAN.md` | Full design spec + key-position index |
| `build.yaml` | CI build matrix (Piantor left/right + nice_view) |

> The board ships a default keymap at
> `boards/arm/piantor_pro_bt/piantor_pro_bt.keymap`, but the repo's
> `config/piantor_pro_bt.keymap` **overrides** it. Only edit the `config/` one.

## Layer summary (see KEYMAP_PLAN.md for grids)

| # | Name | Reached by | Gist |
|---|---|---|---|
| 0 | BASE | default | QWERTY + home-row mods + tap-dance Shift/CapsWord |
| 1 | SYMBOL | hold L inner thumb (`&mo SYM`) | symbols, `€`/`§`, sticky mods, `=+-` outer-right |
| 2 | NAV | combo: R mid + R outer thumbs together | vim arrows, page/home/end, word/line jumps |
| 3 | NUMBER | hold both inner thumbs (tri-layer via HELPER) | right-hand numpad, media/BT/RGB on left |
| 4 | MOUSE | hold R outer thumb (`&mo MOUSE`) | mouse move on hjkl, scroll, click |
| 5 | FN | hold L outer thumb (`&mo FN`) | reserved, empty |
| 6 | HELPER | R inner thumb — transparent, only for NUMBER tri-layer | (no direct use) |

## Conventions & facts

- **macOS, US QWERTY layout.** `CMD=LGUI`, `OPT=LALT`. `€`=`LA(LS(N2))`, `§`=`LA(N6)`.
- Board is **ANSI/US** (not ISO).
- Home-row mods use `hold-trigger-key-positions` (opposite-hand-only) to avoid
  misfires on same-hand rolls. Two behaviors: `hml` (left), `hmr` (right).
- Key positions are 0-based row-major: `0-11` top row, `12-23` home, `24-35`
  bottom, `36-41` thumbs. Diagram in `KEYMAP_PLAN.md`.

## How to build / verify

- Push to `plan` → GitHub Actions (`.github/workflows/build.yml`) builds `.uf2`
  firmware. Check the run for compile errors before assuming success.
- There is no local test suite; the compiler (CI) is the verification.

## Open / next ideas

- Layer 5 (FN) is empty — candidate for F-keys, app shortcuts, or a "game" layer.
- `BT5` and `&sys_reset` / `&bootloader` are not currently mapped (reset via
  physical button). Could add behind the tri-layer if wanted.
- Tune `tapping-term-ms` / `require-prior-idle-ms` on the home-row mods after
  real-world typing.
