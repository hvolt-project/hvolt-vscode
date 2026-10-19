# Changelog

All notable changes to the hvolt VS Code extension are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions are independent of
`hvolt` itself (see [RELEASING.md](RELEASING.md)).

## [Unreleased]

## [0.1.0] — 2026-10-19

First release. Requires `hvolt` 26.0.0 or newer, for `hvolt lsp --stdio`.

### Added

- ArkTS language support through the `hvolt` language server: completion (component
  attributes, declared object arguments, enum members, decorators, `$r`/`$rawfile`, module
  exports with their import edit), hover, signature help, definition, type definition,
  implementation, references, document highlights, outline, workspace symbols, folding, smart
  selection, rename, quick fixes, semantic highlighting, inlay hints and call hierarchy.
- Diagnostics from codelinter and from the SDK's TypeScript service, including buffers that
  are not saved yet.
- Syntax highlighting: TypeScript from the host's built-in `source.ts` grammar, plus ArkTS
  rules for decorators, `struct`, `$r(...)` resources and ArkUI components.
- Commands: Build, Run, Sign, Install, Screenshot, Log. Build state in the status bar.
- Settings: `hvolt.binaryPath`, `hvolt.sdkPath`, `hvolt.device`, `hvolt.lintOnSave`,
  `hvolt.lintOnType`, `hvolt.lintDelay`, `hvolt.lintAllRules`, `hvolt.lintIgnoreRules`,
  `hvolt.typeDiagnostics`, `hvolt.logFile`.
