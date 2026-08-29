# DEVELOPMENT DIARY — TankThilteteYt

This is the **living handoff log** for this project. It is written so that a brand-new AI session (or a fresh collaborator) can open this single file and be **immediately caught up** on: what the game is, which file is the current one, what's done, what's next, and what the human wants.

> For a full plain-English explanation of **what** the game is and how every system works, see **`GAME_STATUS.md`**. This file is the **when/what's-next** log.

---

## TL;DR for the next session (read this first, ~15 seconds)

- **Game:** a single-file 3D auto-aim tank survival arena shooter for phones (`TankThilteteYt01.html`). Feature-complete **v1.0**.
- **Current working version file:** **`TankThilteteYt01_v1.3.html`** — **v1.3 tweaks are APPLIED** (this is the live, updated build to test).
- **Frozen baselines (do NOT edit):** `TankThilteteYt01.html` (v1.0), `TankThilteteYt01_v1.1.html` (v1.1), `TankThilteteYt01_v1.2.html` (v1.2).
- **The human is playtesting.** v1.2 (armor soak + balance) is frozen; v1.3 adds the "HUD tells the truth" Phase-2 fixes. My next job: get their reaction and continue.
- **The single most important question to ask the human:** *"Test v1.3 — do the damage/speed meters now read honestly (bar fills to match the number, shows BOOST/SLOWED)? Does the HP number stop rounding up? Any overflow?"*

**v1.2 change batch (all applied & syntax-verified, now frozen):**
1. **Armor is now a real soak pool** (not a % discount). It absorbs ALL incoming damage until it reaches zero, THEN the leftover hits your HP. Old 55% cap + "always 3 damage" floor removed. Shows `ARMOR DOWN` when it breaks.
2. **Armor refills from regen** — armor rebuilds at the same rate as your regen stat (more regen = faster armor back).
3. **Armor refills from pickups** — repair kits, shield batteries, and airdrops restore armor to full (repair crate/orb, shield crate/orb, Black-Market Full repair, Black-Market Shield charge).
4. **Armor shows on the HUD** — a small blue armor bar under the HP number (with `x/y` value), hidden when you have no armor.
5. **Picking the Composite Armor card** raises the soak pool cap AND tops the pool up by the same amount.
6. **Pause menu now shows Max HP (`❤️ x HP`) and Heal/Kill (`💗 x/kill`)** in addition to the other stats.
7. **Early enemy damage toned down** — enemy damage scale now starts at ~1.0× at Level 1 (was 1.65×), so a Level-1 basic enemy hits near its listed base damage. Still ramps naturally with level.
8. **Early card guarantee changed from 5 picks to 3** — the first 3 upgrades always offer Health Regen + Heal-on-Kill + one other; after pick 3 it's fully random.

**v1.3 change batch (all applied & syntax-verified) — Phase 2 "HUD tells the truth":**
1. **Damage/Speed meter now shows LIVE values** — base % × Overcharge (1.3×) × Blast (1.2×) for damage; base % × Haste/Adrenaline boost × roots slowdown for speed. The bars now fill to match the number (100% = a full bar, not a divided-down half bar).
2. **Added a status label on the SPD meter** — shows **BOOST** (green) during Haste/Adrenaline and **SLOWED** (amber) during the roots biome slow; the bar recolors too.
3. **Meter refreshes every 0.15s** from the animate loop so boosts/slows respond live even when regen is off.
4. **HP no longer rounds up** — the readout uses `Math.floor(player.hp)` so it never falsely shows max while regenerating (armor readout uses floor too).
5. **Big HP/XP numbers are overflow-safe** — the value now auto-shrinks (`clamp`) and ellipsizes instead of overflowing the box on small screens.
6. **Armor pause chip now reads `🛡️ x armor`** so it's clear it's a soak shield, not a level number.

---

## Versioning convention (how we preserve old versions)

We never overwrite. Each "release" is its own file. Old versions stay in the repo forever so we can always revisit them.

| Version | File | Status |
|---|---|---|
| v1.0 | `TankThilteteYt01.html` | **Frozen baseline. Do NOT edit.** Feature-complete. |
| v1.1 | `TankThilteteYt01_v1.1.html` | Frozen. v1.1 tweak batch applied. |
| v1.2 | `TankThilteteYt01_v1.2.html` | Frozen. v1.2 tweak batch applied (armor soak system, early-game balance, card guarantee = 3 picks). |
| v1.3 | `TankThilteteYt01_v1.3.html` | **Current working version.** v1.3 tweak batch applied (Phase 2 HUD-truth fixes). |
| v2.0 | `TankThilteteYt01_v2.html` | (future — when we bump to the next release) |

**Naming rule going forward:** every time we land a batch of confirmed, working changes, copy the current file to the next version name, edit the new file for the next batch, and add a row to this table with a one-line changelog. Adding a new version file is **safe** — the older one is untouched.

---

## Files in the repository (what's what)

