# Word Warriors — design

Learn-to-read game for Julia (4; knows letter names, not letter sounds; comfortable with an Xbox 360 pad and Stardew-style walking; hunt-and-peck on a keyboard). Inspired by Reader Rabbit: minigames earn a spectacle. Here the spectacle is a mock battle between characters she likes. She loves Stardew's room exploration, and her own stories usually start with her being woken up in bed.

## Episode loop (~10–15 min)

1. **Bedroom.** Julia wakes up. Dada Matt (or the helper) wakes her: "Good news, Julia! <Helper> is here to play! Bad news, <Villain> is coming, and he's going to <threat>!" The bedroom is cluttered with cool objects that react when she presses green on them; no reading there. The bedroom comes in variants, and the villain overlays the house's mood (evil Elsa freezes it white; EvilRilla leaves footprints and cracks).
2. **Hub.** A small, slightly modular main house. The helper is there and, in a short story scene that fits them (a spell, a recipe, a gadget, a program, a toy…), gives Julia a word for the fight. Two side-room doors lead off it. A door that isn't usable yet is not shown at all (the front door appears only when it's time to leave).
3. **Two side rooms:** a sentence game each. What she fetches shows up in the battle.
4. **Battle part 1:** the heroes lose to the villain's over-the-top ultimate and retreat. Scripted; never framed as her failure.
5. **Back in the hub:** one more sentence game fetches the counter.
6. **Battle part 2:** the counter (a random thing; see below) beats the ultimate; the heroes win.

Room exploration stays short. Testing defaults: Julia is always the one woken; the helper is Ellie, who fights with summoned spinning silver swords; the villain is Evil Tiamat (a giant purple dragon). Matt changed these on 2026-10-18; they were Elsa and EvilRilla. Normally they'll be a random good/bad pair. No fail states: wrong answers get a gentle retry, no penalty. Outfits remain usable as a secondary reward.

## The sentence game (the one game for now)

Modelled on how Matt reads with Julia: sentences like JULIA LOVES SPAGHETTI, sounded out or recognised one at a time. All text is UPPER CASE.

- A sentence, e.g. EVILRILLA IS SCARED OF MICE. The last word is the key word and is never spoken until she answers.
- Pass 1: voiced karaoke highlight, word by word; at the key word, silence and a pulse.
- Pass 2: each green press steps the highlight one word and speaks it, except the key word, which stays silent. The hint says a frame word, and only sounds out the key word letter by letter.
- She walks to the object the key word names (one of 3) and presses green; then the full sentence is read and the item goes into her bag.
- Sentences come from a few repeating frames so the little words become sight words; a frame she knows well skips pass 1. The counter sentence has several frames (IS SCARED OF, RUNS FROM, HATES…), not one.
- Key words are drawn without replacement from a per-player bag (no repeats until it has gone round, never twice in one episode), leaning toward her shaky words.
- A villain's counter is a random pictured word each episode and needn't make sense (EvilRilla can be beaten by a mop); battle 2 shows that thing beating the villain.

Variants for later: picture-swap (a picture in the sentence, find the written word), yes/no doors (DADA MATT IS A BANANA), do-what-it-says (JUMP ON THE BED), a sentence wall in the bedroom. The v0.1 games (sound → letter, blend path, word → picture, spell the spell) are parked, not deleted.

## Reading and speech

- Everything is voiced except the word she must read. That word is spoken only after she answers, as confirmation. Letter SOUNDS (not names) are voiced as teaching. A hint may sound out letters one by one but never blends the word.
- Selection is always walking to a place and pressing green, never coloured buttons.
- **Phonics first (Matt, 2026-10-19):** what she reads is chosen for her phonics, never limited by who is on screen; err toward phonetic diversity. One tagged word bank (level 1 CVC, 2 blends, 3 digraphs) feeds every pool, weighted by shakiness and by coverage of vowels, onsets and patterns. Distractors differ in the first sound early on, then share onset or rime as a word firms up.
- **Word magic:** reading a word casts it. Any action word can be a battle pad, and her hero fires that word's own effect.
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

