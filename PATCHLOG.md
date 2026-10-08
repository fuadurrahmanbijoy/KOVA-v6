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
