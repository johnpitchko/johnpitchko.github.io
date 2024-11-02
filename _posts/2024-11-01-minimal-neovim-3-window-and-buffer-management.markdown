---
title: "Minimal Neovim pt3: Window and Buffer Management"
date: 2024-11-01
---
The next desperately needed feature is window and buffer management. That is, convenient shortcuts to easily open and navigate between open buffers and windows inside Neovim. 

# Splitting and Closing (Deleting) Windows

Below config is direct from LazyVim:

```
-- windows
map("n", "<leader>w", "<c-w>", { desc = "Windows", remap = true })
map("n", "<leader>-", "<C-W>s", { desc = "Split Window Below", remap = true })
map("n", "<leader>|", "<C-W>v", { desc = "Split Window Right", remap = true })
map("n", "<leader>wd", "<C-W>c", { desc = "Delete Window", remap = true })
```

I used the `<leader>-` and `<leader>|` keys regularly to split windows vertically and horizontally respectively. 

One fun thing about going embarking on this project is picking up so many new shortcuts and features that I never knew before. For example, when ever I had multiple windows open, I always used `:q` to close the active window. But now I see above that I can also use `<leader>wd`, which is more consistent with the other window-management keymaps (i.e. they all use the leader key) _and_ prevents me from accidentally exiting Neovim if I use `:q` on the last open window (instead an error message will be displayed that the last window cannot be closed).

# Buffer Line

Switching between windows/buffers is tricky without knowing which windows/buffers are presently open. The [bufferline.nvim](https://github.com/akinsho/bufferline.nvim) plugin renders open windows in separate 'tabs' at the top of the Neovim editor, highlighting the active buffer and showing all other open buffers.
