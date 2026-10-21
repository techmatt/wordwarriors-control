# wordwarriors — state

Status, plan, rulings and flags. Changed only through conductor requests. Design lives in `design.md`; how the game works lives in the repo's docs (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/engineering.md`, README, CLAUDE.md).

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: never raised by the planner; only when Matt raises it or a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH.

## Where it stands (v0.9; session 8 closed 2026-10-21 ~10:10am; queue empty)

- **The episode:** bedroom wake-up → entry-hall warm-up → the quest place's hub (a story scene ending in a gift word) → two side rooms → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast, places, fights, rooms and words are drawn per episode, with rotation memory across episodes.
- **This session:** on-demand art loading (065); one `DIFFICULTY` knob at base with all words in play and decoding games capped by length (067); general audit (068); bug hunt 2 with 24 fixes, including voice and art timeouts on the wall clock (069); sign placement, the narrow dialogue box and rewording (071); tooling and docs, with `docs/episode.md` and npm scripts (072); new word pictures, MAT/PAN/ROCK picks promoted (070, 073).
- **Art:** no placeholder pictures left in the game (`art:placeholders` reports 0 after 074). **Voice placeholders:** Matt's F recording (Paged); untaught-sound lines (long vowels, schwa) are TTS.
- **Gesture words (074):** a rune gesture that says a bank word (the /e/ rune's "Tap the egg": TAP, EGG) keeps that word out of later reading only in an episode whose Charge word uses that rune; the Charge word is planned up front so this holds (`gestureWords` in `src/rules/charge.ts`).
- Mechanics live in the repo's docs (075 gave every fact from the old "Where it stands" a home and fixed 4 doc lines the code contradicted).

## Queued and running

- Queue empty; everything through 075 reviewed. Conductor through 33 reviewed.
- Parked for the next wordwarriors prompt: 074 found the unit tests' `seeded(n)` gives nearly the same first draw for seeds 1–200, so loops over `seeded(1..N)` test only a few cases; check every such loop and spread the seeds (074 used `seeded(seed * 104729)`).

## Maintenance

The planner checks this at every session start and recommends what is due, with the reason (Matt approves by saying the phrase). Rough triggers: **bug hunt** after a wave of big features or a new surface; **general audit** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test perf audit** when a full run has grown ~1.5× since the last one; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space audit** when art/voice output has grown a lot.

- **Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`** (059): American spelling, nothing covering a target, no letter-matching giveaways, pictures a 4-year-old recognizes, complete natural sentences, words that fit their moment, snappy pacing plus missing voice lines (062). The checker automates `not-american`, `giveaway`, `clipped-line`, `slow-room`, `target-covered`.
- Bug hunt: 069 (2026-10-21; asked 6 h, ran 1.6 h, stopping because its fixes were in and green: partial under the new clock rules, per its own correction; lenses never run: reloading mid-flow, tab/focus switches and resizing, slow or failing network/disk, many episodes back to back at real speed, every URL and dev flag, the grown-ups page and dad lock across a whole episode; 24 fixes, `QA_SET=new` batch, findings "Hunt 2" in `docs/qa-findings.md`); before it 039. General audit: 068 (2026-10-21; dead code out, shared helpers, BattleScene and Episode split into `battle/hud.ts`, `battle/moveChoice.ts`, `episode/cast.ts`, `episode/plans.ts`; 18 stale doc claims from 067 fixed; 8 deferred calls raised in session 8). Cleanup: 017. Test perf: 061 (2026-10-20; fast lane re-cut, two Playwright workers). claude.md cleanup: 050 (2026-10-20; 235 → 211 lines, history cut, stale facts fixed). Disk space audit: 051 (2026-10-20; 15.4 GB of test-shot PNGs freed from `scratch/`; shot runs are ~1 MB a shot, so a big sweep or shot run is the next trigger).

## Waiting on Matt

nothing

## Conductor (hand-pasted)

- **Conductor through 32 is reviewed** (session 8). What is live is in `planner.md` and conductor's HANDOFF *Status*: `alongside`, ask / post-audit, `report_changed`, the run ledger, the bug hunt clock. Still for Matt's eye: whether Windows shows conductor's icon after an app restart, and the first real `alongside` use (HANDOFF *Open*).

## Flags

- Memory: never start the daemon as a Claude Code background command (it dies with that session). Alienware's `OCControl.Service` swings free RAM by ~10 GiB every ~3 min; conductor pauses launches under pressure.
- Art: `art:gen` / `art:alts` / `art:pick` and the studio redesigns are in the repo README and `content/art/prompts.ts`; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used.
- HANDOFF.md: the planner writes its marker only when the ledger shows no conductor prompt running and the last report is reviewed, from a fresh stage, with `expectedMtimeMs`.
- Tests (Matt, 2026-10-20): no full browser suite by default; fast lane plus the browser tests covering the change, full suite only when very clearly needed; misses are fixed later. In the repo's CLAUDE.md (046).
- Worktrees run `npm ci` at creation (`setup` in conductor.toml, Matt 2026-10-19).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy. The planner overwrites it from the repo's `tools/recorder/phonics-recorder.html` after every change, leaving it as an uncommitted file; Matt commits that repo, never an executor or the planner.
- **Conductor prompts start at once (Matt, 2026-10-21):** read `C:\Code\claude-conductor\prompts\ledger.md`'s tail before writing a conductor prompt, editing HANDOFF, or saying one has started (`planner.md` *Bridge*, from 32).
- **Bridge uploads (planner, 2026-10-21):** every file sent with `device_commit_files` is written once to a fresh workspace path and never edited after; the bridge sends a path's first contents (a reused or edited path sent stale text: HANDOFF after 31, a "no change" request, and the slimmed `state.md`'s second pass) (it clobbered conductor's HANDOFF after 31, and turned a request into "no change").
- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge (see 017 deferred call 3).
- Art nitpicks (Matt, 2026-10-21): small art flaws a report notes in passing (halos, slight tints) are fine; don't raise or track them.
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- **Ruled (Matt, 2026-10-20): audits.** The planner adds `audit: true` on its own judgment (a lot has changed since the last audit or cleanup, and the item is a big pass through much of the code), always saying so in the reply where it does; Matt can drop it. Supersedes "audits only when Matt asks". First use: 067.
- Ruled (Matt, 2026-10-20): a word may use sounds the game doesn't teach yet (she learns plenty outside the game); applied in 058 (`UNTAUGHT_SOUNDS`).
- Ruled (Matt, 2026-10-20): no automatic difficulty; everything plays at base until Matt raises it. All words are in the vocabulary (long ones like OCTOPUS are fine: she'll recognize some); decoding games use short words, recognition roles any word (067).
- Ruled (Matt, 2026-10-20): XRAY stays as X's first word, though it starts with the letter's name.
- Ruled (Matt, 2026-10-20): the entry-hall warm-up is a phonics task, never a listening one: no clue or help says the whole word (062 carries it).
- Ruled (Matt, 2026-10-20): MAT stays a bridge word, though it sounds like "Matt".
- Ruled (Matt, 2026-10-19): "Bough to your queen!" stays.
- Ruled (Matt, 2026-10-19): fight style stays fixed per villain (its identity); word-machine blend/digraph families wait until she reads blends.
- Ruled (Matt, 2026-10-18): keep the named-counter boost (3×, now 6× for the doubled pool, 067); Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Next checkpoint (Matt, 2026-10-20)

Accumulated fixes and pipeline-review items; start at the next checkpoint, not before. Every pipeline review's agreed items land here.

**Conductor**
- **Cleanup conductor is due:** `HANDOFF.md` and `docs/app-panels.md` are at 100% of their size budgets after 33.
- Parked for the next conductor prompt: (1) `planner.md`'s upload rule becomes "every upload is written once to a fresh workspace path and never edited after"; (2) support files a prompt reads never sit in `prompts/` as `NN_name.md` (move `32_bug_hunt_template.md` out), and "run the next prompt" goes by the ledger's `done` lines, so a support file is never taken for an unrun prompt; (3) split `docs/control-folder.md`'s `.conductor/` runtime list when it next grows.
- **Planner never edits conductor's HANDOFF.md:** move the `Last report reviewed by the planner` marker into a file the planner owns (or conductor writes), and route the planner's *Open* additions through a file conductor prompts merge.
- **Signal receipts:** a small receipt per signal or request (its event ids, or the refusal), so the planner stops re-staging the inbox to see a write land (~15 extra reads in session 8).
- **Questions seen while Matt talks to the planner:** 071's ask timed out unseen at 9:06am while Matt was working with the planner. A `planner.md` rule: whenever the planner reads the inbox or a report, it raises open questions first (questions with defaults included).
- **Keep the readonly-prototype pattern:** a readonly prototype item first, then the real build from its findings (055 → 057), for any tool whose approach is uncertain; to conductor's HANDOFF *Open*.

**Session 8 pipeline review.** Planner habit (said in chat): write a conductor prompt's whole text before saying it's ready, since Matt pastes at once and the ledger only narrows the edit race (33 started within a minute of an edit). Fixed during the session: reused bridge upload paths (fresh-path rule, 32); edits to running conductor prompts (the ledger, 32); the bug hunt stopping early (template clock, 32); a hand-resumed session editing a reviewed report unseen (`report_changed`, 32); `state.md` at 32 KB resent whole on every request (slimmed, 075); an output file edited after its first write uploaded stale (flag: written once).

## Open questions

none

## Paged

- **`background` globs** for this repo's conductor.toml (long test commands always backgrounded, never hit the 10-minute cutoff); planner's default `["npm test*", "npm run test*", "npx playwright*"]`. 065's full slow-lane run hit the 10-minute cap.

- **KEY/YOYO as counters (045):** special words are never the counter word (keeps 009's decodable-counter rule); default keep.
- **Dad trail tints (046):** Jason's and Matt's in-game trail/palette tints don't follow their new colours.

- **Recordings (Dada Matt):** only F is left (card 2, "ffff" with no "uh"); then `voice:import`. Letter names, silly words and sentence prefixes are later lists for the same tool.
- **Stale voice audio:** clips for retired line ids (e.g. 071's two rainbow lines) stay in the shared voice folder; `voice:build` has no `--prune` run yet. A disk audit's job.
- **072's configs only listed:** the full shots (~5 + ~16 min), perf and qa runs weren't run after 072 moved them to npm scripts and the GPU; the next bug hunt or shot run exercises them.
- **Evil Anna redraw:** still the old copper-curl design; redraw when Anna joins the active cast.
- **Battle polish leftovers (034, minor):** brief edge contact during combos and mid-dash; a bubble can sit over a taller neighbour; full-screen combo flashes at their peak; the cook-off's tall winning cake can cover a hero.
- **Leftover clipped lines (059):** the "X for everybody!" sorries (rated minor).
- **More fight styles:** a building contest for builder Matt, a sea race.