| File | What it is |
|---|---|
| `TankThilteteYt01.html` | **v1.0 — the finished game.** Frozen baseline. |
| `TankThilteteYt01_v1.1.html` | Frozen. v1.1 tweak batch applied (regen cards, airdrop tweaks, Warlord nerf, no water, number HP/XP bars, DMG/SPD meter, cleaner pause + evolution detail page). |
| `TankThilteteYt01_v1.2.html` | Frozen. v1.2 tweak batch applied (armor soak system, early-game balance, card guarantee = 3 picks). |
| `TankThilteteYt01_v1.3.html` | **Current working version.** v1.3 tweak batch applied (Phase 2 HUD-truth fixes: live DMG/SPD meters, BOOST/SLOWED labels, no HP round-up, overflow-safe numbers). |
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

- v1.3 tweak batch **applied and syntax-verified** (all 3 embedded script blocks → **0 errors**).
- `refreshCombatMeter()` extracted and smoke-tested against a stub DOM — runs without throwing; live-value math verified (baseline 100/100, overcharge → 130% dmg, haste → 125% spd, roots slow → 80% spd), 100% = full bar.
- Confirmed via live server: v1.3 serves 200 with `cm-spd-status`, `function refreshCombatMeter`, `_meterHud`, `Math.floor(player.hp)`, and `clamp(10px` all present.
- Armor soak math (from v1.2) still verified: armor absorbs all damage until 0, then leftover hits HP.
- Kept: all 6 bosses, 4 difficulties, save code, embedded Three.js, PWA files.
- v1.0, v1.1, v1.2 are frozen. All older builds untouched.

---

## What the game IS (one paragraph, details in `GAME_STATUS.md`)

3D auto-aim tank survival arena shooter, portrait phone touch controls. You drive a tank; the cannon aims and fires automatically. Core loop: **drive → auto-fire → kill → coins/XP → level up by picking 1 of 3 cards → boss every 5 levels → biome change every 3 levels → die → spend coins in shop → stronger run.** 33 enemies, 6 phased bosses, 10 visual biomes, 15-card build system with 6 evolutions, permanent shop + 6 skins + consumables, 14 achievements, 4 difficulties, revive/save systems, comfort/accessibility settings, PWA offline package.

---

## Completed / frozen versions log

| Date | Version | What changed |
|---|---|---|
| 2026-08-28 | v1.0 | Feature-complete initial release. All 106-question blueprint systems built and verified. |
| 2026-08-29 | v1.1 | First 5 upgrades always offer Health Regen + Heal-on-Kill + one other; airdrops start at L1 and heal 70% of the time for first 5 levels; Warlord (first boss) projectile speed & damage halved; all water removed from every biome; HP/XP bars show numbers (47/100) not %; added live Damage/Speed HUD meter; pause menu redesigned (deduped upgrades with ×counts, tappable evolution detail page). |
| 2026-08-29 | v1.2 | Armor is now a real soak pool (absorbs all damage until it breaks, then HP); armor refills from regen stat + repair/shield/airdrops; armor bar added to HUD; armor card tops pool; pause shows Max HP + Heal/Kill; early enemy damage toned down (~1.0× at L1); early card guarantee reduced to first 3 picks. |
| 2026-08-29 | v1.3 | Phase 2 "HUD tells the truth": DMG/SPD meter shows live values (base × boosts × slows) with bar filling to the number (100% = full); added BOOST/SLOWED status label + recolor; meter refreshes every 0.15s from the loop; HP no longer rounds up (uses floor); big HP/XP numbers overflow-safe (auto-shrink + ellipsis); armor pause chip reads `x armor`. |

---

## ✓ Verified TRUE findings (consolidated from 3 analyses) + what was done

| Finding | Status | Action |
|---|---|---|
| Armor was a hidden % discount (55% cap + 3 dmg floor), wasted past a point | ✅ TRUE | ✅ FIXED in v1.2 (real soak pool). |
| Armor had no visible display / feedback | ✅ TRUE | ✅ FIXED in v1.2 (armor bar + `ARMOR DOWN`). |
| Speed/DMG meter bar looked half-full at 100% (scaled ÷2 / ÷3) | ✅ TRUE | ✅ FIXED in v1.3 (bar fills to match number, 100% = full). |
| Meter only shows base %, ignores Haste/roots slowdown | ✅ TRUE | ✅ FIXED in v1.3 (live values + BOOST/SLOWED labels). |
| Pause menu missing Max HP + Heal/Kill | ✅ TRUE | ✅ FIXED in v1.2. |
| Enemies hit too hard at L1 (×1.65 on top of base) | ✅ TRUE | ✅ FIXED in v1.2 (now ~1.0× at L1). |
| Early card guarantee repeats same 2 cards | ✅ TRUE | ✅ Kept but reduced 5 → 3 picks (user choice). |
| HP rounds up by 1 during regen (cosmetic) | ✅ TRUE | ✅ FIXED in v1.3 (uses floor). |
| Big HP numbers may overflow small screens | ✅ TRUE | ✅ FIXED in v1.3 (auto-shrink + ellipsis). |
| "Skin gives stat bonuses / Glacier name mismatch / skin stats lost on revive" | ❌ **FALSE** | Skins are cosmetic-only (no stat system exists). No fix needed. |

