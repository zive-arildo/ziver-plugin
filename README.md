# Ziver

**See what your Claude Code sessions spend on tokens, and cut it.**

A long session resends its whole transcript on every request. Ziver writes a
compact checkpoint of the session's memory when the harness compacts, so the
next turn carries the ledger instead of the transcript, and returns large
command output through a handle you expand only where you need it.

On one developer's machine over thirty days, that came to 166 million tokens
of context that were never sent. Your own figure is whatever `ziver status`
reports; the point of this plugin is that you can see it.

## What this plugin gives you

`/ziver` — status, usage, where the savings came from, your plan, and a health
check when it looks like nothing is being saved.

That is all it does. The plugin is skills and documentation: it runs Ziver's
own commands and reports what they say.

Install it from Anthropic's directory, or from this repository as a
marketplace:

```
/plugin install ziver --marketplace zive-arildo/ziver-plugin
```

## Ziver itself is a separate install

This plugin does not contain Ziver and will not install it for you. It tells
you how, and once Ziver is on the machine the plugin's commands start
answering with real numbers.

macOS and Linux:

```sh
curl -fsSL https://ziveit.com/ziver/install.sh | sh
```

Windows, in PowerShell:

```powershell
irm https://ziveit.com/ziver/install.ps1 | iex
```

Then sign in, connect it to Claude Code, and restart Claude Code so the
session picks it up:

```sh
ziver login
ziver setup claude
```

`ziver setup claude` writes the hooks that save a checkpoint at compaction and
registers Ziver's MCP tools. It backs up every file it touches and
`ziver setup claude --undo` puts them back.

There is a free tier. Usage is at <https://ziver.ziveit.com/>.

## What it does on your machine

- **Session memory.** A hook saves a checkpoint before the harness compacts,
  so a resumed session gets a ledger of goal, constraints and open questions
  rather than starting from a summary of a summary.
- **Command output through a handle.** `exec` returns errors and status, plus
  a `ctx://` handle for the rest, which you expand by query or line range.
- **An optional local proxy.** Compresses repetitive tool results in flight,
  leaving file contents verbatim. Off unless you turn it on, and
  `ziver setup claude --no-proxy` keeps it off.

## What leaves your machine

This plugin has no code of its own and makes no network request. It runs
Ziver's commands and reports what they print.

Ziver itself does talk to its own service at `ziver.ziveit.com`, and this is
all of what goes there:

- **When you sign in**, the machine is registered: your account email, a
  machine id that is a hash of the system's own identifier and never the
  identifier itself, the machine's hostname as a label, its operating system
  and architecture, and the Ziver version.
- **Periodically after that**, a usage report: for each day and each kind of
  saving, how many times it ran and the token counts before and after.

It does not send your source code, your file names, your prompts or your
transcripts. Two settings govern that, and both are off until you turn them
on: uploading cost telemetry, and sending repository content to a cloud model
for optimisation. `ziver status` prints their state on its `privacy` line.

Account, machine and usage records are kept for as long as the account
exists, and are deleted within thirty days of deleting it. You can disconnect
a machine from the dashboard at any time, or run `ziver logout` on it. The
privacy policy below is the full account, and it governs.

## Links

- Dashboard and plans: <https://ziver.ziveit.com/>
- Privacy policy: <https://www.ziveit.com/ziver/privacy/>
- Terms: <https://www.ziveit.com/ziver/terms/>
- ZiveIT: <https://www.ziveit.com/>

## Licence

Apache-2.0. This repository holds the plugin — its skills and documentation.
Ziver itself is a separate, closed-source program distributed by its
installers above.
