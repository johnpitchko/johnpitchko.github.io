---
title: "Minimal Neovim pt4: Git integration with Lazygit"
date: 2024-11-02
---

My minimal Neovim configuration is coming along nicely. I can perform basic window management, open and close files with Neotree, and have a great foundation with which-key to configure and easily view all the keymaps I set up.

The next core feature I am missing is Git integration. Presently, everytime I want to add and commit files to my repo, then push to Github, I need to open a separate terminal window to run the commands. This is rather annoying when writing a blog (especially a tech blog) because I am frequently writing new content and updating old stuff, followed by publishing immediately after. Having Git integration within Neovim is a real convenience.

I've been enjoying [Lazygit]() and discovered that LazyVim has built-in support for Lazygit. However, it appears to my inexperienced eyes that its a pretty custom implementation rather than relying on a plugin. I am not keen (at least at the moment) for building this level of customization to embed Lazygit within my Minimal Neovim - that would defeat the purpose of a 'minimal Neovim' after all. Fortunately, I did discover [`lazygit.nvim`](https://github.com/kdheepak/lazygit.nvim) plugin for Neovim.

To install, I used the following spec from the lazygit repo:

```
-- nvim v0.8.0
return {
    "kdheepak/lazygit.nvim",
    lazy = true,
    cmd = {
        "LazyGit",
        "LazyGitConfig",
        "LazyGitCurrentFile",
        "LazyGitFilter",
        "LazyGitFilterCurrentFile",
    },
    -- optional for floating window border decoration
    dependencies = {
        "nvim-lua/plenary.nvim",
    },
    -- setting the keybinding for LazyGit with 'keys' is recommended in
    -- order to load the plugin when the command is run for the first time
    keys = {
        { "<leader>g", group = "git", desc = "Git" },
        { "<leader>gg", "<cmd>LazyGit<cr>", desc = "LazyGit" }
    }
}
```

I made a couple of small modifications from the default. I added a group to which-key to display all the Git keymaps in one place.
