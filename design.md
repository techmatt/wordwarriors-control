# Word Warriors — design

Learn-to-read game for Julia (4; knows letter names, not letter sounds; comfortable with an Xbox 360 pad and Stardew-style walking; hunt-and-peck on a keyboard). Inspired by Reader Rabbit: minigames earn a spectacle. Here the spectacle is a mock battle between characters she likes. She loves Stardew's room exploration, and her own stories usually start with her being woken up in bed.

## Episode loop (~10–15 min)

1. **Bedroom.** Julia wakes up. Dada Matt (or the helper) wakes her: "Good news, Julia! <Helper> is here to play! Bad news, <Villain> is coming, and he's going to <threat>!" The bedroom is cluttered with cool objects that react when she presses green on them; no reading there. The bedroom comes in variants, and the villain overlays the house's mood (evil Elsa freezes it white; EvilRilla leaves footprints and cracks).
2. **Hub.** A small, slightly modular main house. The helper is there and teaches Julia a spell, which becomes one of her battle move words. Two side-room doors lead off it. A door that isn't usable yet is not shown at all (the front door appears only when it's time to leave).
3. **Two side rooms:** a sentence game each. What she fetches shows up in the battle.
4. **Battle part 1:** the heroes lose to the villain's over-the-top ultimate and retreat. Scripted; never framed as her failure.
5. **Back in the hub:** one more sentence game fetches the counter.
6. **Battle part 2:** the counter beats the ultimate; the heroes win.

Room exploration stays short. Testing defaults: Julia is always the one woken; the helper is good Elsa; the villain is EvilRilla (a giant gorilla robot). Normally they'll be a random good/bad pair. No fail states: wrong answers get a gentle retry, no penalty. Outfits remain usable as a secondary reward.

## The sentence game (the one game for now)

Modelled on how Matt reads with Julia: sentences like JULIA LOVES SPAGHETTI, sounded out or recognised one at a time. All text is UPPER CASE.

- A sentence, e.g. EVILRILLA IS SCARED OF MICE. The last word is the key word and is never spoken until she answers.
- Pass 1: voiced karaoke highlight, word by word; at the key word, silence and a pulse.
- Pass 2: each green press steps the highlight one word and speaks it, except the key word, which stays silent. The hint says a frame word, and only sounds out the key word letter by letter.
- She walks to the object the key word names (one of 3) and presses green; then the full sentence is read and the item goes into her bag.
- Sentences come from a few repeating frames so the little words become sight words; a frame she knows well skips pass 1.

Variants for later: picture-swap (a picture in the sentence, find the written word), yes/no doors (DADA MATT IS A BANANA), do-what-it-says (JUMP ON THE BED), a sentence wall in the bedroom. The v0.1 games (sound → letter, blend path, word → picture, spell the spell) are parked, not deleted.

## Reading and speech

- Everything is voiced except the word she must read. That word is spoken only after she answers, as confirmation. Letter SOUNDS (not names) are voiced as teaching. A hint may sound out letters one by one but never blends the word.
- Selection is always walking to a place and pressing green, never coloured buttons.
- Battle choices: mid-battle, two or three move words (e.g. FIRE / ICE / ZAP) appear as places in the arena. The partner says which to pick and she walks to the written word. A wrong pick fires nothing: the fight stays paused and the partner says what she picked and what to find ("That wasn't ICE, that was HUG! Find ICE!") until she gets it; the right pick fires a supercharged version.
- Every spoken line is data with an id. edge-tts placeholders now; Adobe (Firefly) voices later via Seraphina's recorded-clip override loop.
- Letter sounds: edge-tts cannot say unvoiced consonants and SSML is impossible, so placeholders by sound class; real phoneme clips later (likely Matt-recorded, ~26–44 clips, one sitting). Each sound is its own line id.
- Narrator: instructions are spoken by the episode's helper, else Dada Matt. Interjections ("Ha!") are SFX, not voice lines.
- Progress is tracked per letter sound, per word and per sentence frame; games lean toward her shaky items. A simple parent screen shows it.
- The repo's `CLAUDE.md` owns the full speech and reading-target rules.

## Movement

Stardew-style walking. Her character is the cursor: answers are places in the room she walks to and presses green on. The character sprite gets only light bob and squash/scale motion.

## Battles

Magicka-style free simulation, not a scripted director. Every fighter moves in their own style and uses abilities on their own cooldowns, each with a taunt: summons on both sides, spells (e.g. polymorph), warriors twirling through the crowd, giants that barely move, dodgers with afterimages. Colorful, overdone particles; teamwork moves. Health bars are cosmetic and steered, so the outcome is fixed: part 1 ends with the villain's ultimate, part 2 with the counter and the heroes' win. Fetched items appear in the fight. Characters, abilities, ultimates, counters and vocab are data.

Characters (each has good and evil versions): Julia, Seraphina (a girl who keeps dragons), Dada Matt, Dada Jason, Jasmine, Elsa, Anna, Ozymandias, Jörmungandr, Smaug, Scar (a robot), Moriarty, Bavmorda, EvilRilla (a giant gorilla robot); more welcome.

## Art

AI art generated by Matt in ChatGPT's image model from prompts the planner writes: one shared style block plus a prompt per asset. Simple sprites, no frame animation; a good and an evil image per character; bedroom, hub and side rooms with their objects; villain overlays; arena backgrounds; props, fetchable items and counter items. Studio-owned characters are written as distinct archetype proxies, not lookalikes.

## Tech

Browser game: Phaser ^3.90 (not 4) + TypeScript + Vite + Playwright, dev port 5174. Plan of record for reuse from `C:\Code\seraphinas\seraphinas-secret` is the 001 audit (gamepad Controls, voice pipeline, WordRibbon, SFX, juice patterns, test harness lessons). Placeholder PNGs (name cards) until AI art; `docs/art.md` in the repo lists every asset id for writing image prompts.
