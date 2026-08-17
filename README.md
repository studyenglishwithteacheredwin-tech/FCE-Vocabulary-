# Elena's Word Lab

A running vocabulary and spelling tracker for Elena's FCE (Cambridge B2 First) course.
One self-contained HTML file. No build step, no dependencies, no server, works offline.

**Live:** enable GitHub Pages (Settings → Pages → Deploy from branch → `main` / root), then open
`https://<user>.github.io/<repo>/` on the tablet and **Add to Home Screen** so it opens like an app.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app: word data, drills, progress engine, styles. Edit this to change words. |
| `words.json` | The same word list as data only — handy for diffing, or for pasting a new week into the app's **More → Add words** box. |

## Adding a new week

Two ways.

**A — regenerate the file (preferred).** Photograph the notebook pages, send them to Claude in the
*FCE Vocabulary – Elena* project and ask it to add the week. You get an updated `index.html` back; commit it.
Elena's scores are **not** stored in the file (they live in the tablet's browser), so replacing the file never
resets her progress.

**B — edit by hand.** Open `index.html`, find the `const WORDS = [` block near the top of the `<script>`
and copy an existing entry:

```js
{id:'p19',cat:'pv1',week:'Week 2 · Unit 2',term:'give up',pos:'phrasal verb',
 en:'stop trying',vi:'bỏ cuộc',focus:['up'],
 ex:'Never give up before the exam.',
 note:'Spelling tip shown after every answer.',
 flag:{src:'elena',wrote:'give of',right:'give up',text:'What went wrong and why.'}}
```

Fields:

- `id` — unique, any short string. `cat` — `nations` | `pv1` | `look` | `person` | `school`.
- `term` — the string she must produce. `alt` — array of other spellings to accept.
- `focus` — the error-prone letter chunks; used for highlighting and for the *Fill the gaps* drill.
- `flag.src` — **`elena`** = she copied it down wrongly (drilled in *Beat your traps*);
  **`teacher`** = the note in the notebook is itself wrong (listed under *Slips* to raise with the teacher, never drilled).
- Countries also take `nat` (nationality), `natFocus`, `lang`.
- Long words can take a hand-checked split in the `PARTS` map (`'calculator':'cal|cu|la|tor'`); anything
  not listed is syllabified by rule.

Test tracking lives in the `TESTED` / `TEST_GOT` arrays at the end of the data block — edit those after each class test.

## What's in it

77 words from Week 1 (Unit 1 *New Worlds*): countries/nationalities/languages, Unit 1 phrasal verbs,
the *look* family, personality adjectives, school objects — plus the auxiliary-verb and
nationality-suffix reference tables from the same lesson.

Every correction is logged and labelled by source: **16 copy slips** (Elena's own spelling/copying errors)
and **15 notebook errors** (meanings or opposites written in the book that are wrong in English —
e.g. *look after = mong chờ*, *language of Lebanon = Lebanese*, *unenergetic*).

## Chunk Rush (the game)

Tap the chunks in order before the clock runs out, with decoy chunks from other words mixed in
(`co`, `op`, `er` from *cooperative* while she is building *hit it off*). A wrong tap costs 3 seconds,
**listening to the answer costs 5 points**, a run of correct words multiplies points up to ×5, and the best score is saved.

**No keyboard** — it is designed for five minutes in the car seat, one-handed. Two lengths: 5 minutes or 90 seconds.
Chunk tiles are 74px minimum, every control is a full-size target, and there is a hint button (places the next chunk,
−5 seconds) for when she stalls.
Words she builds with no wrong taps **and no listens** count towards her review schedule; words she stumbles
over are left alone rather than penalised, so the game can never damage the spacing data. The listen button stays
available for when she is genuinely stuck, but it is never the cheap route — hearing a word is not retrieving it.

The clock is not decoration: chunk recognition has to become *fast* before spelling becomes automatic,
and the decoys force her to discriminate between the endings she actually confuses (-ian / -ion, -er / -or).

## The drills, and why they are in this order

1. **Look · Cover · Write · Check** — study the word in syllables, hear it, cover it, write it from memory.
   The *cover* step is the active ingredient: production, not copying.
2. **Build it from parts** — assemble `un·re·li·a·ble` or the words of a phrasal verb in the right order.
   Chunking beats letter-by-letter memorising for long words.
3. **Listen & Spell** — dictation, with letter-level feedback, then she copies the correct form once.
4. **Meaning → phrase** — the class-test format: no audio, no cue, produce the phrase from the meaning.
5. **Sentence dictation** — the missing word inside a real sentence.
6. **Fill the gaps** — only the hard letters hidden.
7. **Beat your traps** — her own misspellings against the correct form; always ends with her typing the correct one.
8. **Nationality builder** — the `-ian / -ese / -ish / -i` patterns.
9. **Chunk Rush** — the game; see above.
10. **Mock test (25)** — the exact 25 items from the 17 Aug test, scored and logged so the climb from 5/25 is visible.

Scheduling is Leitner: five boxes, intervals 1 · 2 · 4 · 8 · 16 days. A word counts as **Strong** at box 4,
i.e. spelled correctly on four separate days.

## Reading comfort

Three themes via the 🌗 button in the header, or **More → theme**: **auto** (follows the tablet), **light**
(warm off-white, no pure white and no glare) and **dark** (warm charcoal for early or dark mornings —
not pure black, which strobes badly in a moving car). The choice is remembered.
`prefers-reduced-motion` is respected, so the wrong-tap shake and the point animations switch off for anyone
who finds movement uncomfortable in a car.

## Privacy

Scores, streaks and Elena's own memory tricks are held in `localStorage` on her device only.
Nothing is sent anywhere. **More → Back up progress** writes a JSON file she can restore later or on another device.
