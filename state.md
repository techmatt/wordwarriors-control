# wordwarriors — state

Status, plan, open items and flags; the wavefront, not a history (trimmed session 16). Changed only through conductor requests. Design: `design.md`. How the game works: the repo's docs; Matt's game rulings: the repo's `docs/rulings.md` (131) (`docs/episode.md`, `docs/systems.md`, `docs/content.md`, `docs/qa-findings.md`, README, CLAUDE.md). Past items: their reports and git history.

Every item for Matt sits in exactly one place. **Waiting on Matt**: what queued or next work is blocked on, raised every session start. **Open questions**: decisions for upcoming work, asked once, then to **Paged** with the planner's default. **Paged**: raised only by Matt, or when a prompt already touching that code can carry it.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5240 since conductor 119, Nov 14). Voice build needs `uv` on PATH.

## Where it stands (session 18 closed 2026-11-17 ~10:45pm)

- **The episode:** bedroom wake-up → entry-hall warm-up (sounds only, no letter names) → the quest place's hub (a story scene ending in a gift word, on a spot drawn for that story) → two side rooms (door a alternates Charge, two words a visit, and the Stretchy Bridge; door b the Shape-Shifter in 3 episodes of 7, never two running, else the rhyme room, fetch frames or the word machine; no side-room game repeats from last episode) → battle 1 → retreat and the attic's counter sentence → battle 2 → the reformed villain's sorry → victory scene → recap. Cast (14 allies, good Smaug and good Jörmungandr the newest (194; both dragons sit on both lists, never both sides in one episode); 7 villains, Kronos joining in 195), places, fights (Evil Smaug's story fight in about half his episodes), rooms and words are drawn per episode, with rotation memory.
- **Choice mode** (174): an adult starts it with 3 / blue on the title or Dad's 2 in the bedroom; Julia picks the ally and the villain on big cards, the rest is drawn, her picks stay out of rotation memory and her play counts.
- **Words:** about 226 live words, all with their own art. Added this round: FROST POND SAND FANG HELMET GOBLIN; CAPE CAVE FLAME SMOKE ICE; SWORD SHIELD BOW DRAGON CROWN CASTLE WIZARD ROBOT; the stored and `odd` pool and the bedroom toys (DRUM LAMP DUCK BLOCK) are live. UNICORN TEDDY ROCKET BALL are live (189-190). Stored: BUSH only; a word waiting for its own picture is derived (`content/art/waiting.ts`), never a `STORED_WHY` line. X-RAY is live as the one exception to the no-letter-name rule (Matt). Nothing on screen keeps a word out: bedroom toys (Matt, 2026-11-16) and glyphs shown that episode (Matt, 2026-11-17; done in 191; the bed's 🛏️ and Charge's rune-gesture rule are kept). An action word is never a picture she picks. `npm run variety` measures reach and repeats.
- **Code rulings (Matt, 2026-11-16, from 179-180):** cite an item in a code comment only where it records a ruling the code obeys, trimming as files are touched (no sweep); `CharacterSpec.description` stays as a documented optional author's note; `CLAUDE.md` keeps the keyboard and sentence-game laws in place.
- **Heard words (Matt, 2026-11-16):** a word Julia hears in a character's line before reading it is not a problem. Keeping it out of that episode's reads is at most a soft preference, never a reason to drop or avoid a word; existing dialog stays as written.
- **Julia's progress (186):** the save file `C:\Code\gdrive-sync\wordwarriors\progress\progress.json` (Drive-synced, dated daily backups beside it) is the master; the main checkout's dev server mirrors every write to it and a fresh origin restores from it (`WW_DATA_DIR` moves it). It holds 71 episodes (70 merged Nov 16, :5174's 67 with :5240's 3; healthy per 193). A stale tab whose save is refused switches to the file (Matt, 2026-11-17; done in 194: each save names the file stamp its copy builds on, `X-WW-Base`, and the server refuses a stale one). The planner reads her progress there. 177's readout (Nov 16): every pattern 74-87% recent first-try; shaky: short O, -ND/-NT/-ST, N- and R- onsets; long vowels barely met. Her data mixes in Matt's dev play, and F4 auto-answers count as first-try rights.
- **Voice:** Matt's recordings cover every sound the live words use, all passable (Matt, 2026-10-26); F is a whole "fuh" (no hold; blends with F kept off the bridge). `listen.html` plays a word set covering every live sound; the recorder's `?missing` is empty (192 imported Matt's `or`, `er`, `x_name`, `all`).
- **Last session (18, items 177-193):** 177 read Julia's progress (history stranded on :5174 by the port move); 178 turned on the stored pool and added 18 words, 184 the bedroom toys and ROBOT, 188-190 UNICORN TEDDY ROCKET BALL, with art rounds 183/188/189 and promotions 182/187/190; 179-181 and 185 maintenance (cleanup, CLAUDE.md, Hunt 13, disk); 186 the Drive save file (193 audited it); 191 one-step promotion and the glyph ruling; 192 Matt's four recordings.

## Queued and running

- 195_kronos_villain running: a new villain, a looming titan with Chronos time theming; staging defaults taken (counter Clockwork Key / KEY, villain only, ordinary brawl, size 1.8); ends at a picker.

## Maintenance

Triggers: **bug hunt** after a wave of big features or a new surface; **general cleanup** after ~10 feature items or a large rework; **cleanup** when audit notes pile up; **test cleanup** when a full run has grown ~1.5×; **claude.md cleanup** when CLAUDE.md is long or stale; **disk space cleanup** after much generated media; **content cleanup** only when Matt asks; **trim state** past ~25 KB. Bug hunts start from *Categories to hunt (Matt)* at the top of `docs/qa-findings.md`, and resume from the last hunt's *Where the next hunt resumes*.

- Bug hunt: 181 (2026-11-16, Hunt 13; ended early on Matt's word; resume from its *Where the next hunt resumes*).
- General cleanup: 179 (2026-11-16; docs trimmed to ≤15 KB each, current-only).
- Cleanup: 076 (2026-10-21).
- Test cleanup: 105 (2026-10-22, partial; owed: a timed 3-worker run, splitting `episode.spec`'s real-time tests, a 20 ms `WW_POLL_MS` default if two full runs stay green, 4-6 workers if memory allows).
- claude.md cleanup: 180 (2026-11-16; 15.0 KB).
- Disk space cleanup: 185 (2026-11-16; 14.2 → 5.5 GB). Hunt shots are JPEG now (~6x smaller); a hunt's shots thin once its Matt's-calls rows are ruled (`tests/qa/prune.ts`).
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
- **Meryl's two pictures don't match** (172): the rider (fox 6, ranger) and the on-foot pick and face cards (foot 3, star hem) differ in skin tone and robe. Default: leave as picked; the fix is a redraw of one, or face and pick cards cut from fox 6.
- **Meryl's letters are silent** (172): the tiles over her head aren't voiced. Default: leave; voicing the sounds is a small change in `letterRow`.
- **Cosmetic refactors** (132): split `tests/qa/qa.pw.ts`, a home for `sceneGen`, notes out of `content/art/prompts.ts`. No rush; queue only with other work there.
- **M83 rune-gap flake** (179): `charge.spec` M83 (≥240 ms beat) fails on main too, gaps 170-600 ms; may be a real short beat in the volley. Default: a bug-fix item in the rune voicing, not a looser test; queue with other battle work.
- **Small code calls** (179): delete `FLIP_TO_FACE` (always true); VoiceBank warns on a `MANIFEST_VERSION` mismatch; rename `src/scenes/minigames` → `src/scenes/parked` and move `sceneGen.ts` out of `src/fx/` (unblocked by 180). Queue with other work there.
- **Meryl fixes** (181): M91 riders and their letter rows draw above props (she vanishes behind the cook-off cake); M92 her captions read KNIGHTS CAMP (needs `voice:build`, a content item). Queue with other Meryl or battle work.
- **Unify `firstSound` on the sound-based helper** (Matt, 2026-11-16, from 179): bank.ts's spelling-based one goes; SH/TH distractors change. Queue with other work in the bank or rhyme room.
- **Julia outfits beside Smaug / Jörmungandr** (194): most allies give her a matching outfit; these two (like Ellie, Scar, Meryl, Dada Matt) have none. Default: none; a dragon-rider or sea-explorer outfit is a later art round if Matt wants one.

## Pending fixes

Each item names the checkpoint it is due from; due items are top-level bullets that say "due" (the digest copies only those). Conductor findings never go here: only in `C:\Code\claude-conductor\planner-notes.md` *For HANDOFF Open*.

none

## Planner habits

Rules for the planner itself: followed, never listed back to Matt (Matt, 2026-10-25).

- **Bridge and requests:** stage `state.md` fresh before a request and diff the request against it; read the inbox's *Red* before processing a report (conductor can overrule `status: done`); a stranded red branch lands with **land X**; every bridge upload goes to a fresh workspace path, never edited after; `expectedMtimeMs` only when replacing an existing file; request receipts can take ~5 s; once a conductor prompt is called ready, additions are a line Matt pastes into its session; to stop and restart work, **pause R** / **resume R**, never a tell asking an item to wait; after a critical tell, check its receipt says delivered.
- **Sessions 13-14:** re-stage `inbox.md` before **review next** / **check**. A bug hunt item gets `ultracode: true`. An art or candidate prompt ends at `pick:`. Promotion is one `npm run art:pick -- <id> <n|keep> …` plus its commit (191): a parked edit on the next serial item, never an item of its own. Check a `state.md` premise against the repo before it goes in a prompt. Stage `review.md` only after the `review:` signal's receipt exists. Before saying a picker waits, read its `picks\<name>.choices.json`. Stage a write's receipts after the write's result and re-stage the same set once on a miss (one missing receipt fails the whole call); never list a folder or stage the inbox to confirm a write.
- **Session 15:** an investigation prompt for something Matt saw quotes his concrete symptom (the screen, the character, which server) and must reproduce that exact case (148 measured the default cast and missed Jasmine; 150 redid it). A question Matt pastes with no other context: answer it with the planner's best take as the first call (152's answer landed 18 s after its default).
- **Session 18:** check an item is running (inbox *Now*) before a `tell:`; one finished gets a follow-up or a parked edit. A prompt names only paths conductor lets an item write (its worktree and the Drive home `C:\Code\gdrive-sync\wordwarriors`); anything else goes through the planner or Matt. Every bridge commit goes from a fresh `/mnt/user-data/outputs/` path, never one already committed: 184's rewrite arrived as stale bytes (conductor 128), and a receipt's change list (`rewritten: … (needs_pick … added; body +N −M)`) or `identical bytes` shows whether an edit landed. Write a prompt from the goal and Matt's rulings, never from an executor's step list or `carry:` checklist (190 copied 189's and was overbuilt).

## Flags

- **Auto-approve (Matt, 2026-10-22):** every item the planner drafts goes straight to `queue\`; Matt stops what he doesn't want.
- **Memory:** never start the daemon as a Claude Code background command (it dies with that session). Alienware's OCControl/AWCC is gone and memory no longer swings (143, 2026-10-24); the Dell/Alienware Update stack is still installed and could reinstall it (admin removal steps in 143's report). Conductor pauses launches under pressure.
- **Art:** `art:gen` / `art:alts` / `art:pick` in the README; an image costs ~0.25–1% of the 5-hour Codex window, so big art items say what they used. Small art flaws a report notes in passing are fine; don't raise them (Matt).
- **Questions (Matt):** `ask_default_minutes` stays 10; defaults stand when Matt doesn't see a question, and he corrects after. Don't raise timed-out defaults as problems. A question pasted with no context: the planner answers it with its best take.
- **Pauses (Matt, 2026-10-25):** the journey map's 2.6 s, part 1's VS cards (2.3 s) and the hub-to-room ~1.4 s are fine as they are.
- **Ultracode:** on for bug hunts, cleanups and multi-part items; off for items serial on one machine-saturating resource (full test-suite timing runs).
- **Audits (Matt, 2026-10-20):** the planner adds `audit: true` on its own judgment for a big pass through much-changed code, saying so in the reply.
- **Tests (Matt):** faster over thorough where reasonable; `npm test` plus the browser tests covering the change, full suite only when clearly needed (in the repo's CLAUDE.md).
- **Live recorder (Matt, 2026-10-20):** `C:\Code\techmatt.github.io\phonics-recorder.html` is the live hosted copy; since 172 the repo's tools copy it there whenever they rewrite it (`syncHosted`), uncommitted; Matt commits that repo. `?only=<sounds>` gives any targeted set.
- **Storage policy (Matt, 2026-10-18):** git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals`, `voice-gen`), junctioned and shared into worktrees via conductor.toml / nowhere (rebuildable).
- Auto-push on (`push = true`); `background` globs set; worktrees run `npm ci` at creation.

## Conductor

- Reviewed through 131 (marker in `planner-notes.md`). Live behaviour is in `planner.md` and conductor's HANDOFF *Status*. Still to watch: a bug hunt's memory line against Task Manager, and the first real **pause R**.
