---
name: keyball39-edit-keymap
description: Edit and review the ZMK configuration for this Keyball39 repository. Use when changing keys, layers, combos, hold-taps, tap-dances, macros, Bluetooth bindings, mouse behavior, board/shield configuration, or the generated keymap diagram.
---

# Edit the Keyball39 keymap

Work from the repository root.

## Know the source files

- Treat `config/keyball39.keymap` as the source of truth for keys, layers, behaviors, macros, and combos.
- Treat `config/keyball39.conf` as the shared ZMK feature and Bluetooth configuration.
- Treat `config/boards/shields/keyball_nano/` as hardware-specific shield configuration; change it only for hardware or pin behavior.
- Treat `config/keyball39.json` as the physical layout consumed by keymap-drawer.
- Treat `build.yaml` as the list of firmware build targets.
- Treat `keymap_drawer.config.yaml` as diagram parsing and styling configuration.
- Treat `keymap-drawer/keyball39.yaml` and `keymap-drawer/keyball39.svg` as generated outputs. Do not hand-edit them unless the user explicitly requests it.

## Edit safely

1. Read the complete affected behavior and layer blocks before editing.
2. Preserve the 39-binding order in every layer: 10 top keys, 10 home keys, 10 bottom keys, then 9 thumb/outer keys.
3. Keep numeric layer constants, layer node order, `&lt`, `&mo`, `&to`, `&sl`, and combo `layers` references consistent.
4. Check that every custom binding used by a layer or combo is declared under `behaviors` or `macros`.
5. Check combo positions against `config/keyball39.json`; positions follow the flattened physical-layout order.
6. Preserve valid devicetree syntax: angle brackets, semicolons, node braces, and `#binding-cells` arity.
7. Make the smallest requested change and inspect `git diff --check` plus `git diff` afterward.

## Validate the result

- Confirm all edited layers still contain 39 bindings.
- Search for renamed or removed behavior and layer references.
- If local ZMK tooling is unavailable, state that structural checks passed but compilation remains for GitHub Actions.
- Expect `.github/workflows/build.yml` to compile left, right, and settings-reset targets after push or pull request.
- Expect `.github/workflows/keymap_drawer.yml` to regenerate the diagram when `config/**` or its configured inputs change.

Do not commit or push unless the user explicitly asks.
