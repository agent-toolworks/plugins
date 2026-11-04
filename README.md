# agent-toolworks

Tools for working with coding agents in Claude Code. This page is where to
start: one catalogue to add, the tools in it, and the first thing to do with
each. Every tool lives in its own repository and is versioned there; this repo
holds only the catalogue, so a tool published later shows up here with nothing
new to add.

## Start here

You need Claude Code and `python3` (the one that ships with macOS will do). Add
the catalogue once, then install the tools you want, or all of them:

```sh
claude plugin marketplace add agent-toolworks/plugins
claude plugin install note-search@agent-toolworks
claude plugin install toolworks-hub@agent-toolworks
claude plugin install code-search@agent-toolworks
claude plugin install fleet-workspace@agent-toolworks
claude plugin install token-save@agent-toolworks
```

The same works inside Claude Code as `/plugin marketplace add …` and
`/plugin install …`. Restart Claude Code, or run `/reload-plugins`, and then
take the first step for each tool below. You don't need to learn any commands:
each tool comes with a skill, so you ask Claude in your own words and it runs
the tool.

| Tool | What it is for | First step |
|---|---|---|
| **note-search** | Search notes from every project at once: Claude Code's memory folders, a team knowledge base, a notes vault. Agents use it on their own when a question sounds like "do we know…" or "did we decide…". | Ask Claude to **"set up note-search"**. It checks the machine and proposes which folders to search; you decide. The smallest setup searches every project's Claude Code memory. |
| **toolworks-hub** | A local web page for all of it: Claude Code sessions, and a tab for each tool installed (note-search's search, notes and reader; code-search; token-save usage; repo-fleet workspaces). Runs on 127.0.0.1 only. | Type **`/hub`**. It opens `http://127.0.0.1:7437/` in your browser; bookmark it. |
| **code-search** | One search over many repositories: who calls an endpoint, where a symbol is defined, who publishes or consumes an event, which version each repo pins, who owns the code. Every answer says how far to trust it. | Ask Claude to **"set up code search"**, or follow its [install checklist](https://github.com/agent-toolworks/code-search-fleet/blob/main/docs/install.md). It needs a fleet: the repos cloned side by side (fleet-workspace makes one). |
| **fleet-workspace** | Clone a fleet of repos once, then give each ticket a workspace of git worktrees holding only the repos it changes. | Ask Claude to **"set up the fleet"** and name the repos. Then: "start ticket PROJ-123, it changes X and Y". |
| **token-save** | Measures what your sessions actually cost and advises from your own transcripts: where the tokens went, what was re-read every turn, which fixes are worth it here. | Ask Claude **"why is my token usage high?"** |

They work alone and get better together. code-search searches the fleet that
fleet-workspace builds, and follows a ticket's branches. The hub shows every
tool that is installed, and links each session's page to the searches, costs
and workspace behind it.

## Each tool's repository

| Tool | Repository | Read first |
|---|---|---|
| note-search | [note-search](https://github.com/agent-toolworks/note-search) | its README: groups, the hub page, adding notes |
| toolworks-hub | [toolworks-hub](https://github.com/agent-toolworks/toolworks-hub) | its README; [writing a source](https://github.com/agent-toolworks/toolworks-hub/blob/main/docs/writing-a-source.md) to add your own tab |
| code-search | [code-search-fleet](https://github.com/agent-toolworks/code-search-fleet) | [docs/install.md](https://github.com/agent-toolworks/code-search-fleet/blob/main/docs/install.md) |
| fleet-workspace | [repo-fleet](https://github.com/agent-toolworks/repo-fleet) | [GETTING-STARTED.md](https://github.com/agent-toolworks/repo-fleet/blob/main/GETTING-STARTED.md) |
| token-save | [token-save](https://github.com/agent-toolworks/token-save) | its README's quick start |

To update later: `claude plugin marketplace update agent-toolworks`, then
`claude plugin update <tool>@agent-toolworks`. The hub's Claude Code tab lists
the installed plugins with their versions.

## The house style

They were all built the same way, and it is the reason they exist:

- **A benchmark the tool can lose.** `code-search` scores itself against
  individual engines and reports when one of them wins. `note-search` gates
  every release on a question set with known answers. `token-save` verifies
  that its two Bash detectors give *opposite* advice on opposite inputs.
  A tool that cannot fail its own test is marketing.
- **Evidence labels on every answer.** They distinguish what was measured from
  what was inferred, in the output, where a reader will see it.
- **Degrade, never fail silently.** Every dependency is optional and reported.
  The one hard requirement is `python3`.
- **Honest negatives.** "Nothing found" and "this would not help you" are
  results. `token-save` will actively tell you *not* to install a compressor
  when your numbers say so.
- **Local and read-only by default.** Nothing is sent anywhere. The hub listens
  on 127.0.0.1 only; note-search writes a note only into a folder you name.

## Installed a tool from its own repository?

Nothing is broken. To move it to this catalogue, so that every tool updates
from one place:

```sh
claude plugin uninstall note-search@note-search          # the tool and the name it was installed under
claude plugin marketplace remove note-search
claude plugin install note-search@agent-toolworks
```

Settings and data stay where they were: they live in `~/.config` and `~/.cache`,
not in the plugin.

The old `repo-fleet` catalogue (from before these repositories moved from
`my-organization-for-testing-067` to `agent-toolworks`) keeps working for
existing installs; GitHub redirects the old URLs. To move off it:

```sh
claude plugin marketplace add agent-toolworks/plugins
claude plugin marketplace remove repo-fleet
```

then reinstall whichever plugins you had. This catalogue is the only one that
lists new tools.

## Licence

Each repository carries its own; all are Apache-2.0.
