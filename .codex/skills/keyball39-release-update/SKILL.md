---
name: keyball39-release-update
description: Validate, commit, and publish updates to this Keyball39 ZMK repository. Use when preparing a repository update, reviewing changed firmware files, creating a commit, pushing to GitHub, or checking the GitHub Actions firmware build and keymap-drawer result.
---

# Release a Keyball39 update

Work from the repository root and preserve unrelated user changes.

## Review before publishing

1. Run `git status --short --branch`, `git diff --check`, and `git diff`.
2. Confirm the change belongs in one or more of these areas:
   - `config/keyball39.keymap`: logical keymap
   - `config/keyball39.conf`: common firmware options
   - `config/boards/shields/keyball_nano/`: hardware shield
   - `build.yaml`: build matrix
   - `config/west.yml`: ZMK and module revisions
   - `keymap_drawer.config.yaml`: diagram parsing or style
3. Treat `keymap-drawer/keyball39.yaml` and `.svg` as generated files. Allow the drawing workflow to update them unless the user requests a local regeneration.
4. For keymap edits, apply the checks in `$keyball39-edit-keymap` before publishing.

## Commit and push

Only commit or push when the user explicitly requests it.

1. Pull or fetch only after checking for local changes; never discard user work.
2. Stage only the files relevant to the requested update.
3. Use a concise commit message describing the user-visible keymap or firmware change.
4. Show the staged diff summary before committing.
5. Push the current branch to its configured upstream; never force-push unless explicitly requested.

## Verify GitHub automation

- `.github/workflows/build.yml` runs on push, pull request, and manual dispatch using ZMK `v0.3`.
- `build.yaml` builds `keyball39_left`, `keyball39_right` with `studio-rpc-usb-uart`, and `settings_reset` for `nice_nano_v2`.
- `.github/workflows/keymap_drawer.yml` commits generated diagram changes with a `[Draw]` prefix.
- After pushing, report the commit and whether both workflows passed. If GitHub access or CLI authentication is unavailable, provide the exact verification still needed instead of claiming success.

Do not alter firmware files merely to make a release; stop and report validation failures.
