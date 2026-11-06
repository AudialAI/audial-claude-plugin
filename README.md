# Audial

[Audial](https://audialmusic.ai?utm_source=github&utm_medium=readme&utm_campaign=claude-plugin) is a Claude Code plugin that brings Audial's hosted audio tools into Claude as MCP tools and a routing skill. It gives Claude the ability to split stems, analyze tempo/key/loudness, find a song's sections, tempo and bars in about half a minute and add audio features, tags or timed lyrics to that analysis, master a mix, generate sample packs, convert audio to MIDI, generate or remix music, turn a one-shot sample into a Vital or Serum 2 synth preset, and sing lyrics in a reference voice, all powered by the Audial music model running on Audial's servers. Grab the companion plugins from the [downloads page](https://audialmusic.ai/downloads?utm_source=github&utm_medium=readme&utm_campaign=claude-plugin).

Audio and text you pass to a tool are uploaded to Audial's API (https://api.audialmusic.ai) over HTTPS and processed on Audial's servers; results are downloaded into your results folder. Adding features, tags, lyrics or a sample pack to an analysis uploads nothing more. To fill in artist tags, Audial's servers look up the track's title and artist in a public music database; that lookup gets the title and artist, never the audio. Some tools require an active Audial subscription.

## Install

Before this plugin is listed in the Claude directory, install it from its marketplace:

```
claude plugin marketplace add AudialAI/audial-claude-plugin
claude plugin install audial@audial
```

You will be asked for a results folder (defaults to `~/Audial`). Leave the user id and API
key fields empty: the first time you use an Audial tool, a sign-in page opens in your browser,
and once you approve it the tool carries on. Each connected computer is listed, and can be
disconnected, under Apps & API Keys in your profile at audialmusic.ai.

## Requirements

- `uv`/`uvx` available on your `PATH` (the plugin runs `uvx audial-mcp`).
- An Audial account with an active subscription (every tool except `list_results` calls the Audial API, which requires one).

## What it adds

- The `audial` MCP server (stem splitting, analysis, song sections with audio features,
  tags and timed lyrics, mastering, sample packs, MIDI, music generation, resynthesis to Vital
  or Serum 2 presets, vocal synthesis, and job listing). An analysis counts as one run, and
  everything added to it (features, tags, lyrics, a sample pack) is included.
- An `audial` skill that routes requests to the right tool and reports back where results
  were written.

---

Powered by [Audial](https://audialmusic.ai?utm_source=github&utm_medium=readme&utm_campaign=claude-plugin).
