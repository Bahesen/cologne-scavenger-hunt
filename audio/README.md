Put your recorded voice messages here, named to match the STOPS list in index.html:

  audio/stop1.mp3
  audio/stop2.mp3
  audio/stop3.mp3
  audio/stop4.mp3

If a file is missing, the app falls back to reading the stop's `message`
text aloud with the phone's built-in text-to-speech — so you can test
the whole flow before recording anything.

Recording tips:
- Voice Memos (iPhone) or the stock Recorder app (Android) both export
  to a format that works fine — just rename the export to match the
  list above and drop it in this folder.
- Keep each clip short (under ~30s) so it doesn't stall the group.
- Export/share as .mp3 or .m4a — if you use .m4a, update the file
  extension in the `audioSrc` value in index.html to match.
