# Cologne Scavenger Hunt — Field Trail

A single-page app that points a compass needle toward each stop using the
phone's GPS and compass, and unlocks a voice message when the group
arrives.

## Project structure

```
cologne-scavenger-hunt/
├── index.html          the whole app (edit the STOPS list here)
├── audio/               drop your recorded voice messages here
│   └── README.md
├── images/               optional — drop an image here for a real texture
│   └── README.md
├── .vscode/
│   └── extensions.json  recommends the Live Server extension
├── package.json         optional alternative to Live Server
└── .gitignore
```

## 1. Open it in VS Code

Unzip the project, then in VS Code: **File → Open Folder…** and select
`cologne-scavenger-hunt`.

## 2. Edit your stops

Open `index.html`, find the `STOPS` array near the top of the
`<script>` block, and edit each entry:

- `name` — shown at the top of the screen
- `lat` / `lng` — right-click the spot on Google Maps → the two
  numbers at the top of the menu are your coordinates
- `radius` — how close (in meters) counts as "arrived". Phone GPS is
  typically accurate to 5-15m outdoors (worse near tall buildings), so
  a very small radius can feel precise but also more sensitive to GPS
  noise — the app now filters out clearly bad fixes and shows a
  "warmer/colder" hint that stays reliable at close range even when
  the compass needle itself gets a little shaky, so smaller radii
  (5-10m) are more usable than they used to be. Still worth testing
  each location in person before relying on it.
- `letter1` / `letter2` — each is `{ audioSrc, message }`, same rules
  as before: `audioSrc` is a filename in `audio/` (leave `""` to read
  `message` aloud instead)
- `password` — the word someone needs to find at that location to
  unlock `letter2`. Checked case-insensitively with whitespace
  trimmed. Leave it `""` (or remove `letter2`) to skip the puzzle —
  that stop then goes straight to the next location after letter1

At each stop the flow is: arrive → open letter1 → enter the password
→ open letter2 → compass leads to the next stop.

Add or remove stops by adding/removing entries in the array — the app
adapts automatically.

**Story Mode** — a "Story Mode" button on the start screen (next to
the bottle) lets anyone browse every letter in order — the intro
plus each stop's letter1/letter2 — with audio, no walking, GPS, or
password-solving required. Useful for previewing the whole narrative,
or for anyone who can't do the physical hunt. It's built from the
same `STOPS` array automatically, so editing your stops updates
Story Mode too — except the intro letter, which is duplicated as a
separate `INTRO_LETTER_TEXT` constant near the bottom of the
`<script>` block (search for it) since the hardcoded intro screen
doesn't store its text as a plain string anywhere else. If you edit
the intro letter's wording, update both places.

## 3. Record the voice messages

See `audio/README.md`. You don't need real recordings to test —
leave the files out and the app reads the `message` text aloud
instead.

## 4. Preview it locally

GPS and the compass only work over a "secure context" — `https://`,
or `http://localhost`. Opening the file directly (`file://...`)
will *not* work for location/compass.

**Easiest: Live Server extension**
1. Install the recommended extension when VS Code prompts you (or
   search "Live Server" by Ritwick Dey in the Extensions panel).
2. Right-click `index.html` → **Open with Live Server**.
3. It opens at `http://127.0.0.1:5500` — that counts as secure, so
   GPS/compass prompts will work on your computer. (A laptop won't
   have a real compass, but you can test with the **Test mode**
   drawer at the bottom of the page.)

**Alternative: npm**
```
npm start
```
Serves the folder at `http://localhost:5500`.

## 5. Test without real GPS

Open the **Navigator's notes** drawer at the bottom of the page, enter
a latitude/longitude/heading manually, and hit **Apply simulated
position** — this lets you verify the compass math without walking
anywhere. The same drawer has **Previous Step** / **Next Step**
buttons that simulate the entire journey without needing GPS or the
coordinate fields at all: each press moves through exactly what a
real hunt would show — arriving at a stop, the letter prompt, the
letter itself, the password screen (if that stop has one), the
second letter, then on to the next stop.

The app also saves your exact progress to the browser's local storage
as you go — not just which stop, but which letter, or whether you're
mid-password — so a crashed tab or accidental reload picks up right
where it left off (you'll see a "Reise fortsetzen" button instead of
the bottle). **Reset Journey**, also in the drawer, clears that saved
progress and reloads the page to start over from the bottle.

## Keeping tracking alive on a locked/sleeping phone

The app requests a screen wake lock once the trail starts, which
stops the phone from auto-locking on its own timeout while this tab
is open and visible — the most common reason GPS/compass updates
seem to "stop" mid-hunt. It's supported in most current mobile
browsers and fails silently where it isn't.

What it can't do: if someone manually locks their phone, or switches
to a different app, the browser releases the wake lock immediately
and — this is a platform restriction, not something fixable from a
web page — background tabs get suspended by the OS, so location
updates, audio, and vibration all stop until the tab is foregrounded
again. True background tracking (screen off, app switched away)
would need a native app with background location permission; a web
page fundamentally can't do that reliably on iOS or Android. The
practical guidance for players: keep the tab open and the phone
unlocked during the hunt rather than switching apps.

## 6. Deploy so phones can actually use it

Phones need the page hosted somewhere with a real `https://` address.
Two free options:

**Netlify Drop (fastest, no account needed for a quick test)**
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag the whole `cologne-scavenger-hunt` folder onto the page
3. You get a live `https://...netlify.app` URL immediately — send it
   to the group's phones

**GitHub Pages (better if you want to keep editing it)**
1. Push this folder to a new GitHub repo
2. Repo → Settings → Pages → set source to the `main` branch, root
   folder
3. GitHub gives you a `https://<username>.github.io/<repo>/` URL

## 7. On the day

Each team opens the deployed link on their phone, taps **Start the
trail**, and allows location + motion access when prompted. iPhones
will show a separate "Motion & Orientation Access" prompt on top of
the location one — both need to be allowed for the compass to work.

## Troubleshooting

**My mp3 isn't playing / message gets read aloud instead**
The app now shows the real reason under the play button instead of
failing silently. The most common causes:
- **Stale deploy** — if you used Netlify Drop, it's a one-time
  snapshot. Adding a file to your local `audio/` folder afterward
  does nothing until you drag the folder onto Netlify Drop again (or
  push again, for GitHub Pages).
- **Case sensitivity** — most static hosts are case-sensitive.
  `Stop1.mp3` on disk won't match `audio/stop1.mp3` in `index.html`.
- **Verify directly** — open `https://your-site/audio/stop1.mp3` in
  a browser tab. If that doesn't play on its own, the deploy is the
  problem, not the app.

**Compass still feels off**
The needle is now smoothed, but phone compasses are still affected
by nearby metal/magnets. If it drifts, waving the phone in a
figure-8 usually recalibrates it (this is a phone OS behavior, not
something the page controls).
