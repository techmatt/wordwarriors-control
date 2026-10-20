# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

Every item for Matt sits in exactly one of three places. **Waiting on Matt** holds only what queued or next work is blocked on; it is raised at every session start until resolved. **Open questions** are real decisions the planner needs to author upcoming work; each is asked once, in the reply where it arises, and if Matt doesn't take it up it moves to **Paged** with the planner's default. **Paged** is everything else that is Matt's to do or decide whenever he gets to it: nothing waits on it, so the planner never asks about it, never lists it at session start or closeout, and never asks when. It comes up only when Matt raises it, or when a prompt already touching the same code can carry a paged polish item (said in one line).

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.5 + 034; session 4 opened 2026-10-19 5:05pm)

- The episode: bedroom wake-up (primary dad, maybe the other dad, the ally, good/bad news, the villain's house overlay, the ally's quest line) → entry-hall warm-up (033) → the quest place's hub (ally teaches a spell) → two rooms drawn from the minigame pool → battle 1 → retreat, attic counter sentence → battle 2 → the reformed villain's sorry → a victory scene (8 scenes, 2–5 people, ~20 s) → recap with a picture per word.
- **Casting (025):** every episode draws its own cast (`src/rules/cast.ts`, `CAST_ODDS`): villain from all characters (her last 4 avoided), any good ally, primary dad Matt 60% / Jason 40%, other dad present 50%. Dad forms are roster characters: Matt builder / lifter / cyber / blade; Jason chef / warrior / warlock (purple fire). Julia's forms: chef (chef Jason), knight (warrior Jason). The fixed default episode (Julia + Ellie vs Evil Tiamat) is `?cast=default` / `randomCast: false`; overrides `?seed= ?ally= ?villain= ?form= ?primary= ?secondary= ?place=` (README).
- **Active cast (030):** `ACTIVE_CAST` in `src/config.ts` — allies Dada Matt (4 forms), Dada Jason (3), Scar, Ellie; villains Jörmungandr, Smaug, Bavmorda, Tiamat (last two villains sit out). All 36 pairs played green. Scar is a tiny gold mech (size 0.9, just under Julia; style-ref only) with his own Robot Workshop place; casts stand to their sizes everywhere (`castScale`).
- **Fight styles (031):** data in `content/battle/fights.ts`, staging in `src/battle/stages/`: Smaug sky race, Jörmungandr rope pull (never called TUG), Bavmorda and evil warlock Jason spell-beam clash, Tiamat brawl, cook-off (chef Jason ally 70%, evil chef Jason's own); others brawl. `?fight=` forces one. 
- **Entry-hall warm-up (033):** `src/scenes/EntryScene.ts`; 9 labelled pictures, a letter board, clue by level (1 word+names+sounds, 2 names+sounds, 3 sounds), per-word ramp in `grabLevels`, start `GRAB.startLevel = 2` in `src/config.ts` (lower to 1 if she should hear the word); the grabbed thing is her first battle item; exposure only (never a read). Letter-name lines `letter_<x>_name` (placeholders; `voice:clip` replaces).
- Weightlifter Dada Matt redrawn (032): fit not bulky, sleeved gym T-shirt, a modest dumbbell; Dumbbell Spin.
- **Battle polish (034):** Matt's 030–032 picks are in. Fighters stay a body width apart, landings spaced, contests use their stage's places, no line said twice in a row, bag reveal clear of everyone. Every dad form is `ADULT_HEIGHT` (1.5 in `src/config.ts`) times Julia's height everywhere (drawn height only; `size` drives the fight). Abilities can carry a `callout` (Pig Curse says "Curly Tail Curse!"). Battle shots: `tests/shots/polish.pw.ts` + contact sheets (README *Battle shots*).
- **Quests (025):** every character has a setup line; 12 places (treehouse workshop, forest gym, hacker den, rune dojo, secret kitchen, knights' camp, moon tower, bubble castle, dragon mountain, ice castle, desert oasis, sea grotto), each with hub, two rooms and a secret room; Julia, Scar, Moriarty, Bavmorda, Rilla visit others' places as guests. Home appears every episode as the grab-before-leaving warm-up (033).
- **Minigame pool (025/026):** `MINIGAMES` in `src/rules/minigames.ts`; sentence frames + the **word machine** (mode 1 make-the-picture; in ~half of episodes, weighted to shaky families; every built word becomes a battle item). Families from pictured words: -AT, -AN, -AP, -EN, -ET, -OG, -UG (BUG MUG RUG JUG; sillies KUG, WUG; 035). Modes flip / real-or-silly are hooks.
- **Speaker UI (024):** a cream dialogue box with the speaker's framed face card and name on their side, a tail, placed top or bottom to keep clear of targets; compact in battle; face chips on bark bubbles.
- **Words:** key words from a per-player bag of 33 CVC words (new words join a round under way: `topUpBag`, `bagKnown` in ProgressStore; 035); CUP is a teacup on a saucer so it never looks like MUG; counter frames SCARED OF THE / HATES THE / RUNS FROM THE / IS NO MATCH FOR THE; random counter with named counters 3× (Magic Hat etc.); 26 move words from a move bag; every character has two reformed lines (the sorry ends battle 2, the second is said in the victory scene). Text wraps everywhere.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: unusable doors aren't drawn; a wrong move pick holds the fight until she finds the right word; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `036_test_perf` (running, test_perf template): the full run crept from ~12 to ~45 min per item. 034 and 035 skipped the slow lane on Matt's word, for this run to cover.
- `037_hub_scenes_and_move_words` (ultracode, 4h; rewritten 9:10pm before launch): phonics first — one tagged word bank (level 1 CVC balanced by vowel/onset, level 2 blends, level 3 digraphs) with coverage-weighted draws for every pool and reading-based distractors; word magic (any action word can be a battle pad; her hero casts that word's own effect); story hub scenes with 2–3 variants per character, the ally's word drawn from the bank; picker `art_alts_037_words`; report enumerates every pool and coverage.

## Waiting on Matt

nothing

## Conductor (hand-pasted)

- 12a done: "audit pending: N audit notes" in inbox, `conductor status` and the app. 14 done: **disk space audit R**, **claude.md cleanup R**; run logs compacted.
- Picker shipped (13, 13a: images never altered): `pick:` opens a manifest in the browser; choices land in `picks/<name>.choices.json`, and the planner carries them into the next prompt.

## Flags

- Worktrees run `npm ci` at creation (`setup` in conductor.toml, Matt 2026-10-19).
- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge (see 017 deferred call 3).
- Generated voice (~5,100 lines) left git in 008; ~50 MB of old voice remains in git history.
- Run the daemon in its own terminal (`uv run conductor run C:\Code\wordwarriors-control`), not from the app: a daemon started by the app died with it when the app was killed for low memory (2026-10-19).
- Codex image budget: 025 used ~40% of a 5-hour window and 23% of the weekly one; big art items should say so.
- Heavy items get `ultracode: true` front-matter (Matt, 2026-10-18); it is launch-only, a mid-run `tell:` does nothing.
- A rewrite of a queued item does take effect (conductor 14); the 015 rewrite never reached disk. Conductor logs an `edited` event when a queued file changes; no `edited` event means the write didn't land.
- Homographs for TTS go in a line's `say:` respelling (020: "Bough to your queen!", "Whined-up Mice"); reword if a respelling sounds off.
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- Word families: -IT and -OP skipped (no clear pictures / move words).
- Art: `npm run art:gen -- <ids…>` draws with Codex's image tool on Matt's ChatGPT Plus login (prompts in `content/art/prompts.ts`; `--reprocess` re-cuts from originals for free). ~35 s and ~0.3–1% of the 5-hour window per image. Candidate rounds: `art:alts` draws candidates and writes a picker manifest; Matt picks; `art:pick` promotes (`0` restores). Studio redesigns: Elsa a white-and-gold winter queen, Evil Elsa a silver-pixie frost witch, Anna (good + face) a dark-brown ponytail with purple ribbon, plum tunic and magenta cape, Jasmine short black curls in coral and saffron. The family is drawn from Matt's photos (`REFS` in `content/art/prompts.ts`; photos only in git-ignored `art-originals/refs/`). Ellie's image is the original bubble-wand one (Matt's pick 0).
- Move words are spoken by the partner by design, so a villain line containing a pad's word (Evil Bavmorda's "Everybody Pigs!") gives nothing away; only key words are protected.
- Ruled (Matt, 2026-10-19): "Bough to your queen!" stays.
- Ruled (Matt, 2026-10-18): keep the 3× named-counter boost; Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Open questions

none

## Paged

- **Recordings (Dada Matt):** 26 letter sounds and letter names (and the silly words, KUG/WUG included) via `npm run voice:clip`, replacing the placeholders (only "Mmm" doubled; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh; letter names `letter_<x>_name`). Sentence prefixes and read-backs are the next recordings worth making after those.
- **035 picker** (`art_alts_035_ug`: MUG, RUG, JUG, CUP): the executor's picks are already in the game; saving only matters to change one.
- **Evil Anna redraw:** still the old copper-curl design; redraw when Anna joins the active cast.
- **Battle polish leftovers (034, minor):** brief edge contact during combos and mid-dash; a bubble can sit over a taller neighbour; full-screen combo flashes at their peak; the cook-off's tall winning cake can cover a hero.
- **More fight styles:** a building contest for builder Matt, a sea race.
