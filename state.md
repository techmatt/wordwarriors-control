# wordwarriors — state

Status, plan, open items and flags; the wavefront, not a history (trimmed session 14). Changed only through conductor requests. Design: `design.md`. How the game works: the repo's docs; Matt's game rulings: the repo's `docs/rulings.md` (131) (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/qa-findings.md`, README, CLAUDE.md). Past items: their reports and git history.

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: raised only by Matt, or when a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH.

## Where it stands (session 15 closed 2026-10-25 ~6:00pm)

- **The episode:** bedroom wake-up → entry-hall warm-up (sounds only, no letter names) → the quest place's hub (a story scene ending in a gift word, on a spot drawn for that story) → two side rooms (door a alternates Charge, two words a visit, and the Stretchy Bridge; door b the Shape-Shifter in 3 episodes of 7, never two running, else the rhyme room, fetch frames or the word machine; no side-room game repeats from last episode) → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast (11 allies, 7 villains), places, fights (Evil Smaug's story fight in about half his episodes), rooms and words are drawn per episode, with rotation memory.
- **Words:** about 140 live words (BED, TUB, NUT, BAG back live in 153; PUP, CUB, COT, KID new in 157; TAP and EGG read again in 156); risky ones are stored (`STORED_WHY`, grown-ups page 3); the bank has enough variety (Matt). An action word is never a picture she picks. `npm run variety` measures reach and repeats.
- **Session 14 (132-146):** general cleanup and its rulings, Hunts 10 and 11 with their rulings, Matt's playtest fixes (137), gift spots, the rhyme room, two-word Charge, the BattleScene/rooms split, pacing (Charge ≤ 40 s a visit, rhyme room ≤ 45 s, battle 1's first choice under ~26 s), Hunt 11 art. Conductor 52-53.
- **Session 15 (147-160):** general cleanup; fresh dev server ~3.6 s (148-149: scratch moved to `C:\Code\wordwarriors-scratch`, pruned and thinned automatically, 152); voice loading on slow servers fixed (150: background voice low priority, boot no longer awaits core clips); 147's and 132's code calls (153, 154, 159); four flakes fixed, three of them game bugs (155); content rulings (156: Comet Crash fire, Evil Elsa summons Grumpy Snowmen, Anna's ice-castle lines); Shape-Shifter words, draw change (`SHIFTER.wordsOut: 3`) and art (157, 160: MAN ~46% → ~23%, about a fifth of visits now 2-3 links); recorder `?only=` and a derived `?missing` (158). Conductor 54.

## Queued and running

nothing

## Maintenance

Triggers: **bug hunt** after a wave of big features or a new surface; **general cleanup** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test cleanup** when a full run has grown ~1.5×; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space cleanup** after much generated media; **content cleanup** only when Matt asks; **trim state** past ~25 KB. Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`, and resume from the last hunt's *Where the next hunt resumes*.

- **Bug hunt, due:** 142 (2026-10-24, done; resume from Hunt 11). Since then the Shape-Shifter draw and words, rhyme redraws, the giant edge clamp, TAP/EGG in reading, Evil Elsa's summon, Comet Crash and voice priority/boot all changed (147-160): the planner recommends one, best overnight.
- General cleanup: 147 (2026-10-24).
- Cleanup: 076 (2026-10-21).
- Test cleanup: 105 (2026-10-22, partial; owed: a timed 3-worker run, splitting `episode.spec`'s real-time tests, a 20 ms `WW_POLL_MS` default if two full runs stay green, 4-6 workers if memory allows).
- claude.md cleanup: 118 (2026-10-22).
- Disk space cleanup: 151 (2026-10-25; then 152 thinned hunts 9-11, scratch home 89 GB → 1.3 GB). Hunt shots are now pruned and thinned by `tests/qa/prune.ts`, so this is rarely needed.
- Content cleanup: 127 (2026-10-23, the word audit).

## Waiting on Matt

- **Recordings (Dada Matt):** five sounds, on `phonics-recorder.html?missing` (derived from the live words by `npm run recorder:missing`): A as in CAT (the old take is stale), F as in FAN (every take so far was "fuh"), OO as in ZOO, the schwa at the end of ZEBRA, OW as in COW. Hosted copy synced 2026-10-25; Matt commits and publishes techmatt.github.io, or uses `file:///C:/Code/wordwarriors/tools/recorder/phonics-recorder.html?missing`. Then a small item runs `voice:import` on the zip and `voice:build` (which also re-cuts the A carrier once, from 159).

## Open questions

none

## Paged

- **More fight styles:** a building contest for builder Matt, a sea race. Matt revives these when Julia seems bored of the current fights.
- **KID in the Shape-Shifter** (160): it never comes up there; its only neighbour is LID (LIP-LID-KID, too short to be drawn, all fix-it). KIT or KIN would fix it but are poor words. Default: leave; KID is read in the other rooms.
- **DOT looks like a blue ball** standing on the sand (160, Matt's pick 2). Watch whether Julia says "ball".
- **Shape-Shifter sound-out on a miss:** 160 ms gaps vs 400-700 ms elsewhere. Matt listens; default: leave.
- **Voice fingerprint gaps** (159): `TAIL_SECONDS` / `trimMp3` and `MP3_KBPS` are outside line fingerprints; including them re-synthesises every line. Default: leave (changing them needs `--force`).
- **Voice manifest split per group** (148): saves 30-50 ms a boot. Default: leave (Matt agreed).
- **Cosmetic refactors** (132): split `tests/qa/qa.pw.ts`, a home for `sceneGen`, notes out of `content/art/prompts.ts`. No rush; queue only with other work there.

## Pending fixes

Each item names the checkpoint it is due from; due items are top-level bullets that say "due" (the digest copies only those). Conductor findings never go here: only in `C:\Code\claude-conductor\planner-notes.md` *For HANDOFF Open*.

- **Planner habits, due (sessions 13-14; due from checkpoint #3859):** re-stage `inbox.md` before **review next** / **check**. A bug hunt item gets `ultracode: true`. An art or candidate prompt ends at `pick:`; promotion rides a later prompt. Check a `state.md` premise against the repo before it goes in a prompt. Stage `review.md` only after the `review:` signal's receipt exists. Before saying a picker waits, read its `picks\<name>.choices.json`. Stage a write's receipts after the write's result and re-stage the same set once on a miss (one missing receipt fails the whole call); never list a folder or stage the inbox to confirm a write.

- **Planner habits, due (session 15; due from checkpoint #4481):** an investigation prompt for something Matt saw quotes his concrete symptom (the screen, the character, which server) and must reproduce that exact case (148 measured the default cast and missed Jasmine; 150 redid it). A question Matt pastes with no other context: answer it with the planner's best take as the first call (152's answer landed 18 s after its default).
- **Parked edits, due (ride the next wordwarriors prompt; due from checkpoint #4481):** fix `charge.spec.ts:276` (the rune picture pulses to 1.15× forever, so its second height read can land lower: check once, or at rest); the `hunt10.spec.ts:14` spell-clash rings flake; delete the empty `C:\Code\wordwarriors\scratch\` (no longer in `shared`, conductor.toml request 20261025-1756).

## Flags

- **Auto-approve (Matt, 2026-10-22):** every item the planner drafts goes straight to `queue\`; Matt stops what he doesn't want.
- **Memory:** never start the daemon as a Claude Code background command (it dies with that session). Alienware's OCControl/AWCC is gone and memory no longer swings (143, 2026-10-24); the Dell/Alienware Update stack is still installed and could reinstall it (admin removal steps in 143's report). Conductor pauses launches under pressure.
- **Art:** `art:gen` / `art:alts` / `art:pick` in the README; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used. Small art flaws a report notes in passing are fine; don't raise them (Matt).
- **Questions (Matt):** `ask_default_minutes` stays 10; defaults stand when Matt doesn't see a question, and he corrects after. Don't raise timed-out defaults as problems. A question pasted with no context: the planner answers it with its best take.
- **Pauses (Matt, 2026-10-25):** the journey map's 2.6 s, part 1's VS cards (2.3 s) and the hub-to-room ~1.4 s are fine as they are.
- **Ultracode:** on for bug hunts, cleanups and multi-part items; off for items serial on one machine-saturating resource (full test-suite timing runs).
- **Audits (Matt, 2026-10-20):** the planner adds `audit: true` on its own judgment for a big pass through much-changed code, saying so in the reply.
- **Tests (Matt):** faster over thorough where reasonable; `npm test` plus the browser tests covering the change, full suite only when clearly needed (in the repo's CLAUDE.md).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy; the planner overwrites it from the repo's `tools/recorder/phonics-recorder.html` after every change, uncommitted, including when `voice:lines`, `voice:import` or `recorder:missing` rewrite its missing block; Matt commits that repo. `?only=<sounds>` gives any targeted set.
- **Storage policy (Matt, 2026-10-18):** git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals`, `voice-gen`), junctioned and shared into worktrees via conductor.toml / nowhere (rebuildable).
- Auto-push on (`push = true`); `background` globs set; worktrees run `npm ci` at creation.
- **Planner habits:** stage `state.md` fresh before a request and diff the request against it; read the inbox's *Red* before processing a report (conductor can overrule `status: done`); a stranded red branch lands with **land X**; every bridge upload goes to a fresh workspace path, never edited after; `expectedMtimeMs` only when replacing an existing file; request receipts can take ~5 s; once a conductor prompt is called ready, additions are a line Matt pastes into its session; to stop and restart work, **pause R** / **resume R**, never a tell asking an item to wait; after a critical tell, check its receipt says delivered.

## Conductor

- Reviewed through 54 (marker in `planner-notes.md`); 54: question cards wrap; `disk_audit` → `disk_cleanup` and `content_audit` → `content_cleanup` (old names alias); finished run logs ≥256 KB gzip (wordwarriors' backlog at its daemon's next start); preamble: irreversible step last, long-lived servers detached. Earlier: live behaviour is in `planner.md` and conductor's HANDOFF *Status*. 53: a Windows job object per executor, so an item's orphaned browsers count as its own; memory ticks every 2 s on a rise; the bug hunt template caps one browser lane plus one checker sweep; `session.md` / `inbox.md` *Now* show the next item number; "picks saved" shows on a pending pick. Still to watch: the next bug hunt's memory line against Task Manager, and the first real **pause R**.
