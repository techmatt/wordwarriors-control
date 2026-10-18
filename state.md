# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.2)

- v0.2 plays end to end: bedroom wake-up (Dada Matt, good/bad news, EvilRilla's overlay) → hub (Elsa teaches ICE) → two sentence rooms → battle 1 (fetched items used; walk-onto word pads for move choices) → retreat to hub, attic counter sentence (EVILRILLA IS SCARED OF MICE) → battle 2 → victory recap. Defaults Julia + Elsa vs EvilRilla (`EPISODE_DEFAULTS`); pick screens, v0.1 prep games, alarm and camp parked.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: doors that aren't usable yet aren't drawn (finished side doors stay, with prize badge); a wrong move pick holds the fight and the partner says "That wasn't ICE, that was HUG! Find ICE!" until she's right; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `wordwarriors/006_art_batch_1`: real art for the default episode (done: 68 ids, no refusals), then the rest in order. PNGs palette-quantized with `sharp`; stops committing new art at 20 MB for the batch (an unanswered ask's default) until Matt OKs more.

## Waiting on Matt

- Playing v0.2.
- Art: `npm run art:gen -- <ids…>` draws with Codex's image tool on Matt's ChatGPT Plus login (prompts in `content/art/prompts.ts`; `--reprocess` re-cuts from originals for free; `--sheet` rebuilds the contact sheet). ~40 s per image; 68+ images used ~15% of a 5-hour window. Elsa is a white-and-gold winter queen (the film-like designs were refused). Julia's art is the generic placeholder description until Matt describes her.
- Whether to commit art past 20 MB (all ~190 ids quantized ≈ 25 MB).
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds); sentence prefixes and read-backs are the next recordings worth making.

## Flags

- `art-originals/` and `scratch/` are shared untracked folders across worktrees (conductor.toml), so full-res originals and contact sheets survive cleanup.
- Voice folder is ~42 MB committed (v0.2 added 16.2 MB, 004 another 6 MB); narration is composed per possible friend. More narrators or many more lines need Matt's call.
- Counter word ≠ counter item for the non-default villains (e.g. Smaug: SCARED OF THE CUP, battle 2 uses the Frost Shield); only EvilRilla fits. Reachable only with picks/random villain on.
- Prompts that benefit get "Use ultracode." in their text (Matt, 2026-10-18); a mid-run `tell:` delivers the words but it is unconfirmed that it switches the mode.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
