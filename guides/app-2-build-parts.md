# APP · STEP 2 OF 3 · BUILD ONE PART · edition 2 (rev 4)
`CONTRACT-FP:b02dcf20`. One chat per part. You need: **this file**, **app-kit.zip**, **blueprint-<id>.json**.

## STOP. READ THIS FIRST
1. **Wait for the Blueprint.** Missing → ask and stop. No stamps.
2. If the person did not say which part, ask: *"Which part number?"*
3. Run the setup command, then read **only** `guides/part.md` and follow it.
4. Never draw icons. Write each file once. Do not run or launch anything.
5. Repair bundle or pasted repair note → read only `guides/repair.md`.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files:** `mkdir -p proj/app && cd proj && unzip -oq /mnt/user-data/uploads/app-kit.zip -d /tmp/k && cp -r /tmp/k/app-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Check (one capped command), then pack.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.
