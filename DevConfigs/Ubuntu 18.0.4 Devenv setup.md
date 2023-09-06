## Neovim
[NEOVIM GITHUB](https://github.com/neovim/neovim)
- Installed build requirements outlined in Building Neovim doc
- Cloned neovim
- cd into neovim dir and and ran `make CMAKE_BUILD_TYPE=RelWithDebInfo`
- Ran `cd build && cpack -G DEB && sudo dpkg -i nvim-linux64.deb`

## TMUX
[TMUX GITHUB](https://github.com/tmux/tmux)
- Install build dependencies
	- `sudo apt-get install libevent-dev`
	- `sudo apt-get install ncurses-dev`
- 