Characters (each has good and evil versions): Julia (rainbow twirl dress), Ellie (her toddler sister), Seraphina (a girl who keeps dragons), Dada Matt (beefy builder with a hammer), Dada Jason (a chef), Jasmine, Elsa, Anna, Ozymandias, Jörmungandr, Smaug, Scar (a tiny gold robot), Moriarty, Bavmorda, EvilRilla (a giant gorilla robot), Tiamat (a giant purple dragon); more welcome.

## Art

AI art generated by Matt in ChatGPT's image model from prompts the planner writes: one shared style block plus a prompt per asset. Simple sprites, no frame animation; a good and an evil image per character; bedroom, hub and side rooms with their objects; villain overlays; arena backgrounds; props, fetchable items and counter items. Studio-owned characters are written as distinct archetype proxies, not lookalikes. The family characters are drawn from Matt's photos, which never enter the tracked tree.

## Tech

Browser game: Phaser ^3.90 (not 4) + TypeScript + Vite + Playwright, dev port 5174. Plan of record for reuse from `C:\Code\seraphinas\seraphinas-secret` is the 001 audit (gamepad Controls, voice pipeline, WordRibbon, SFX, juice patterns, test harness lessons). Placeholder PNGs (name cards) until AI art; `docs/art.md` in the repo lists every asset id for writing image prompts.

## Casting, quests and endings (Matt, 2026-10-18)

- Each episode casts at random: the villain from every evil roster version and evil form (no repeat of the last one); the ally from the good roster, sometimes a dad. The primary dad (wakes Julia, narrates when needed) is Dada Matt 60% / Dada Jason 40%; half the time the other dad is also in the bedroom. Dada Matt's forms: builder, weightlifter, programmer/cyberdecker, spell-blade; Dada Jason's: chef, fantasy warrior, warlock. Julia's form follows a matching ally form (chef Julia with chef Jason).
- Each ally has a quest: they take Julia to their own place to train (weightlifter Matt's secret forest gym, chef Jason's secret kitchen…), set up with an imaginative line. The side rooms are set there; their minigames are sampled from a pool (sentence game, word machine, …) independent of the quest.
- Active cast (Matt, 2026-10-18; data, to grow toward almost all pairs): allies Dada Matt, Dada Jason, Scar (a tiny gold robot, just shorter than Julia), Ellie; villains Jörmungandr, Smaug, Bavmorda, Tiamat.
- Fights vary by style per villain: Magicka-style brawls, races, cook-offs, spell-beam clashes, building contests, dance-offs… always over-the-top particles, character moves and teamwork, same reading beats and fixed outcome.
- Before leaving for the quest place, a home warm-up: the ally asks for one of 9 labelled objects by letter names then letter sounds (the whole word only at the easiest ramp level); she finds it; per-word ramp, starting without the word (Matt, 2026-10-19).
- Whoever is speaking is shown by a prominent face-card portrait beside their words.
- After battle 2, a short random victory scene (dessert at the table, a picnic, climbing a mountain…) with everyone, the villain now good, and a few lines, then the recap.

## Phonics games that force the phonics (Matt, 2026-10-20)

The older games can be won from letter names (first-letter matching) or by sweeping through the choices, and she never has to say anything. The new games follow five rules:

- She says sounds aloud and Dad confirms with keyboard `1` (no / help) or `2` (yes). There is no speech recognition. Assistance is normal: she sometimes won't say sounds on request, so a "no", or no answer, makes the game model the sound for her to copy, and it never gets stuck.
- Choices can't be won from the first letter: they share the start and differ later.
- Help fades per item (voiced → on request → none).
- A wrong pick is never punished, but guessing is slower than reading.
- Blending is continuous ("mmmaaat"); words starting with a sound you can hold come before words starting with a stop sound.

The two games:

- **Charge the Spell:** a letter rune; she says its sound, Dad presses 2, and the rune charges a move for the next battle. Each sound has a gesture (Jolly Phonics style). Help fades from sound + gesture, to gesture only, to the rune alone.
- **Stretchy Bridge:** letter stepping stones across a gap. Each sound plays held while she stands on it, so how slowly she slides is how slowly she stretches the word. Then she picks among pictures that share the word's start. At the top level she says the word before the pictures appear.

For beta testing, one of the two is in every episode; long term they are random pool entries. Matt's real letter-sound recordings matter most for the bridge, because the placeholders add "uh" to stop sounds.
