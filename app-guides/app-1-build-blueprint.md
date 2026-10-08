# APP · STEP 1 OF 3 · BLUEPRINT (or the whole app, if it is small) · edition 2 (rev 4)
`CONTRACT-FP:b02dcf20`. You need: **this file** and **app-kit.zip**.

## STOP. READ THIS FIRST
1. Ask only for what the app should do if it is missing (everything else has defaults; say them in one line). No stamps, no confirmations.
2. **Small app** (about 12 files or fewer: reader, notes, clock, converter, Profile app): run the setup command, mint the id tag with `python scripts/mint-id.py`, read `guides/small-app.md` (and `guides/profile.md` for the Profile app), build the **whole app in this chat**, run `python scripts/verify.py app 2>&1 | tail -n 12` (fix each FAIL once), then pack it. You are done; steps 2 and 3 are not needed.
3. **Large app** (browser, torrent client, editor, player with library...): write the Blueprint below and stop.
4. Repair bundle or pasted repair note → read only `guides/repair.md`.
5. Never draw icons. The app must work alone.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files:** `mkdir -p proj/app && cd proj && unzip -oq /mnt/user-data/uploads/app-kit.zip -d /tmp/k && cp -r /tmp/k/app-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Check (one capped command), then pack.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.

## The Blueprint (large apps only)
`id = <name-slug>-<type-slug>-<tag>`; the tag is minted once by `python scripts/mint-id.py`. Never copy a tag from an example (`<tag>` below is a placeholder). Rules `pack-part.py` enforces:
- 3 to 6 parts (each about 600 lines or less), `n` counting 1, 2, 3...
- `owns` globs are relative to `app/` (no `..`, not absolute) and disjoint between parts.
- Every `exports[].file` is matched by its own part's `owns`.
- Every message name starts with the id (or is in the S2.5 vocabulary).
- `setId` is `<name-slug>-<type-slug>-<tag>` with a minted tag.

File rules: relative imports use an explicit `.js` extension; styles live in `ui/*.css`; no JSX. Parts never edit `kova.json`, `backend/main.ts`, `ui/index.html`, `ui/app.ts`: the Seal writes those from the Blueprint. A backend part exports `register(kova)` (no `kova.ready()`); a screen part exports `mount(root: HTMLElement)`; list them in `exports` in run/mount order. Everything parts exchange goes in `messages`. `card` holds the optional ID-card fields (icon, description, dependencies, opens, announces, answers, runsInBackground...).
```json
{ "setId": "kitush-torrent-client-<tag>", "name": "Kitush", "type": "torrent client",
  "plan": "Peer engine, download manager, screens.",
  "card": { "icon": "arrow_download", "dependencies": { "webtorrent": "^2.0.0" }, "opens": ["link:magnet","file:torrent"], "announces": ["download.progress"], "runsInBackground": true },
  "parts": [
    { "n": 1, "title": "Engine", "owns": ["backend/engine/**"], "exports": [{ "kind": "backend", "file": "backend/engine/index.ts", "fn": "register" }], "needs": [] },
    { "n": 2, "title": "Screens", "owns": ["ui/screens/**", "ui/style.css"], "exports": [{ "kind": "screen", "file": "ui/screens/index.ts", "fn": "mount" }], "needs": ["messages: download.progress"] },
    { "n": 3, "title": "Settings", "owns": ["backend/settings/**"], "exports": [{ "kind": "backend", "file": "backend/settings/index.ts", "fn": "register" }], "needs": [] } ],
  "messages": [ { "name": "kitush-torrent-client-<tag>.add", "kind": "send", "body": "{ magnet: string }" } ] }
```
Replace `<tag>` with the minted tag, save as `proj/blueprint.json`, then `python scripts/verify.py blueprint blueprint.json 2>&1 | tail -n 10` (fix each FAIL once) and `python scripts/pack-part.py blueprint`.

## Reply exactly (large app; max 8 lines)
```
Done: Blueprint for <name> (<n> parts) → blueprint-<id>.json
NEXT STEPS
1. Download blueprint-<id>.json and keep it safe.
2. For each part 1 to <n>: new chat, upload app-kit.zip, blueprint-<id>.json and app-2-build-parts.md, then say "part <N>".
3. When all parts exist: new chat with app-3-seal-parts.md, app-kit.zip, the blueprint and all part files.
```
