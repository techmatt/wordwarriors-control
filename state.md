# wordwarriors — state

Status, plan, open items and flags; the wavefront, not a history (trimmed session 14). Changed only through conductor requests. Design: `design.md`. How the game works: the repo's docs; Matt's game rulings: the repo's `docs/rulings.md` (131) (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/qa-findings.md`, README, CLAUDE.md). Past items: their reports and git history.

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: raised only by Matt, or when a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH.

## Where it stands (session 14 closed 2026-10-24 ~12:00pm)

- **The episode:** bedroom wake-up → entry-hall warm-up (sounds only, no letter names) → the quest place's hub (a story scene ending in a gift word, on a spot drawn for that story) → two side rooms (door a alternates Charge, two words a visit, and the Stretchy Bridge; door b the Shape-Shifter in 3 episodes of 7, never two running, else the rhyme room, fetch frames or the word machine; no side-room game repeats from last episode) → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast (11 allies, 7 villains), places, fights (Evil Smaug's story fight in about half his episodes), rooms and words are drawn per episode, with rotation memory.
- **Words:** 133 live words; risky ones are stored (`STORED_WHY`, grown-ups page 3); the bank has enough variety (Matt). An action word is never a picture she picks. `npm run variety` measures reach and repeats.
- **Session 14 (132-146):** general cleanup and its rulings, Hunts 10 and 11 with their rulings, Matt's playtest fixes (137), gift spots, the rhyme room, two-word Charge, the BattleScene/rooms split, pacing (Charge ≤ 40 s a visit, rhyme room ≤ 45 s, battle 1's first choice under ~26 s), Hunt 11 art. Conductor 52-53.

## Queued and running

nothing

## Maintenance

