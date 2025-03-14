---
title: Notes on vim
permalink: /vim/
---

## Log
* 2/18/2023 - Found good reasoning and explanation of syntax highlights for vim [here](https://www.cduan.com/technical/vi/vi-4.shtml) 
* 2/25/2023 - Great advanced vim resource especially vimscripting [here](https://learnvimscriptthehardway.stevelosh.com/)
* 3/02/2023 - Cool new tricks in this 14-minute MAKC [Youtube video](https://www.youtube.com/watch?v=B-EPvfxcgl0) titled "My Favorite Vim Tricks". Outline:
	* Tabs, Custom Workspaces, Multi-language Spell Checking, (auto) completon Ctrl-p/n, File Explorers, Visual Block mode, Macros 
* 3/03/2023 - From The Valuable Dev. [A Vim Guide for Advanced Users](https://thevaluable.dev/vim-advanced/) ... part of series. 
	* First article for beginners is [here](https://thevaluable.dev/vim-commands-beginner/).
	* Guide for intermediate users is [here](https://thevaluable.dev/vim-intermediate/)
* 3/03 - [*Vim Tips for the Intermediate Vim User*](https://jemma.dev/blog/intermediate-vim-tips) By Jemma Issroff, starts with talking about mini-golf and then starts goes into interesting examples. 
* 3/04 - From this Hacker News [comment](https://news.ycombinator.com/item?id=33812893)
	* Best user manual and [guide with examples](https://vimhelp.org/usr_01.txt.html#usr_01.txt) is built into the editor.
	* [Table of contents](https://vimhelp.org/usr_toc.txt.html) accessible via *:h user_toc.txt*
	* [Reference Manual](https://vimhelp.org/#reference_toc) accessible via *:h reference_toc*
	* [Cheatsheet](https://vimhelp.org/quickref.txt.html) accessible via *:h quickref*
* 3/05 Famous Stackover Flow [answer from 8/09/2009](https://stackoverflow.com/questions/1218390/what-is-your-most-productive-shortcut-with-vim/1220118#1220118)--epic explanation about how to grok vi.
	* From same thread is this [answer from 2010](https://stackoverflow.com/a/2559262) which has a ton of shortcuts, a starter .vimrc file etc.
* 3/10 Figured out proper autocommands to change colorscheme based on Insert or Command mode.
* 3/11 Decide which new colorschemes to add. Partially inspired by [this YouTube video](https://www.youtube.com/watch?v=7R7LOxOoAw0)
	* [Gruvbox](https://github.com/morhetz/gruvbox)
	* [Solarized](https://ethanschoonover.com/solarized/)
	* [Nord](https://www.nordtheme.com/)
* 3/12 Successfully followed [these instructions](https://www.cyberciti.biz/programming/vim-plug-a-beautiful-and-minimalist-vim-plugin-manager-for-unix-and-linux-users/) to install vim-plug
	* Also installed dracula, codedark, and personal favorite: Kolor.
* 3/21 Lots of progress documented in OneNote. For autocomplete based on other words in the document, go into Insert mode and try Ctrl-n and Ctrl-p. For more, see [this help doc](https://vimdoc.sourceforge.net/htmldoc/insert.html#i_CTRL-N) or [this help doc](https://vimdoc.sourceforge.net/htmldoc/insert.html#ins-completion)
* 3/23 Delighted by typing ci{ or di{ where i refers to "inside" and you can (c)hange or (d)elete everything inside those curly braces.
	* Works for ci* where * = parentheses, quotes, brackets, curly braces, any open/closed tokens.
* 3/25 Need to rewatch this [video](https://www.youtube.com/watch?v=bQfFvExpZDU) on g commands. Off the top of my head:
	* gj and gk in the context of a long line of text which appears visually as a single paragraph allows one to move up and down *within* that paragraph without going to different lines
		* Also works by adding movement so g5j will move 5 lines down within the visual block of text
	* gu [text object] makes everything lowercase. gU [text object] makes everything uppercase.
		* e.g., gu$ makes everything lowercase to the end of the line.
		* e.g., gU5w makes the next 5 words uppercase
* 5/04 [List of vim-friendly apps and utilities](https://github.com/erikw/vim-keybindings-everywhere-the-ultimate-list) and associated [HN thread](https://news.ycombinator.com/item?id=35816361)
* 7/11 Vim's implementation of grep. Some links discussing various flavors of regex related to perl, vim, Basic Regular Expression (BRE) synatx, Extended Regular Expression (ERE) synatx, etc.
	* Very short [comparison of regex flavors](http://vimregex.com/#compare) from this [Guide to regex in vim](http://vimregex.com/)
	* [Stack overflow question from 2010](https://stackoverflow.com/questions/3864467/whats-the-difference-between-vim-regex-and-normal-regex). See this [comment](https://stackoverflow.com/a/14851587) and also use vim *:help perl-patterns*
	* vim's regex mode, invoked by prepending with \v. See vim *:help /\v*
	* See also vim *:help pattern*
* 8/05 - Creator and maintainer of vim [Bram Moolenaar](https://en.wikipedia.org/wiki/Bram_Moolenaar) passed away. :( [HN thread with personal anecdotes](https://en.wikipedia.org/wiki/Bram_Moolenaar)
* 8/27 - Created distinct [page for my sed notes](/sed/)

## 9/16/2023

* Got back into [vim-plug](https://github.com/junegunn/vim-plug) because I want to have proper \*.astro syntax highlighting. Referencing the [vim-astro plugin](https://github.com/wuelnerdotexe/vim-astro). Adapted instructions from this [Linux vim-plug guide](https://www.linuxfordevices.com/tutorials/linux/vim-plug-install-plugins). Main steps: (1) add a new line to `.vimrc`; (2) start new terminal window; and (3) Open a vim file and type `:PlugInstall`.
* I also edited my `.gitignore` file within `/proj-4/a2-astro` so that temporary vim files like `*.swp` and `*.swo` are not tracked/pushed by git, per [these instructions](https://stackoverflow.com/questions/4824188/git-ignore-vim-temporary-files#comment28311078_4824199)
	* Should read more about how [.gitignore works](https://git-scm.com/docs/gitignore)
* Note. I currently am able to indent pretty effectively with the `ctrl-v`, select how many rows with `j`, `shift-I`, type text or tabs to apply to all lines sequence. However, deletion (aka outdenting) doesn't seem to work to well. Reread section 5 [Blockwise operators](https://vimdoc.sourceforge.net/htmldoc/visual.html#blockwise-operators) to see if I can fix this.
	* Another potential [resource](https://vim.fandom.com/wiki/Shifting_blocks_visually)

## 9/24/2023
* to switch immediately to tab number 'n', type `ngt`. e.g, to move to tab 5, type `5gt`.
* when invoking vim on the command line, typing `vim -p filename1.txt filename2.txt` will automatically open desired files all at once, each in its own tab all in the same instance of vim.


## 9/27/2023
* Very handy way of deleting to a `search string` e.g., 'Nashville'. Instead of typing `dtN`, type `d/Nashville` followed by <CR> or `Enter` key. See [this answer](https://vi.stackexchange.com/questions/14459/delete-to-next-search-result)
* Note that to search backwards, `Shift-/` aka `?` works just like usual reverse search. e.g., instead of typing `dTN`, type `d?Nashville` followed by <CR> or `Enter` key. 

## 10/11/2023
* vim has a built in sort utility works very well. If you want to sort all lines `:%sort u`. For more see [this article](https://vim.fandom.com/wiki/Sort_lines#:~:text=Yes%2C%20it%27s%20that%20simple.,%27%3E%20on%20the%20command%20line.)

## 2/05/2024
* Notes on `qq` macro recordings can be found in a7 > History of Technology section > Pasquinelli Chapter 2 *aka* `54-pas-chap2`.
* Notes on new `qq` macro recordings can be found in a7 > Eng > Part II Diallectics *aka* `72-p2`.

## 2/06/2024
* This is how you paste into the `:` command line, officially called the *Ex command line*. Add something to the default register using `y` for yank, e.g., `yl` for 1 letter, `yw` for 1 word.
	* e.g., `yb` for one word backward
	* Then, go to ex cmd line by typing <esc> and typing `:`
	* `<Ctrl> + r` and then type *"* to access the default register
	* Can type `"a` to access the **a** register
* For more detailed instructions in how to enter in escape/control characters, see [this comment](https://stackoverflow.com/questions/3997078/how-to-paste-yanked-text-into-the-vim-command-line)

## 2/15/2024
* Began thinking of transitioning from vim to Neovim. See comparisons in this [Baeldung Linux article](https://www.baeldung.com/linux/vim-vs-neovim)


## 6/25/2024
* When using the `:%s` regex, remember that `\n` refers to the newlines in the search field, and `\r` refers to newlines in the replace field.
	* So for example, if you want to replace *text* \<newline\> with *text* **;** \<newline\>, you would type `%s|\n|;\r|gc`.
* Use [this article](https://www.brianstorti.com/vim-registers/) to understand how to add and retrieve characters from registers. For cut and paste. 
	* For example, to add everyting from the cursor to the end of the line `$` to the register `a`, type `"ay$`. B/c y = (y)ank and $ indicates the end of the current line.
	* Then, to paste what's in the register `a`, simply type `"ap`.

## 7/07/2024
* Repeated instructions on how to store and paste with register
#### Example 1
* to yank next 3 words and store in register **a**, type `"ay3w`.
* to paste item in register **a**, type `"ap`.
#### Example 2
* to yank from current cursor to end of line and store in register **b**, type `"by$`.
* to paste item in register **b**, type `"bp`.

## 7/09/2024
* Equivalent to **Save As...** in macOS / Windows / Office. Type `:w {pathname}/{NEW filename}` will write current file contents into the NEW file. Note that this does *not* save current contents into the current file so you must type `:w` separately to make sure that happens. See more [here](https://stackoverflow.com/a/4980194).

***

## 8/03/2024
* Let's install LSP server and relevant plugins for syntax highlighting snd CoC code completion for TypeScript and React
* Note: `:bd` in vim clears the current buffer (aka closes the window like if you are in PlugInstall) without quitting vim. Before this, I was using `:q` to quit vim entirely to clear away PlugInstall. For more, see [Stack Overflow](https://stackoverflow.com/a/23592407)

### Steps
1. Watched this YouTube [video](https://youtu.be/n6JEqPuWOxg?si=hI6hUuiYtQym2EFJ&t=51) by [Nir Lichtman](https://www.youtube.com/@nirlichtman) at 51 seconds. You can see his [.vimrc file](https://github.com/nir9/welcome/blob/86d44256e856fede939ba33088f2631b3335cb5e/.vimrc) at GitHub
1. Edit my own `.vimrc` file
1. Make sure these plug-ins are included within the `call plug#begin( expand() )` and `call plug#end()` lines. 

```vim
Plug 'prabirshrestha/vim-lsp'
Plug 'mattn/vim-lsp-settings'
```
1. Hm. Looks like I may need to upgrade my version of vim which is currently at 9.0. But CoC requires 9.0.0438 per [these instructions](https://github.com/neoclide/coc.nvim/wiki/Install-coc.nvim#requirements). 
1. So I will use brew to update my vim. Currently using default that came with macOS, stored in `/usr/bin/vim`. 
1. Went through `brew update; doctor; upgrade` cycle for all machines.
1. Now installing vim using `brew install vim`. For more context, see the [Homebrew vim page](https://formulae.brew.sh/formula/vim)
1. Success. Now, running updated vim version 9.1 (02 Jan 2024)
	* On x86, running from the  `/usr/local/bin/vim` directory . 
	* On arm64 Apple Silicon, running from the  `/opt/homebrew/bin/vim` directory .

### More steps
* Open up vim, and run plug install with `:PlugInstall` and choose Yes to install the new vim plugins.
* Next time you open up any particular filetype with a `*.c`, `*.js`, `*.ts`, etc. type **:LspInstallServer** and press `Y` for yes. This will ensure that the desired Language Server is installed.
* To disable everything, just go to the .vimrc file and comment out the 2 lines for the lsp plugins: prabir.../vim-lisp` and `mattn/vim-lsp-settings`.
* No need to rerun :PlugInstall, uninstall, etc, it will all be turned off.
* Also, looks like there is a TypeScript LSP that automatically pops up when I open `*.js` files. But *not* any default JS Lsp's.
* Ok got all machines working. Can easily toggle on/off lsp functionality by commenting on/off 2 plugins in `.vimrc`.

***

## 8/31/2024
* Let's install neovim so i can take advantage of code completion etc for TypeScript, Vue, and React projects.
* Reran usual brew hygeine commands, see OneNote

## Some tutorials for today's setup
1. Feb 2024 - [Ultimate Vim Vue Setup](https://pragmaticpineapple.com/ultimate-vim-vue-setup/). Vim, not neovim
1. Feb 2024- YouTube by Dreams of Code: [The perfect Neovim setup for Next.js (it's back)](https://www.youtube.com/watch?v=8um8OYwvz3c)


## Notes on Neovim setup from Dreams of Code tutorial
### Part 1: Initial setup
1. Installing latest stable build of neovim, release 0.10. In video, they are using 0.9.4.
1. Installed with `brew install neovim`
1. Updated .vimrc file for shortcut for nvim commands
1. In addition to installing neovim, need to install **git** and **nerdfonts**. Both are installed already.
1. Next, go with basic config. [DoC](https://youtu.be/8um8OYwvz3c?si=_khivyr_ukthnrER&t=86) recomends NVChad.
	* config file usually lives at `~/.config/nvim`
	* command to clone NVChad: `git clone -b v2.0 https://github.com/NvChad/NvChad ~/.config/nvim --depth 1`
	* creates **~/.config/nvim** directory.
1. To quickly switch the color theme, in *Cmd* mode, just type `<space>th`
	* CoD recommends 'catpuccino' theme
	* Because many themes break my macOS Terminal setup, i chose **pastelbeans** which seems to work OK in both Alacritty and Terminal. 
	* Also don't mind **decay** on iMac display. Note, need to type `:match Error /\t/` to reactivate tab coloring

### Part 2: Configuring for JS and TS
1. Starting at 2:27, [CoD](https://youtu.be/8um8OYwvz3c?si=453isFitqTzkH81g&t=147) talks about what's needed.
1. LSP install. Navigate to `~/.config/nvim/lua/custom/`
	* Edit the `.../nvim/lua/custom/chadrc.lua` file. Add these lines below the `M.ui = { theme = 'pastelbeans' }`: 
	```lua
	M.plugins = "custom.plugins"
	return M
    ```
***

3. Create a new **plugins.lua** file in that location like this: `~/.config/nvim/lua/custom/plugins.lua`
4. Verify that this is entered into `.../nvim/lua/custom/plugins.lua`. **Note that you must edit this file again below to make sure the TypeScript LSP is installed**

```lua
local plugins = {
  {
    "neovim/nvim-lspconfig",
    config = function()
      require "plugins.configs.lspconfig"
    end,
  }
}
return plugins
```
***
5. Create a file named **lspconfig.lua** and store in `.../nvim/lua/custom/configs/lspconfig.lua` and add these contents. **Note that this is *one level down* with a new *configs* subdirectory!**

```lua
local base = require("plugins.configs.lspconfig")
local on_attach = base.on_attach
local capabilities = base.capabilities

local lspconfig = require("lspconfig")

lspconfig.tsserver.setup({
  on_attach = on_attach,
  capabilities = capabilities,
})
```
***
6. Now to install the TypeScript lsp server. There are 2 ways of doing this:
    1. Using brew or other package managers on my local machine to download. Or perhaps use the PlugInstall for vim.
    1. Use the nvim specific installer **mason.nvim**. Advantage of this method is that this follows our config to another machine. Let's use *mason.nvim*.
7. So let's edit `.../nvim/lua/custom/plugins.lua` and add new lines ensuring that the typescript server is installed. **Here is the final version of the `plugins.lua` file up to this point:**

```lua
local plugins = {
  {
    "neovim/nvim-lspconfig",
    config = function()
      require "plugins.configs.lspconfig"
    end,
  },
  {
    "williambowman/mason.nvim",
    opts = {
      ensure_installed = {
        "typescript-language-server",
      }
    }
  }
}
return plugins
```
***
8. Now, let's quit *nvim* and reopen it to reload our plugins.
9. Type `:MasonInstallAll` and we will see the LSPs for **Lua** and **Typescript** being installed.
10. After that, autocomplete is ready to go for lua and TS. We can verify this is working by going into any JS or TS file and typing `:LspInfo` which will show that the server is installed. Also, by typing in standard JS/TS keywords will show have autocomplete working.

***
11. Not sure if I need this, but I added `"vue-language-server",` so the complete version of `.../nvim/lua/custom/plugins.lua` is:

```lua

local plugins = {
  {
    "neovim/nvim-lspconfig",
    config = function()
      require "plugins.configs.lspconfig"
    end,
  },
  {
    "williambowman/mason.nvim",
    opts = {
      ensure_installed = {
        "typescript-language-server",
        "vue-language-server",
      }
    }
  }
}
return plugins
```

12. and also within nvim, typed `:MasonInstall vue-language-server`.
### Part 3: Instructions on setting up autocomplete for Tailwind.css
* Starts at [6:30](https://youtu.be/8um8OYwvz3c?si=-_h0ZbqVgs7tCHfW&t=390)

### Part 4: Instructions for installing ESlint
* Starts at [7:29](https://youtu.be/8um8OYwvz3c?si=Pdvjjm9IvXNokTmA&t=449)

### Part 5: Instructions for installing Prettier
* Starts at [10:02](https://www.youtube.com/watch?v=8um8OYwvz3c&t=602s)

### Part 6: Instructions for installing HTML auto tag closers
* Starts at [12:39](https://youtu.be/8um8OYwvz3c?si=d66SdgoShr4wgH4K&t=759)

***

## 9/01/2024
* Commented out legacy LSP plugins from .vimrc because I'm relying on Mason, etc. in NVChad.
* Tried out various new color themes (see OneN).
* On champ, installed vue LSP with command `MasonInstall vue-language-server`. Hopefully this handles most cases and I don't need to still install volar or tree-sitter

### Vim folding
* Based on [this article](https://vim.fandom.com/wiki/Folding), one can manually fold with `zf{motion}`.
	* Handy to use this to automatically make indent aware folding (regardless of tabs or spaces). `:setlocal foldmethod=indent`.
	* After that, `zo` to open a fold and `zc` to close a fold, for wherever the cursor is.
	* At some point, perhaps explore folding based on syntax `:setlocal foldmethod=syntax`

***
### Relative line numbering isn't working in Neovim
* I asked phind and got [this answer](https://www.phind.com/search?cache=tmz8kq336ddce3nz7vyvdiwx)
* Here is what works in my `~/.vimrc` file:

```
" Turn on absolute line numbers
set number

" Turn on relative iine numbers
set relativenumber
```

* According to phind, these are the equivalent lines I need to enter into my `~/.config/nvim/init.lua` file:

```
-- Enable line numbers
vim.opt.number = true

-- Enable relative line numbers
vim.opt.relativenumber = true
```

***

## 9/08/2024
### vim relative line numbers
* To toggle between relative line numbers on or off, use **!** at end.
	* **`set rnu!`** shorthand command
	* *:set relativenumber!* unabbreviated version
* To turn off/on directly
	* **`set rnu`** shorthand to turn on
	* *:set relativenumber* to turn on (unabbreviated command)
	* **`set nornu`** shorthand to turn off
	* *:set norelativenumber* to turn off (unabbreviated command)

### vim absoluteline numbers
* To toggle between having line numbers on or off, use **!** at end.
	* **`set nu!`** shorthand command
	* *:set number!* unabbreviated version
* To turn off/on directly
	* **`set nu`** shorthand to turn on
	* *:set number* to turn on (unabbreviated command)
	* **`set nonu`** shorthand to turn off
	* *:set nonumber* to turn off (unabbreviated command)

***

## 12/30/2024
* While playing around with tabs/spaces/indents in a Scheme program, two simple commands. 
	* **`:set ruler`** to turn on column/line number display in bottom right.
	* **`xx |`** (pipe) jumps the cursor to the xx column. e.g., to jump to the 24th column on the current line, type **`23 |`**.
	* Note that column numbers are 1-indexed rather than zero-indexed. So if each tab is 2 spaces, the proper indent for each successive indent is `1, 3, 5, 7, etc.`.

***

## 1/25/2025
* Vim / NeoVim plugin by [Georgi Gerganov](https://ggerganov.com), creator of llama.cpp, whisper.cpp, and many other projects. [HN thread](https://news.ycombinator.com/item?id=42806328), [legacy about page](https://github.com/ggml-org/llama.vim) which has helpful intro. [Latest llama.vim page](https://github.com/ggml-org/llama.vim)
	* [December 2024 paper](https://arxiv.org/abs/2412.16589) explaining code completion, benchmarking Fill-In-the-Middle (FIM). FIM gathers context both before and after where the cursor is, in contrast to older methods that only have context of the stuff before the cursor (aka "left to right" prefix-only completion). 

## 2/08/2025
* vim browser links below
* I've started playing around with vim motions in the browser, esp. for macOS. First step has been installing the [vimari](https://televator.net/vimari/) Safari extension. I'll also try the [vimb](https://fanglingsu.github.io/vimb/). Both of the above use [WebKit 2](https://en.wikipedia.org/wiki/WebKit#WebKit2).
* I'll also check the Chrome extension [Vimium](https://vimium.github.io) on Chrome and Firefox. And probably install [Qutebrowser](https://www.qutebrowser.org) to see how I like it. I found the list of *Similar Projects* on the Qutebrowser site to be very helpful.
* These explorations were encouraged by this [vim broswer blog post from 2017](https://blog.al4.co.nz/2017/10/vimperator-vimium-and-the-switch-to-qutebrowser/) and more recently by ['A mouseless tale: trying for a keyboard-driven desktop'](https://lwn.net/Articles/1005332/) with related [HN thread](https://news.ycombinator.com/item?id=42884099).


## 3/14/2025 test
