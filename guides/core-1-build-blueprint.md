# CORE · STEP 1 OF 3 · BUILD THE BLUEPRINT · edition 2
`CONTRACT-FP:8209dbec`. This chat writes **one small file** (the Blueprint) and no code. Then: `core-2-build-parts.md` (five chats), then `core-3-seal-parts.md`.
You need: **this file** and **core-kit.zip**.

## STOP. READ THIS FIRST
1. Ask the person for the choices below in **one** message (skip any they already gave). Then write the Blueprint. No stamps, no confirmations.
2. Never draw icons.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files:** `mkdir -p proj && cd proj && unzip -oq /mnt/user-data/uploads/core-kit.zip -d /tmp/k && cp -r /tmp/k/core-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Pack first, check after.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.

## The choices
| Field (requestCard key) | Default | Used by |
|---|---|---|
| Core name → `name` | you propose (short, brand-like) | pack-core, window title, first-run card (Frame) |
| Theme color → `accent` (hex `#RRGGBB`) | `#0F6CBD` (blue) | Foundation default accent when no profile file exists; Core defaults in `core.json` |
| Layout → `layout` | `rail-left` (left icon rail + one main area; rail: Home, What's running, apps, Settings, Profile at the bottom) | Frame |
| Optional capabilities → `capabilities[]` | `["tray","status"]`; allowed: `tray`, `status`, `blocklist`, `globalShortcuts` | Frame and Runner enable only these |
| Extra features → `extras[]` | `[]` | Manager lists them under "Planned extras"; nothing is silently dropped |
| Look and feel | Teams-style (Fluent), light; fixed, not a requestCard key | design system |
Say every default in one line.

## Write `blueprint.json`
`{ "setId": "<name>-core-<tag>", "name": "<Name>", "requestCard": { "name", "accent", "layout", "capabilities", "extras" }, "parts": 5 }` in `proj/`. The tag comes from `python scripts/mint-id.py` (never invent it), run once; every part, file and fix reuses it. Get the tag with `python scripts/mint-id.py`. Then run `python scripts/pack-part.py blueprint` (adds the build stamp for you).

## Reply exactly (max 8 lines)
```
Done: Blueprint for <name> → blueprint-<id>.json
NEXT STEPS
1. Download blueprint-<id>.json and keep it safe.
2. Build the five parts, one NEW chat each: upload core-kit.zip, blueprint-<id>.json and core-2-build-parts.md, then say "part 1" (Foundation), "part 2" (Installer), "part 3" (Runner), "part 4" (Frame), "part 5" (Manager). Any order.
3. When all five .kvpart files exist: new chat with core-3-seal-parts.md, core-kit.zip, the blueprint and the five files.
```
