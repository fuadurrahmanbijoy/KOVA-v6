# CORE · STEP 2 OF 3 · BUILD ONE PART · edition 2
`CONTRACT-FP:8209dbec`. One chat per part. You need: **this file**, **core-kit.zip**, **blueprint-<id>.json**. (To fix a broken Core instead, upload the repair bundle and kit; see rule 5.)

## STOP. READ THIS FIRST
1. **Wait for the Blueprint** (or a repair bundle). Missing → ask for it and stop. There is no stamp to ask for.
2. If the person did not already say which part, ask one question: *"Which part: 1 Foundation, 2 Installer, 3 Runner, 4 Frame, 5 Manager?"*
3. Run the setup command below, then read **only** `guides/part-<N>-<name>.md` (`cat` it) and follow it. Never read the other guides or the kit's code.
4. Never draw icons. Write each file once. Do not run or launch anything.
5. **Repair:** a repair bundle (`*-repair.zip`) or a pasted repair prompt → read only `guides/repair.md` and follow it. No questions.

### TOKEN RULES (chat limits are tight; follow strictly)
- **Set up with one command and never read the kit files:** `mkdir -p proj && cd proj && unzip -oq /mnt/user-data/uploads/core-kit.zip -d /tmp/k && cp -r /tmp/k/core-kit/. . && (cp /mnt/user-data/uploads/blueprint*.json blueprint.json 2>/dev/null; true)` (if the zip has another name: `ls /mnt/user-data/uploads`).
- **Write each file once.** No rewrites, polish passes or extra features.
- **Never paste file contents into your reply. Never re-read a file you just wrote. Cap every command output** (`| tail -n 10`).
- **No audits, no checklists, no explanations.** The final reply has a fixed shape.
- **Pack first, check after.** You cannot run Kova or Electron here; never try to launch anything.
- **Budget guard:** running low? Stop adding features, write `PROGRESS.md` (max 10 lines) in your part folder, pack what exists, say what remains.
- There is **no build stamp to ask for**: packers add one automatically.

Part files: 1 `guides/part-1-foundation.md` · 2 `part-2-installer.md` · 3 `part-3-runner.md` · 4 `part-4-frame.md` · 5 `part-5-manager.md`.
