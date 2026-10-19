# wordwarriors — state

Status, plan and flags. Changed only through conductor requests. Design lives in `design.md`.

## Repos

- `wordwarriors`: ../wordwarriors (game code). Run target `game` (port 5174). Voice build needs `uv` on PATH (Python edge-tts via `uvx`; the npm port is refused).

## Where it stands (v0.2)

- v0.2 plays end to end: bedroom wake-up (Dada Matt, good/bad news, EvilRilla's overlay) → hub (Elsa teaches ICE) → two sentence rooms → battle 1 (fetched items used; walk-onto word pads for move choices) → retreat to hub, attic counter sentence (EVILRILLA IS SCARED OF MICE) → battle 2 → victory recap. Defaults Julia + Elsa vs EvilRilla (`EPISODE_DEFAULTS`); pick screens, v0.1 prep games, alarm and camp parked.
- Sentences are read by the phonics voice as a prefix clip plus the key word's own clip, so no line can leak a key word and Matt's recordings can replace them; the read-back may sound choppy.
- Julia's first play (2026-10-18) fixed by 004: doors that aren't usable yet aren't drawn (finished side doors stay, with prize badge); a wrong move pick holds the fight and the partner says "That wasn't ICE, that was HUG! Find ICE!" until she's right; the read pass speaks each word as it lights (key word silent).

## Queued and running

- `011_apply_art_picks`: promotes Matt's 7 picks from `art_alts_009` (Ellie ×3, Rilla footprint, bedroom, Anna good + face), keeps the other 6 current and reverts their 009 text; Anna's look split so good (redesign) and evil (old) each match.
- `012_julia_chef`: new id `char_julia_chef` (Julia as a chef, for a future scenario; not used in any scene yet); 3 candidates + manifest, best promoted, sheet opened in Explorer.

## Waiting on Matt

- Art: `npm run art:gen -- <ids…>` draws with Codex's image tool on Matt's ChatGPT Plus login (prompts in `content/art/prompts.ts`; `--reprocess` re-cuts from originals for free; `--sheet` rebuilds the contact sheet). All 183 art ids are real art (006), palette-quantized; `public/art` is 15 MB. ~35 s per image, three streams in parallel; ~0.3% of the 5-hour window per image. Studio redesigns: Elsa a white-and-gold winter queen, Evil Elsa a silver-pixie frost witch, Anna a copper curly bob in moss green, Jasmine short black curls in coral and saffron. The family (Julia in a rainbow twirl dress, Ellie, Dada Matt the builder, Dada Jason the chef) is drawn from Matt's photos (007): crops attached via `REFS` in `content/art/prompts.ts`, photos only in git-ignored `art-originals/refs/`.
- Voice recordings: Matt will do them at some point, not immediately.
- Letter-sound placeholders: only "Mmm" kept its doubling; l/n/r/v/z are Luh/Nuh/Err/Vuh/Zuh. Real clips via `npm run voice:clip` (26 sounds); sentence prefixes and read-backs are the next recordings worth making.

## Conductor (hand-pasted)

- 12a (optional "cleanup pending" wording): paste or skip.
- 13 picker shipped: `pick:` opens a manifest in the browser; choices land in `picks/<name>.choices.json`, and the planner carries them into the next prompt.

## Flags

- Counter sentences now name the battle-2 item for all 15 villains (009; table in the repo's `docs/content.md`, guarded by a test). The parked Spell the Spell `counter.words` no longer match: fix if it's unparked.
- 009 left 1 audit note (the audit test run); a **cleanup wordwarriors** would use it.

- Storage policy (Matt, 2026-10-18): one home per file — git (source, data, recordings, game-sized art) / Drive `C:\Code\gdrive-sync\wordwarriors\` (`art-originals` incl. family photos, `voice-gen` = generated edge-tts audio + manifest), junctioned into the main checkout and shared into worktrees via conductor.toml (`art-originals`, `scratch`, `public/voice-gen`) / nowhere (rebuildable). A worktree build that changes a line's text overwrites the shared mp3 before merge.
- Generated voice (~42 MB) left git in 008; ~50 MB of old voice remains in git history.; narration is composed per possible friend. More narrators or many more lines need Matt's call.
- Counter word ≠ counter item for the non-default villains (e.g. Smaug: SCARED OF THE CUP, battle 2 uses the Frost Shield); only EvilRilla fits. Reachable only with picks/random villain on.
- Heavy items get `ultracode: true` front-matter (Matt, 2026-10-18); it is launch-only, a mid-run `tell:` does nothing.

## Open questions (not blocking)

- Who records the real letter-sound clips (the audit recommends Matt's own voice).
