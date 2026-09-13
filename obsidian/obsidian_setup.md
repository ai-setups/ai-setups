# Obsidian Setup

Obsidian has no global config layer: themes, hotkeys and plugins all live in each
vault's own `.obsidian/`. Every new repo means redoing the setup, so here it is.

```bash
brew install --cask obsidian
```

"Open folder as vault" can point straight at an existing Git repo — Obsidian only
adds `.obsidian/` to it.

## Enable the official CLI

Obsidian 1.12+ ships a [command line interface](https://obsidian.md/help/cli), so plugin
installs no longer need the GUI. One-time setup: Settings → General → Advanced →
Command line interface, then follow the registration prompt (on macOS it symlinks
`/usr/local/bin/obsidian` and asks for an admin password). Restart the terminal afterwards.

```bash
obsidian plugins filter=community versions
```

The CLI talks to the running Obsidian instance and acts on the currently open vault.

## Do not commit `.obsidian/`

`workspace.json` is rewritten on every cursor move, `plugins/` holds builds owned by
their own repos, and the remaining settings only apply to this machine. Ignore it:

```gitignore
.obsidian/
```

## Plugins

| Plugin | Why |
| --- | --- |
| [Heading Level Indent](https://github.com/svonjoi/obsidian-heading-level-indent) | Indents body text by heading level, so a long note's structure is visible in the text itself instead of only in the outline pane. |
| [Portable Folds](https://github.com/ai-setups/obsidian-portable-folds) | Obsidian stores fold state as absolute line numbers in `localStorage` — edit anything above a heading and folds land on the wrong sections, and the state never leaves the machine. This plugin writes the state into the note as a `%% fold %%` comment. |

Store plugins are a single command:

```bash
obsidian plugins:restrict off
obsidian plugin:install id=heading-level-indent enable
```

Portable Folds is not in the store and has no GitHub Release yet, so BRAT cannot pick it
up — copy the build in by hand:

```bash
mkdir -p .obsidian/plugins/portable-folds
cp <build>/main.js <build>/manifest.json .obsidian/plugins/portable-folds/
obsidian plugin:enable id=portable-folds
```

Once that repo publishes a release containing `main.js` and `manifest.json`,
[BRAT](https://github.com/TfTHacker/obsidian42-brat) can install and auto-update it instead.

## Hotkeys

The CLI can read hotkeys but not set them, so these two are assigned by hand under
Settings → Hotkeys. Folding is the most frequent action when reading long notes.

| Command | Hotkey |
| --- | --- |
| Fold all | `Cmd+Opt+[` |
| Unfold all | `Cmd+Opt+]` |

## Core plugins

Left at defaults, except for turning off the ones that are never used, to keep the
command palette quiet:

```bash
for id in slides audio-recorder webviewer zk-prefixer random-note markdown-importer; do
  obsidian plugin:disable id=$id filter=core
done
```
