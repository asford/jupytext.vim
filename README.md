# jupytext.vim

[Vim][1]/[Neovim][2] plugin for editing [Jupyter notebook][3] (ipynb) files
through [jupytext][4].

This is a successor to the [`ipynb_notedown.vim` plugin][5].


## Installation

1.  Copy the `jupytext.vim` script to your vim plugin directory (e.g. `$HOME/.vim/plugin`). Refer to `:help add-plugin`, `:help add-global-plugin` and `:help runtimepath` for more details about Vim plugins.
2.  Restart Vim.


## Usage

When you open a Jupyter Notebook (`*.ipynb`) file, it is automatically converted from json to markdown or python through the [`jupytext` utility][4], and the result is loaded into the buffer. Upon saving, the `ipynb` file is updated with any modifications.

In more detail, opening a file `notebook.ipynb` in vim will create a temporary file `notebook.md` or `notebook.py` (depending on `g:jupytext_fmt`). This file is the result of calling e.g.

    jupytext --to=md --output notebook.md notebook.ipynb

The contents of the file is loaded into the buffer instead of the original `notebook.ipynb`. When saving the buffer, its contents is written again to `notebook.md`, and the original `notebook.ipynb` is updated with a call to

    jupytext --to=ipynb --from=md --update --output notebook.ipynb notebook.md

The `--update` flag ensures the output for any cell whose corresponding input in `notebook.md` is unchanged will be preserved.

On closing the buffer, the temporary `notebook.md` will be deleted. If `notebook.md` already exist when opening `notebook.ipynb`, the existing file will be used (instead of being generated by `jupytext`), and it will be preserved when closing the buffer.


## Configuration

The following settings in your `~/.vimrc` may be used to configure the plugin:

*   `g:jupytext_enable=1`

    You may disable the automatic conversion of `ipynb` files (i.e., deactivate this plugin) by setting this to 0.

*   `g:jupytext_fmt='md'`

    One of `'md'` or `'py'`. The format to which to convert the `ipynb` data, and extension of the linked text file.

*   `g:jupytext_filetype_map = {'md': 'markdown', 'py': 'python'}`

    A mapping of `g:jupytext_fmt` to the filetype that should be used for the buffer (`:help filetype`). This determines the syntax highlighting.


[1]: http://www.vim.org
[2]: https://neovim.io
[3]: http://jupyter.org
[4]: https://github.com/mwouts/jupytext
[5]: https://github.com/goerz/ipynb_notedown.vim
