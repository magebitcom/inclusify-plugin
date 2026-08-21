# Inclusify for AI agents

Connect your AI assistant to [Inclusify](https://inclusifyapp.com) and ask about the
accessibility of your own websites: what is failing, where it lives in your source, and whether
the fix you just wrote actually fixes it.

This repository is the install surface — the plugin manifests, the registry entry and one skill.
The MCP server itself runs at `https://app.inclusifyapp.com/api/mcp/customer` and is not open
source.

## Install

**Cursor** — [Add to Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=inclusify&config=eyJ1cmwiOiJodHRwczovL2FwcC5pbmNsdXNpZnlhcHAuY29tL2FwaS9tY3AvY3VzdG9tZXIifQ==),
or install the Inclusify plugin from the Cursor marketplace.

**Claude Code**

```bash
claude mcp add --transport http inclusify https://app.inclusifyapp.com/api/mcp/customer
```

Or install this repository as a plugin marketplace, which brings the skill with it:

```bash
/plugin marketplace add magebitcom/inclusify-plugin
```

**Gemini CLI**

```bash
gemini extensions install https://github.com/magebitcom/inclusify-plugin
```

**Everything else** — Claude web and desktop, ChatGPT, VS Code, Windsurf, Continue and the rest
are one URL each. The exact file and field name per client are documented at
[inclusifyapp.com/docs/integrations/mcp](https://inclusifyapp.com/docs/integrations/mcp).

## First connection

Your client registers itself and opens a browser tab. You sign in to Inclusify or create an
account; if you have no organisation yet you are asked to name one, which is your workspace.
A consent screen shows what the client gets — your basic profile and email address, nothing
else. No API key is involved anywhere.

## What you need for it to say anything useful

- The website has to be in your Inclusify account. Asking about a domain you have not added
  returns "no website by that name here" rather than scanning a stranger's site.
- The tools work per website on the Pro plan. Account-wide questions across every site need
  Enterprise on at least one website.
- A site that has never been scanned has no score yet.

## What it can do

Twenty-two tools: where a site stands, the fix list with the strings to grep for in your own
templates, live keyboard and screen-reader checks, rendering under forced colours and 400% zoom,
alt-text review, checking a fix before you deploy it, and a pass/fail gate for CI. Each one is
documented, along with what it deliberately does not know, at
[inclusifyapp.com/docs/integrations/claude](https://inclusifyapp.com/docs/integrations/claude).

They are the same tools on every client, and the reference lives in one place on purpose.

## The skill

`skills/accessibility-fix-loop` teaches the loop that actually resolves issues rather than
silencing them: read the fix list, grep your source for the strings it hands you, validate the
markup before deploying, then confirm against a later scan. It also tells the assistant to take
a `masked` verdict seriously — `aria-hidden`, `display: none` and swapping a button for a div
all make a scanner go quiet while leaving the barrier in place.

## Contributing

Issues and pull requests on the manifests, the skill and the docs are welcome. Problems with the
server itself, your account or your billing go to support@inclusifyapp.com.

## Licence

MIT, see [LICENSE](LICENSE). The Inclusify name and logo are trademarks of Magebit.
