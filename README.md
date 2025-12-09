# Bullets.nvim

A lua port of [bullets.vim](https://github.com/dkarter/bullets.vim)

With additional functions added

## Setup

- Include the plugin using your plugin manager of choice.
- config is a table containing your chosen options (see the code for available options; no helpfile provided at this time).
- Include in your init.lua `require('Bullets').setup({ config })` **or** for Lazy:

## Fork Enhancements

This fork extends `kaymmm/bullets.nvim` with several improvements:

- **Bulk checkbox operations**: commands to check or uncheck all items in the current list, or across all lists in the buffer.
- **Additional keybinding hooks**: new actions are configurable via `config.keys`, letting users assign or disable mappings as needed.
- **Safer mapping behaviour on new buffers**: keybindings are attached only when a normal file buffer is created, avoiding prompts, temporary, or special buffers.
- **More accurate nested-list indentation**: improved demotion/indent logic aligns child bullets with parent content — including multibyte text — and **conforms to common markdownlint list-indentation rules**.

These enhancements improve checkbox handling, mapping consistency, markdownlint-friendly list formatting, and nested-list alignment, while remaining fully compatible with the original plugin.

## Example Setup's

```lua
{
  "thecontinium/bullets.nvim",
  opts = {
    colon_indent = true,
    delete_last_bullet = true,
    empty_buffers = true,
    file_types = { 'markdown', 'text', 'gitcommit' },
    line_spacing = 1,
    mappings = true,
    outline_levels = {'ROM','ABC', 'num', 'abc', 'rom', 'std*', 'std-', 'std+'},
    renumber = true,
    alpha = {
      len = 2,
    },
    checkbox = {
      nest = true,
      markers = ' .oOx',
      toggle_partials = true,
    },
  }
}
```

LazyVim Setup

```lua
  {
    "thecontinium/bullets.nvim",
    ft = "markdown",
    opts = {
      outline_levels = { "num", "std*", "std-", "std+" },
      keys = {
        newline_cr = { key = "<cr>", desc = "Insert New Bullet" },
        newline_o = { key = "o", desc = "Insert New Bullet Below" },
        renumber_visual = { key = "gR", desc = "Renumber Items" },
        renumber_normal = { key = "gR", desc = "Renumber Entire List" },
        toggle_checkbox = { key = "<localleader>xx", desc = "Toggle" },
        check_all = { key = "<localleader>xl", desc = "Entire List" },
        check_all_lists = { key = "<localleader>xb", desc = "Entire Buffer" },
        uncheck_all = { key = "<localleader>ul", desc = "Entire List" },
        uncheck_all_lists = { key = "<localleader>ub", desc = "Entire Buffer" },
        demote_insert = { key = "<C-t>", desc = "Demote Bullet " },
        demote_normal = { key = ">>", desc = "Demote Bullet " },
        demote_visual = { key = ">", desc = "Demote Bullets" },
        promote_insert = { key = "<C-d>", desc = "Promote Bullet" },
        promote_normal = { key = "<<", desc = "Promote Bullet" },
        promote_visual = { key = "<", desc = "Promote Bullets" },
      },
    },
    config = function(_, opts)
      require("Bullets").setup(opts)
      local wk = require("which-key")

      vim.api.nvim_create_autocmd("FileType", {
        pattern = "markdown",
        callback = function()
          wk.add({
            { "<localleader>x", group = "markdown check", buffer = true },
            { "<localleader>u", group = "markdown uncheck", buffer = true },
          })
        end,
      })
    end,
  },

```
