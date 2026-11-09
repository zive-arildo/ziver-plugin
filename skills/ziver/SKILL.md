---
name: ziver
description: Ziver's status, token usage and savings on this machine and in this session, and how to install Ziver if it is not here yet. Use when the user types /ziver, or asks whether Ziver is running, how many tokens a session is spending or saving, or about their Ziver plan or monthly limit.
---

# Ziver

Ziver is a separate command-line program. This plugin is the front door to it:
it runs Ziver's own commands and reports what they say.

## Find the binary first

Ziver installs to `~/.ziver/bin`, which its installer does not add to `PATH`.
So resolve it once, with the Bash tool, before anything else:

```sh
command -v ziver || ls ~/.ziver/bin/ziver
```

Use whichever answered as `ziver` in every command below. If neither does,
Ziver is not installed on this machine: go to **When Ziver is not installed**.

## Answer what was asked

Run the one command for what the user asked, with the Bash tool and directly
rather than through Ziver's `exec` tool. Answer in the user's language, with
the figures that matter and without pasting the raw output.

- **Status** (`/ziver` or `/ziver status`): run `ziver status`. Also say
  whether Ziver's MCP tools, such as `mcp__ziver__exec`, are available to you
  in this session, because that is what shows Ziver is loaded here and not
  merely installed. If they are not, Claude Code needs restarting after
  `ziver setup claude`.
- **Usage** (`/ziver usage`): run `ziver stats --today` and
  `ziver stats --month`, and give the dashboard link that `ziver status`
  prints.
- **Where the savings came from** (`/ziver why`): run `ziver why`.
- **Account and plan** (`/ziver account`): run `ziver account`.
- **Health** (`/ziver doctor`, or any report that Ziver stopped saving): run
  `ziver doctor`. Read its `memory hooks` and `last checkpoint` lines out to
  the user. Most of what Ziver saves is the checkpoint it writes when a
  session compacts, so a `last checkpoint` of days ago on a machine that has
  been compacting is the thing to report, not the total.
- **Update** (`/ziver update`): only when `status` shows a newer version, or
  the user asks. Run `ziver update`, then say that sessions already running
  keep the old version until they restart.

Never invent a number. If a command fails or prints nothing, say so and show
what it printed.

## When Ziver is not installed

Do not install it yourself. Tell the user what it is in one or two sentences
and give them the command for their system, which they run in their own shell:

- macOS and Linux: `curl -fsSL https://ziveit.com/ziver/install.sh | sh`
- Windows, in PowerShell: `irm https://ziveit.com/ziver/install.ps1 | iex`

Then: `ziver login` to sign in, `ziver setup claude` to connect it to Claude
Code, and restart Claude Code so the session loads it. Mention that there is
a free tier, and that `https://ziver.ziveit.com/` is where usage is shown.

## Turning it off

In this session, the user can type `/ziver-disable` and `/ziver-enable`, which
Ziver installs itself once `ziver setup claude` has run. From the shell it is
`ziver disable` for the session and `ziver disable --machine` everywhere.
