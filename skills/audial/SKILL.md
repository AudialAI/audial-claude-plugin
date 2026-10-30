---
name: audial
description: Use when the user wants to split stems, analyze or master audio, make a sample pack, convert audio to MIDI, generate music, turn a one-shot into a Vital or Serum 2 synth preset, or sing lyrics in a reference voice. Routes each request to the right Audial MCP tool and explains results.
---

# Audial tools

All tools take full local file paths and write results into the user's Audial results folder.
Report the `output_dir` and file names back to the user after every job.

| User wants | Tool | Notes |
|---|---|---|
| separate vocals/drums/bass, "remove vocals", change tempo/key of stems | `stem_split` | `full_song_without_vocals` gives an instrumental |
| tempo, key, loudness of a track | `analyze` | fast; answer from `metadata` |
| song sections, arrangement | `segment` | |
| louder/polished mix, "master this" | `master` | pass a reference track if they name one |
| drum hits, loops, sample pack | `generate_samples` | |
| audio → MIDI | `generate_midi` | |
| write/generate a song, cover, remix, extend | `generate_music` | tempo/key words in the prompt beat the numeric fields |
| synth patch from a sample | `sound2vital` | default; one-shot ≤ 20 s; free Audial Synth plugin |
| Serum / Serum 2 preset from a sample | `sound2serum` | one-shot ≤ 20 s; opens in Xfer Serum 2, no plugin needed |
| sing these lyrics in this voice | `text2vox` | needs reference clip and a melody (MIDI or audio) |
| "where did that go", earlier outputs | `list_results` | |

Every tool except `list_results` requires an active Audial subscription. Jobs run remotely and take seconds to minutes; progress is reported. If a tool returns a
subscription or credentials message, relay it verbatim and stop.

No API key is needed. If the user is not signed in, the first tool call opens a sign-in page in their browser and continues once they approve. If a tool returns a sign-in link instead, give the user the link and the code, and run the tool again when they say they have approved it. `account` shows who is signed in; `sign_in` and `sign_out` change it.
