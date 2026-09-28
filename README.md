# layer-check-cross-local-driver-layer

A cross-deployment check fixture: the host (`target: local`) driver venue for the
`check-cross-local-http` bed.

The `check-cross-local-driver-layer` candy establishes a **host venue** for the
bed's local **DRIVER** member: a `command:` check placed under this member runs on
the host against a **separate** pod SUBJECT — a cross-kind pair (local driver,
pod subject). It is USER-level only (a marker under `$HOME`, no root, no sudo, no
gates) so `bringUpMembers` applies it unattended via `charly fleet add`.

The candy is a **fixture**: it ships no user-facing service and has no `skill:`
entity. Its acceptance steps live in its `plan:` (`mkdir:` + `write:` run steps,
`file:` `check:` probes, and two `context: [runtime]` `command:` probes) and are
baked into the `ai.opencharly.description` OCI label. The owning family skill is
`/charly-check:check`; the missing owning `skill:` entity is tracked by
[opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `check-cross-local-driver-layer` |
| Venue | host (`target: local`), user-level only |
| Effect | writes `$HOME/.cache/charly-cross-local-driver-marker` (mode `0644`) |
| Plan | `mkdir:` + `write:` run steps, `file:` `check:` probes, two `runtime` `command:` probes |
| Owns | 0 `skill:` entities (fixture) |
| Service / port | none |

## How to use it

Compose it as a layer ref on a `target: local` deploy (a `local:` node with a
`host:` field). A box is a `candy:` node carrying the box's `base:` image and a
nested `candy:` list of layer refs (the nested `candy:` is the composition list;
the outer `candy:` is the box body):

```yaml
my-box:
  candy:                  # the box body (an IMAGE is a `candy:` node carrying `base:`)
    base: fedora          # the box's base image
    candy:                # the box's composition list
      - '@github.com/opencharly/layer-check-cross-local-driver-layer:v2026.239.1625'
```

The fixture is driven by the `check-cross-local-http` bed as its local DRIVER
member, not by a user box.

## Layout

- `charly.yml` — the `check-cross-local-driver-layer:` candy entity (no `skill:`
  entity).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning family skill: `/charly-check:check`
- Missing `skill:` entity: [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291)
- Authoring reference: `/charly-image:layer`
- [`opencharly/marketplace`](https://github.com/opencharly/marketplace) — the projected corpus
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
