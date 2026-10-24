# wordwarriors — state

Status, plan, open items and flags; the wavefront, not a history (trimmed session 13). Changed only through conductor requests. Design: `design.md`. How the game works: the repo's docs; Matt's game rulings: the repo's `docs/rulings.md` (131) (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/qa-findings.md`, README, CLAUDE.md). Past items: their reports and git history.

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: raised only by Matt, or when a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH.

## Where it stands (session 13 closed 2026-10-23 ~10:30am)

- **The episode:** bedroom wake-up → entry-hall warm-up → the quest place's hub (a story scene ending in a gift word) → two side rooms (door a Charge/Bridge; door b Shape-Shifter about half the time, else fetch frames or the word machine) → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast (11 allies, 7 villains), places, fights (Evil Smaug's story fight in about half his episodes), rooms and words are drawn per episode, with rotation memory.
- **Words:** 133 live words; risky ones are stored (`STORED_WHY` in `content/phonics/bank.ts`, grown-ups page 3); the bank has enough variety (Matt). `npm run variety` measures reach and repeats over 300 episodes.
- **Session 13 (116-130):** bug hunts 7-9, general and claude.md cleanups, solo Charge for the session, cast heights, story-fight art, variety fixes, familiar words, the word audit, banners that fit their words, Shape-Shifter chains from the smaller pool. Conductor 47-51 and cleanup 2026-10-23.
- **Session 14 (132):** general cleanup (~140 verified findings; Stretchy Bridge sparkle bug fixed; soak's story-fight red since 126 fixed; docs match the code). Its big refactors are in *Paged*. 133: its deferred calls as ruled (W39 fixed: pictures 40 px lower, step-back follows them; made-things out of the battle; charge-gesture lines pruned; `?seed=` replays the house plan for the first episode after load; `perf` times the build). 134: arena ambience on `ARENAS`, nursery/street candidates at a picker. 135: Hunt 10 (28 fixes, 133-160 in qa-findings). 136: Hunt 10's M45-M60 done as picked (MOM/DAD never fired in battle, nor warm-up words; "word minus its first or last sound" counts as said: CLOCK→LOCK, LEG→EGG, BELT→BELL…; pictures fit their own aspect); ambience: nursery blocks, street leaves, trials gone. Short Shifter visits 22/150 (was 17/153), as the hall now draws MAN more on a fresh store. 137 (Matt's playtest): no letter names in clues or hints (sounds only, every level); games rotate strictly (no side-room game from last episode, door a alternates Charge/Bridge, Shifter never two running: 3 in 7); an action word is never a picture to pick (DRIP stays in play). 138: gift spots drawn per story (magic circle for casters; plate, tool table, charging pad, training spot, blanket, nest, treasure), the word machine's slot clear of the rime, Bluerilla said "Blue-rilla" (a roster `sayName` now respells every line). 139: the rhyme room (door b in episodes without the Shifter, ~1 in 6; ten families, two of them with action-word rhyme cards; -OG/-ED wait for words). 140: Charge says all sounds first, two words a visit (~51-55 s; battle 1 fires 6-8 runes). 141: BattleScene split into sim/volleys/beats, room planning in `rules/rooms.ts`. 142: Hunt 11 (75 fixes, 161-235; overnight memory went critical from parallel browser jobs, conductor 53 caps a hunt at one browser lane plus one checker sweep). Conductor 52.

## Queued and running

- **143_alienware_check** (readonly): is any Alienware/Dell service back, and does free memory still swing on a cycle (the *Memory* flag's OCControl claim is unverified since Matt uninstalled it).
- **144_hunt11_rulings:** M61-M77 as the hunt picked (Matt, session 14); pacing ruled by the planner: Charge ≤ 40 s a visit, the rhyme room ≤ 45 s with her moving ≤ 8 s into a round, battle 1's first choice back under ~26 s.
- **145_hunt11_art** (alongside): candidates for M67's rune pictures (K, U, N, A) and M68's odd gift props, ending at `pick:`.


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

- **`gestureWords`** (`src/rules/charge.ts`, from 133): still counts a charge gesture's words (TAP, EGG) as said in the episode, keeping them out of reading though nothing speaks them since 058. Default (asked session 14): leave.
- **Recordings (Dada Matt):** open `C:\Code\wordwarriors\tools\recorder\phonics-recorder.html?missing` locally (F as FAN, A as CAT; its zip goes to `voice:import`; afterwards empty the page's `MISSING` list). F ("ffff" with no "uh") and A are left (short A is TTS from "Add" until he re-records a steady CAT vowel). Letter names, silly words, sentence prefixes and the 14 `letter_<x>_hides` lines are later lists for the same tool.
- **115's optional calls (default: leave):** Evil Ozymandias's Comet Crash and Evil Elsa's Forever Winter are both icy-blue waves; Evil Elsa has no summon ability; Anna's quest line against Evil Elsa still says "train at my sister's ice castle".
- **More fight styles:** a building contest for builder Matt, a sea race.
- **Shape-Shifter:** MAN is still in ~46% of visits (more words would fix it; Matt ruled none); its islands (DOG-LOG-LEG, NUT-NET-VET, FOX-BOX, LIP-LID) never chain; 130's rotation order can revert in one line if Matt prefers short chains to repeated links.
- **132's own-item refactors** (clear, too big for a sweep; `BattleScene.ts` and `rules/sentences.ts` are 141): split `tests/qa/qa.pw.ts`; a `SceneKey` union; `VoiceBus` → `src/voice/`, a home for `sceneGen`; a relock hook for rooms' `narrate`/`speak` + shared `flow` counter (needs design: changes Entry, Hub, Bedroom); one hard C/K helper (must not fold BELT/BELL); one voice-manifest schema shared by `VoiceBank` and `tools/voice/types.ts`; shared spec page helpers (fake-hidden-tab copies differ); pick notes out of `content/art/prompts.ts`; restructure `docs/systems.md`'s long cells; voice split/fingerprint coupling (`--force` note or a version).
- **Pickers:** face-card picker `scratch/art_alts_113_faces.json` (if still on disk).

## Pending fixes

Each item names the checkpoint it is due from; due items are top-level bullets that say "due" (the digest copies only those). Conductor findings never go here: only in `C:\Code\claude-conductor\planner-notes.md` *For HANDOFF Open*.

- **Planner habit, due:** on **review next** / **check**, always re-stage `inbox.md` first.
- **Planner habit, due:** an art or candidate prompt ends at `pick:`; promotion rides a later prompt.
- **Session 13 pipeline review** (2026-10-23; due from checkpoint #3848): the 5 h blocked pause (fixed by conductor 48 and **pause R**), slow request receipts (conductor 50), session-start extra calls (conductor 47), the watch footer warnings (50) are done; one habit below.
- **Planner habit, due (session 13):** a bug hunt item gets `ultracode: true` (the vocab's rule; 125 and 129 went without). A `state.md` premise is checked against the repo before it goes in a prompt (118's "Matt says" table had moved long before). Stage `review.md` only after the `review:` signal's receipt exists (missed once, read a stale bundle).

- **Planner habit, due (session 14 pipeline review; due from checkpoint #3859):** before saying a picker waits on Matt, stage its `picks\<name>.choices.json` (134's were saved hours before the planner asked twice). Stage a fresh write's receipts in their own call after the write's result, re-staging once on a miss: one missing receipt fails the whole stage call. Never stage the inbox to confirm a queue write; the receipt says it.

## Flags

- **Auto-approve (Matt, 2026-10-22):** every item the planner drafts goes straight to `queue\`; Matt stops what he doesn't want.
- **Memory:** never start the daemon as a Claude Code background command (it dies with that session). Alienware's `OCControl.Service` swings free RAM by ~10 GiB every ~3 min; conductor pauses launches under pressure.
- **Art:** `art:gen` / `art:alts` / `art:pick` in the README; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used. Small art flaws a report notes in passing are fine; don't raise them (Matt).
- **Questions (Matt):** `ask_default_minutes` stays 10; defaults stand when Matt doesn't see a question, and he corrects after. Don't raise timed-out defaults as problems.
- **Ultracode:** on for bug hunts, cleanups and multi-part items; off for items serial on one machine-saturating resource (full test-suite timing runs).
- **Audits (Matt, 2026-10-20):** the planner adds `audit: true` on its own judgment for a big pass through much-changed code, saying so in the reply.
- **Tests (Matt):** faster over thorough where reasonable; `npm test` plus the browser tests covering the change, full suite only when clearly needed (in the repo's CLAUDE.md).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy; the planner overwrites it from the repo's `tools/recorder/phonics-recorder.html` after every change, uncommitted; Matt commits that repo.
- **Storage policy (Matt, 2026-10-18):** git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals`, `voice-gen`), junctioned and shared into worktrees via conductor.toml / nowhere (rebuildable).
- Auto-push on (`push = true`); `background` globs set; worktrees run `npm ci` at creation.
- **Planner habits:** stage `state.md` fresh before a request and diff the request against it; read the inbox's *Red* before processing a report (conductor can overrule `status: done`); a stranded red branch lands with **land X**; every bridge upload goes to a fresh workspace path, never edited after; `expectedMtimeMs` only when replacing an existing file; stage all of a write's receipts in one call and re-stage the same set once on a miss (request receipts can take ~5 s); once a conductor prompt is called ready, additions are a line Matt pastes into its session; to stop and restart work, **pause R** / **resume R**, never a tell asking an item to wait; after a critical tell, check its receipt says delivered.

## Conductor

- Reviewed through 52 (planner.md holds the common path; planner-start.md retired; marker in `planner-notes.md`; unreviewed conductor reports now show in the inbox); live behaviour is in `planner.md` and conductor's HANDOFF *Status*. Still to watch: the first real **pause R** (proven only with the fake executor) and the first real `alongside` use.
