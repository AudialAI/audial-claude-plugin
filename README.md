# Audial

Audial is a Claude Code plugin that brings Audial's hosted audio tools into Claude as MCP tools and a routing skill. It gives Claude the ability to split stems, analyze tempo/key/loudness, segment a song's arrangement, master a mix, generate sample packs, convert audio to MIDI, generate or remix music, turn a one-shot sample into a synth preset, and sing lyrics in a reference voice, all powered by the Audial music model running on Audial's servers.

Audio and text you pass to a tool are uploaded to Audial's API (https://api.audialmusic.ai) over HTTPS and processed on Audial's servers; results are downloaded into your results folder. Some tools require an active Audial subscription.

## Install

Before this plugin is listed in the Claude directory, install it from its marketplace:

```
claude plugin marketplace add AudialAI/audial-claude-plugin
claude plugin install audial@audial
```

You will be prompted for your Audial user id and API key (from your dashboard at
audialmusic.ai) and a results folder (defaults to `~/Audial`).

## Requirements

- `uv`/`uvx` available on your `PATH` (the plugin runs `uvx audial-mcp`).
- An Audial account; some tools (`sound2vital`, `text2vox`) require an active subscription.

## What it adds

- The `audial` MCP server (stem splitting, analysis, mastering, sample packs, MIDI,
  music generation, resynthesis, vocal synthesis, and job listing).
- An `audial` skill that routes requests to the right tool and reports back where results
  were written.
