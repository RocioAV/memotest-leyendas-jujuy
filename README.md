# 🎃 Ancestral Memory · Legends of Jujuy Halloween Memotest

A **Halloween memory game (memotest)** themed around the **myths and legends of northwestern
Argentina**, built as a single HTML file with all the CSS and JavaScript included: no
dependencies, no build step, works offline.

> 🌐 **Language**: the whole UI is in **English**, while the **bestiary is bilingual** — the
> legends keep their original Spanish names with the English translation next to them
> (e.g. *"La Llorona — The Weeping Woman"*). Cards and the speaking voice use the English names.

## 🕯️ How to play

1. Open `index.html` in any browser (a double click is enough).
2. Choose a mode:
   - **🌙 One Player**: solo mode with an attempts counter and a timer.
   - **🔥 Two Players (Local / Turns)**: enter the names; each matched pair scores a point for
     the player whose turn it is, and a miss passes the turn to the rival.
3. Flip two cards: if they show the same legend, the pair stays revealed, a mystical spark plays
   and **an ancestral voice speaks the name in English** (Web Speech Synthesis API) while,
   **at the same time and with the volume ducked down**, **the characteristic horror ambience
   of that beast** starts playing (Web Audio API). When the voice finishes, the sound rises back
   to its normal volume and fades out by itself after a **maximum of 5 seconds**.
4. Discover all 8 pairs on the 4 × 4 board to complete the ritual.

## 👻 Bestiary (the 8 cards)

| Legend (Spanish) | Name in English | Domain |
| --- | --- | --- |
| La Llorona | The Weeping Woman | The rivers |
| El Ucumar | The Ape-Man | The woods |
| El Pombero | The Forest Guardian | The woods |
| El Duende | The Goblin | The homes |
| La Salamanca | The Devil's Cave | The cave |
| El Familiar | The Witch's Familiar | Witchcraft |
| El Ahogado | The Drowned Man | The river |
| La Telesita | The Little Star | The sky |

## ✨ Technical details

- **Mandatory dark mode**: deep blacks/greys, fire orange (pumpkin), mystical purples and
  rustic golden borders.
- **3D flip** card animation with `transform-style: preserve-3d` and `backface-visibility`.
- **Multimedia sequence on a matched pair**:
  1. ✨ a brief mystical spark as feedback;
  2. 🎙️ `speechSynthesis` **names the legend in English** (`lang = "en-US"`, an English voice is
     picked automatically when available) and, **at the same time**, the **horror ambience of
     that beast** comes in with the volume **ducked** until the voice ends — so the name is
     clearly heard;
  3. ⏱️ the ambience **fades out by itself after at most 5 seconds** (short fade): it works even
     with very long files (tested with a 40 s MP3 → cut to 5 s).
- **A roar / wail / creak per creature**, synthesized live with the Web Audio API (oscillators,
  filtered noise, vibrato, echo and panning):

  | Legend | Ambience |
  | --- | --- |
  | La Llorona | rising and falling wail with echo and icy water breath |
  | El Ucumar | dull gutural roar with trembling guts |
  | El Pombero | branch creaks + his warning whistle |
  | El Duende | mischievous giggle with hiding-hole echo |
  | La Salamanca | cave rumour + bronze bell + whisper |
  | El Familiar | snake hiss and dry rattle |
  | El Ahogado | cold current, bubbles and underwater breathing |
  | La Telesita | celestial flash, twinkling light |

  The game always prefers the **own file** (`sound/<legend>.mp3`, if it exists) and uses the
  synthesized one as a fallback: it's **100 % local audio (no external URLs)**, it doesn't need
  the network, there are no licence issues, and it remains a single HTML file with its `img/`
  and `sound/` folders.
- Other effects (flip, miss, victory, click) also with the Web Audio API.
- **🔊 Sound** button to mute voice + ambience at any moment.
- Visual turn indicator, per-player scoreboard, timer and final statistics.
- Accessibility: cards are real buttons with dynamic `aria-label`, an `aria-live` region,
  visible focus and `prefers-reduced-motion` support.

## 🖼️ Legend images (optional)

Every legend has its own illustration in the **`img/`** folder. You can replace them with yours:

| Legend | File name |
| --- | --- |
| La Llorona | `img/llorona.jpg` (or `.png` / `.webp` / `.svg`) |
| El Ucumar | `img/ucumar.jpg` |
| El Pombero | `img/pombero.jpg` |
| El Duende | `img/duende.jpg` |
| La Salamanca | `img/salamanca.jpg` |
| El Familiar | `img/familiar.jpg` |
| El Ahogado | `img/ahogado.jpg` |
| La Telesita | `img/telesita.jpg` |

- **Any size and aspect ratio works**: square, landscape or portrait. The CSS uses a fixed-height
  box with `object-fit: contain`, so the image always stays **proportional, centred and undistorted**.
- Extensions probed automatically, in order: `.jpg` → `.jpeg` → `.png` → `.webp` → `.svg`.
- Other names are also accepted: `img/la llorona.jpg`, `img/el duende.png`, etc. (tried as a
  second option — this is why the Spanish `name` field must not be changed).
- You can force an exact path by adding the field `img:"path/file.jpg"` to the character inside
  the `LEGENDS` array.
- If the image **doesn't exist**, a fallback is shown (SVG with the rune and the name, or the
  emoji) so no card is ever blank.
- Images with a **white or transparent background** look best on the dark card.

## 🔊 Own beast sounds (optional)

Besides the synthesized ambience, each legend can have **its own sound file** in the **`sound/`**
folder. If it exists, **that** file is played (simultaneously with the voice naming the legend);
if not, the synthesized ambience from the table above is used. Same scheme as the images:
automatic probing and fallback without touching the code.

| Legend | File name |
| --- | --- |
| La Llorona | `sound/llorona.mp3` ✔ |
| El Ucumar | `sound/ucumar.mp3` ✔ |
| El Pombero | `sound/pombero.mp3` ✔ |
| El Duende | `sound/duende.mp3` ✔ |
| La Salamanca | `sound/salamanca.mp3` ✔ |
| El Familiar | `sound/familiar.mp3` ✔ |
| El Ahogado | `sound/ahogado.wav` ✔ *(cold current, bubbles and underwater breathing)* |
| La Telesita | `sound/telesita.wav` ✔ *(celestial flash: chimes, twinkles and background light)* |

✔ = file included in the repository. The last two (Ahogado and Telesita) were **generated to
order** with audio synthesis (PCM WAV, ~170-190 KB each): swap them for your own whenever you
want, with the same name, and the game picks them up without editing anything.

- Extensions searched, in order: `.mp3` → `.ogg` → `.m4a` → `.wav`.
- Other names are also accepted: `sound/la llorona.mp3`, `sound/el duende.mp3`, etc.
- You can force an exact path with the field `sound:"path/file.mp3"` in the `LEGENDS` array.
- **Duration**: 2 to 4 seconds is ideal. Even if the file is longer (or much longer), the game
  **fades it out and cuts it off by itself at 5 seconds** — no file can slow the game down.
- The sound starts **simultaneously with the voice**, with the volume ducked until the voice ends.
- The 🔊 Sound button cuts the file instantly, just like the voice.

## 🚀 Publish on GitHub Pages

Push the repo and enable **Settings → Pages → Deploy from a branch → `main` / root**. The game
will be available at `https://<user>.github.io/<repo>/`.

## 📄 Licence

Use and modify freely for personal, educational or Halloween projects. 🎃
