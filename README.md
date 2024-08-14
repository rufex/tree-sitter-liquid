# tree-sitter-liquid #

[![Build/test](https://github.com/hankthetank27/tree-sitter-liquid/actions/workflows/ci.yml/badge.svg)](https://github.com/hankthetank27/tree-sitter-liquid/actions/workflows/ci.yml)
[![Lint](https://github.com/hankthetank27/tree-sitter-liquid/actions/workflows/lint.yml/badge.svg)](https://github.com/hankthetank27/tree-sitter-liquid/actions/workflows/lint.yml)

Liquid grammar for [tree-sitter](https://github.com/tree-sitter/tree-sitter).

### Usage in neovim with nvim-treesitter ###

tree-sitter-liquid is included in [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter) and will work out of the box with any files using the `.liquid` extension, injecting HTML over the template file. That being said, liquid also allows for templating in JavaScript, CSS, and SCSS files using the `.js.liquid` `.css.liquid` and `.scss.liquid` file extensions. Since in nvim-treesitter there is no way to distinguish and inject different languages depending on the extension, you can optionally add the following custom query and injections to your neovim configuration to add the correct highlighting for these additional file types.

``` lua

-- custom query predicate for allowing injections based on file extension
require"vim.treesitter.query".add_directive("set-lang-by-filetype!", function (_, _, bufnr, pred, metadata)
    local filename = vim.fn.expand("#"..bufnr..":t")
    local extension_index = filename:find("%.")
    if not extension_index then
        return
    end
    if pred[2] == filename:sub(extension_index + 1) then
        metadata["injection.language"] = pred[3]
    end
end, true)

local liquid_injections = [[
    ((template_content) @injection.content
     (#set-lang-by-filetype! "liquid" "html")
     (#set-lang-by-filetype! "js.liquid" "javascript")
     (#set-lang-by-filetype! "css.liquid" "css")
     (#set-lang-by-filetype! "scss.liquid" "scss")
     (#set! injection.combined))
]]

vim.treesitter.query.set("liquid", "injections", liquid_injections)

```
---

This repository was originally forked from Shopify's archived [tree-sitter-liquid](https://github.com/Shopify/tree-sitter-liquid.git) repository.

