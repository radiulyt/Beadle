# 🎵 Beatlesdle

A daily Beatles Heardle — same song globally every day, no backend required.

Built as a tribute to [beadle.gg](https://beadle.gg) which shut down in 2024.

---

## How it works

- **Global daily rotation**: the song is picked using `UTC date → index % songCount`. Every player in the world gets the same song, with zero backend.
- **Audio**: Uses the YouTube IFrame API to stream clips (no audio files to host).
- **State & streaks**: Everything saved in `localStorage` — no accounts, no server.
- **Share**: Generates a Wordle-style emoji grid you can copy/share.

---

## Deploy to GitHub Pages (5 minutes)

1. **Create a new GitHub repository** — e.g. `beatlesdle`

2. **Upload `index.html`** to the root of the repo (just this one file is needed)

3. **Enable GitHub Pages**:
   - Go to your repo → **Settings** → **Pages**
   - Source: `Deploy from a branch`
   - Branch: `main` → `/root`
   - Click **Save**

4. Your game will be live at:
   ```
   https://YOUR-USERNAME.github.io/beatlesdle/
   ```

That's it. No build step, no npm, no config files.

---

## Customising the song list

Edit the `SONGS` array in `index.html`. Each entry:

```js
{ 
  title: "Come Together",      // used for matching guesses (case-insensitive)
  album: "Abbey Road",         // shown in autocomplete & end card
  youtubeId: "45cEn30WRpQ",   // YouTube video ID (from the URL after ?v=)
  startSec: 0                  // seconds into the video to start the clip from
}
```

**Finding the right `startSec`**: Open the YouTube video, pause at the point where the song's musical intro begins (skip long intros/silence), note the time in seconds.

**Important**: Only add songs that have official YouTube uploads. The Beatles' official channel (`@TheBeatles`) has most tracks.

---

## Adding your own audio clips (optional — for offline/no-YouTube mode)

If you want to self-host audio instead of using YouTube:

1. Create a `clips/` folder next to `index.html`
2. Add MP3 files named exactly as: `Come Together.mp3`, `Hey Jude.mp3` etc.
3. Replace the YouTube player section in the JS with:

```js
function playClip() {
  const audio = new Audio('clips/' + encodeURIComponent(state.song.title) + '.mp3');
  audio.currentTime = state.song.startSec || 0;
  audio.play();
  // ... rest of clip logic
}
```

Note: Self-hosting Beatles audio is legally grey. YouTube streaming is safer for a public site.

---

## Changing the rotation epoch

The day counter starts from `2025-01-01`. To change the launch date, edit this line:

```js
const EPOCH = new Date('2025-01-01T00:00:00Z');
```

Set it to your actual launch date so `#1` = your first day.

---

## Streak & share format

Streaks are tracked in `localStorage` keyed by UTC day number, so they survive refreshes but reset if the browser storage is cleared. There is no cross-device sync (no backend).

Share output looks like:
```
Beatlesdle #42 3/6
🟥⬛🟩
beatlesdle.github.io
```

Update the URL in `buildShareText()` to match your actual GitHub Pages URL.

---

## License

Fan project — not affiliated with The Beatles, Apple Corps, or Sony Music.
# Beadle
