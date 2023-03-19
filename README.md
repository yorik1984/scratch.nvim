## Create scratch file

Help you to create tmp playground files, which can be found later, 
with one stroke and without worrying about what's the filename and where to put it.

- With other nvim's goodies.
  - with `treesitter` to have syntax highlighting
  - with `lsp` and `cmp` to have auto-cmp, auto-format and other lsp goodies
  - with `michaelb/sniprun` or `metakirby5/codi.vim` to run scratch file
  
![scratch](https://user-images.githubusercontent.com/95092244/198858745-b3bc9982-e3e8-44fb-b690-7edca030235e.gif)

## Install

using your favorate plugin manager, for example packer

```lua
use {
	"LintaoAmons/scratch.nvim",
	-- tag = "v0.5.0" -- use tag for stability, or without this to have latest fixed and functions
}
```

I will continue add some changes to main branch, so if you meet some issue due to new changes, you can just downgrade to your former version.

## Configuration

### Default Configuration

```lua
require("scratch").setup {
  scratch_file_dir = vim.fn.stdpath("cache") .. "/scratch.nvim",  -- Where the scratch files will be saved
  filetypes = { "xml", "go", "lua", "js", "py", "sh" }, -- you can simply put filetype here
  filetype_details = { -- you can have more control here
    json = {}, -- not required to put this to `filetypes` table, even though you still can
    go = {
      requireDir = true,
      filename = "main",
      content = { "package main", "", "func main() {", "  ", "}" },
      cursor = {
        location = { 4, 2 },
        insert_mode = true
      }
    },
  }
}
```

### Check current Configuration

```lua
:lua require("scratch").checkConfig()
```

### Commands | Keymappings | Functions

No default keymappings, here's functions you can mapping to.

#### Scratch

This can create a new scratch file in your config's `scratch_file_dir`

```lua
vim.keymap.set("n", "<M-C-n>", "<cmd>Scratch<cr>")
-- or
vim.keymap.set("n", "<M-C-n>", function() require("scratch").scratch() end)

```

#### ScratchWithName

This can create a new scratch file with user provided filename (But actually you can use `scratch` to create a file then rename the file)

```lua
vim.keymap.set("n", "<M-C-m>", "<cmd>ScratchWithName<cr>")
-- or
vim.keymap.set("n", "<M-C-m>", function() require("scratch").scratchWithName() end)
```

#### ScratchOpen

This can open an old scratch file in your config's `scratch_file_dir`

```lua
vim.keymap.set("n", "<M-C-o>", "<cmd>ScratchOpen<cr>")
-- or
vim.keymap.set("n", "<M-C-o>", function() require("scratch").openScratch() end)
```

#### ScratchOpenFzf

Fuzzy find the content of your scratch files and open

```lua
vim.keymap.set("n", "<M-C-o>", "<cmd>ScratchOpenFzf<cr>")
-- or
vim.keymap.set("n", "<M-C-o>", function() require("scratch").fzfScratch() end)
```

#### ScratchCheckConfig

This function can print out your current configuration.

I don't think you want to bind this to a shortcut, just use it in command mode to check the config

## Todo

- [x] Template codes when create specific filetype(configurable)
- [x] fzf scratch file content and open
- [x] create user command
