# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.1)

- One full episode plays end to end: picks → alarm → two rotating prep games → battle 1 → camp + Spell the Spell → battle 2 → victory recap. Placeholder name cards and edge-tts voices. Grown-ups page: F9, or LB+RB on the title.
- Matt has played it: reasonable for a v0.1. He brings his change list at the next session.

## Queued and running

nothing

## Waiting on Matt

- His v0.1 change list (next session opens with it).
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds).
- Real art into `public/art/<id>.png`; ids in the repo's `docs/art.md` (source for the AI image prompts the planner writes).

## Flags

- Voice is ~20 MB committed; narration is composed per possible friend (1,684 lines, ~1.4 MB per extra narrator). More narrators or many more lines need Matt's call.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
