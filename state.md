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

- 080_bug_hunt_lenses running (drawn from the backlog 12:43pm; hunt to ~3:43pm). Everything through 079 reviewed.
- 083_faster_tests_2 next (ultracode: voice skip, split real-time episode, teleport hook, short battle mode, one part per fight style, rope-pull `padPlace` fix). Everything through 082 reviewed (the victory recap advances only on Dad's 2, cue "DAD: PRESS 2 TO PLAY AGAIN"; M18 sorries reworded; M19 captions from `lines.json` when the manifest fails). `background` globs set (session 9). Conductor through 39 and cleanup 2026-10-21 reviewed; 40 (autopilot switch, header, message boxes) written. Auto-push on for wordwarriors (`push = true`, Matt 2026-10-21; repos are public, Matt knows): conductor pushes `main` after each merge and at closeout.

## Maintenance

The planner checks this at every session start and recommends what is due, with the reason (Matt approves by saying the phrase). Rough triggers: **bug hunt** after a wave of big features or a new surface; **general cleanup** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test cleanup** when a full run has grown ~1.5× since the last one; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space audit** when art/voice output has grown a lot.

- **Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`** (059): American spelling, nothing covering a target, no letter-matching giveaways, pictures a 4-year-old recognizes, complete natural sentences, words that fit their moment, snappy pacing plus missing voice lines (062). The checker automates `not-american`, `giveaway`, `clipped-line`, `slow-room`, `target-covered`.
- Bug hunt: 080 (2026-10-21; partial at Matt's word after round 1 of 3 h: reload, tab/focus, resize, slow/failing network, every URL flag and dev key, grown-ups page and dad lock all run, `QA_SET=lenses` checker batch; 7 fixes (qa-findings 77-83, Hunt 3), M18/M19 raised in session 9; never run: many episodes back to back at real speed, battle polish leftovers, `npm run shots`); before it 069, 039.. General cleanup: 068 (2026-10-21, as general audit; dead code out, shared helpers, BattleScene and Episode split into `battle/hud.ts`, `battle/moveChoice.ts`, `episode/cast.ts`, `episode/plans.ts`; 18 stale doc claims from 067 fixed; 8 deferred calls raised in session 8). Cleanup: 076 (2026-10-21; 067's notes used up; spread seeds in unit loops, `withDifficulty`, shared ramp clamp/step, legacy store fields into `recent`, Episode.ts state/draws split into `episode/state.ts` and `draws.ts`, `bridgeTier`→`bridgeEase`, `BRIDGE_WORDS`→`BRIDGE_PICTURES`; 4 deferred calls raised in session 9); before it 017. Test cleanup: 079 (2026-10-21; suite serves a production build on 3 GPU workers; `npm test` = unit + 3 @smoke ~20 s, `test:browser` ~50 s before a commit, `test:slow` ~10 min, `test:all` ~10 min; `WW_DEV_SERVER=1` for the old dev-server run); before it 061. claude.md cleanup: 077 (2026-10-21; facts checked and fixed, still ~249 lines; the real shrink is moving the "Matt says" table, raised in session 9); before it 050. Disk space audit: 051 (2026-10-20; 15.4 GB of test-shot PNGs freed from `scratch/`; shot runs are ~1 MB a shot, so a big sweep or shot run is the next trigger).

## Waiting on Matt

nothing

## Conductor (hand-pasted)

- **Conductor through 37 is reviewed, plus cleanup 2026-10-21** (session 9). 37: only Matt's acts (app/cli signal, approve, queue or backlog write, answer) unlock a back-to-back full-length draw; `pending` receipts for waiting requests; a bare item number two items share names neither (receipt says `queued as <id>`). Cleanup: docs matched to code, no behaviour change, seven conductor docs at 100% of budget. 36: night shift (`docs/night-shift.md`: 10-min stall checks, readonly watch items, `backlog\<repo>\`, 6 h nightly cap), done-when / adversarial review / `alongside` rules, `general_cleanup` and `test_cleanup` (old names aliases). Its first real nights are worth a look. What is live is in `planner.md` and conductor's HANDOFF *Status*: `alongside`, ask / post-audit, `report_changed`, the run ledger, the bug hunt clock, settled events hidden from the digest, receipts for every planner write (`docs/receipts.md`; stage the receipt, never the inbox), the planner's marker and *Open* lines in `planner-notes.md`. Still for Matt's eye: whether Windows shows conductor's icon after an app restart, and the first real `alongside` use (HANDOFF *Open*).

## Flags

- Memory: never start the daemon as a Claude Code background command (it dies with that session). Alienware's `OCControl.Service` swings free RAM by ~10 GiB every ~3 min; conductor pauses launches under pressure.
- Art: `art:gen` / `art:alts` / `art:pick` and the studio redesigns are in the repo README and `content/art/prompts.ts`; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used.
- **Questions (Matt, 2026-10-21):** `ask_default_minutes` stays 10; Matt often won't see questions and that's fine: defaults stand and he corrects after the fact. Don't raise timed-out defaults as problems.
- **Planner habits (session 9):** stage a receipt in a call of its own (it lands 1–2 s after the write; a stage fails whole if one path is missing) and retry once; always stage `state.md` fresh before building a request from it. Read inbox sections with non-overlapping extracts (overlapping `sed` ranges doubled lines and cost conductor 38 a wild-goose chase).
- **Tests: faster over thorough (Matt, 2026-10-21):** where reasonable, prefer faster tests and lanes to thorough ones; Matt scales coverage up when he notices problems.
- Tests (Matt, 2026-10-20): no full browser suite by default; `npm test` plus the browser tests covering the change (`test:browser` before a commit, 079), full suite only when very clearly needed; misses are fixed later. In the repo's CLAUDE.md (046).
- Worktrees run `npm ci` at creation (`setup` in conductor.toml, Matt 2026-10-19).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy. The planner overwrites it from the repo's `tools/recorder/phonics-recorder.html` after every change, leaving it as an uncommitted file; Matt commits that repo, never an executor or the planner.
- **Conductor prompts start at once (Matt, 2026-10-21):** read `C:\Code\claude-conductor\prompts\ledger.md`'s tail before writing a conductor prompt or saying one has started (`planner.md` *Bridge*, from 32).
- **Bridge uploads (planner, 2026-10-21):** every file sent with `device_commit_files` is written once to a fresh workspace path and never edited after; the bridge sends a path's first contents (a reused or edited path sent stale text: HANDOFF after 31, a "no change" request, and the slimmed `state.md`'s second pass) (it clobbered conductor's HANDOFF after 31, and turned a request into "no change").
- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge (see 017 deferred call 3).
- Art nitpicks (Matt, 2026-10-21): small art flaws a report notes in passing (halos, slight tints) are fine; don't raise or track them.
- Plural key words (CANNOT STAND MICE) may come later as a special case (Matt, 2026-10-18).
- Ruled (Matt, 2026-10-21, 076's deferred calls): Charge has no help ramp (removed in 078); the rune `tier` stays as a documented label; the pick screens' surprise-villain flag is fixed only if the pick screens return.
- **Ruled (Matt, 2026-10-20): audits.** The planner adds `audit: true` on its own judgment (a lot has changed since the last audit or cleanup, and the item is a big pass through much of the code), always saying so in the reply where it does; Matt can drop it. Supersedes "audits only when Matt asks". First use: 067.
- Ruled (Matt, 2026-10-20): a word may use sounds the game doesn't teach yet (she learns plenty outside the game); applied in 058 (`UNTAUGHT_SOUNDS`).
- Ruled (Matt, 2026-10-20): no automatic difficulty; everything plays at base until Matt raises it. All words are in the vocabulary (long ones like OCTOPUS are fine: she'll recognize some); decoding games use short words, recognition roles any word (067).
- Ruled (Matt, 2026-10-20): XRAY stays as X's first word, though it starts with the letter's name.
- Ruled (Matt, 2026-10-20): the entry-hall warm-up is a phonics task, never a listening one: no clue or help says the whole word (062 carries it).
- Ruled (Matt, 2026-10-20): MAT stays a bridge word, though it sounds like "Matt".
- Ruled (Matt, 2026-10-19): "Bough to your queen!" stays.
- Ruled (Matt, 2026-10-19): fight style stays fixed per villain (its identity); word-machine blend/digraph families wait until she reads blends.
- Ruled (Matt, 2026-10-18): keep the named-counter boost (3×, now 6× for the doubled pool, 067); Ellie's sword word stays ZIP; no asleep chef-Julia image for now; voice-manifest hashing deferred until items that change voice run concurrently. Later word-machine modes: flip it, real or silly.

## Pending fixes

Accumulated fixes and pipeline-review items (every pipeline review's agreed items land here). Each item or group names the checkpoint it is due from ("due from checkpoint #N"), never "next checkpoint"; at session start the planner raises every item already due. Everything below is due now (from #1994, session 9 start).

**Conductor**
- **38 done (session 9):** the doubled inbox was the planner's own read (overlapping `sed` ranges print a line twice), not conductor; 38 closed a real temp-file race anyway. Cleanup's calls recorded in HANDOFF.

**Session 8 pipeline review.** Planner habit (said in chat): write a conductor prompt's whole text before saying it's ready, since Matt pastes at once and the ledger only narrows the edit race (33 started within a minute of an edit). Fixed during the session: reused bridge upload paths (fresh-path rule, 32); edits to running conductor prompts (the ledger, 32); the bug hunt stopping early (template clock, 32); a hand-resumed session editing a reviewed report unseen (`report_changed`, 32); `state.md` at 32 KB resent whole on every request (slimmed, 075); an output file edited after its first write uploaded stale (flag: written once).

## Backlog (night shift)

Pre-approved by Matt (2026-10-21), in `backlog\wordwarriors\`: `disk_space_audit` (`bug_hunt_lenses` drawn as 080). General cleanup joins when its trigger is due.

## Open questions

none

## Paged

- **KEY/YOYO as counters (045):** special words are never the counter word (keeps 009's decodable-counter rule); default keep.

- **Recordings (Dada Matt):** only F is left (card 2, "ffff" with no "uh"); then `voice:import`. Letter names, silly words and sentence prefixes are later lists for the same tool.
- **Evil Anna redraw:** still the old copper-curl design; redraw when Anna joins the active cast.
- **More fight styles:** a building contest for builder Matt, a sea race.
