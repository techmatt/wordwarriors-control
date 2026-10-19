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

- `019_test_perf` (test_perf template): test cost, fast/slow lanes, faster tests; report gives timings.

## Waiting on Matt

- **Picks:** `art_alts_016_julia_chef` (face_julia_chef; 2 promoted) and `art_alts_018_moves` (20 new move-word pictures; executor's best promoted). Choices that differ need an apply item.
- **017 deferred calls:** (1) the parked Spell the Spell triple `CounterItem.words`: drop it and give the parked game its own lists (executor's pick), regenerate from `word`, or leave; (2) the scare swarm for named `scare` counters (Brave Rat) uses an emoji: use `pic_<word>` when it exists (executor's pick), a `swarm` art id, or keep; (3) per-branch voice manifest / content-hashed mp3 names (pipeline change; documented only); (4) `item_*` green halo: change the item brief to a gold glow (executor's pick) or default items to `NO_GREEN`.
- **016 questions:** Ellie's sword move word ZIP or BAM; an asleep-in-bed chef Julia image (one `art:alts` run).
- **Word-family minigame** (CAT/HAT/BAT, SIT/FIT/PIT): planner proposed a "word machine" side room — (1) make the picture: fixed rime, walk to the onset tile that builds the pictured word; (2) flip it: machine swaps the onset, she picks the matching picture; (3) real or silly: nonsense words make it burp. Progress per rime. Suggested mode 1 first. Matt to choose.
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

## Open questions (not blocking)

- 015: keep the 3× boost for the villain's own named counter word (Magic Hat), or plain random? (planner leans keep)
- Replace the CAN NOT STAND THE frame with IS NO MATCH FOR THE? (Matt: legal but not great phrasing)
- Who records the real letter-sound clips (the audit recommends Matt's own voice).
