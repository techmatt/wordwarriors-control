# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

Every item for Matt sits in exactly one of three places. **Waiting on Matt** holds only what queued or next work is blocked on; it is raised at every session start until resolved. **Open questions** are real decisions the planner needs to author upcoming work; each is asked once, in the reply where it arises, and if Matt doesn't take it up it moves to **Paged** with the planner's default. **Paged** is everything else that is Matt's to do or decide whenever he gets to it: nothing waits on it, so the planner never asks about it, never lists it at session start or closeout, and never asks when. It comes up only when Matt raises it, or when a prompt already touching the same code can carry a paged polish item (said in one line).

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.6; session 5 closed 2026-10-20 11:10am, queue empty)

- The episode: bedroom wake-up (primary dad, maybe the other dad, the ally, good/bad news, the villain's house overlay, the ally's quest line) → entry-hall warm-up (033) → the quest place's hub (the ally's short story scene ends with a gift word) → two rooms drawn from the minigame pool → battle 1 → retreat, attic counter sentence → battle 2 → the reformed villain's sorry → a victory scene (8 scenes, 2–5 people, ~20 s) → recap with a picture per word.
- **Casting (025):** every episode draws its own cast (`src/rules/cast.ts`, `CAST_ODDS`): villain from all characters (her last 4 avoided), any good ally, primary dad Matt 60% / Jason 40%, other dad present 50%. Dad forms are roster characters: Matt builder / lifter / cyber / blade; Jason chef / warrior / warlock (purple fire). Julia's forms: chef (chef Jason), knight (warrior Jason). The fixed default episode (Julia + Ellie vs Evil Tiamat) is `?cast=default` / `randomCast: false`; overrides `?seed= ?ally= ?villain= ?form= ?primary= ?secondary= ?place=` (README).
- **Active cast (030):** `ACTIVE_CAST` in `src/config.ts` — allies Dada Matt (4 forms), Dada Jason (3), Scar, Ellie; villains Jörmungandr, Smaug, Bavmorda, Tiamat (last two villains sit out). All 36 pairs played green. Scar is a tiny gold mech (size 0.9, just under Julia; style-ref only) with his own Robot Workshop place; casts stand to their sizes everywhere (`castScale`).
- **Fight styles (031):** data in `content/battle/fights.ts`, staging in `src/battle/stages/`: Smaug sky race, Jörmungandr rope pull (never called TUG), Bavmorda and evil warlock Jason spell-beam clash, Tiamat brawl, cook-off (chef Jason ally 70%, evil chef Jason's own); others brawl. `?fight=` forces one. 
- **Entry-hall warm-up (033):** `src/scenes/EntryScene.ts`; 9 labelled pictures, a letter board, clue by level (1 word+names+sounds, 2 names+sounds, 3 sounds), per-word ramp in `grabLevels`, start `GRAB.startLevel = 2` in `src/config.ts` (lower to 1 if she should hear the word); the grabbed thing is her first battle item; exposure only (never a read). Letter-name lines `letter_<x>_name` (placeholders; `voice:clip` replaces).
- Weightlifter Dada Matt redrawn (032): fit not bulky, sleeved gym T-shirt, a modest dumbbell; Dumbbell Spin.
- **Battle polish (034):** Matt's 030–032 picks are in. Fighters stay a body width apart, landings spaced, contests use their stage's places, no line said twice in a row, bag reveal clear of everyone. Every dad form is `ADULT_HEIGHT` (1.5 in `src/config.ts`) times Julia's height everywhere (drawn height only; `size` drives the fight). Abilities can carry a `callout` (Pig Curse says "Curly Tail Curse!"). Battle shots: `tests/shots/polish.pw.ts` + contact sheets (README *Battle shots*).
- **Quests (025, 037):** every quest owner has 3 setup-line variants; 12 places (treehouse workshop, forest gym, hacker den, rune dojo, secret kitchen, knights' camp, moon tower, bubble castle, dragon mountain, ice castle, desert oasis, sea grotto, plus Scar's robot workshop), each with hub, two rooms and a secret room; guests visit others' places. **Hub scenes (037):** `content/house/scenes.ts`, 2–3 short story scenes per helper ending in a **gift word** drawn from the bank's actions (`drawGift`; the helper's own roster words count double); the spell lesson (`spell.ts`) is gone. Home appears every episode as the warm-up (033).
- **Minigame pool (025/026/037):** `MINIGAMES` in `src/rules/minigames.ts`; sentence frames + the **word machine** (make-the-picture uses pictured words only); 17 families incl. -UG and the 037 additions (ig in eg am op ox od un ut ub). Modes flip / real-or-silly are hooks.
- **Speaker UI (024):** a cream dialogue box with the speaker's framed face card and name on their side, a tail, placed top or bottom to keep clear of targets; compact in battle; face chips on bark bubbles.
- **Words (037, 040): one tagged bank** `content/phonics/bank.ts` (L1 CVC, L2 blends, L3 digraphs; 68 pictured familiar words after 040); every draw (key words, counter, pads, gift, warm-up, machine) goes through one path in `src/rules/bank.ts` (042): shakiness × coverage (vowel, onset, level) × level gate (`BANK_DRAW` in `src/config.ts`: L2 opens once 3% of L1 is solid, at weight 0.15). Distractors differ in first letter while a word is new, then share onset or rime. **Word magic:** any action word can be a pad and her hero fires its effect (`content/phonics/effects.ts`); roster words are flavour; POW and ICE are ability names only. Room words never repeat as pad words in an episode. Parent page: coverage by level/vowel/onset, then every word. Counter frames (8, see 040); named counters 3×. Text wraps everywhere.
- **Dad lock (038):** backquote/tilde toggles it anywhere (`src/input/dadLock.ts`); she can walk, no press or letter does anything, re-prompts wait, a 🔒 badge shows bottom-left; F9 still works. **Villain names (038):** reading sentences and the narrator's need lines use the bare name (JORMUNGANDR, RILLA); "Evil" stays where the villain is announced (wake-up bad news, name barks, nameplates). **Pads and gifts (038):** wrong pads rotate through a pad bag; casters (`CASTERS` in `content/house/scenes.ts`: Elsa, Bavmorda, Tiamat, Moriarty, warlock Jason, spell-blade Matt) give spell-flagged words ~82% of the time; DET/LAN are no longer silly words.
- **Familiar words (040):** bank entries carry an `odd` flag; only familiar words fill picture roles (rooms, counter, warm-up, word machine, fetch); odd action words stay pads/gift only. Out of play as unfamiliar: YAK VAT PEG FIG KIT COG ROD POD SUB HUT GUM WIG PIN RAFT PLUG SLUG TWIG VEST SLED PLUM MOTH SHED; pads/gift only: RAM TOP JET FIN. Added familiar: VET CHEST BIN ROCK CLOCK STICK BRUSH TRUCK BATH PLANT CRIB. 68 pictured words now; word-machine families -AN -AP -AT -EN -ET -OG -OX -UG -UN (no short-i family). **Variety (040):** 3 variants of the wake-up/good-news/door lines, villain taunts drawn from 3, reformed lines 3 sorry + 3 ending each, counter frames + CAN NOT BEAT THE / HIDES FROM THE / DOES NOT LIKE THE / SAYS YUCK TO THE. **039's fixes (52)** landed with 040.
- **Art briefs (041):** `art:alts --brief=<scratch file>` draws a candidate round from a brief; a round writes only `art-originals/alts` and `scratch`, so it runs as a readonly item beside other work (043, 044 did). Promotion (`art:pick`) is a normal item and writes the printed brief into the roster `look` (characters) or a `HAND` entry in `prompts.ts`. Cyber Dada Matt is the gauntlet engineer (good 10, evil 5, face 4 in 046); his drone moves became hologram tools / grid / gauntlet shield / blast (Scar's drone minion and the Drone Hangar stay).
- **Green family art:** a green family form must be in `LIGHT_GREEN` / `GREEN_JASON` (out of `NO_GREEN`) in `content/art/prompts.ts` before `art:pick`, or its green is washed out (049).
- **039's M1–M6 (045):** move-choice prompts never light or say the right word; the phonics face shows Dada Matt only when he is in the episode (`phonicsFace`); banners try two 56 px rows before shrinking; the stick hint (`src/ui/stickHint.ts`, `STICK_HINT_MS` 4 s) also shows in move choices; teammates step off signs when a choice opens (least-covered spot when none is clear).
- **K and Y (045, 048):** KEY and YOYO are ordinary bank words with hand-written sound units (`spelled` in `content/phonics/bank.ts`: K + long E; Y + long O twice), so hints and warm-up clues sound them in full and either may be the counter; level 1, no vowel tag, never in a family. Long-vowel lines `letter_long_e_sound` / `letter_long_o_sound` ("Ee"/"Oh" placeholders). PIN is familiar again, so -IN (PIN BIN) is back; -IG stays off (PIG is its only familiar picture). The secret-door sign is 🧭, not 🗝️.
- **Dad art (046):** Matt's palette picks promoted (Jason chef 2, warrior 5, warlock 4; Matt builder 4, lifter 7; evil chef Jason 1 with his own goatee; cyber Matt face 4 in `HAND`), each brief now the look. Jason's good forms and faces are `GREEN_JASON`, out of `NO_GREEN`; his evil forms and Matt's blue forms stay keyed. Face cards: Matt's `art_alts_046_faces` picks (049) — Jason chef 1, warrior 5, warlock 5; Matt builder 4, lifter 7.
- **Green keying (049):** `keyGreen` modes `keep` / `noGreen` / `lightGreen`; `keyMode(id)` in `content/art/prompts.ts` picks it for every art command (gen, reprocess, alts, pick). Jason's six green ids (`LIGHT_GREEN`) un-mix only bright screen green (green ≥120), so his forest green stays solid; his evil forms stay `noGreen`. Matt's 046/043 picks are in (Jason faces chef 1, warrior 5, warlock 5; YOYO 3).
- **Audit follow-ups (047):** the warm-up word avoids everything said before battle (stemmed); roster abilities carry one `words` list; `lines.json` is one object per line; Playwright serves itself on `CONDUCTOR_PORT`, else `TEST_PORT` 5184 (kept off the 5174 dev port).
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: unusable doors aren't drawn; a wrong move pick holds the fight until she finds the right word; the read pass speaks each word as it lights (key word silent).

## Queued and running

nothing (queue empty since 10:39am)

## Maintenance

The planner checks this at every session start and recommends what is due, with the reason (Matt approves by saying the phrase). Rough triggers: **bug hunt** after a wave of big features or a new surface; **general audit** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test perf audit** when a full run has grown ~1.5× since the last one; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space audit** when art/voice output has grown a lot.

- Bug hunt: 039 (2026-10-19; killed overnight, merged and finished through 040 on 2026-10-20; QA checker `tests/qa/`, findings `docs/qa-findings.md`). General audit: 042 (2026-10-20; ids/draw/voice-id/font consolidation, dead code out). Cleanup: 017. Test perf: 036 (full run ~18 min). claude.md cleanup: never. Disk space audit: never (037 added 243 art candidates and 3,708 voice lines).

## Waiting on Matt

nothing

## Conductor (hand-pasted)

- Live in the 11:06am daemon (detached, heartbeat): everything through conductor 23. Reports carry `slow:` (21; feeds maintenance triggers). The Repos tab is a split with the selected item's **Conversation** thread (22: tells with tagged replies, amendments, questions, progress, finish; Tell… / Outline? / Amend… at the bottom). **Outline** (23): executors post a terse section list with finish times (pinned in Conversation, one line in the inbox *Now*); **outline X** requests a fresh one. Memory sampling, pressure pauses, orphan reaping and `daemon_died` (20). The 11:06am `daemon_died` red (last heartbeat 7:01am, "4h05m") is an artifact of the old code having no heartbeat; it ran until ~10:41am and lost nothing.
- Picker (13, 13a): `pick:` opens a manifest in the browser; choices land in `picks/<name>.choices.json`, and the planner carries them into the next prompt. **review all** also covers conductor reports past HANDOFF's marker (now 23).
- Planner: write conductor's `HANDOFF.md` marker only when no conductor prompt is running, from a fresh stage (a stale write at 10:32am clobbered 22's Status; 23 restored it).

## Flags

- Memory (2026-10-20, conductor 20): last night was not the OS. A Claude Code session reaped its background `conductor app`, and the daemon (the app's child) and 039's executor (the daemon's child) died with it. The box's memory swing is Alienware's `OCControl.Service` (~3 GiB/min growth to ~9.7 GiB, released every ~3 min). Conductor now samples memory (inbox *Now* line, `memory.jsonl`), pauses launches under pressure (free RAM < 3 GiB), tells running items to cut parallelism, reaps orphans when an item ends, starts the daemon detached, and logs `daemon_died` after a silent death. Never start the daemon as a Claude Code background command.
- Tests (Matt, 2026-10-20): no full browser suite by default; fast lane plus the browser tests covering the change, full suite only when very clearly needed; misses are fixed later. In the repo's CLAUDE.md (046).
- Worktrees run `npm ci` at creation (`setup` in conductor.toml, Matt 2026-10-19).
- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge (see 017 deferred call 3).
- Generated voice (~5,100 lines) left git in 008; ~50 MB of old voice remains in git history.
- Codex image budget: 025 used ~40% of a 5-hour window and 23% of the weekly one; big art items should say so.
- Heavy items get `ultracode: true` front-matter (Matt, 2026-10-18); it is launch-only, a mid-run `tell:` does nothing.
- Changing a queued item: a rewrite is for a changed plan (discards a stage); **amend X** adds to a plan in any state but finished and keeps the stage. Check for the `edited` / `amended` event after every write (once, a bridge write landed stale). A reorder renumbers and discards stages.
- Homographs for TTS go in a line's `say:` respelling (020: "Bough to your queen!", "Whined-up Mice"); reword if a respelling sounds off.
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- Art: `npm run art:gen -- <ids…>` draws with Codex's image tool on Matt's ChatGPT Plus login (prompts in `content/art/prompts.ts`; `--reprocess` re-cuts from originals for free). ~35 s and ~0.3–1% of the 5-hour window per image. Candidate rounds: `art:alts` draws candidates and writes a picker manifest; Matt picks; `art:pick` promotes (`0` restores). Studio redesigns: Elsa a white-and-gold winter queen, Evil Elsa a silver-pixie frost witch, Anna (good + face) a dark-brown ponytail with purple ribbon, plum tunic and magenta cape, Jasmine short black curls in coral and saffron. The family is drawn from Matt's photos (`REFS` in `content/art/prompts.ts`; photos only in git-ignored `art-originals/refs/`). Ellie's image is the original bubble-wand one (Matt's pick 0).
- Move words are spoken by the partner by design, so a villain line containing a pad's word (Evil Bavmorda's "Everybody Pigs!") gives nothing away; only key words are protected.
- Ruled (Matt, 2026-10-19): "Bough to your queen!" stays.
- Ruled (Matt, 2026-10-19): fight style stays fixed per villain (its identity); word-machine blend/digraph families wait until she reads blends.
- Ruled (Matt, 2026-10-18): keep the 3× named-counter boost; Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Open questions

none

## Paged

- **`background` globs** for this repo's conductor.toml (long test commands always backgrounded, never hit the 10-minute cutoff); planner's default `["npm test*", "npm run test*", "npx playwright*"]`. Less pressing since 047 made Playwright serve itself.

- **KEY/YOYO as counters (045):** special words are never the counter word (keeps 009's decodable-counter rule); default keep.
- **Dad trail tints (046):** Jason's and Matt's in-game trail/palette tints don't follow their new colours.

- **Recordings (Dada Matt):** 26 letter sounds, the long E and long O sounds (`letter_long_e_sound`, `letter_long_o_sound`), and letter names (and the silly words, KUG/WUG included) via `npm run voice:clip`, replacing the placeholders (only "Mmm" doubled; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh; letter names `letter_<x>_name`). Sentence prefixes and read-backs are the next recordings worth making after those.
- **Bank thin spots (040):** G, V, W 1–2 pictured words each; PL/SL/TW blend pictures gone; -IG off unless WIG is made familiar.
- **Evil Anna redraw:** still the old copper-curl design; redraw when Anna joins the active cast.
- **Battle polish leftovers (034, minor):** brief edge contact during combos and mid-dash; a bubble can sit over a taller neighbour; full-screen combo flashes at their peak; the cook-off's tall winning cake can cover a hero.
- **More fight styles:** a building contest for builder Matt, a sea race.
