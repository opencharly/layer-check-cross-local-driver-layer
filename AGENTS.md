# AGENTS.md — layer-check-cross-local-driver-layer

Standalone candy repo for the `check-cross-local-driver-layer` fixture — the host
(`target: local`) DRIVER venue for the `check-cross-local-http` bed. It writes a
user-level marker under `$HOME/.cache` and carries **no `skill:` entity**.

Canonical files:

- `charly.yml` — the `check-cross-local-driver-layer:` candy entity (`mkdir:` +
  `write:` run steps, `file:` `check:` probes, two `context: [runtime]`
  `command:` probes; no `skill:` entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-check:check` — the owning family skill: the check plan authoring
  reference, the cross-deployment driver/subject model, the disposable beds, and
  the R10 change classes. Load before editing any `plan:` step.
- `/charly-local:local-deploy` — the `target: local` deploy surface (the `host:`
  field, the `local:` substrate, the install ledger) this member runs on. Load
  when a change touches the host-venue path.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, package sections, service declarations).
  Load before editing any entity field or plan step.
- **Missing owning skill:** this fixture has no `skill:` entity, so no
  `/charly-check-cross-local-driver-layer:*` page is projected for it. The gap is
  recorded against the named batch
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).

## Build / validate / test

- `charly box validate` at the repo root — the structural check: the manifest
  must parse and validate at the installed charly.
- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has no
  per-repo candy gate. Its only workflow file is
  `.github/workflows/tag-on-merge.yml`.
- The fixture's proof is its `plan:` — the marker write plus the `file:` probes
  and the two `runtime` `command:` probes — exercised by the
  `check-cross-local-http` bed.

## Modify this repo

- Keep the fixture USER-level: no root, no sudo, no gates, so
  `bringUpMembers` can apply it unattended.
- Keep the marker path and content stable: the bed reads
  `$HOME/.cache/charly-cross-local-driver-marker` back to confirm the host-driver
  member applied.
- If an owning skill is authored, add the `skill:` entity here and update this
  signpost and the README in the same change.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
