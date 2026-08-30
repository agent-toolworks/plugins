# agent-toolworks

The plugin marketplace for [agent-toolworks](https://github.com/agent-toolworks).
Add it once and every tool below is installable — including ones published
later.

```
/plugin marketplace add agent-toolworks/plugins
/plugin install code-search
/plugin install token-save
```

## What's in it

| plugin | what it does | repo |
|---|---|---|
| **code-search** | One search interface over a fleet of repositories, routed to whichever of five engines can answer the question. Across nine scored queries the best single engine gets 5/9; this gets 9/9. | [code-search-fleet](https://github.com/agent-toolworks/code-search-fleet) |
| **token-save** | Measures what an AI coding session actually costs and advises from *your* transcripts. Found 646× amplification on the first real machine — 98% of everything billed was a cache read. | [token-save](https://github.com/agent-toolworks/token-save) |

Each plugin lives in its own repository and is versioned there. This repo holds
only the catalogue, so adding a tool never means re-adding a marketplace.

## The house style

Both tools were built the same way, and it is the reason they exist:

- **A benchmark the tool can lose.** `code-search` scores itself against
  individual engines and reports when one of them wins. `token-save` verifies
  that its two Bash detectors give *opposite* advice on opposite inputs.
  A tool that cannot fail its own test is marketing.
- **Evidence labels on every answer.** Both distinguish what was measured from
  what was inferred, in the output, where a reader will see it.
- **Degrade, never fail silently.** Every dependency is optional and reported.
  The one hard requirement is `python3`.
- **Honest negatives.** "Nothing found" and "this would not help you" are
  results, and both tools are built to say them. `token-save` will actively
  tell you *not* to install a compressor when your numbers say so.

## Licence

Each repository carries its own; both are Apache-2.0.