**Open policy:** The three analyses agreed on two real problems — armor, and "metabars don't match reality." Both are now resolved: the **armor soak redesign** (v1.2) and the **Phase-2 HUD-truth fixes** (v1.3). All originally-flagged items are now fixed except the cosmetic "add armor to the bottom HP panel" (see v1.4 candidates below).

---

## The current plan (next steps, in order)

1. **Playtest v1.3 (human).** On the live preview **and ideally a real phone.** Open `http://localhost:8123/TankThilteteYt01_v1.3.html`. Focus: do the DMG/SPD meters now read honestly (bar fills to match the number, shows BOOST/SLOWED), does the HP number stop rounding up, any overflow.
2. **Collect feedback.** Is the armor still good after both phases? Are the meters clear? Any balance note?
3. **v1.4 candidates (not done yet):** optionally add an armor readout to the bottom HP panel; cap run-card speed if it gets absurd; give Adrenaline stack 1 its own real bonus. Ask the human which to include.
4. **Publish over HTTPS** so it installs as an app. Suggested free static hosts: GitHub Pages, Netlify, Vercel, or Surge. Upload `TankThilteteYt01_v1.3.html` (or whichever is current) + `manifest.webmanifest` + `sw.js` + the two icons.
   - **PWA note to handle at publish time:** the manifest's `start_url`/`scope` is `./`, and the sw caches `./`. On many hosts `./` serves an `index.html`. Right now the game file is named `TankThilteteYt01*.html`, not `index.html`. So before publishing, decide whether to (a) add an `index.html` that loads the current game, or (b) point the manifest/sw at the actual game filename, or (c) rename the game file to `index.html` for that deploy. Keep this in mind so the install-as-app works.
5. **Log every decision** in this diary so any future session is caught up.

---

## Open questions for the human (ask these at the start of the next session)

- Test v1.3 — do the **DMG/SPD meters** now read honestly (bar fills to match the number, shows BOOST/SLOWED)? Is the **HP number** no longer rounding up? Any **overflow** on big numbers?
- After both phases, how does the **armor soak system** feel — right pool size, good break pace, good regen refill?
- Is the **early game** fairer now?
- Do you want the **v1.4 items** (armor readout on the bottom HP panel; cap run-card speed; make Adrenaline stack-1 its own real bonus)?
- Which difficulty are you mostly playing (Easy/Normal/Hard/Nightmare) — too easy or too hard?
- Do you want a dedicated `index.html` so the game loads at `./` (cleaner for the PWA install)?
- Any new feature you want next, or are we purely polishing?

---

## If the game needs a change — the workflow

1. **Edit the current working file** (`TankThilteteYt01_v1.3.html`). **Never edit the frozen baselines** `TankThilteteYt01.html`, `TankThilteteYt01_v1.1.html`, `TankThilteteYt01_v1.2.html`.
2. Test on the live preview (`python3 -m http.server` in the repo root, open `/TankThilteteYt01_v1.3.html`).
3. When the change works and the human is happy, copy current → next version filename, and add a row to the "versions log" table above with a one-line changelog.
4. Update this diary's "TL;DR", "current version", and "current plan" so the next session reads the right thing.

---

## Technical reference (safe commands)

```bash
# Run the live preview (serves everything in this folder)
cd /home/user/4tanksrealm
python3 -m http.server 8123 --bind 0.0.0.0
# then open http://localhost:8123/TankThilteteYt01_v1.3.html
```

```bash
# Verify each embedded <script> block has valid syntax (no errors)
node -e '
const fs=require("fs"),vm=require("vm");
const html=fs.readFileSync("./TankThilteteYt01_v1.3.html","utf8");
const re=/<script\b([^>]*)>([\s\S]*?)<\/script>/gi; let m,i=0,ok=0,bad=0;
while((m=re.exec(html))){ if(/src\s*=/.test(m[1]))continue; i++; try{new vm.Script(m[2]);ok++;}catch(e){bad++;console.log("ERR",e.message);} }
console.log("blocks="+i+" ok="+ok+" err="+bad);'
```

```bash
# Check md5 to confirm two files are identical
md5sum TankThilteteYt01.html TankThilteteYt01_v1.1.html TankThilteteYt01_v1.2.html TankThilteteYt01_v1.3.html
```

```bash
# Quick armor soak math check (node one-liner)
node -e '
function h(p,a){let i=a,s=0,c=Math.max(0,p.armor||0),h=c>0;if(c>0){if(a<=c){s=a;p.armor=c-a;i=0;}else{s=c;p.armor=0;i=a-c;}}const d=Math.max(0,i);p.hp-=d;return{d,s,a:p.armor,h&&p.armor<=0};}
let p={armor:24,hp:100};console.log("armor24 hit30 ->",h(p,30),"hp:",p.hp);'

---

## Intent of this project

Make a genuinely fun, playable, installable mobile tank survival game that lives in a single HTML file, keep a clean archive of every version so we never lose work, and make sure any future AI session can pick up the exact plan in seconds.
