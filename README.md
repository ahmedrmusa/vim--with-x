# Configure Vim --with-x
---
Compiling a custom vim to support +xterm_clipboard support for Unix systems.
This will include (`vim --version`)
```
+client-server
+clipboard
+X11
+xterm_clipboard
+etc...
```

## 1. Uninstall /usr/local/bin/vim
### If you have Homebrew installed
`brew uninstall vim`
> Run `brew doctor` to check for any issues.

### If not consider [installing homebrew.](https://brew.sh/)


> __Do Not Remove__`/usr/bin/vim`

## 2. Clone the latest vim repo

    git clone https://github.com/vim/vim.git && cd /vim


## 3. Configuration flags:
> Use --disable-darwin incase of "Quickdraw.h error".

For more options : `less vim/src/feature.h` , `:help feature-list` or [Vim Docs](http://vimdoc.sourceforge.net/htmldoc/eval.html#feature-list).
> Example : `--with-features=huge` : Includes the most features

    ./configure --with-x


## 4. Installing our configured vim

    sudo make & make install
    
## 5. Run the right vim
__Verify:__
`which vim` outputs: `/usr/local/bin/vim`

__If not:__
Adding the following snipet to your `~/.zshrc` or `~/.bashrc` will allow `echo $PATH` variable to locate __vim__ from `/usr/local/bin/` *not* `/usr/bin/`

    export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:$PATH"
> __Re-launch Terminal__

## To verify :

`type -a vim` should locate dirs of all vim instances
```
vim is /usr/local/bin/vim
vim is /usr/bin/vim
```
 
`which vim` should locate our installed vim in
```
/usr/local/bin/vim
```

## ! TO UNINSTALL VIM !
    make uninstall
---

# X11 Support
## Server-side 
- `xauth` program
- `/etc/ssh/ssh_config` contains `ForwardX11 yes`

## Client-side (Unix)
- `XQuartz.app` installed 
- `~/.ssh/config` contains
```
Host *
    ForwardX11 yes
```
> This will allow running graphical applications remotely without the need to add -X


## To verify :

    ssh user@hostname & xterm

> This will open the server's graphical terminal. If not consult [___ssh docs___](https://linux.die.net/man/1/ssh) & [___x docs___](https://www.x.org/wiki/Documentation/).

# Configure clipboard
## Server & Client 
- `vim --version` supports `+xterm_clipboard`

## Client-side (Unix)
The `unnamed "*"` & `unnamedplus "+"` register will sync to system clipboard for MacOS and Windows.
While the `unnamedplus "+"` register will sync to linux system clipboard and the other "selection" clipboard is mapped to `unnamed "*"`.
To use cross-platform vim's system clipboard and "selection" clipboard, edit server-side and client-side `.vimrc` to include :

    set clipboard^=unnamed,unnamedplus

> This setting sets 'clipboard' option to prepend the "string" values.

# Copy/Paste

- `Ctrl+C` in other programs
- `p` to all vim platforms.


- `y` yank in Vim
- `Ctrl+V` in other programs on all platforms.
---
