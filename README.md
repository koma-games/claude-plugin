# koma

KOMA as a Claude plugin.

## Installing

In Claude, Settings, Customize, Plugins, Add marketplace, and paste:

```
koma.im/claude-plugins
```

Then install **koma** from the marketplace that appears.

### In Claude Code

```
/plugin marketplace add koma-games/claude-plugin
/plugin install koma@koma
```

Then run `/mcp`, pick `plugin:koma:koma` and sign in. The browser opens, you sign in to KOMA and
approve what Claude may do; the token is stored and refreshed from then on.

### Updating

Every change published here is a new version, because the plugin is versioned by commit. Claude
Code does not update plugins from marketplaces outside Anthropic's own unless asked, so turn it on
once: `/plugin`, the Marketplaces tab, **koma**, enable auto-update. Or update by hand with
`/plugin marketplace update koma`, then `/reload-plugins`.

New tools need no update at all: they are served by KOMA and appear on the next session.

## What is in it today

**Two skills**: one for the board and the files beside it, teaching Claude how to read and answer
questions about your projects well, and one for the platform itself, its products and how anything
written for it is spelled.

**Thirteen tools**: list your projects, read what you are working on, read a project's whole board,
create and change and move and comment on an issue, read its history, and send one to the trash or
bring it back. Plus a project's files: browse its folders the way the Files page does, and read a
file, with text read as text and pictures shown to Claude as images.

Signing in happens the first time a tool is used: Claude sends you to sign in, you approve what it
may do, and it receives access that can hold strictly less than you do and never more. Every action
is checked both against what was approved and against what you yourself have access to.

The vocabulary your project actually uses (statuses, priorities, labels, who is on the team) is read
live rather than guessed, so Claude works with your board's real values.
