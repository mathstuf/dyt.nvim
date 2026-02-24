# dyt.nvim

Neovim plugin for [DictateYourTerms](https://github.com/nicolasayotte/dictate-your-terms) — zero-latency voice dictation inside the editor.

Opens a floating terminal running `dyt --record`, waits for you to speak and press Enter, auto-closes the float, then inserts the transcript at the cursor. Works from both normal and insert mode.

## Prerequisites

- `stt-daemon` must be running before invoking the keymap.
- The `dyt` binary must be on `PATH` in the environment that launches Neovim.

## Installation

**lazy.nvim**

```lua
{
  'nicolasayotte/dyt.nvim',
  opts = {},
}
```

**lazy.nvim (local clone)**

```lua
{
  dir = '/path/to/dyt.nvim',
  opts = {},
}
```

**packer.nvim**

```lua
use 'nicolasayotte/dyt.nvim'
```

**vim-plug**

```vim
Plug 'nicolasayotte/dyt.nvim'
```

The plugin auto-initialises with defaults on startup via `plugin/dyt.lua`. If you call `setup()` yourself before that fires, the shim is a no-op.

## Configuration

Call `require('dyt').setup(opts)`. All keys are optional.

```lua
require('dyt').setup({
  keymap     = '<leader>v',             -- trigger in normal and insert mode
  daemon     = 'http://127.0.0.1:3030', -- stt-daemon address
  win_width  = 0.5,                     -- float width as fraction of editor width
  win_height = 10,                      -- float height in rows
  border     = 'rounded',               -- any nvim_open_win border style
  notify     = true,                    -- emit vim.notify status messages
})
```

With lazy.nvim the same table goes in `opts`:

```lua
{
  'nicolasayotte/dyt.nvim',
  opts = {
    keymap = '<C-r>',
  },
}
```

### Options

| Option       | Type    | Default                    | Description                                           |
|--------------|---------|----------------------------|-------------------------------------------------------|
| `keymap`     | string  | `'<leader>v'`              | Key bound in normal and insert mode. `false` disables.|
| `daemon`     | string  | `'http://127.0.0.1:3030'`  | HTTP base URL of the running `stt-daemon`             |
| `win_width`  | number  | `0.5`                      | Float width as a fraction of the editor width         |
| `win_height` | number  | `10`                       | Float height in rows                                  |
| `border`     | string  | `'rounded'`                | Border style passed to `nvim_open_win`                |
| `notify`     | boolean | `true`                     | Emit `vim.notify` status messages                     |

### Disable the default keymap

```lua
require('dyt').setup({ keymap = false })
-- then bind yourself:
vim.keymap.set('n', '<C-r>', require('dyt').start_dictation)
```

## Behaviour

1. The keymap opens a floating terminal and runs `dyt --record`.
2. Speak. Press Enter in the terminal to stop recording.
3. The float closes automatically.
4. The transcript is read from the system clipboard and inserted at the cursor.
5. A re-entrancy guard prevents a second invocation while the float is open.
6. On non-zero exit, an error notification is shown and state is cleaned up.

## License

MIT
