# Pannonico for VS Code

Pannonico provides template completion, hover, definitions, and conservative
diagnostics through a pinned Go/WASI language server. The extension discovers
projects and owns VS Code and WASI lifecycle integration. Each language-server
process owns one project's indexing and template semantics.

> **Pre-1.0 development notice:** Pannonico is under active development. Until version 1.0.0, public contracts and user-visible behavior may change between releases. Expect breaking changes while the program and distribution model are being stabilized.

## Requirements

- VS Code 1.91 or newer
- [WASM WASI Core](https://marketplace.visualstudio.com/items?itemName=ms-vscode.wasm-wasi-core)
- A trusted, file-backed local workspace or Remote-WSL workspace
- A regular `pannonico.yaml` or `.pannonico` project marker, unless the project
  is selected manually

Remote-SSH, Dev Containers, Codespaces, other remote providers, Restricted
Mode, virtual workspaces, and VS Code for the Web are not supported.

## Install

Install **Pannonico** from the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=vx-rs.pannonico),
or search for extension ID `vx-rs.pannonico` in VS Code. The required WASM WASI
Core extension is declared as a dependency.

For an exact-byte fallback, download `pannonico.vsix` from the matching
[`vx-rs/pannonico-vscode` GitHub Release](https://github.com/vx-rs/pannonico-vscode/releases)
and install it with **Extensions: Install from VSIX...**. In Remote-WSL, install
both Pannonico and WASI Core in the WSL extension group.

The extension and its VSIX contain no language-server WASM or GitHub
credentials. The pinned module is downloaded from the immutable
[`vx-rs/pannonico-lsp` release](https://github.com/vx-rs/pannonico-lsp/releases)
when a project first needs it.

## Language-server runtime

The extension downloads only when a detected project needs the pinned release
and no valid cached module exists. It verifies the committed release target,
byte size, SHA-256 digest, and WASM bytes before atomically installing the module
in extension global storage. Each new project session revalidates the cached
module's file type, size, SHA-256 digest, and WASM bytes before use.

Each marked project receives an isolated language-server process. Sibling and
nested projects use separate sessions, and the deepest marked root owns a file.
Creating or removing a marker reconciles only the affected project and its
direct marked parent.

Use the Pannonico Output channel for release identity, project roots, session
identity, timings, diagnostics, and lifecycle errors.

## Commands

- `Pannonico: Start Language Server`
- `Pannonico: Restart Language Server`
- `Pannonico: Restart All Language Servers`
- `Pannonico: Stop Language Servers`
- `Pannonico: Show Output`

Start discovers all marked projects. When the window has no marker, it can
select one configuration-free project folder manually. Restart targets the
active editor's project when ownership is unambiguous; Restart All rediscovers
the workspace.

## Language features

Pannonico provides completion, hover, definitions, and definite saved-workspace
diagnostics for project configuration, templates, layouts, partials, data, and
the scalar-free `.nav` hierarchy. Navigation completion covers `current`,
`parent`, and `tree`, including directory and page identities, page metadata,
parent chains, and referenced-page frontmatter.

Direct navigation links use `tree.c` for directories and `tree.p` for pages:

```html
<a href="{{.nav.tree.p.index.url}}">Home</a>
<a href="{{.nav.tree.c.guides.p.install.url}}">Install</a>
```

VS Code's normal Problems collection and Explorer problem decorations show
definite saved-file failures. Pannonico does not add a custom decoration
provider. Unsaved template text takes precedence over saved direct-path
findings until it is saved.

## Remote-WSL

Open the project through `WSL: Open Folder in WSL`. Confirm Pannonico and WASI
Core are installed in the WSL extension group and run in the remote workspace
Extension Host. The selected Linux workspace remains a `file` URI inside that
host.

If startup reports an unsupported environment, confirm the window is connected
to WSL, the workspace is trusted and file-backed, and both extensions run on
the WSL side.

## Current limits

- Trusted local and Remote-WSL file workspaces only
- One WASI process per project root
- No general Go-template interpretation
- No remote-data fetch in the IDE path
- No standalone partial completion when caller context is unknown
- No automatic LSP release discovery

## License

Pannonico Free is available under either the
[PolyForm Noncommercial License 1.0.0](https://github.com/vx-rs/pannonico-vscode/blob/master/LICENSES/PolyForm-Noncommercial-1.0.0.md)
or the
[PolyForm Small Business License 1.0.0](https://github.com/vx-rs/pannonico-vscode/blob/master/LICENSES/PolyForm-Small-Business-1.0.0.md),
at your option. Organizations whose use is not permitted by either license
require a separate commercial Pannonico license. See the
[license chooser](https://github.com/vx-rs/pannonico-vscode/blob/master/LICENSE).

## Support

Read the [support guide](https://github.com/vx-rs/pannonico-vscode/blob/master/SUPPORT.md)
before opening a
[Pannonico VS Code issue](https://github.com/vx-rs/pannonico-vscode/issues). Report suspected
vulnerabilities through the shared
[private security process](https://github.com/vx-rs/pannonico/security/advisories/new),
not through a public issue.
