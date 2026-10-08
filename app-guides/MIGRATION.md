# MIGRATION · edition 2 (rev 3 -> rev 4)
The contract edition stays **2**. Rev 4 is a hardening revision of the kits, the guides and the shared scripts.

## Contract (S2) edits
- **S2.11 added** (Security and integrity rules): untrusted input, safeExtract only, npm `--ignore-scripts`, DOM via `dom.ts`, RPC allowlist, sandboxed windows, no body logging.
- **S2.1, S2.6, S2.8 edited** (Batch 3; the exact wording changes are listed in PATCHLOG "Batch 3").
- **S2.1 / S2.9 examples**: real-looking id tags replaced by `<tag>`; mint a tag with `python scripts/mint-id.py`. No rule changed.
- **S2.10 extended**: new look variable `--k-accent-text` (additive; old apps keep working).
- S2.2, S2.3, S2.4, S2.5 unchanged. CONTRACT-FP is now `b02dcf20` in every guide and launcher.

## What you must do
- **`.kvpart` files built with rev 3 must be rebuilt** (their guides carried the old contract and `.js`-less imports); use the rev 4 launchers.
- Apps (`.kvx`) built before still run: edition 1 and 2 are accepted. For new apps, relative imports need an explicit `.js` extension and styles live in `ui/*.css`.
- Existing Libraries are read unchanged; the index gains a `format` field the first time it is written.
- A Core built with rev 3 keeps working. Switching Cores is gone (D1 = drop): install the new Core package and start it yourself.

## New in the kit
`scripts/verify.py` (fp, contract, blueprint, core, app), `scripts/mint-id.py`, strict `assemble.py`, `tests/e2e.py`, fixtures in `tests/fixtures/`, and the Windows smoke harness (`npm run smoke`, `KOVA_SMOKE=1`, off by default).
