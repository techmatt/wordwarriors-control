# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.2)

- v0.2 plays end to end: bedroom wake-up (Dada Matt, good/bad news, EvilRilla's overlay) → hub (Elsa teaches ICE) → two sentence rooms → battle 1 (fetched items used; walk-onto word pads for move choices) → retreat to hub, attic counter sentence (EVILRILLA IS SCARED OF MICE) → battle 2 → victory recap. Defaults Julia + Elsa vs EvilRilla (`EPISODE_DEFAULTS`); pick screens, v0.1 prep games, alarm and camp parked.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: doors that aren't usable yet aren't drawn (finished side doors stay, with prize badge); a wrong move pick holds the fight and the partner says "That wasn't ICE, that was HUG! Find ICE!" until she's right; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `wordwarriors/005_art_pipeline_test`: Codex `$imagegen` → `public/art/` pipeline, 6-image test batch + contact sheet (`scratch/art_contact.png`).

## Waiting on Matt

- Playing v0.2.
- Art: Codex CLI is installed and logged in on the box (ChatGPT Plus, no API key); 005 is proving the pipeline. Julia's own character art should come from Matt's description, not a guess.
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds); sentence prefixes and read-backs are the next recordings worth making.

## Flags

- Voice folder is ~42 MB committed (v0.2 added 16.2 MB, 004 another 6 MB); narration is composed per possible friend. More narrators or many more lines need Matt's call.
- Counter word ≠ counter item for the non-default villains (e.g. Smaug: SCARED OF THE CUP, battle 2 uses the Frost Shield); only EvilRilla fits. Reachable only with picks/random villain on.
- Prompts that benefit get "Use ultracode." in their text (Matt, 2026-10-18); a mid-run `tell:` delivers the words but it is unconfirmed that it switches the mode.

## Parked for the next wordwarriors prompt

- Worktree test runs keep attaching to the main checkout's dev server on 5174 (the `game` run target) through Playwright's `reuseExistingServer`; make tests use their own port by default instead of a README workaround.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
