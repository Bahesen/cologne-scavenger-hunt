Optional — the app works fine without anything in this folder.

Three optional slots, all with the same behavior: drop the file in
with the exact name below, and it appears automatically — no code
changes needed. If the file is missing, the app falls back to the
current drawn look, exactly like the audio fallback.

- `parchment-texture.jpg` (or `.png`) — a blended texture behind the
  parchment card
- `bottle.png` — replaces the hand-drawn bottle on the very first
  screen. Recommended size around 130×204px (or similar aspect
  ratio) with a transparent background so it sits on the parchment
  cleanly
- `letter.png` — replaces the envelope icon used both under the
  compass (small, ~46×33px) and in the "a letter awaits you" prompt
  (larger, ~110×78px). The same file is used at both sizes, scaled
  down for the small one — transparent background recommended here
  too

What works well for the texture specifically:
- A photo or scan of real aged paper, parchment, or an old nautical
  chart, fairly high resolution (at least 1000px on the short side)
  so it doesn't look blurry when stretched to cover the screen
- Fairly neutral/warm tones — it's blended with `mix-blend-mode:
  multiply`, so a busy or very dark image can make text hard to read.
  Test it and back off if the card starts feeling muddy.

To use different filenames, formats, or sizes:
- Texture: the `background-image` url in the `.frame::before` rule
  near the top of `index.html`'s `<style>` block
- Bottle/letter: the `src` (and `width`/`height`) on the `<img>` tag
  right before each corresponding `<svg>` in the body

Where to find images:
I can't fetch and embed actual images into this project myself —
most images online are stock-licensed, and I'd rather not guess at
licensing on your behalf. A couple of reliable public-domain / CC0
sources if you want to search yourself:
- publicdomainvectors.org or unsplash.com (search "old paper texture"
  or "vintage map") — check the individual image's license, not just
  the site's general policy
- Or scan/photograph a real piece of aged paper, draw your own
  bottle/letter icon, or commission/generate one — anything you have
  the rights to use

If you want, I can also wire up additional optional slots the same
way — e.g. `images/compass-rose.png` to replace the hand-drawn SVG
rose, or `images/wax-seal.png` for the arrival panel — just ask and
tell me the filename you're using.