Triggers: **bug hunt** after a wave of big features or a new surface; **general cleanup** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test cleanup** when a full run has grown ~1.5×; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space audit** after much generated media; **content audit** only when Matt asks; **trim state** past ~25 KB. Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`, and resume from the last hunt's *Where the next hunt resumes*.

- Bug hunt: 142 (2026-10-24, done; resume from Hunt 11).
- General cleanup: 132 (2026-10-23).
- Cleanup: 076 (2026-10-21).
- Test cleanup: 105 (2026-10-22, partial; owed: a timed 3-worker run, splitting `episode.spec`'s real-time tests, a 20 ms `WW_POLL_MS` default if two full runs stay green, 4-6 workers if memory allows).
- claude.md cleanup: 118 (2026-10-22).
- Disk space audit: 084 (2026-10-21; shots are ~1 MB each, so big sweeps or shot runs are the trigger).
- Content audit: 127 (2026-10-23, the word audit).

## Waiting on Matt

nothing

## Open questions

none

## Paged

- **Medal word offset** (146): CLAP sits ~10 px high on `prop_medal` (the ribbon); a per-prop word offset in `HubScene.propBehind` fixes it. Default: leave.
- **`gestureWords`** (`src/rules/charge.ts`, from 133): still counts a charge gesture's words (TAP, EGG) as said in the episode, keeping them out of reading though nothing speaks them since 058. Default (asked session 14): leave.
- **Recordings (Dada Matt):** open `C:\Code\wordwarriors\tools\recorder\phonics-recorder.html?missing` locally (F as FAN, A as CAT; its zip goes to `voice:import`; afterwards empty the page's `MISSING` list). F ("ffff" with no "uh") and A are left (short A is TTS from "Add" until he re-records a steady CAT vowel). Silly words and sentence prefixes are later lists for the same tool (letter names and the name bridges were retired by 137).
- **115's optional calls (default: leave):** Evil Ozymandias's Comet Crash and Evil Elsa's Forever Winter are both icy-blue waves; Evil Elsa has no summon ability; Anna's quest line against Evil Elsa still says "train at my sister's ice castle".
- **More fight styles:** a building contest for builder Matt, a sea race.
- **Shape-Shifter:** MAN is still in ~46% of visits (more words would fix it; Matt ruled none); its islands (DOG-LOG-LEG, NUT-NET-VET, FOX-BOX, LIP-LID) never chain.
- **132's own-item refactors** (clear, too big for a sweep; `BattleScene.ts` and `rules/sentences.ts` are 141): split `tests/qa/qa.pw.ts`; a `SceneKey` union; `VoiceBus` → `src/voice/`, a home for `sceneGen`; a relock hook for rooms' `narrate`/`speak` + shared `flow` counter (needs design: changes Entry, Hub, Bedroom); one hard C/K helper (must not fold BELT/BELL); one voice-manifest schema shared by `VoiceBank` and `tools/voice/types.ts`; shared spec page helpers (fake-hidden-tab copies differ); pick notes out of `content/art/prompts.ts`; restructure `docs/systems.md`'s long cells; voice split/fingerprint coupling (`--force` note or a version).
- **Pickers:** face-card picker `scratch/art_alts_113_faces.json` (if still on disk).

## Pending fixes

Each item names the checkpoint it is due from; due items are top-level bullets that say "due" (the digest copies only those). Conductor findings never go here: only in `C:\Code\claude-conductor\planner-notes.md` *For HANDOFF Open*.

- **Planner habits, due (sessions 13-14; due from checkpoint #3859):** re-stage `inbox.md` before **review next** / **check**. A bug hunt item gets `ultracode: true`. An art or candidate prompt ends at `pick:`; promotion rides a later prompt. Check a `state.md` premise against the repo before it goes in a prompt. Stage `review.md` only after the `review:` signal's receipt exists. Before saying a picker waits, read its `picks\<name>.choices.json`. Stage a write's receipts after the write's result and re-stage the same set once on a miss (one missing receipt fails the whole call); never list a folder or stage the inbox to confirm a write.

## Flags

- **Auto-approve (Matt, 2026-10-22):** every item the planner drafts goes straight to `queue\`; Matt stops what he doesn't want.
- **Memory:** never start the daemon as a Claude Code background command (it dies with that session). Alienware's OCControl/AWCC is gone and memory no longer swings (143, 2026-10-24); the Dell/Alienware Update stack is still installed and could reinstall it (admin removal steps in 143's report). Conductor pauses launches under pressure.
- **Art:** `art:gen` / `art:alts` / `art:pick` in the README; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used. Small art flaws a report notes in passing are fine; don't raise them (Matt).
- **Questions (Matt):** `ask_default_minutes` stays 10; defaults stand when Matt doesn't see a question, and he corrects after. Don't raise timed-out defaults as problems.
- **Ultracode:** on for bug hunts, cleanups and multi-part items; off for items serial on one machine-saturating resource (full test-suite timing runs).
- **Audits (Matt, 2026-10-20):** the planner adds `audit: true` on its own judgment for a big pass through much-changed code, saying so in the reply.
- **Tests (Matt):** faster over thorough where reasonable; `npm test` plus the browser tests covering the change, full suite only when clearly needed (in the repo's CLAUDE.md).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy; the planner overwrites it from the repo's `tools/recorder/phonics-recorder.html` after every change, uncommitted; Matt commits that repo.
- **Storage policy (Matt, 2026-10-18):** git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals`, `voice-gen`), junctioned and shared into worktrees via conductor.toml / nowhere (rebuildable).
- Auto-push on (`push = true`); `background` globs set; worktrees run `npm ci` at creation.
- **Planner habits:** stage `state.md` fresh before a request and diff the request against it; read the inbox's *Red* before processing a report (conductor can overrule `status: done`); a stranded red branch lands with **land X**; every bridge upload goes to a fresh workspace path, never edited after; `expectedMtimeMs` only when replacing an existing file; request receipts can take ~5 s; once a conductor prompt is called ready, additions are a line Matt pastes into its session; to stop and restart work, **pause R** / **resume R**, never a tell asking an item to wait; after a critical tell, check its receipt says delivered.

## Conductor

- Reviewed through 53 (marker in `planner-notes.md`); live behaviour is in `planner.md` and conductor's HANDOFF *Status*. 53: a Windows job object per executor, so an item's orphaned browsers count as its own; memory ticks every 2 s on a rise; the bug hunt template caps one browser lane plus one checker sweep; `session.md` / `inbox.md` *Now* show the next item number; "picks saved" shows on a pending pick. Still to watch: the next bug hunt's memory line against Task Manager, and the first real **pause R**.
