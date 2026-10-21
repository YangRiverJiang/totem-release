# Totem release repository: agent guide

This repository distributes the Totem APK, user manual and release checksums.
It is not the Android, GNSS, server or numerical engine source repository.
Instructions are relative to this checkout and do not require a workstation path.

## Ownership

- `README.md`: download instructions, package/version/build/source identity and
  release notes. `docs/`: user manual; `media/`: documentation images.
- Root APK and `checksums.sha256`: the actual published binary and its digest.
- [totem](https://github.com/YangRiverJiang/totem) owns application/AAR sources.
  [sleepy](https://github.com/YangRiverJiang/sleepy) owns the separately licensed
  embedded GNSS engine. Build/algorithm fixes belong there, not in this repository.
- Server, BEV and Studio development releases are separate. Do not infer that a
  historical Totem APK here matches the latest internal TotemX/server deployment.

## Before editing

Inspect `git status --short`, branch and remote. Read the current README, LICENSE
and checksum manifest. Preserve existing APK/manual assets for documentation-only
changes. Credentials, keystores, private datasets, internal diagnostic logs and
local operational notes do not belong in this distribution repository.

## When a release is explicitly requested

1. Obtain the exact authorized signed build from the source build workflow. Verify
   its package/edition, version, source commit, build date, ZIP alignment and signer
   using Android build tools (`apksigner verify --print-certs` and `zipalign`).
   Do not rebuild or re-sign a binary here or substitute a debug certificate.
2. Update APK filename, README identity/changelog, manual source/PDF dates and the
   checksum manifest together. Manuals should explain actual user operations;
   inspect the rendered PDF, links and layout before publishing it.
3. Default public materials describe Totem. Include TotemX or other editions only
   when the user's requested release scope includes them; do not accidentally
   distribute a full-feature internal build as the restricted edition.
4. Compute SHA-256 from the actual final APK; do not copy a stale digest. Preserve
   license notices. Signing keys, map API keys and private server access are
   external release prerequisites, never repository content.
5. Prefer an emulator/disposable device for clean-install acceptance. Never clear
   or uninstall a field-data phone app to test the download.

Only publish artifacts or rewrite release history with explicit session scope.
An earlier one-commit release layout is not standing permission to reset Git,
force-push or delete old artifacts. Normal documentation updates are ordinary
commits and do not require replacing the APK, changing its version or regenerating
the existing manual/checksums unless those corresponding assets changed.

## Validation for documentation-only work

Check relative links and `git diff --check`; verify the APK, manual and checksum
manifest are untouched. No Android build, device operation or server restart is
needed. Report source changes separately from published-binary validation.
