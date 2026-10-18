# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands

- One full episode plays end to end (picks → alarm → two rotating prep games → battle 1 → camp + Spell the Spell → battle 2 → victory recap), with placeholder name cards and edge-tts. Grown-ups page: F9, or LB+RB on the title.
- Verified headless only: no real pad, nobody has listened yet.

## Queued and running

nothing

## Waiting on Matt

- Play it with a real pad and listen.
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z became Luh/Nuh/Err/Vuh/Zuh (inferred from timing, unheard). Real clips via `npm run voice:clip` (26 letter sounds).
- Real art drops into `public/art/<id>.png`; ids in the repo's `docs/art.md` (source for the AI image prompts).

## Flags

- Voice is ~20 MB committed; narration is composed per possible friend (1,684 lines, ~1.4 MB per extra narrator). More narrators or many more lines need Matt's call.

## Open questions

none blocking
