# Changelog

## 0.3.3

- Selected the exact Pannonico LSP 0.3.3 release while keeping the LSP module
  outside the VSIX.
- Added completion, hover, unique-source definitions, and definite saved-file
  diagnostics for standalone partials reached through calls that forward the
  unchanged root context. Mixed, replaced, unknown, and unreachable contexts
  remain suppressed.
- Raised the current extension requirement to VS Code 1.100. The published
  0.2.0 VSIX retains its historical VS Code 1.91 minimum.

## 0.2.0

- Released the independently versioned VSIX with an exact pinned language-server
  dependency.
- Added signed-tag and GitHub Release provenance for the dedicated
  `pannonico-vscode` repository.
- Made Visual Studio Marketplace publication a manual upload of the exact
  verified GitHub VSIX, followed by credential-free public package auditing.

## 0.1.1

- Moved versioned VSIX release assets to the dedicated `pannonico-vscode`
  GitHub repository.
- Updated extension repository, support, and issue links to
  `vx-rs/pannonico-vscode` while retaining the shared private vulnerability
  reporting channel.

## 0.1.0

- First public release of Pannonico for VS Code.
- Added completion, hover, definitions, and conservative saved-workspace
  diagnostics for Pannonico projects.
- Added pinned, integrity-checked Pannonico language-server acquisition for
  trusted local and Remote-WSL workspaces.
