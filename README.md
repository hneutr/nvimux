# NVIMUX

Nvimux maps a set of keybindings that mirror those in TMUX.

It does so by mapping tmuxs keybindings to neovim, using its windows, buffers and terminals.

## Configuring

Nvimux is built on [lua](https://github.com/neovim/neovim/pull/4411), meaning that you must use a somewhat recent version of neovim.

Use lua to configure nvimux.

```lua
lua << EOF
local nvimux = require('nvimux')

-- Nvimux configuration
nvimux.config.set_all{
  prefix = '<C-a>',
  open_term_by_default = true,
  new_window_buffer = 'single',
  quickterm_direction = 'botright',
  quickterm_orientation = 'vertical',
  -- Use 'g' for global quickterm
  quickterm_scope = 't',
  quickterm_size = '80',
}

-- Nvimux custom bindings
nvimux.bindings.bind_all{
  {'s', ':NvimuxHorizontalSplit', {'n', 'v', 'i', 't'}},
  {'v', ':NvimuxVerticalSplit', {'n', 'v', 'i', 't'}},
}

-- Required so nvimux sets the mappings correctly
nvimux.bootstrap()
EOF
```

In case you don't set configuration options, please do run the following for nvimux to work:
```lua
lua require('nvimux').bootstrap()
```

## Credits & Stuff

This plugin is was originally developed by [Henry Kupty](http://github.com/hkupty) and it's completely free to use.
The rationale behind the idea is described [in this article](http://hkupty.github.io/2016/Ditching-TMUX/).

## Purpose of this fork:
There are a couple things I want to address:

- stability: 
	- your configuration should not change much when changes come out.
- bare bones: 
	- there's some fancy (and cool!) 'quickterm' functionality in the
	original repo. That stuff is cool, but to my eye doesn't belong in plugin.
	(Full disclosure: I may be biased, as I don't use that functionality either.)
- consistency/cleanliness: 
	- configuration should do what you think it will. I.e.,
	  `nvimux_open_term_by_default` should effect vertical and horizontal
	  splits, not just tabs.
	- I don't really see a compelling reason to have two separate commands,
	  `nvimux.config.set_all` and `nvimux.bindings.bind_all`. I imagine
	  replacing both of these with something like: `nvimux.config`, which will
	  take a dictionary with two keys, `settings` and `bindings`
- tweaks: 
	- I'd really like a chordal prefix. Save the pinky!

## To Do:
- Add:
	- documentation:
		- on bind_all
			- subsume call to nvimux_custom_bindings
- Fix:
	- variables:
		- name: g:nvimux_open_term_by_default
		- problem: should not behave this way only for prefix-c
- Remove:
	- commands:
		- NvimuxToggleTerm
	- functions:
		- NvimuxToggleTermFunc()
		- NvimuxRawToggleTerm
	- variables:
		- g:nvimux_no_neoterm
		- g:nvimux_quickterm_provider
		- g:nvimux_quickterm_scope
		- g:nvimux_quickterm_direction
		- g:nvimux_quickterm_orientation
		- g:nvimux_quickterm_size
		- g:nvimux_override_{command}
		- g:nvimux_vertical_split
		- g:nvimux_vertical_split
		- g:nvimux_horizontal_split
