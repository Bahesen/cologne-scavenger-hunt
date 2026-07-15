Optional — the app works fine without anything in this folder.

Drop a file named `parchment-texture.jpg` (or `.png`) here and it will
automatically appear as a blended texture behind the parchment card —
no code changes needed. If the file is missing, the app just falls
back to the current CSS-drawn look, exactly like the audio fallback.

What works well:
- A photo or scan of real aged paper, parchment, or an old nautical
  chart, fairly high resolution (at least 1000px on the short side)
  so it doesn't look blurry when stretched to cover the screen
- Fairly neutral/warm tones — it's blended with `mix-blend-mode:
  multiply`, so a busy or very dark image can make text hard to read.
  Test it and back off if the card starts feeling muddy.

To use a different filename or format, change the `background-image`
url in the `.frame::before` rule near the top of `index.html`'s
`<style>` block.

Where to find one:
I can't fetch and embed an actual texture image into this project
myself — most "old paper" images online are stock-licensed, and I'd
rather not guess at licensing on your behalf. A couple of reliable
public-domain / CC0 sources if you want to search yourself:
- publicdomainvectors.org or unsplash.com (search "old paper texture"
  or "vintage map") — check the individual image's license, not just
  the site's general policy
- Or scan/photograph a real piece of aged paper or a printed
  reproduction you own

If you want, I can also wire up additional optional slots the same
way — e.g. `images/compass-rose.png` to replace the hand-drawn SVG
rose, or `images/wax-seal.png` for the arrival panel — just ask and
tell me the filename you're using.
