# Assets

> **There is an easier way now.** `/editor.html` uploads photos and audio for
> you, resizes oversized images, and wires them to the right slot — see
> [EDITING.md](../EDITING.md). This file describes the manual route, which still
> works: drop a file at the exact path below and the site picks it up.

Drop files here and the site picks them up — no code changes needed.

## Journey photos — `assets/journey/`

Chapters now hold a FAN of photos — tap to flip through them. Each card shows the exact filename it wants.
Until a file exists the slot stays a dashed placeholder; the moment the file
loads it becomes the photo.

| File | Chapter | What it should show |
|---|---|---|
| `01a-piano.png`    | 01 The piano | At the piano *(supplied placeholder)* |
| `01b-teaching.jpg` | 01 The piano | Teaching a lesson |
| `01c-flute.png`    | 01 The piano | Playing flute *(supplied placeholder)* |
| `01d-bedroom.png`  | 01 The piano | The room the first record was made in *(supplied placeholder)* |
| `02a-hague.svg`    | 02 The Hague | The conservatoire's logo. **The file currently there is the Royal Conservatory of Music (Toronto) — wrong institution and trademarked. Replace before launch.** |
| `02b-studio.png`   | 02 The Hague | At work in a studio at the conservatoire *(supplied placeholder)* |
| `03a-choir.png`    | 03 The choir | Conducting, mid-rehearsal *(supplied placeholder)* |
| `03b-guitar.png`   | 03 The choir | Teaching guitar *(supplied placeholder)* |
| `04a-desk.png`     | 04 Now | At the desk today *(supplied placeholder)* |

Frames are **3:2**. Supply roughly **1200×800** so they stay sharp on
retina screens. `.jpg` for photographs; if you use a different extension,
update the matching `file` in `content.js` — or just use the editor, which
sets it for you.

## Track audio — `assets/`

| File | Card |
|---|---|
| `track-1.mp3` | Selected work, card 1 |
| `track-2.mp3` | Selected work, card 2 |
| `track-3.mp3` | Selected work, card 3 |

Each card HEAD-probes its file on load. Missing ones show **Unavailable**
with the play button disabled. Present ones play through a Web Audio
`AnalyserNode`, so the meter is reading the real signal.

Files must be served from this same origin — the analyser cannot read audio
cross-origin, which is exactly why the SoundCloud embeds could not drive a
real meter.
