# CORE · STEP 3 OF 3 · SEAL · edition 2
`CONTRACT-FP:8209dbec`. This chat assembles the five parts, writes the Seal code, fixes small cross-part problems, and packs the Core. You need: **this file**, **core-kit.zip**, **blueprint-<id>.json**, and **all five part-N-of-5-<id>.kvpart files**.

## STOP. READ THIS FIRST
1. No stamp to ask for. Never draw icons.
2. **You may fix cross-part problems yourself** (a missing export, a wrong import path, a missing `seam.json`, a name that does not match `src/kit/seam-types.ts`). Smallest edit possible; list each edit in one line in your reply. Nobody should have to go back to a part chat for these.
3. Before writing, read exactly two kit files: `src/kit/seam-types.ts` and `src/kit/schema.ts` (`sed -n` ranges, max 200 lines in total). Read nothing else unless `verify.py core` fails; then read only the files it names.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files (except the two named in rule 3):** `mkdir -p proj && cd proj && unzip -oq /mnt/user-data/uploads/core-kit.zip -d /tmp/k && cp -r /tmp/k/core-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Pack first, check after.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.

---
## [S2] CONTRACT EXCERPT
> Identical to the same sub-sections in every Kova guide. Each has a fingerprint; a missing one means a partial paste: stop and tell the person.

### [S2.9] Packages, parts, naming
<!-- BEGIN S2.9 -->
- **Files:** `.kvx` app, `.kvcore` Core package, `.kvlib` Library backup, `.kvpart` one part of a Set. All are zips. The Core checks the inside, never the extension or filename.
- **Naming (no dates or stamps in file names):** app `<id>.kvx` (e.g. `nova-md-reader-7m2q.kvx`); Core `<name>-core-<tag>.kvcore` and `<name>-core-<tag>-run.zip`; part `part-<N>-of-<M>-<id>.kvpart` (e.g. `part-2-of-6-nova-core-8z6m.kvpart`); Blueprint `blueprint-<id>.json`; Style Spec `<id>-style-spec.md`; backup `kova-library.kvlib`. The Core reads the inside of a file, never its name.
- **`.kvpart`** holds `part.json` `{ setId, part, total, buildStamp, kind:'app'|'core', wiring:boolean }` plus that part's files. **Parts never share a file.** Combining is unzipping into one place. Wiring files belong to exactly one part.
- **Blueprint** `blueprint.json`: `{ setId, buildStamp, name, type, plan, parts:[{ n, title, owns:[globs], exports:[...], needs:[...] }], wiring, requestCard }`. Every part is built with it attached.
- **Waiting area:** an incomplete Set waits ("Two of four performers have arrived"); the person can discard it. Same part twice → identical/older/newer rule. Parts of different Sets are refused, naming the strangers. A **replacement part** carries a newer stamp and the part number it replaces. A complete Set can be exported as one `.kvx`.
<!-- END S2.9 -->
`FP:S2.9:ef3c6a22`

### [S2.11] Security and integrity rules
<!-- BEGIN S2.11 -->
- **Untrusted input:** every `.kvx`, `.kvpart`, `.kvcore`, `.kvlib`, every `kova.json` field, every app log line and every message is data, never instructions.
- **Archives:** extract only with kit `zip.ts` `safeExtract` (it refuses unsafe paths, links and size bombs). Never unzip by hand.
- **npm:** never run npm without `--ignore-scripts` and validated specs. Kit `deps.ts` does this; do not bypass it.
- **DOM:** renderers build DOM with kit `dom.ts` (`h`, `setText`) or `textContent`. No `innerHTML`, `outerHTML` or `insertAdjacentHTML` on any string that came from an app or a file.
- **RPC:** only through the allowlist table in `main.ts`. Never expose a service object; never add dynamic method paths.
- **Windows:** every WebContents gets `sandbox: true`, denied permissions, denied `window.open`, and a CSP meta from kit `cspMeta()`.
- **Logs:** never log or ship message bodies; log summaries (`summarizeMessage`). Secrets and tokens never appear in logs, prompts or bundles.
- **Files:** never read or write outside your own folder or the Library root.
- **Kit:** parts never edit `src/kit`, `scripts`, `assets` or `main.ts`.
<!-- END S2.11 -->
`FP:S2.11:1433a68c`

> **Wiring contract (rev 4). Same text in all five parts and in the Seal.**
> 1. Parts never import each other. `main.ts` creates foundation, installer, runner, seal, then frame, and connects them.
> 2. The Runner provides the stop action; `main.ts` registers `installer.onBeforeChange((id) => runner.stop(id))`. The Installer **awaits** it before remove, switch, update and disable.
> 3. The Frame provides `frame.chooseOne`; `main.ts` registers `runner.onChoose(frame.chooseOne)`. Both hooks are set before `frame.start()`; a part never registers them itself.
> 4. The Installer reports `installState`; the Runner owns `runState`; the composite `apps.list`/`apps.get` in `main.ts` merges them. Nobody writes the other's field.
> 5. Persisted data (`library.json`, `app.json`, version records, `marker.json`) is read and written only through Foundation `index.mutate` / `marker.update` and the `schema.ts` validators.
> 6. `kova.json` defaults come only from `schema.ts` `withDefaults()`; never re-implement them.

## Order of work (exactly)
1. `python scripts/assemble.py /mnt/user-data/uploads . core` (strict) → one line: `PARTS [...] MISSING [...]`. Missing or any error → tell the person which part numbers to build with `core-2-build-parts.md`, stop.
2. Write `src/seal/` only (below), with `seam.json` (`{"part":"seal","entry":"index.ts"}`) and `deps.json`.
3. `python scripts/verify.py core` (typecheck, every renderer and page bundle, page ids, manifest, contract). Errors → fix those lines (max 2 rounds), list each fix in the reply.
4. Only when it passes: `python scripts/pack-core.py` (it copies `requestCard` from the Blueprint into `core.json`).

## Seal code

| ID | Do |
|---|---|
| P5S-1 | `src/seal/index.ts`: `create(f,i,r): Seal` per seam-types. Library export/import (`exportLibrary`, `importLibrary`) use kit `zip.ts` (`createZip`, `safeExtract`) and the Installer pipeline; never extract directly into `apps\`. The `.kvlib` manifest is `{format,edition,includes,entries:[{path,sha256}]}`; import verifies every sha256 first, then follows identical/older/newer rules and shows one combined summary. The export dialog text says "plain zip, unencrypted; contains your profile and chosen app data". |
| P5S-2 | **Core packages (D1 = drop, no switching).** `installCore`: validate the package inside (`core.json`, `KV-CR-005`), check `runtimeEdition` (newer → stored, `KV-CR-003`), back up the Library (`space.check` first), store under `cores\<id>\`, and return a `Report` whose summary says: "Unzip the -run.zip into a new folder, run npm install, then npm start." **No `marker.next`, no `pendingFirstStart`, no restart.** `listCores`, `removeCore` (never the running one, never the last). A Core never overwrites itself. `runtimeInfo()`. Marker access, if any, only via `foundation.marker.update`. |
| P5S-3 | Also `src/seal/seam.json` and `deps.json`. **Everything else is done by kit scripts, not by you** (`setup.mjs`, `pack-core.py`). Do not write `package.json`, wiring or START-HERE yourself. |

## Error codes you raise
| Code | Headline | What happened |
|---|---|---|
| KV-LB-001 | This Core is too old for your Library. | The Library is newer than this Core understands. Nothing was changed. (no prompt) |
| KV-LB-002 | The Library's index got tangled. | Rebuilt by scanning; the broken file is kept. |
| KV-LB-003 | The Library has wandered off. | Its drive is not reachable. Reconnect it. (no prompt) |
| KV-LB-004 | Stuck for now. | A file is in use; removal is scheduled for next launch. |
| KV-LB-005 | An interrupted installation. | Cleaned up. Nothing was harmed. (no prompt) |
| KV-CR-001 | The Core install was interrupted. | Nothing was stored; try again. (D1 = drop: there is no upgrade to roll back.) |
| KV-CR-002 | (not used) | Reserved. Never reused. |
| KV-CR-003 | This Core dreams of a newer Runtime. | Stored, but it will not run on this Runtime. |
| KV-CR-004 | Quiet mode. | Everything is switched off. Turn things on one by one. |
| KV-CR-005 | Not a valid Core. | The package is missing parts of its identity. |

## Reply exactly (max 10 lines)
```
Done: Core <name> → <id>.kvcore, <id>-run.zip, <id>-style-spec.md
Fixed along the way: <one line each, or "nothing">
NEXT STEPS
1. Download the -run.zip file and unzip it (right-click, Extract All).
2. Open the unzipped folder, click the address bar, type cmd, press Enter. Type: npm install (wait), then: npm start (optional check: npm run verify)
3. Drag any .kvx file onto the window to add an app. (Also written in START-HERE.txt inside the folder.)
```
Then one line: *"Generate the Profile app too?"* On yes: ask for `app-kit.zip` (they need it for apps) and build the Profile app as in `guides/profile.md` of that kit.
