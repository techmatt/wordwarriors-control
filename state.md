# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.2)

- v0.2 plays end to end: bedroom wake-up (Dada Matt, good/bad news, EvilRilla's overlay) → hub (Elsa teaches ICE) → two sentence rooms → battle 1 (fetched items used; walk-onto word pads for move choices) → retreat to hub, attic counter sentence (EVILRILLA IS SCARED OF MICE) → battle 2 → victory recap. Defaults Julia + Elsa vs EvilRilla (`EPISODE_DEFAULTS`); pick screens, v0.1 prep games, alarm and camp parked.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Not yet heard or played by anyone.

## Queued and running

nothing

## Waiting on Matt

- Playing v0.2.
- Art pipeline: proposed route is Codex CLI `$imagegen` on his ChatGPT Plus login (`codex exec`, headless; one-time install + `codex login` on the box), executor batches from `docs/art.md`, contact sheet, Matt names rejects. Fallbacks: paid OpenAI image API, then computer use.
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds); sentence prefixes and read-backs are the next recordings worth making.

## Flags

- Voice folder is ~36 MB committed (v0.2 added 16.2 MB of audio); narration is composed per possible friend. More narrators or many more lines need Matt's call.
- Counter word ≠ counter item for the non-default villains (e.g. Smaug: SCARED OF THE CUP, battle 2 uses the Frost Shield); only EvilRilla fits. Reachable only with picks/random villain on.
- Prompts that benefit get "Use ultracode." in their text (Matt, 2026-10-18); a mid-run `tell:` delivers the words but it is unconfirmed that it switches the mode.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
