# Pinework plugins

Pinework's plugin marketplace. It lists the plugins from Anthropic's, OpenAI's and Cursor's catalogs, one entry per brand.

> **Trust a plugin before you install it.** Each entry points at its vendor's or host's repo, pinned to one commit. Pinework does not write or control those plugins. See each plugin's homepage.

## Install

In Pinework, the marketplace is built in. Open **Customize**, then **Add plugin**.

In Claude Code:

```
/plugin marketplace add pinework-ai/plugins
/plugin install linear@pinework
```

## What is in it

- `.claude-plugin/marketplace.json` lists every plugin. Each entry's `source` is a `url` or `git-subdir` pointer pinned at a sha. This repo copies no plugin code.
- Each entry also carries `icon`, `connectors` and `sources`. Pinework reads them. Claude Code ignores them.
- `sources` names every upstream catalog entry that was merged into the entry, with the commit it was read at.

## How it is built

`scripts/marketplace-sync.ts` in Pinework's own repo writes the file from three upstream catalogs, each pinned to a commit:

- `anthropics/claude-plugins-official`, `.claude-plugin/marketplace.json`
- `openai/plugins`, `.agents/plugins/marketplace.json`
- `cursor/plugins`, `.cursor-plugin/marketplace.json`

It leaves out OpenAI entries with no license or a proprietary one, entries that need an OpenAI-only connector, and `npm` or `command` sources. It never copies an upstream MCP auth block.

## Plugin names never change

An entry's `name` is the slug people install under. A rerun of the sync keeps every name already published here.

## License

Apache-2.0 for this repo's own files. Each plugin keeps its own license, shown in its entry.

