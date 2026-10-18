# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands

- v0.1 plays end to end (picks → alarm → two rotating prep games → battle 1 → camp + Spell the Spell → battle 2 → victory). Matt played it and gave his change list on 2026-10-18; it reshapes the episode (see `design.md`).
- v0.2 direction (Matt, 2026-10-18): wake-up in a bedroom → small hub house with the helper → two sentence-game side rooms → battle 1 loss → counter sentence game in the hub → battle 2 win. Testing defaults: Julia woken, good Elsa helper, EvilRilla villain. One game type for now (the sentence game); the v0.1 games are parked. All text upper case; selection is walking everywhere, the battle move choice included.

## Queued and running

- `wordwarriors/003_house_and_sentence_game`: builds v0.2 as above.

## Waiting on Matt

- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds).
- Real art into `public/art/<id>.png`; ids in the repo's `docs/art.md` (source for the AI image prompts the planner writes).

## Flags

- Voice is ~20 MB committed; narration is composed per possible friend (1,684 lines, ~1.4 MB per extra narrator). More narrators or many more lines need Matt's call.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
