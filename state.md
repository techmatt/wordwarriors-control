# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.4, overnight 2026-10-19)

- The episode: bedroom wake-up (primary dad, maybe the other dad, the ally, good/bad news, the villain's house overlay, the ally's quest line) → the quest place's hub (ally teaches a spell) → two rooms drawn from the minigame pool → battle 1 → retreat, attic counter sentence → battle 2 → the reformed villain's sorry → a victory scene (8 scenes, 2–5 people, ~20 s) → recap with a picture per word.
- **Casting (025):** every episode draws its own cast (`src/rules/cast.ts`, `CAST_ODDS`): villain from all characters (her last 4 avoided), any good ally, primary dad Matt 60% / Jason 40%, other dad present 50%. Dad forms are roster characters: Matt builder / lifter / cyber / blade; Jason chef / warrior / warlock (purple fire). Julia's forms: chef (chef Jason), knight (warrior Jason). The fixed default episode (Julia + Ellie vs Evil Tiamat) is `?cast=default` / `randomCast: false`; overrides `?seed= ?ally= ?villain= ?form= ?primary= ?secondary= ?place=` (README).
- **Quests (025):** every character has a setup line; 12 places (treehouse workshop, forest gym, hacker den, rune dojo, secret kitchen, knights' camp, moon tower, bubble castle, dragon mountain, ice castle, desert oasis, sea grotto), each with hub, two rooms and a secret room; Julia, Scar, Moriarty, Bavmorda, Rilla visit others' places as guests. A random episode never trains at home now (giving some characters the home quest is a data change).
- **Minigame pool (025/026):** `MINIGAMES` in `src/rules/minigames.ts`; sentence frames + the **word machine** (mode 1 make-the-picture; in ~half of episodes, weighted to shaky families; every built word becomes a battle item). Families from pictured words: -AT, -AN, -AP, -EN, -ET, -OG; -IT/-OP/-UG have no pictured non-move words yet. Modes flip / real-or-silly are hooks.
- **Speaker UI (024):** a cream dialogue box with the speaker's framed face card and name on their side, a tail, placed top or bottom to keep clear of targets; compact in battle; face chips on bark bubbles.
- **Words:** key words from a per-player bag of 30 CVC words; counter frames SCARED OF THE / HATES THE / RUNS FROM THE / IS NO MATCH FOR THE; random counter with named counters 3× (Magic Hat etc.); 26 move words from a move bag; every character has two reformed lines (the sorry ends battle 2, the second is said in the victory scene). Text wraps everywhere.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: unusable doors aren't drawn; a wrong move pick holds the fight until she finds the right word; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `030_cast_and_scar_resume` (ultracode): 028 was killed at ~3:55am by low memory (art generation + 36 browser pair-plays at once); red, worktree kept with uncommitted changes. 030 salvages it and finishes: active cast (allies Dada Matt ×4 forms, Dada Jason ×3, Scar, Ellie; villains Jörmungandr, Smaug, Bavmorda, Tiamat; every pair played) and Scar as a tiny gold robot just shorter than Julia; memory rule (never art + browser at once).
- `031_fight_styles` (after 030, ultracode): fight style as villain data — races, cook-offs, beam clashes, contests alongside brawls. (029 cancelled and requeued as 031 since its dependency went red.)
- `032_picks_and_lifter`: applies Matt's 025–027 picks (18 + word machine 3, re-fit its window/panel + fort 3), and redraws weightlifter Dada Matt (good, evil, face): less buff, sleeved weightlifting T-shirt, a modest dumbbell, no Olympic lift.

## Waiting on Matt

- Picks for 025–027 saved (Matt, 2026-10-19) and carried in 032.
- Word families -IT/-OP/-UG need new pictured words (e.g. MUG/RUG/JUG, MOP is a key word) — Matt's call whether to add.
- Art: `npm run art:gen -- <ids…>` draws with Codex's image tool on Matt's ChatGPT Plus login (prompts in `content/art/prompts.ts`; `--reprocess` re-cuts from originals for free). ~35 s and ~0.3–1% of the 5-hour window per image. Candidate rounds: `art:alts` draws candidates and writes a picker manifest; Matt picks; `art:pick` promotes (`0` restores). Studio redesigns: Elsa a white-and-gold winter queen, Evil Elsa a silver-pixie frost witch, Anna (good + face) a dark-brown ponytail with purple ribbon, plum tunic and magenta cape while Evil Anna is still the old copper-curl design (a redraw makes them match), Jasmine short black curls in coral and saffron. The family is drawn from Matt's photos (`REFS` in `content/art/prompts.ts`; photos only in git-ignored `art-originals/refs/`). Ellie's image is the original bubble-wand one (Matt's pick 0).
- Voice recordings: Matt will do them at some point, not immediately.
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds); sentence prefixes and read-backs are the next recordings worth making.

## Conductor (hand-pasted)

- 12a (optional "cleanup pending" wording): paste or skip.
- Picker shipped (13, 13a: images never altered): `pick:` opens a manifest in the browser; choices land in `picks/<name>.choices.json`, and the planner carries them into the next prompt.

## Flags

- Every worktree starts without `node_modules`, so executors run `npm ci` first (~1 min each; README *Run it* says so). `setup = ["npm ci"]` in conductor.toml would do it up front: Matt's call.
- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge (see 017 deferred call 3).
- Generated voice (~5,100 lines) left git in 008; ~50 MB of old voice remains in git history.
- Run the daemon in its own terminal (`uv run conductor run C:\Code\wordwarriors-control`), not from the app: a daemon started by the app died with it when the app was killed for low memory (2026-10-19).
- Codex image budget: 025 used ~40% of a 5-hour window and 23% of the weekly one; big art items should say so.
- Heavy items get `ultracode: true` front-matter (Matt, 2026-10-18); it is launch-only, a mid-run `tell:` does nothing.
- A rewrite of a queued item does take effect (conductor 14); the 015 rewrite never reached disk. Conductor logs an `edited` event when a queued file changes; no `edited` event means the write didn't land.
- Homographs for TTS go in a line's `say:` respelling (020: "Bough to your queen!", "Whined-up Mice"); reword if a respelling sounds off.
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- Ruled (Matt, 2026-10-18): keep the 3× named-counter boost; Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
