---
title: "Minimal Neovim pt6: Syntax Highlighting with Treesitter"
date: 2024-11-07
---

So far, editing code in my minimal Neovim has been pretty ugly. There is no syntax highlighting available, making reading code slightly annoying. Its funny how much one misses a seemingly minor feature like syntax highlighting until one no longer has it.

Time to install Treesitter, which can not only highlight different elements of code based on what they are (e.g. variables vs function/method names vs class names), but includes many other helpful features, such as folding and indenting.

Whatever I want pretty colours when I edit code, and Treesitter seems to be the way to go.

Time to install another plugin, which means adding a new spec to the plugins directory. I grabbed the below from the LazyNvim reference spec, and added a few more parsers for languages that I frequently work in:

```
--- lua/plugins/treesitter.lua

return {
  "nvim-treesitter/nvim-treesitter",
  build = ":TSUpdate",
  opts = {
    highlight = { enable = true },
    indent = { enable = false },
    ensure_installed = {
      "bash",
      "diff",
      "hcl",
      "html",
      "javascript",
      "json",
      "lua",
      "luadoc",
      "luap",
      "markdown",
      "markdown_inline",
      "regex",
      "ruby",
      "toml",
      "terraform",
      "vim",
      "vimdoc",
      "yaml",
    },
  },
  config = function(_, opts)
    require("nvim-treesitter.configs").setup(opts)
  end,
}
```

I disabled indenting because I recall having some weird indent issues when I write code - sometimes the line gets auto-indented to the appropriate depth, but then as I type, the indent is deleted and the start of the line that I am writing returns to column 0. So I thought maybe there was a collision with indenting being performed by Treesitter and whatever LSP that I am using.

Anyways, the above spec worked great and now my syntax is highlighted nicely.
