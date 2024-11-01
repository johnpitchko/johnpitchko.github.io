---
title:  "Minimal Neovim pt1: Factory Reset, Package Management, and File Management"
date:   2024-10-31
---

I have been a Neovim fan for years, although I would consider myself at an intermediate skill level at best. That is, I know how to quite Vim, but have not delved into autocommands, autogroups, or other configuration. Heck, I still haven't used jumplists.

I have relied on packages such as Lunarvim, Astrovim, and Lazyvim (my most recent and favourite) to get me started by establishing a foundational Neovim configuration that is sensible but not too bloated, auto-installing and configuring key packages that transform base Neovim into a powerhouse IDE for software development.

However I recently watched an interview were the founder of the Odin programming language expressed his disdain for LSPs (and package managers as well), claiming that his work is far more productive without the help of an LSP. That got me thinking, "Do I really need an LSP? Is it helping or hurting me?" I then further questioned, "Do I really need all these things that Lazyvim includes? Especially when half of them (completions) either do not fully work or are just annoying?"

So I decided maybe I should ditch the canned configurations all together and perform a factory-reset of my Neovim environment, where each plugin and configuration added is done so because it makes my workflow better. It _should_ also improve my technical skill by learning more about Vim/Neovim and the Lua language.

# Key Objectives

What are the features that I need in Neovim to accomplish my day-to-day job?

1. Cool theme (obviously)
2. Ruby on Rails conveniences
3. Executing unit tests within the editor
4. File explorer/management
5. File and text searching within a project/directory
6. Core IDE features, such as 'Go-to-declaration'/'Go-to-definition'
  * Note I will (for now at least) skip things like autocompletion and intellisense.
7. Format/lint on save
8. Plugin management
9. Git integration
10. Syntax highlighting
11. Status bar

Other functional requirements might arise over time. Let's see how this goes.

# Factory Reset

The first thing to do was removing Lazyvim. Since all configuration and plugins existed in a single directory (`~/.config/nvim`), I archived the old config, purged the directory:

```
$ tar -czvf ~/.config/nvim ~/.config/nvim/lazyvim-backup.tar.gz
$ rm -rf ~/.config/nvim/
```

Bonus: what a fun opportunity to remind myself of `tar` command.

# Install Package Manager

Lazy.nvim seemed like a decent enough and common package manager, so I installed it following the installation steps in the documentation.

Opening Neovim (and ignoring the warning message `No specs found for module 'plugins'`) and running `:Lazy` presented the Lazy.nvim menu:

Lazy can be opened using the command `:Lazy`.

Other commands are intuitive and are marked in the panel: `I` to install new packages, `U` to update packages, etc...

# Install File Manager

I installed Neo-tree using the quickstart example for Lazy on the repo homepage. I dumped the configuration into `~/.config/nvim/plugins/neo-tree.lua` file and installed via Lazy. The `:Neotree` command opened the file explorer sidebar.
