# DEVELOPMENT DIARY — TankThilteteYt

This is the **living handoff log** for this project. It is written so that a brand-new AI session (or a fresh collaborator) can open this single file and be **immediately caught up** on: what the game is, which file is the current one, what's done, what's next, and what the human wants.

> For a full plain-English explanation of **what** the game is and how every system works, see **`GAME_STATUS.md`**. This file is the **when/what's-next** log.

---

## TL;DR for the next session (read this first, ~15 seconds)

- **Game:** a single-file 3D auto-aim tank survival arena shooter for phones (`TankThilteteYt01.html`). Feature-complete **v1.0**.
- **Current working version file:** `TankThilteteYt01_v1.1.html` — **v1.1 tweaks are APPLIED** (this is the live, updated build to test).
- **Frozen baseline (do NOT edit):** `TankThilteteYt01.html` (v1.0).
- **The human is playtesting.** They asked for a batch of v1.1 tweaks (all applied — see the changelog below). My job next: get their reaction, fix anything that's still off, bump to the next version when confirmed, and log here.
- **The single most important question to ask the human:** *"Test v1.1 — did the changes land the way you wanted? What else feels off?"*

**v1.1 change batch (all applied & syntax-verified):**
1. First 5 upgrades always offer Health Regen (Nano Repair) + Heal-on-Kill (Field Medic) + one other random card.
2. Airdrops start from Level 1, and for the first 5 levels they give a repair (health) reward 70% of the time; after Level 5 fully random.
3. First boss (Warlord) projectiles: speed halved (36→18) and damage halved (20→10).
4. All water removed from every biome (no water shown anywhere).
5. HP bar & XP bar now show numbers (e.g. `47/100`, `80/120`) instead of a percentage; the bar width still fills by percent.
6. Added a live **Damage / Speed meter** on the in-game HUD.
7. Pause menu redesigned: upgrades listed once each with a count (e.g. `Missile ×2`), cleanly aligned; Evolutions listed below.
8. Tapping an Evolution in the pause menu opens a detail page showing what it needs, what you've picked, and its active/locked status.

---

## Versioning convention (how we preserve old versions)

We never overwrite. Each "release" is its own file. Old versions stay in the repo forever so we can always revisit them.

| Version | File | Status |
|---|---|---|
| v1.0 | `TankThilteteYt01.html` | **Frozen baseline. Do NOT edit.** Feature-complete. |
| v1.1 | `TankThilteteYt01_v1.1.html` | **Current working version.** v1.1 tweak batch applied (see changelog). |
| v1.2 | `TankThilteteYt01_v1.2.html` | (future — next minor tweak batch, if needed) |
| v2.0 | `TankThilteteYt01_v2.html` | (future — when we bump to the next release) |

**Naming rule going forward:** every time we land a batch of confirmed, working changes, copy the current file to the next version name, edit the new file for the next batch, and add a row to this table with a one-line changelog. Adding a new version file is **safe** — the older one is untouched.

---

## Files in the repository (what's what)

| File | What it is |
|---|---|
| `TankThilteteYt01.html` | **v1.0 — the finished game.** Frozen baseline. |
| `TankThilteteYt01_v1.1.html` | **Current working version.** v1.1 tweak batch applied (sanctuary regen cards, airdrop tweaks, Warlord nerf, no water, number HP/XP bars, DMG/SPD meter, cleaner pause + evolution detail page). |
| `tank realm HUD.html` | Older/experimental build from an earlier stage. Preserved, not the main one. |
| `tank realm HUD (2).html` | Older/experimental build. Preserved. |
| `tank realm HUD3.html` | Older/experimental build. Preserved. |
| `tank-eternal_1.13_biome.html` | Older/experimental build. Preserved. |
| `manifest.webmanifest` | PWA manifest (name, icons, portrait, standalone). |
| `sw.js` | PWA offline service worker (network-first pages, cache-first assets). |
| `icon-192.png` / `icon-512.png` | PWA app icons. |
| `GAME_STATUS.md` | Full plain-English explanation of the whole game. |
| `DEVELOPMENT_DIARY.md` | **This log.** |

---

## Current status (verified this session)

- v1.1 tweak batch **applied and syntax-verified** (all 3 embedded script blocks → **0 errors**).
- Verified present: all 6 boss names (Warlord, Colossus, Nova, Titan, Tempest, Fortress), all 4 difficulties (Easy/Normal/Hard/Nightmare), `localStorage` save code, embedded Three.js, PWA manifest + service worker + icons.
- Confirmed via live server: v1.1 serves 200 with all changes present; no `hasWater: true` remains.
- New build-UI functions (`renderBuildList`, `bindEvoButtons`, `openEvolutionDetail`) smoke-tested in a Node harness (run without throwing).
- v1.0 (`TankThilteteYt01.html`) is the frozen baseline and is untouched. All older builds left untouched.

---

## What the game IS (one paragraph, details in `GAME_STATUS.md`)

