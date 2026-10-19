# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.3)

- The episode plays end to end: bedroom wake-up (Dada Matt, good/bad news, the villain's house overlay) → hub (the ally teaches a spell) → two sentence rooms → battle 1 (fetched items used; walk-onto word pads for move choices) → retreat to hub, attic counter sentence → battle 2 → the reformed villain speaks → victory recap with a picture per word. Pick screens, v0.1 prep games, alarm and camp parked.
- **Defaults (Matt, 2026-10-18):** Julia + Ellie vs Evil Tiamat (`EPISODE_DEFAULTS` in `src/config.ts`). Ellie is a bubble fighter (Giant Bubbles = BIG, her spell; Bubble Trap POP; Bubble Shield; Peekaboo HOP; one sword move, Spinny Swords ZIP; Mega Bubble Storm); team move Star Bubble Spin. Tiamat (013) is the biggest roster character, staged as a giant; her named counter is HAT (Magic Hat swallows her storm), drawn 3× as often. Roster: 16 characters.
- **Julia's forms (016):** data in `content/battle/forms.ts`; chef Julia (`char_julia_chef`, `face_julia_chef`) when the ally is `dada_jason`, from the wake-up burst on. Chef episode = change `ally: 'ellie'` → `ally: 'dada_jason'` in `EPISODE_DEFAULTS`; `?ally=dada_jason` tries it.
- **Word bag (015):** key words (side rooms + attic) from a per-player bag of 30 decodable CVC words, spent only when read right first time, leaning to shaky words, none repeated in an episode, nothing said or shown earlier. Frames: 5 fetch (incl. JULIA NEEDS THE), 4 counter (SCARED OF THE, HATES THE, RUNS FROM THE, CAN NOT STAND THE). A drawn counter word sends a swarm of its picture ("NOT THE MOP!"). F9 grown-ups page shows the bag. MICE unused (not decodable). `voice:build --prune` would clear 20 orphaned mp3s.
- **Move words (018):** pool of 26; each fighter answers to 6–10; per episode two choices per battle part (first is the spell), the rest from a per-player move bag; wrong pads unseen this episode; a super throws its word's picture. Lines that would say a pad word still to come are skipped. Every character has two `reformed` lines. Speech bubbles are upper case.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: unusable doors aren't drawn; a wrong move pick holds the fight until she finds the right word; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `020_fixes_and_calls`: Tiamat's "bow" (and other homographs), text wrapping everywhere, 017 calls (drop `CounterItem.words`, `pic_` swarm, gold item glow, IS NO MATCH FOR THE), picks pic_zap 1 / pic_pow 1.
- `024_speaker_ui` (ultracode): speaker face cards shown prominently with every line, one dialogue-box style for non-battle scenes, polish from screenshot review; before/after in `scratch/ui_024_before_after.png`.
- `025_casting_and_quests` (ultracode, 6h): random villain (all evil roster + evil forms, no repeat) and ally; primary dad 60% Matt / 40% Jason, other dad present 50%; dads sometimes ally; new forms with good + evil + face + kit + quest: Matt weightlifter, programmer/cyberdecker, spell-blade; Jason fantasy warrior, warlock (original, nothing WoW-specific); ally quests (place + setup line, new backgrounds); rooms sample minigames from a pool.
- `026_word_machine` (ultracode): word-family minigame mode 1 "make the picture" in the pool.
- `027_victory_scenes` (ultracode): random short warm scenes (dessert, picnic, mountain…) with the reformed villain, before the recap.
- `028_cast_and_scar` (ultracode): active cast as data — allies Dada Matt (4 forms), Dada Jason (3 forms), Scar, Ellie; villains Jörmungandr, Smaug, Bavmorda, Tiamat; every pair played; Scar redesigned as a tiny gold-and-black robot just shorter than Julia (Matt's reference `art-originals/refs/scar_reference.png`, private).
- `029_fight_styles` (ultracode, 5h): fight style as villain data — races, cook-offs, beam clashes, contests alongside Magicka brawls; same part-1-lose / part-2-win shape and move words; starts with the active villains, plus a cook-off chef Jason triggers.
- (021–023 were cancelled and requeued as 025–027 to add the new Dada forms and put the speaker UI first.)

## Waiting on Matt

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
- Heavy items get `ultracode: true` front-matter (Matt, 2026-10-18); it is launch-only, a mid-run `tell:` does nothing.
- A rewrite of a queued item's file is not picked up (015 ran its original text); queue a new item instead (conductor HANDOFF *Open*).
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- Ruled (Matt, 2026-10-18): keep the 3× named-counter boost; Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
