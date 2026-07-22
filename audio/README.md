Put your recorded voice messages here, named to match the STOPS list in index.html:

  audio/intro.mp3       plays automatically when the bottle is tapped
  audio/paper.mp3       short sound effect — plays whenever a letter is opened (a stop's letter, or reopening one under the compass)
  audio/success.mp3     short sound effect — plays on "Die Reise beginnt", on reaching each stop, on solving each password, and on each "Next Step" test button press
  audio/stop1-1.mp3      stop 1's first letter (before the password)
  audio/stop1-2.mp3      stop 1's second letter (after the password)
  audio/stop2-1.mp3
  audio/stop2-2.mp3
  audio/stop3-1.mp3
  audio/stop3-2.mp3
  audio/stop4-1.mp3
  audio/stop4-2.mp3

If a letter's file is missing, the app falls back to reading that
letter's `message` text aloud with the phone's built-in
text-to-speech — so you can test the whole flow before recording
anything. `intro.mp3`, `paper.mp3`, and `success.mp3` have no fallback: if any
is missing, that moment just plays silently — nothing is blocked
either way.

To skip the password puzzle at a given stop, leave its `password` as
`""` (or remove `letter2`) in `index.html` — that stop then goes
straight to the next location after letter1, same as before, and you
only need one audio file for it.

Recording tips:
- Voice Memos (iPhone) or the stock Recorder app (Android) both export
  to a format that works fine — just rename the export to match the
  list above and drop it in this folder.
- Keep each clip short (under ~30s) so it doesn't stall the group.
- Export/share as .mp3 or .m4a — if you use .m4a, update the file
  extension in the `audioSrc` values (and the `intro.mp3` reference in
  the bottle's click handler) in index.html to match.