3D auto-aim tank survival arena shooter, portrait phone touch controls. You drive a tank; the cannon aims and fires automatically. Core loop: **drive → auto-fire → kill → coins/XP → level up by picking 1 of 3 cards → boss every 5 levels → biome change every 3 levels → die → spend coins in shop → stronger run.** 33 enemies, 6 phased bosses, 10 visual biomes, 15-card build system with 6 evolutions, permanent shop + 6 skins + consumables, 14 achievements, 4 difficulties, revive/save systems, comfort/accessibility settings, PWA offline package.

---

## Completed / frozen versions log

| Date | Version | What changed |
|---|---|---|
| 2026-08-28 | v1.0 | Feature-complete initial release. All 106-question blueprint systems built and verified. |
| 2026-08-29 | v1.1 | First 5 upgrades always offer Health Regen + Heal-on-Kill + one other; airdrops start at L1 and heal 70% of the time for first 5 levels; Warlord (first boss) projectile speed & damage halved; all water removed from every biome; HP/XP bars show numbers (47/100) not %; added live Damage/Speed HUD meter; pause menu redesigned (deduped upgrades with ×counts, tappable evolution detail page). |

---

## The current plan (next steps, in order)

1. **Playtest v1.1 (human).** On the live preview **and ideally a real phone.** Open `http://localhost:8123/TankThilteteYt01_v1.1.html`.
2. **Collect feedback.** Anything that *feels* off — difficulty spike, poor pacing, an unfair boss, a touch-control problem, a confusing card, the new pause/evolution UI, the number bars, balance too easy or too hard.
3. **Apply the next tweak batch.** Keep v1.0 frozen. When a batch is confirmed working, copy the current file to the next version name (`TankThilteteYt01_v1.2.html`) and log it.
4. **Publish over HTTPS** so it installs as an app. Suggested free static hosts: GitHub Pages, Netlify, Vercel, or Surge. Upload `TankThilteteYt01_v1.1.html` (or whichever is current) + `manifest.webmanifest` + `sw.js` + the two icons.
   - **PWA note to handle at publish time:** the manifest's `start_url`/`scope` is `./`, and the sw caches `./`. On many hosts `./` serves an `index.html`. Right now the game file is named `TankThilteteYt01*.html`, not `index.html`. So before publishing, decide whether to (a) add an `index.html` that loads the current game, or (b) point the manifest/sw at the actual game filename, or (c) rename the game file to `index.html` for that deploy. Keep this in mind so the install-as-app works.
5. **Log every decision** in this diary so any future session is caught up.

---

## Open questions for the human (ask these at the start of the next session)

- Did the v1.1 changes land the way you wanted? (regen cards, airdrops, Warlord nerf, no water, number bars, DMG/SPD meter, pause UI + evolution detail)
- What still feels off after v1.1? (the big one)
- Which difficulty are you mostly playing (Easy/Normal/Hard/Nightmare) — too easy or too hard?
- Is the first boss now fair? Should we also tone the other bosses, or leave them?
- Do you want a dedicated `index.html` so the game loads at `./` (cleaner for the PWA install)?
- Any new feature you want in the next release, or are we purely polishing?

---

## If the game needs a change — the workflow

1. **Edit the current working file** (`TankThilteteYt01_v1.1.html`). **Never edit the frozen baseline** `TankThilteteYt01.html`.
2. Test on the live preview (`python3 -m http.server` in the repo root, open `/TankThilteteYt01_v1.1.html`).
3. When the change works and the human is happy, copy current → next version filename, and add a row to the "versions log" table above with a one-line changelog.
4. Update this diary's "TL;DR", "current version", and "current plan" so the next session reads the right thing.

---

## Technical reference (safe commands)

```bash
# Run the live preview (serves everything in this folder)
cd /home/user/4tanksrealm
python3 -m http.server 8123 --bind 0.0.0.0
# then open http://localhost:8123/TankThilteteYt01_v1.1.html
```

```bash
# Verify each embedded <script> block has valid syntax (no errors)
node -e '
const fs=require("fs"),vm=require("vm");
const html=fs.readFileSync("./TankThilteteYt01_v1.1.html","utf8");
const re=/<script\b([^>]*)>([\s\S]*?)<\/script>/gi; let m,i=0,ok=0,bad=0;
while((m=re.exec(html))){ if(/src\s*=/.test(m[1]))continue; i++; try{new vm.Script(m[2]);ok++;}catch(e){bad++;console.log("ERR",e.message);} }
console.log("blocks="+i+" ok="+ok+" err="+bad);'
```

```bash
# Check md5 to confirm two files are identical
md5sum TankThilteteYt01.html TankThilteteYt01_v1.1.html
```

---

## Intent of this project

Make a genuinely fun, playable, installable mobile tank survival game that lives in a single HTML file, keep a clean archive of every version so we never lose work, and make sure any future AI session can pick up the exact plan in seconds.
