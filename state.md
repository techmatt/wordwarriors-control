# wordwarriors — state

Status, plan, open items and flags; the wavefront, not a history (trimmed session 16). Changed only through conductor requests. Design: `design.md`. How the game works: the repo's docs; Matt's game rulings: the repo's `docs/rulings.md` (131) (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/qa-findings.md`, README, CLAUDE.md). Past items: their reports and git history.

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: raised only by Matt, or when a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH.

## Where it stands (session 16 closed 2026-10-26 ~10:10am)

- **The episode:** bedroom wake-up → entry-hall warm-up (sounds only, no letter names) → the quest place's hub (a story scene ending in a gift word, on a spot drawn for that story) → two side rooms (door a alternates Charge, two words a visit, and the Stretchy Bridge; door b the Shape-Shifter in 3 episodes of 7, never two running, else the rhyme room, fetch frames or the word machine; no side-room game repeats from last episode) → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast (11 allies, 7 villains), places, fights (Evil Smaug's story fight in about half his episodes), rooms and words are drawn per episode, with rotation memory.
- **Words:** about 140 live words; risky ones are stored (`STORED_WHY`, grown-ups page 3); the bank has enough variety (Matt). An action word is never a picture she picks. `npm run variety` measures reach and repeats.
- **Voice:** Matt's recordings cover every sound the live words use, all passable (Matt, 2026-10-26); F is a whole "fuh" (no hold; blends with F kept off the bridge). `listen.html` plays a word set covering every live sound; the recorder's `?missing` is empty.
- **Last session (16, items 161-167):** recordings and the listen page, Hunt 12 and its calls ruled, art for COT, DOT and Evil Elsa's Grumpy Snowman. Conductor 55 (light preamble for small items).

## Queued and running

nothing

## Maintenance

Triggers: **bug hunt** after a wave of big features or a new surface; **general cleanup** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test cleanup** when a full run has grown ~1.5×; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space cleanup** after much generated media; **content cleanup** only when Matt asks; **trim state** past ~25 KB. Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`, and resume from the last hunt's *Where the next hunt resumes*.

- Bug hunt: 164 (2026-10-26, done; Hunt 12; resume from its *Where the next hunt resumes*).
- General cleanup: 147 (2026-10-24).
- Cleanup: 076 (2026-10-21).
- Test cleanup: 105 (2026-10-22, partial; owed: a timed 3-worker run, splitting `episode.spec`'s real-time tests, a 20 ms `WW_POLL_MS` default if two full runs stay green, 4-6 workers if memory allows).
- claude.md cleanup: 118 (2026-10-22).
- Disk space cleanup: 151 (2026-10-25; then 152 thinned hunts 9-11, scratch home 89 GB → 1.3 GB). Hunt shots are now pruned and thinned by `tests/qa/prune.ts`, so this is rarely needed.
- Content cleanup: 127 (2026-10-23, the word audit).

## Waiting on Matt

none

## Open questions

none

## Paged

- **More fight styles:** a building contest for builder Matt, a sea race. Matt revives these when Julia seems bored of the current fights.
- **KID in the Shape-Shifter** (160): it never comes up there; its only neighbour is LID (LIP-LID-KID, too short to be drawn, all fix-it). KIT or KIN would fix it but are poor words. Default: leave; KID is read in the other rooms.
- **Opening's time budget** (165): the 250 ms rune beat leaves `opening.spec`'s 26 s limit to PICK A MOVE! about 1 s of room (seed 2 at 24.9 s). Default: leave; trim the opening if it goes red.
- **Crushing Coil's head is a little blobby** (165). Default: leave until a polish pass touches battle art.
- **Voice fingerprint gaps** (159): `TAIL_SECONDS` / `trimMp3` and `MP3_KBPS` are outside line fingerprints; including them re-synthesises every line. Default: leave (changing them needs `--force`).
- **Voice manifest split per group** (148): saves 30-50 ms a boot. Default: leave (Matt agreed).
- **Cosmetic refactors** (132): split `tests/qa/qa.pw.ts`, a home for `sceneGen`, notes out of `content/art/prompts.ts`. No rush; queue only with other work there.

## Pending fixes

Each item names the checkpoint it is due from; due items are top-level bullets that say "due" (the digest copies only those). Conductor findings never go here: only in `C:\Code\claude-conductor\planner-notes.md` *For HANDOFF Open*.

- **Recorder sync, due (rides the next wordwarriors prompt; due from checkpoint #4813):** whatever rewrites `tools/recorder/phonics-recorder.html` (`recorder:missing`, `voice:import`, `voice:lines`) also copies it to `C:\Code\techmatt.github.io\phonics-recorder.html` when that folder exists (uncommitted; Matt commits). Session 16 the planner hand-synced it three times (161-163), ~3 bridge calls each. Then drop the *Live recorder* flag's planner step.

## Planner habits

Rules for the planner itself: followed, never listed back to Matt (Matt, 2026-10-25).

- **Bridge and requests:** stage `state.md` fresh before a request and diff the request against it; read the inbox's *Red* before processing a report (conductor can overrule `status: done`); a stranded red branch lands with **land X**; every bridge upload goes to a fresh workspace path, never edited after; `expectedMtimeMs` only when replacing an existing file; request receipts can take ~5 s; once a conductor prompt is called ready, additions are a line Matt pastes into its session; to stop and restart work, **pause R** / **resume R**, never a tell asking an item to wait; after a critical tell, check its receipt says delivered.
- **Sessions 13-14:** re-stage `inbox.md` before **review next** / **check**. A bug hunt item gets `ultracode: true`. An art or candidate prompt ends at `pick:`; promotion rides a later prompt. Check a `state.md` premise against the repo before it goes in a prompt. Stage `review.md` only after the `review:` signal's receipt exists. Before saying a picker waits, read its `picks\<name>.choices.json`. Stage a write's receipts after the write's result and re-stage the same set once on a miss (one missing receipt fails the whole call); never list a folder or stage the inbox to confirm a write.
- **Session 15:** an investigation prompt for something Matt saw quotes his concrete symptom (the screen, the character, which server) and must reproduce that exact case (148 measured the default cast and missed Jasmine; 150 redid it). A question Matt pastes with no other context: answer it with the planner's best take as the first call (152's answer landed 18 s after its default).

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

## Conductor

- Reviewed through 55 (marker in `planner-notes.md`). Live behaviour is in `planner.md` and conductor's HANDOFF *Status*. Still to watch: a bug hunt's memory line against Task Manager, and the first real **pause R**.
