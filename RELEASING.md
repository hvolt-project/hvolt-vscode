# Releasing hvolt-vscode

The extension is versioned **independently** of `hvolt`. The two are coupled by the LSP
protocol and by the `hvolt` binary it launches, not by matching numbers: `hvolt` numbers its
releases after the SDK it targets (`26.0.0-0`), while the extension is bound to the VS Code
API it compiles against (`engines.vscode`) and to the protocol it speaks. Sharing a number
would promise a compatibility that neither side can keep, and would stop a UI fix from
shipping between SDK releases.

Compatibility is declared, not inferred:

- `engines.vscode` — the oldest host the extension runs on.
- the minimum `hvolt` in this document and in the README — currently **26.0.0**, the first
  release with `hvolt lsp --stdio`.

So a version is "extension 0.2.0, works with hvolt ≥ 26.0.0". Raising the minimum `hvolt`
version is a breaking change for the extension and gets a minor bump while it is pre-1.0.

## Release procedure

1. Bump `version` in `package.json`, and add a `CHANGELOG.md` entry for it.
2. Open a pull request; the `ci` workflow typechecks, builds, runs the tests and lists what
   the package would contain.
3. Merge (squash), then tag and push:

   ```bash
   git tag -a v0.2.0 -m "hvolt-vscode 0.2.0"
   git push origin v0.2.0
   ```

4. `.github/workflows/release.yml` then:
   - runs the typecheck, the build and the tests,
   - fails if the tag and `package.json`'s version disagree,
   - packages `hvolt-vscode-<version>.vsix`,
   - creates the GitHub release with that file attached and generated notes,
   - publishes to the Marketplace **only if** the `VSCE_PAT` secret exists. Without it the
     release page still carries a working `.vsix`.

`workflow_dispatch` runs the same steps with `dry_run` (default `true`) and stops before
anything is published — useful to check the pipeline without cutting a version.

## One-time setup

- **Marketplace publisher** — the `hvolt-project` publisher must exist on the Marketplace
  and the VSIX must be published by that account.
- **`VSCE_PAT`** — an Azure DevOps personal access token with *Marketplace (Manage)*, stored
  as the repository secret `VSCE_PAT`. Leave it unset to release `.vsix` only.

## Not done automatically

The binary is not bundled. Users install `hvolt` themselves (or point
`hvolt.binaryPath` at it), which keeps the extension's download small and its licence
position clean.
