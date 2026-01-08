# tree-sitter-liquid

A grammar of [Silverfin's Liquid templating language](https://developer.silverfin.com/docs/where-to-start) to be used with [tree-sitter](https://tree-sitter.github.io/tree-sitter/).

## Installation

### Node.js

Install directly from GitHub:

```bash
npm install github:rufex/tree-sitter-liquid
```

Or with a specific version:

```bash
npm install github:rufex/tree-sitter-liquid#v0.6.0
```

The package will automatically use prebuilt binaries if available for your platform, or compile from source as a fallback.

### Prebuilt Binaries

You can also download prebuilt binaries directly from [GitHub Releases](https://github.com/rufex/tree-sitter-liquid/releases):

```bash
# Download the appropriate Node.js binary for your platform
curl -L -o tree_sitter_liquid_binding.node \
  "https://github.com/rufex/tree-sitter-liquid/releases/latest/download/tree_sitter_liquid_binding-linux-x64.node"
```

### Using in Your Project

```javascript
const Parser = require('tree-sitter');
const Liquid = require('tree-sitter-liquid');

const parser = new Parser();
parser.setLanguage(Liquid);

const code = `
{% assign name = "World" %}
Hello {{ name }}!
`;

const tree = parser.parse(code);
console.log(tree.rootNode.toString());
```

## Covered

This grammar covers the following Silverfin specific Liquid tags and filters:

- [Result](https://developer.silverfin.com/docs/result)
- [Translations](https://developer.silverfin.com/docs/translations)
- [Push & Pop](https://developer.silverfin.com/docs/push-pop)
- [Locale](https://developer.silverfin.com/docs/locale)

## Development

### Creating a Release

To create a new release with prebuilt binaries:

```bash
# Create and push a new tag (this triggers the release workflow)
git tag v0.6.1
git push origin v0.6.1
```

Or with a message:

```bash
git tag -a v0.6.1 -m "Release description"
git push origin v0.6.1
```

The GitHub Actions workflow will automatically:
- Build Node.js binaries for Linux, macOS, and Windows
- Create a GitHub release
- Upload all `.node` files and checksums as release assets

## Mentions

This repository was originally forked from [tree-sitter-liquid](https://github.com/hankthetank27/tree-sitter-liquid)
