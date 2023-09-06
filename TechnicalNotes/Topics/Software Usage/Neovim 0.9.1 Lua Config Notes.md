

## Keybindings

```vim
vim.keymap.set({mode}, {lhs}, {rhs}, {opts})
```
- `{mode}`: Mode where the keybinding should execute. Can be a list of modes. Modes are specified using their short names, listed below:
	- `n`: Normal
	- `i`: Insert
	- `x`: Visual
	- `s`: Selection
	- `v`: Visual & Selection
	- `t`: Terminal
	- `o`: Operator-pending
	- `''`: Empty string, equivalent to `n` + `v` + `o`
- `{lhs}`: the key you want to bind.
- `{rhs}`: the action you want to execute. Can be a string with a command or an expression. You can also provide a lua function.
- `{opts}`:  A lua table with the following properties:
	- `desc`: A string that describes what the keybinding does.
	- `remap`: A boolean that determines if the keybinding can be recursive. The default is `false`.
	- `buffer`: A boolean or a number. Assigning `true` means the keybinding will only be effective in the current file. If you assign it a number, it must be id of an open buffer.
	- `silent`: A boolean. Determines if the keybinding can show a message. Default value is `false`.
	- `expr`: A boolean. If enabled it gives the ability for vimscript or lua to calculate the value of `{rhs}`. Default value is `false`.