# getkagaz/homebrew-kagaz

The Homebrew tap for [Kagaz](https://github.com/getkagaz/kagaz) — a
local-first document vault manager for macOS.

## Install

```sh
brew tap getkagaz/kagaz
brew install kagaz
```

That gives you three binaries from a prebuilt arm64 bottle:

| Binary | What it is |
|---|---|
| `kagaz` | The CLI — ingests, classifies, files and tags documents, and keeps a searchable offline index |
| `kagaz-mcp` | A stdio MCP server, so an AI agent can drive a vault |
| `kagaz-machelper` | Apple Vision OCR and on-device classification via Apple Foundation Models |

### The MLX classifier is separate, on purpose

```sh
brew install getkagaz/kagaz/kagaz-mlx
```

It is not part of the base install because it pulls the whole MLX-Swift stack,
needs full Xcode to build its Metal shader library, and its model weights are a
multi-gigabyte `kagaz model pull`. Kagaz is a complete vault manager without
it: the offline rules classifier always works, and Apple's on-device tiers add
no download at all.

## Requirements

- **Apple silicon** (M1 or later). Intel is unsupported on purpose — both
  semantic classifier tiers are `arm64`-only frameworks.
- **macOS 15 (Sequoia)** or later. The Apple Foundation Models tier
  additionally wants macOS 26; below that, Kagaz uses Apple Vision OCR plus the
  rules classifier.

## There is no Cask for the app

Kagaz for Mac, the menu-bar app, is a separate paid product and is not
distributed here. Its source is not public. This tap carries the open-source
CLI only.

## Contributing

**`Formula/` is generated — edits here do not survive.** `release.yml` in the
main repo builds the bottle at tag time, rewrites each formula's `url`,
`sha256` and bottle block, and pushes the result over whatever is here. A fix
committed to this repository is overwritten by the next release, so a pull
request against it costs you the work twice.

Send formula changes to
[`getkagaz/kagaz/Formula`](https://github.com/getkagaz/kagaz/tree/main/Formula)
instead, where they persist and ship with the next tag. Bugs and features
belong in the [main repository's
issues](https://github.com/getkagaz/kagaz/issues).

If a formula here is actually broken — a bad URL, a failing `brew audit`, a
bottle that will not pour — that is worth reporting. Open an issue on the main
repo and say which formula; do not spend time on a patch that the release
workflow will discard.

## License

The formulae here, like the Kagaz CLI they install, are MIT-licensed —
see [LICENSE](LICENSE).
