# Theurian plugins

The Claude Code plugin marketplace for [Theurian](https://github.com/theurian/theurian).

```text
/plugin marketplace add theurian/theurian-plugins
/plugin install theurian@theurian-plugins
/theurian:setup
```

Installing the plugin does nothing on its own — no daemon starts, no OS service is
registered. `/theurian:setup` is the only command that installs anything, it shows a
plan first, and running it twice changes nothing.

## What this repository holds

One file: `.claude-plugin/marketplace.json`.

The plugin itself lives in the Theurian monorepo at
[`plugins/claude-code/`](https://github.com/theurian/theurian/tree/main/plugins/claude-code),
and this marketplace points at that subdirectory with a `git-subdir` source. Claude
Code fetches it with a sparse partial clone, so a reader of this catalogue never
downloads Core.

Keeping the plugin where it is built is deliberate. Core and the plugin release
independently with their own versions, changelogs and pipelines
([ADR-0001](https://github.com/theurian/theurian/blob/main/docs/adr/0001-monorepo-with-independent-artifacts.md)),
and the plugin never imports Core's Python — a CI job fails the build if it does.
Splitting the plugin into its own repository has a recorded condition list, and
"the marketplace requires a dedicated repository layout" is one of them. It does
not: `git-subdir` reaches into the monorepo, so that condition has not fired.

## Versions

No `version` is pinned here, so the plugin's own `plugin.json` decides — first in
Claude Code's resolution order. Releases are tagged `plugin-v*` in the monorepo; see
its [release process](https://github.com/theurian/theurian/blob/main/docs/contributing/release.md).

## Issues

Everything is tracked in the monorepo:
[theurian/theurian/issues](https://github.com/theurian/theurian/issues).

## License

Apache-2.0, the same as Theurian.
