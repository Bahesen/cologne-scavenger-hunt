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
- `radius` — how close (in meters) counts as "arrived"
- `audioSrc` — filename of the voice clip in `audio/` (e.g.
  `"audio/stop2.mp3"`)
- `message` — text shown on screen, and read aloud automatically if
  the audio file is missing

Add or remove stops by adding/removing entries in the array — the app
adapts automatically.

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

Open the **Test mode** drawer at the bottom of the page, enter a
latitude/longitude/heading manually, and hit **Apply simulated
position** — this lets you verify the compass math and the arrival
trigger without walking anywhere.

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
