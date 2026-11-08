# LinkClipper Workflows

Procedures and learned workflows — the repeatable operational paths. Deep context lives in `Knowledgebase/` and `research/`; this is what you *run*. Each workflow = trigger, steps, verification.

## Release (extension)

**Trigger:** feature set closed for a version; changelog written.

1. Bump `manifest.json` version + `CHANGELOG.md` entry (user-visible truths only).
2. `runbooks → Knowledgebase/runbooks/cws-submission.md`: any new permission ⇒ changelog line + justification update + review impact note. No permission change ⇒ plain resubmission.
3. `git tag -a vX.Y.Z -m "summary"` (with `-c user.name` if the repo has no identity — see pitfalls) → push tag.
4. CI `release` workflow builds + attaches the zip; verify the asset exists (`gh release view vX.Y.Z --json assets`).
5. Local: run `tools/pack.ps1`, confirm zip size plausible (48 KB for 0.3.0), upload to CWS.
6. Close: update `Progress-Memory/STATUS.md` (Shipped) + month ledger.

Verification: release zip loads from repo root in a fresh Chromium profile without console errors.

## Screenshot regeneration (marketing/listing)

**Trigger:** dashboard visual language changed, or listing copy changed.

1. Follow `brand/README.md` states table (`?state=` grid/reader/item; larger virtual-time budget for photos).
2. **Read every PNG** — no shipping unseen pixels.
3. Copy into `brand/webstore-screenshots/` AND `linkclipper.github.io/assets/` (stable names — README embeds them).
4. Site push; CDN check with cache-bust query (~1 min lag).

## Working session (continuity)

**Trigger/end:** every session that changes code, docs, or a release.

1. Start: read `Progress-Memory/STATUS.md` (never archaeology).
2. Work in product repo; commit in coherent units.
3. End: update `STATUS.md` (Now / Shipped / In flight / Blocked+unblock / Next) and append to the month ledger. New persistent lessons → `Knowledgebase/research/` (that's how the cp1252 incident file was born).

## Store update (listing copy)

**Trigger:** listing text/asset change (not code).

1. Edit listing in CWS dashboard; screenshots from `brand/webstore-screenshots/`.
2. Listings re-review automatically on metadata change; expect up to a week.
3. Log the change in Progress-Memory (vX.Y.Z listing edits matter for reviewer consistency).

## Bug intake

1. Bug template lands in `linkclipper/issues`.
2. Triage labels: `bug` + area (`content-script`/`dashboard`/`reader`/`sync`).
3. Fix PRs reference the issue; harness reproduction preferred (`dev.html?state=`); screenshot-diff for visual bugs before/after.
