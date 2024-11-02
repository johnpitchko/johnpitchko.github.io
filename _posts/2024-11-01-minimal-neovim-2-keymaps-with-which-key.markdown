---
title: "Minimal Neovim pt2: Keymaps and which-key"
date: 2024-11-01
---

After installing Neo-tree for directory browsing, I remembered how useless these plugins, and most of Neovim, will be without custom key maps. That is, it would be must better to use `<leader>-e` to open the Neo-tree window rather than running the `:Neotree` command.

To resolve this, my plan was to:
1. Set up a global keymaps configuration
2. Start adding plugin-specific keymaps to each of Lazy's plugin spec files
3. Install the `which-key` plugin to help me recall which keys do what

# Add Global Keymaps File

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

# Add Plugin-specific Keymaps

One benefit (_I think_) of Lazy.nvim plugin manager is that keymaps defined in the plugin spec are automatically enabled. Adding the following to the Neotree spec was sufficient to enable the keymaps to show/hide the Neotree explorer based in the current working directory.:

```
-- config/plugins/neo-tree.lua

return {
...
    keys = {
        {
          "<leader>fe",
          function()
            require("neo-tree.command").execute({ toggle = true, dir = vim.uv.cwd() })
          end,
          desc = "Explorer NeoTree (cwd)",
        },
        { "<leader>e", "<leader>fe", desc = "Explorer NeoTree (cwd)", remap = true },
    }
...
}

# Install which-key

Adding ths plugin was straightforward - create the plugin spec and install via Lazy. Below is the barebones spec that I added:

```
return {
 "folke/which-key.nvim",
  event = "VeryLazy",
  opts = {
    -- your configuration comes here
    -- or leave it empty to use the default settings
    -- refer to the configuration section below
  },
  keys = {
    {
      "<leader>?",
      function()
        require("which-key").show({ global = false })
      end,
      desc = "Buffer Local Keymaps (which-key)",
    },
  },
}
```

A couple of which-key notes (mostly for my future reference):

1. Keymaps can be grouped together for easier navigation. That is, group all the Git-related keymaps under `G`. Example:

```
        { "<leader>g", group = "git", desc = "Git" },
        { "<leader>gg", "<cmd>LazyGit<cr>", desc = "LazyGit" }
```

After these changes, I can see all availble keymaps simply by pressing my leader key (currently `<space>`). And, now I can open and close the Neotree window with `<leader>e`.
