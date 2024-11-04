---
title: "Minimal Neovim pt5: Basic Options"
date: 2024-11-03
---

In the Minimal Neovim so far, there are a number of basic and _essential_ options that have not been enabled yet, but I am sorely missing. Things like line numbers, my handy colour column, and using spaces instead of tabs. It was time to create the options configuration file.

```lua
--- ~/.config/nvim/lua/config/options.lua


-- Configure Neovim-specific options
-- Neovim options quick reference: https://neovim.io/doc/user/quickref.html#option-list

vim.g.mapleader = " "					                          -- Set leader key to space

local opt = vim.opt

opt.clipboard = vim.env.SSH_TTY and "" or "unnamedplus" -- Sync with system clipboard
opt.colorcolumn = "80" 					                        -- Display coloured columns as a guide for when lines are running too long
opt.confirm = true 					                            -- Confirm to save changes before exiting modified buffer
opt.cursorline = true 					                        -- Enable highlighting of the current line
opt.expandtab = true 					                        -- Use spaces instead of tabs
opt.number = true					                            -- Show line numbers; necessary with `relativenumber` to show the line number of the cursor line
opt.relativenumber = true                                       -- Use relative line numbers; use `<n>j` and `<n>k` to jump up or down `n` lines respectively
opt.shiftround = true 					                        -- Round indents to an even number?
opt.shiftwidth = 2 					                            -- Size of an indent
opt.showmode = false 					                          -- Dont show mode since we have a statusline
opt.signcolumn = "yes" 					                        -- Always show the signcolumn, otherwise it would shift the text each time
opt.smartcase = true 					                          -- Don't ignore case with capitals
opt.smartindent = true 					                        -- Insert indents automatically?
opt.smoothscroll = true
opt.spelllang = { "en" }
opt.splitbelow = true 					                        -- Open new split windows below current
opt.tabstop = 2 					                              -- Number of spaces tabs count for, i.e. 1 indent = 2 spaces
opt.termguicolors = true 				                        -- True color support
opt.undofile = true
opt.undolevels = 10000
opt.virtualedit = "block" 				                      -- Allow cursor to move where there is no text in visual block mode
opt.wrap = true                               					-- Enable line wrap
```

Do not forget to parse this line in the main init Lua file, or else none of your configuration will load (I learned this the hard way):

```lua
--- ~/.config/nvim/init.lua

require("config.lazy")
require("config.keymaps")
require("config.options")
```

Like most other configuration, these options were sourced from Lazyvim. However, I only grabbed the subset of options that I understood - there are a lot of options in that file and I figured its best to grab what I understand/need now then add more options later on based on need. The [official Neovim options quick reference](https://neovim.io/doc/user/quickref.html#option-list) lists descriptions of each option and was a handy reference to understand _exactly_ what each of these options does.
