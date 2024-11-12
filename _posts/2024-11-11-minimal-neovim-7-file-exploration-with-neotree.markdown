---
title: 'Minimal Neovim pt7: File Exploration with Neotree'
date: 2024-11-11
---

Neotree is a great plugin to use as a file explorer within Neovim. Neotree provides full file and directory management functions; add/remove/rename/move both files and directories, navigate up and down the directory tree, and much more.

Below is my minimal plugin spec, mostly taken from Lazy.nvim:

```lua
return {
  "nvim-neo-tree/neo-tree.nvim",
  cmd = "Neotree",
  branch = "v3.x",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-tree/nvim-web-devicons", -- not strictly required, but recommended
    "MunifTanjim/nui.nvim",
    -- "3rd/image.nvim", -- Optional image support in preview window: See `# Preview Mode` for more information
  },
  keys = {
    {
      "<leader>fe",
      function()
        -- require("neo-tree.command").execute({ toggle = true, dir = LazyVim.root() })
        require("neo-tree.command").execute({ toggle = true, dir = vim.uv.cwd() })
      end,
      desc = "Explorer NeoTree (Root Dir)",
    },
    {
      "<leader>fE",
      function()
        require("neo-tree.command").execute({ toggle = true, dir = vim.uv.cwd() })
      end,
      desc = "Explorer NeoTree (cwd)",
    },
    { "<leader>e", "<leader>fe", desc = "Explorer NeoTree (Root Dir)", remap = true },
    { "<leader>E", "<leader>fE", desc = "Explorer NeoTree (cwd)", remap = true },
  },
  opts = {
    close_if_last_window = true,    -- closes Neovim if all non-Neotree windows are closed (i.e. after closing a window, if Neotree is the last open window, close Neovim).
    popup_border_style = "rounded"  -- fixes top half of popup menu from being cutof
  },
}
```

A few important notes:

## Explore Root Directory

LazyNvim default binds `<leader>e` to open Neotree in the root directory for the project. I believe that means it traverses up the directory tree until it finds the `.git` directory, which is typically placed at the root of a project.

This is a very handy function, however it relies on a custom function for determining the root directory in a project, which I have not found/fully understood yet. Once I do, I will re-enable that keymap.

## Fix Popup Window Render 

Adding or renaming a file in Neotree is supposed to display a popup window in the Neotree window for the user to input the file name. I noticed in my minimal configuration, the top half of this window appears to be missing/cutoff. Upon closer look, the prompt text in the window also appears to be quite dark.

![Popup cutoff in Neotree window of Neovim]({{ site.url }}{{ site.baseurl }}/assets/images/2024-11-11-neotree-popup-cutoff.png)

By chance, I added the option `popup_border_style = "rounded"` as this option is present in Lazyvim and noticed that the popup now displays correctly.

![Popup fixed in Neotree window of Neovim]({{ site.url }}{{ site.baseurl }}/assets/images/2024-11-11-neotree-popup-fixed.png)

Neotree offers great file exporation capabilities, while also being pretty simple to add. Its unfortunate that there does not appear to be a built-in ability to open Neotree to the root project directory, or atleast if there is, it is not implemented in Lazyvim. I did file a [bug report for the cutoff popup window](https://github.com/nvim-neo-tree/neo-tree.nvim/issues/1600) but I cannot confirm if this is a true bug in the code or a conflict with my configuration. Either way, navigating files in projects is now far easier than via the command line.
