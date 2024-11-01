---
title: "Minimal Neovim pt2: Keymaps and which-key"
date: 2024-11-01
---

After installing Neo-tree for directory browsing, I remembered how useless these plugins, and most of Neovim, will be without custom key maps. That is, it would be must better to use `<leader>-e` to open the Neo-tree window rather than running the `:Neotree` command.

To resolve this, my plan was to:
1. Set up a global keymaps configuration
2. Start adding plugin-specific keymaps to each of Lazy's plugin spec files
3. Install the `which-key` plugin to help me recall which keys do what

# Set Up Global Keymaps File

Following the Lazyvim example, I created `lua/config/keymaps.lua` file, starting with a core keymap for saving a file:

```
-- lua/config/keymaps.lua

-- A convenience function for setting keymaps
-- `mode`: the editor modes where the keymap may take effect (string or table)
-- `lhs`: ???
-- `rhs`: ???
-- `opts`: table of additional options ???
function map(mode, lhs, rhs, opts)
  vim.keymap.set(mode, lhs, rhs, opts)
end

-- save file
map({ "i", "x", "n", "s" }, "<C-s>", "<cmd>w<cr><esc>", { desc = "Save File" })

```

With this config, I have a foundation available for creating future global keymaps _plus_ I can now save buffers/files using `<ctrl-s>`.
