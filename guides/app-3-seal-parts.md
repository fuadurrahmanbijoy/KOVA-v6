# APP · STEP 3 OF 3 · SEAL · edition 2 (rev 4)
`CONTRACT-FP:b02dcf20`. You need: **this file**, **app-kit.zip**, **blueprint-<id>.json**, and **every part-N-of-M-<id>.kvpart**.

## STOP. READ THIS FIRST
1. Write no new code. Run the commands below in order, output capped. No stamps. Do not read the parts or the kit unless a check fails.
2. **You may fix small cross-part problems yourself** (a wrong import path, a missing export, a name that differs from the Blueprint): smallest edit, list each in one line. Nobody should go back to a part chat for these.
3. **Never fix strangers or collisions silently.** If assemble reports parts from another set or files owned by two parts, stop and tell the person exactly which parts to rebuild with `app-2-build-parts.md`.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files:** `mkdir -p proj/app && cd proj && unzip -oq /mnt/user-data/uploads/app-kit.zip -d /tmp/k && cp -r /tmp/k/app-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Check (one capped command), then pack.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.

## Commands
1. `python scripts/assemble.py /mnt/user-data/uploads app app 2>&1 | tail -n 12` (strict; exits non-zero on any problem). Missing parts, strangers (`KV-PT-002`) or collisions → reply "Rebuild part(s) <numbers> with `app-2-build-parts.md`" with the reason in one line; stop.
2. `python scripts/wire-app.py 2>&1 | tail -n 10` → writes `kova.json`, `backend/main.ts`, `ui/index.html`, `ui/app.ts` (with `.js` import specifiers).
3. `python scripts/verify.py app 2>&1 | tail -n 12` (syntax, import graph, `kova.json`). Fix only cross-part problems: wrong import path, missing export, name mismatch with the Blueprint; max 2 rounds, list each fix.
4. `python scripts/pack-kvx.py app` → `OK <id>.kvx` or `FAIL <reason>`.

## Reply exactly (max 10 lines)
```
Done: <name> <type> → <id>.kvx
Fixed along the way: <one line each, or "nothing"> (or: Rebuild part(s) <N> with app-2-build-parts.md: <reason>)
NEXT STEPS
1. Download the .kvx file.
2. Open your Kova Core and drag the file onto the window (or double-click it, or press "Add app").
3. If anything goes wrong, press "Copy repair prompt" in Kova and paste it into a new chat together with the repair bundle and app-kit.zip.
```
