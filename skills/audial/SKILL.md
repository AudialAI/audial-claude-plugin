---
name: audial
description: Use when the user wants to split stems, analyze or master audio, find a song's sections, get its audio features, tags or lyrics, make a sample pack, convert audio to MIDI, generate music, turn a one-shot into a Vital or Serum 2 synth preset, or sing lyrics in a reference voice. Routes each request to the right Audial MCP tool and explains results.
---

# Audial tools

All tools take full local file paths and write results into the user's Audial results folder.
Report the `output_dir` and file names back to the user after every job.

| User wants | Tool | Notes |
|---|---|---|
| separate vocals/drums/bass, "remove vocals", change tempo/key of stems | `stem_split` | `full_song_without_vocals` gives an instrumental |
| a quick tempo or key reading | `analyze` | fastest; answer from `metadata` |
| song sections, arrangement, bars | `segment` | fast (about half a minute); keep the `analysis_id` it returns |
| energy, danceability, loudness, mode, key | `audio_features` | song and each section |
| genre, mood, instruments, a written description of the track | `tag_audio` | |
| lyrics, the words of a song, a transcription of the vocals | `get_lyrics` | timed lines |
| louder/polished mix, "master this" | `master` | pass a reference track if they name one |
| drum hits, loops, sample pack | `generate_samples` | |
| audio → MIDI, the notes of a part | `generate_midi` | |
| write/generate a song, cover, remix, extend | `generate_music` | tempo/key words in the prompt beat the numeric fields; with no lyrics Audial writes them (show them to the user so they can edit and run again); `instrumental=true` for no vocals |
| synth patch from a sample | `sound2vital` | default; one isolated sound, not a loop; free Audial Synth plugin |
| Serum / Serum 2 preset from a sample | `sound2serum` | one isolated sound, not a loop; opens in Xfer Serum 2, no plugin needed |
| sing these lyrics in this voice | `text2vox` | needs reference clip and a melody (MIDI or audio); a MIDI must be one note at a time: a single melody line, not chords or harmony |
| "where did that go", earlier outputs | `list_results` | |

`segment` returns an `analysis_id`. When the user then asks for features, tags, lyrics or a sample pack of the same track, pass that `analysis_id` to `audio_features`, `tag_audio`, `get_lyrics` or `generate_samples`: nothing is uploaded again and it does not count as another run. Without one, those tools take the file and run `segment` first. Tags, lyrics and sample packs need the track's stems, which Audial makes after each analysis, so right after a new one they wait a few minutes; say so if the user is waiting. If one of them fails or times out after analysing a file, its error gives the new `analysis_id`: retry with that, not with the file.

`sound2vital` and `sound2serum` model one isolated sound: a single note, chord stab or hit, ideally 1-4 seconds and dry, 20 seconds at most. A loop, melody or drum pattern gives a poor preset even under 20 seconds, so if the file looks like one (a tempo or "loop" in its name is a clue), say so before running it and suggest trimming it to one note. If a result's `summary` says the match is weak, or the user says it sounds wrong, check whether the input was a single sound before anything else.

An analysis counts as one run, and everything added to it with its `analysis_id` is included. Every other job counts as one run except `analyze`, and a failed run does not count. Accounts without a subscription get a small free allowance, then need a subscription. Jobs run remotely and take seconds to minutes; progress is reported. If a tool returns a
subscription or credentials message, relay it verbatim and stop.

No API key is needed. If the user is not signed in, the first tool call opens a sign-in page in their browser and continues once they approve. If a tool returns a sign-in link instead, give the user the link and the code, and run the tool again when they say they have approved it. `account` shows who is signed in; `sign_in` and `sign_out` change it.
