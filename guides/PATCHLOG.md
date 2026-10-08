# PATCHLOG (cumulative)
## Batch 1 (rev 4): scripts and tooling
- C5/H2 assemble.py: temp-dir validate then merge; samefile fix, total from blueprint, path/symlink/owns/dup/setId rules, REPLACED; test: asm_* (11)
- H2/H3 pack-part.py: blueprint validation (setId, 3-6 parts, disjoint owns, messages), --out/KOVA_OUT, per-part stamp, junk; test: pp_* (7)
- H5/H3 pack-kvx.py: validation (edition, entry, deps, opens, sizeHint), NFKD slug, stamped copy in zip only, --keep-stamp; test: kvx_* (4)
- C4 (wiring) wire-app.py: .js specifiers, try/catch, all ui/*.css, missing-export check; test: wire_* (4, ESM import in Node)
- H1 pack-core.py + verify.py (fp|contract|blueprint|core|app) + make-manifest.py + kit.manifest.json; test: core_pack_*, verify_*, manifest_clean_kit
- H1 setup.mjs/build.mjs/apply-part.mjs: 4 page ids, dep conflicts, npm status, basename collisions, setId guard; test: setup_mjs_checks, build_mjs_collision, apply_part_mjs
- fp.py (alias of verify fp --write), mint-id.py, tools/sync-kits.py, tests/run_tests.py (43 tests), README.txt, package.json scripts
- Added scripts/kvlib.py (shared validation code; also synced to app-kit). Guides, S2 blocks and src/kit untouched (verify fp ok, CONTRACT-FP 7da9cd3b).
- Not done: npm-install failure message untested (no network in tests); contract check still reports dangling S10/S11/S12.x/S14 (guide fix is for a later batch); "rev 4" label is only in README so far.
- Run `python scripts/make-manifest.py` again at the end of Batches 2 and 5.

## Batch 2 (rev 4): kit libraries (D1=drop, D2=keep-autohide-with-fixes)
- C4 2.1 convert.ts: relative specifiers -> .js/.mjs/index.js (static, dynamic, export-from), html src/href, root package.json {"type":"module"}, sourcesContent kept; test: convert.test.mjs (loads with --no-experimental-detect-module)
- C6 2.2 zip.ts (new; yauzl/yazl deps): listEntries/readEntry/safeExtract/createZip/inspectZip + checkEntries (KV-IN-001 unsafe, KV-IN-011 size); test: zip.test.mjs (18 crafted-zip cases)
- C6 2.3 deps.ts: validate, --ignore-scripts, specs after "--", npm ci with lockfile, tree kill, reasons invalid-spec|offline|timeout|failed; test: deps.test.mjs
- C2 2.4 schema.ts (new): types, validators, withDefaults, parseAccent, npm validators; test: schema.test.mjs
- C1/C2 2.5 seam-types.ts, main.ts: index.mutate, marker, AppInfo split, onBeforeChange/onChoose, install confirm, Seal without switching, Frame chooseOne/restart; main.ts composite apps.list + hooks before frame.start(); test: typecheck (shimmed), rpc.test.mjs
- H6 2.6 atomic.ts retry/async/unique tmp/cleanupTmp: atomic.test.mjs | C6/H5 2.7 fingerprint.ts: fingerprint.test.mjs | 2.8 stamp.ts: stamp.test.mjs
- C6 2.9 accent/look/base.css (--k-accent-text, parseAccent fallback; NEW VARIABLE for S2.10 in Batch 5): accent.test.mjs | H3 2.10 redact.ts + MessageLog: redact.test.mjs
- 2.11 envelope.stamp + handshake phases/firstStartGraceMs (HsCtx.neverStartedOk): envelope.test.mjs | C6/D2 2.12 rpc allowlist, sandboxed window, CSP, focus-only polling, Ctrl+Shift+M, DRAG_REGION_PX=28: rpc.test.mjs, polling.test.mjs
- C6 2.13 dom.ts + lint.test.mjs | 2.14 icons Map, select a11y + one listener, SVG glyphs: lint.test.mjs | H6/H1 2.15 package.json (electron ^43.0.0), tsconfig.json, scripts, README
- New files: src/kit/schema.ts, src/kit/zip.ts, src/kit/dom.ts, tsconfig.json, tests/kit/** (run-all.mjs, *.test.mjs, stubs/, zipmake.py, zipdir.mjs, _setup.mjs).
- Not done / limits (no network): electron ^43.0.0 is the offline fallback, esbuild ^0.25.0 unverified; npm install not run; typecheck run with ambient shims (no @types/node/electron) so electron/node typings are unchecked; tests transpile with TypeScript + stubs (electron, esbuild) instead of esbuild bundles.
- yauzl/yazl code paths (listEntries/safeExtract/createZip) are UNTESTED here (round trip test skips when not installed); rejection rules are tested on the central directory via checkEntries. Ratio rule skips entries < 64 KiB (ratioMinBytes). main.ts untested (parts absent). Guides/S2 blocks untouched (CONTRACT-FP 7da9cd3b); guides still describe the old Seal/index API (later batch).

## Batch 3 (rev 4): core guides (D1=drop, D2=keep-autohide-with-fixes)
- 3.1/3.13 S2.11 added (identical in parts 1-5 and core-3); S2.1/S2.6/S2.8 edited as listed; fp.py --write run; CONTRACT-FP now 8209dbec; test: verify_fp_real_kit_ok (core guides), verify_contract_core_guides_ok
- 3.2 Wiring contract box (6 lines, same text) in parts 1-5 and core-3; test: tests/guides_check.py (onBeforeChange, onChoose, "Wiring contract", S2.11 in every part)
- 3.3-3.8 parts 1-5 rewritten rows (schema.ts "Use kit", index.mutate/marker.update, retention, repair bundle, zip.ts/consent pipeline, sandbox+partition, RPC method list, first-run card, page-id check, Manager dom.ts/Cores tab/backup warning); S12.1..S12.11 numbering (old D1..D11) + references fixed; test: guides_check.py (stale "S10","S14","repair note","index.write","switchCore"), verify contract
- 3.9 core-3: two kit reads allowed, verify.py core before pack-core, P5S-* table with header, D1=drop Core handling, KV-CR re-scoped | 3.10 core-1: mint-id, requestCard table; pack-core.py copies requestCard to core.json; verify.py checks keys (blueprint/core/contract); test: verify_request_card
- 3.11/3.12 "repair prompt"/"repair bundle" everywhere (S2.2/S2.3 keep old words: not authorised to edit); START-HERE.txt, README.txt, repair.md updated; sync-kits.py run (app-kit verify.py/fp.py refreshed)
- Deviations: main.ts (kit) registers onBeforeChange/onChoose, so the guides say the Runner/Frame PROVIDE the callbacks; Frame (not Manager) draws the consent dialog/result sheet because RPC cannot pass UI callbacks; consent spec lives in [S12.8].
- Not done: "Delete now" has no seam parameter, so it uses settings key remove.deleteNow (needs a seam change in a later batch); app guides still carry old S2.1/6/8 blocks and old CONTRACT-FP (Batch 4); seam-types.ts comment still says "repair note" (src/kit untouched); tests 38/45, 7 skipped (no esbuild).
## Batch 4 (rev 4): app guides (shared scripts/ guides kept in sync)
- 4.1 C4: small-app/part/profile.md carry the 4-line import rule (.js extension, no CSS-from-JS, no JSX, type:module); small-app example now imports ./util.js; test: app_guides_test no_extensionless_relative_import, js_extension_rule_present
- 4.2 libraries: exact recipes (a) vendor-npm relative ESM, (b) createRequire in backend; no-bare-import reason, no lifecycle scripts; small-app.md, part.md
- 4.3 identity: tags -> <tag> in guides (core part-1/2 and small-app, incl. S2.1/S2.9 examples, FPs regenerated); mint-id.py in app-1 and small-app; test: no_example_tags
- 4.4 H1: "Check (one capped command), then pack" in app-1/2/3, small-app, part.md (verify.py app; for a lone part ignore the kova.json FAIL, no partial mode)
- 4.5 repair.md (app): active-version bundle, UNTRUSTED EVIDENCE rule, verify then pack, source kova.json untouched | 4.6 app-1: rules list, example blueprint now 3 parts with <tag>; test: example_blueprint_valid
- 4.7 app-3: assemble strict -> wire -> verify app -> pack; strangers/collisions = rebuild list, no silent fix | 4.8 profile.md: root.json order, atomic write+EPERM, #RRGGBB, railLabels | 4.9 app-kit README
- S2 blocks in small-app/part.md replaced by canonical text (S2.11 added); CONTRACT-FP now e2bf40f7; verify.py contract now accepts several dirs (synced to app-kit); manifest regenerated; test: app_guides_test.py (6), verify_contract_both_kits
- Not done/limits: verify.py app has no partial-app mode; tests core_pack_ok_and_junk, verify_core_positive_and_negatives fail only where Electron types are missing (sandbox), pass-or-skip otherwise; build_mjs_collision skipped
## Batch 5 (rev 4): integration and release
- 5.1 a-e: contract ok across core, app guides and launchers (CONTRACT-FP b02dcf20); fp clean; stale-term grep clean (hits only in tests, ProfileBasics, kit window.ts, S2.3/seam-types "repair note" comments: not edited); S2.10 + `--k-accent-text` in all 5 carrying files; style-spec: variable + D2 note; labels "edition 2 (rev 4)"; test: app_guides_test (6), verify_contract
- 5.2 fixtures: tests/fixtures/mini-app (+ mini-app.kvx), mini-core-parts (5 parts + seal + 4 pages, inert, type-valid); negatives are mutations built inside e2e.py
- 5.3 tests/e2e.py (17): assemble -> verify core (tsc + bundles) -> pack-core -> .kvcore contents; pack-kvx x2 -> safeExtract -> fingerprint -> convert -> backend in Node ESM; negatives: missing page, tampered kit, hostile path, extensionless import, overlapping owns, stale FP
- 5.4 KOVA_SMOKE: src/kit/smoke.ts, src/kit/debug.ts (hooks in handshake.ts and deps.ts), main.ts guard, scripts/smoke.mjs, `npm run smoke`; typechecked and bundled by e2e (main_bundles_with_smoke_guard); NOT run
- 5.5 no kova-core-4/5 md existed; MIGRATION.md added; core-1/2/3 launcher md files were not in my inputs (not checked, not renamed)
- run_tests.py now finds KOVA_TOOLS, links node_modules, uses type-valid fixture parts; fixed a stale assertion; test: 45/45
## Final QA (audit ids are mapped from the patch logs; the audit text itself was not provided to me)
| id | status | proof |
|---|---|---|
| C1 index/marker/seam | fixed | typecheck in e2e, rpc.test |
| C2 schema/index format | fixed | schema.test |
| C3 | not traceable in the logs (no entry) | n/a |
| C4 imports (.js, wiring) | fixed | wire_*, convert.test, e2e backend run |
| C5 assemble | fixed | asm_* (11), e2e neg_hostile_part_path |
| C6 zip/deps/rpc/dom/CSP | fixed in code; runtime unverified | zip/deps/rpc tests |
| H1 verify/pack order | fixed | verify_*, e2e |
| H2 pack-part/blueprint | fixed | pp_*, neg_overlapping_owns |
| H3 stamps/repair/redact | fixed | kvx_*, e2e stamp test |
| H4 | not traceable in the logs (no entry) | n/a |
| H5 kvx validation/fingerprint | fixed | kvx_*, fingerprint.test |
| H6 atomic/package | fixed | atomic.test |
| Medium: libraries, identity | fixed | app_guides_test |
| D1 core switching | by decision (drop) | seam-types, guides |
| D2 chrome | by decision (autohide + fixes) | style-spec; behaviour unverified |
Unverified until run on Windows: npm install with --ignore-scripts, Defender rename retries, first-start grace timing, titleBar/controls behaviour, session partitions, and the smoke harness itself.
