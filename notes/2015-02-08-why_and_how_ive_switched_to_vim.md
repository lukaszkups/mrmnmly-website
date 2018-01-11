title: Why (and how) I've switched to vim
date: 2015-02-08
tags: Vim, editor, code, programming, ide

## Let's play good & bad cop

For the last couple years I was developing web apps using [Sublime Text](http://www.sublimetext.com/) exclusively. During that time I was also constantly monitoring code editors market and tried some of its newcomers (e.g. github's [atom](https://atom.io/) or adobe's [brackets](http://brackets.io/)), but in the long run I was always coming back to Sublime.

## Cool kids from the block

Besides old habits and laziness about learning new tool that should help me write code I was always curious about those oldschool, antique at the first look, console editors like [emacs](https://www.gnu.org/software/emacs/) or [vim](http://www.vim.org/). There is something magical about these apps - all those badass hackers and world-class conference speakers are using it. Why?

## Back to the roots

Emacs and vim exist on the code editors scene for some time now. That means they are hardened in the (code development) battle. You can find plugins for them for almost any purpose. Their UI's simplicity and harshness means that they can launch in milliseconds. You can also pimp Your editor like a true gangsta and gain some respect in the neighbourhood. Their advanced keymapping options will make Your fingers dance on the keyboard like John Travolta and Karen Lynn Gorner without getting saturday night fever.

## Coders just wanna have fun

In the earliest days of my carreer I had pleasure to work with awesome programmers who used vim as their main tool for code. At that day I was mainly focused to learn programming itself, rather than text editor usage - I think it would be a huge waste of time (especially that I was a beginner programmer).

In my current job some programmers switched from their advanced IDEs to emacs. Their first days of work with new tool were quite funny - they make code many times slower than before, and have problems with handling basic text editor operations :) However, after some time I've noticed significant improvement in their workflow - they're now coding as fast as in the days when they used their IDEs. Now they have tools that are easier to re-setup on every new machine they have to work on, and it uses much less their computer resources. These pros convinced me to give a shot and try something new.

![hobbit_adventure.gif](/public/1514977245626-hobbit_adventure.gif)

## First days of summer

I don't want to start next Text Editors (flame) War, so I'll tell why I've chosen vim over emacs: just because I could :) I've seen how coders are working on both of then and vim's workflow is just more intuitive for me(I think it's very personal taste/preference).

At the moment of writing this sentence I have configured my vim on pretty advanced level - it works (almost) completely like I want it to work (only couple shortcuts are missing but before publishing this post I think my `.vimrc` file will be complete).

If You are curious where to start I can recommend `vimtutor`. It is an interactive, ~30 minutes long lesson which will learn You most of the vim fundamentals. It was my only source of information about vim, before I decided to switch (so You should probably try it right now).

I've configured my vim basing on my current needs - when I've found something really annoying or difficult I just googled how to customize/modify/remove it using `.vimrc` file & its plugins.

## Ladies and gentleman..

Here's my complete `.vimrc` file (state from the day 08/02/2015):

<pre><code class="no-highlight">&quot;vundler config
&quot;
set nocompatible
filetype off 
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#rc()
&quot;vim plugin list
&quot;
&quot;this is required for vim bundler
&quot;
Plugin &#39;gmarik/Vundle.vim&#39;  
Plugin &#39;godlygeek/tabular&#39;
Plugin &#39;jelera/vim-javascript-syntax&#39;
Plugin &#39;ervandew/supertab&#39;
Plugin &#39;vim-scripts/Better-CSS-Syntax-for-Vim&#39;
Plugin &#39;plasticboy/vim-markdown&#39;
Plugin &#39;wincent/command-t&#39;
Plugin &#39;scrooloose/nerdcommenter&#39;
Plugin &#39;docunext/closetag.vim&#39;
Plugin &#39;godlygeek/csapprox&#39;
Plugin &#39;scrooloose/nerdtree&#39;
Plugin &#39;flazz/vim-colorschemes&#39;
Plugin &#39;mattn/emmet-vim&#39;
Plugin &#39;bling/vim-airline&#39;
Plugin &#39;cdmedia/itg_flat_vim&#39;
&quot;vim configuration
&quot;
autocmd vimenter * NERDTree
set tabstop=4
set shiftwidth=4
set softtabstop=4
set expandtab
set number
set t_Co=256
syntax enable
set autoindent
set hlsearch
set ignorecase
colorscheme itg_flat
set encoding=utf-8
set laststatus=2
set esckeys
set timeoutlen=1000 ttimeoutlen=0
set hidden
syntax on
set scrolloff=8
set backup
set backupdir=~/.vim/backups/tmp
set dir=~/.vim/swaps/tmp
set ttyfast
set cursorline
&quot;airline-vim font stuff
&quot;
let g:airline#extensions#tabline#enabled=1
set guifont=Liberation\ Mono\ for\ Powerline:h13
let g:airline_powerline_fonts=1
if !exists(&#39;g:airline_symbols&#39;)
    let g:airline_symbols={}
endif
set fillchars+=stl:\ ,stlnc:\ &quot; 
&quot;
&quot;vim keymap
&quot;
map tn :tabn&lt;CR&gt;
map tp :tabp&lt;CR&gt;
map &lt;C-j&gt; 10j
map &lt;C-k&gt; 10k
map &lt;A-s&gt; :w
nmap &lt;Space&gt; i
nnoremap &lt;C-]&gt;&lt;C-]&gt; :bn&lt;CR&gt;&lt;Esc&gt; 
nnoremap &lt;C-[&gt;&lt;C-[&gt; :bp&lt;CR&gt;&lt;Esc&gt;
nnoremap &lt;C-e&gt; :Explore&lt;CR&gt;
nnoremap &lt;C-[&gt;&lt;C-]&gt; &lt;C-w&gt;&lt;C-w&gt;
nnoremap &lt;Delete&gt; &lt;Delete&gt;i
nnoremap \\ A&lt;Esc&gt;
nnoremap &lt;CR&gt; :noh&lt;CR&gt;&lt;CR&gt;
nnoremap qq :bd&lt;CR&gt;
</code></pre>

## But it's a nightmare! How to handle it?!

I've tried to start working with vim 3 times in total. Previous 2 times was a huge disappointments due to lack of real understanding how to use it.

At first, You have to realise, that there's no point in copy-paste'ing other's people *absolute perfect vimrc configuration* - this is **YOUR** code editor and it should be configured absolutelly just-any-only by YOURSELF. I've read many vim haters blog posts and most of them were using someone's vimrc configs - I had to try code with vim two times before I've realise that.

Secondly - before jumping deep into vim adventure try couple courses - personally (as I've mentioned earlier in this post) `vimtutor` explained me well all vim basics.

And finally - don't use vim because someone told You so. To be honest - I've tried vim because I was bored with my previous (~5 years old) workflow - I knew that I have to change something to have fun again from making code - and I've found vim to be the solution.

![try_vim_racoon.jpg](/public/1514976911582-try_vim_racoon.jpg)

If my story inspired You to use some of the oldschool editors (not necessarily vim) - make me happy and [let me know about it](/about/).

-- mrmnmly








