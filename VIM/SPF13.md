**The VIM**

  

- spf13 mods

- .vimrc.bundles.local  
    Bundle 'OmniSharp/omnisharp-vim'
- Bundle 'w0rp/ale'
- Bundle 'prabirshrestha/asyncomplete.vim'
- Bundle 'prabirshrestha/async.vim'
- Bundle 'prabirshrestha/vim-lsp'
- Bundle 'prabirshrestha/asyncomplete-lsp.vim'
- .vimrc.local  
    set nospell

- "let g:OmniSharp_server_path = '/Users/sandeepdivekar/Documents/code/omnisharp-osx/run'
- let g:OmniSharp_server_use_mono=1
- let g:OmniSharp_start_without_solution = 1
- let g:OmniSharp_server_stdio = 1
- let g:OmniSharp_highlight_types = 3
- let g:OmniSharp_highlight_groups = {
- let g:OmniSharp_selector_ui = 'ctrlp'  " Use ctrlp.vim

- \ 'csUserIdentifier': [
- \   'constant name', 'enum member name', 'field name', 'identifier',
- \   'local name', 'parameter name', 'property name', 'static symbol'],
- \ 'csUserInterface': ['interface name'],
- \ 'csUserMethod': ['extension method name', 'method name'],
- \ 'csUserType': ['class name', 'enum name', 'namespace name', 'struct name']
- \}
- let g:OmniSharp_highlight_debug = 1

- " Use the vim-plug plugin manager: [https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)
- " Remember to run :PlugInstall when loading this vimrc for the first time, so
- " vim-plug downloads the plugins listed.
- "silent! if plug#begin('~/.vim/plugged')
- "Plug 'OmniSharp/omnisharp-vim'
- "Plug 'w0rp/ale'
- "call plug#end()
- "endif

- " Note: this is required for the plugin to work
- filetype indent plugin on

- " Use the stdio OmniSharp-roslyn server
- let g:OmniSharp_server_stdio = 1

- " Set the type lookup function to use the preview window instead of echoing it
- let g:OmniSharp_typeLookupInPreview = 1

- " Timeout in seconds to wait for a response from the server
- let g:OmniSharp_timeout = 5

- " Don't autoselect first omnicomplete option, show options even if there is only
- " one (so the preview documentation is accessible). Remove 'preview' if you
- " don't want to see any documentation whatsoever.
- set completeopt=longest,menuone,preview

- " Fetch full documentation during omnicomplete requests.
- " By default, only Type/Method signatures are fetched. Full documentation can
- " still be fetched when you need it with the :OmniSharpDocumentation command.
- "let g:omnicomplete_fetch_full_documentation = 1

- " Set desired preview window height for viewing documentation.
- " You might also want to look at the echodoc plugin.
- set previewheight=5

- " Tell ALE to use OmniSharp for linting C# files, and no other linters.
- let g:ale_linters = { 'cs': ['OmniSharp'] }

- " Update semantic highlighting after all text changes
- let g:OmniSharp_highlight_types = 3
- " Update semantic highlighting on BufEnter and InsertLeave
- " let g:OmniSharp_highlight_types = 2

- augroup omnisharp_commands
-     autocmd!

-     " Show type information automatically when the cursor stops moving.
-     " Note that the type is echoed to the Vim command line, and will overwrite
-     " any other messages in this space including e.g. ALE linting messages.
-     autocmd CursorHold *.cs OmniSharpTypeLookup

-     " The following commands are contextual, based on the cursor position.
-     autocmd FileType cs nnoremap <buffer> gd :OmniSharpGotoDefinition<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fi :OmniSharpFindImplementations<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fs :OmniSharpFindSymbol<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fu :OmniSharpFindUsages<CR>

-     " Finds members in the current buffer
-     autocmd FileType cs nnoremap <buffer> <Leader>fm :OmniSharpFindMembers<CR>

-     autocmd FileType cs nnoremap <buffer> <Leader>fx :OmniSharpFixUsings<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>tt :OmniSharpTypeLookup<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>dc :OmniSharpDocumentation<CR>
-     autocmd FileType cs nnoremap <buffer> <C-\> :OmniSharpSignatureHelp<CR>
-     autocmd FileType cs inoremap <buffer> <C-\> <C-o>:OmniSharpSignatureHelp<CR>

-     " Navigate up and down by method/property/field
-     autocmd FileType cs nnoremap <buffer> <C-k> :OmniSharpNavigateUp<CR>
-     autocmd FileType cs nnoremap <buffer> <C-j> :OmniSharpNavigateDown<CR>

-     " Find all code errors/warnings for the current solution and populate the quickfix window
-     autocmd FileType cs nnoremap <buffer> <Leader>cc :OmniSharpGlobalCodeCheck<CR>
- augroup END

- " Contextual code actions (uses fzf, CtrlP or unite.vim when available)
- nnoremap <Leader><Space> :OmniSharpGetCodeActions<CR>
- " Run code actions with text selected in visual mode to extract method
- xnoremap <Leader><Space> :call OmniSharp#GetCodeActions('visual')<CR>

- " Rename with dialog
- nnoremap <Leader>nm :OmniSharpRename<CR>
- nnoremap <F2> :OmniSharpRename<CR>
- " Rename without dialog - with cursor on the symbol to rename: `:Rename newname`
- command! -nargs=1 Rename :call OmniSharp#RenameTo("<args>")

- nnoremap <Leader>cf :OmniSharpCodeFormat<CR>

- " Start the omnisharp server for the current solution
- nnoremap <Leader>ss :OmniSharpStartServer<CR>
- nnoremap <Leader>sp :OmniSharpStopServer<CR>

- " Enable snippet completion
- " let g:OmniSharp_want_snippet=1
- .vimrc.before.local  
    let g:spf13_bundle_groups=['general', 'writing', 'programming', 'python', 'html', 'misc',]

- Plugins

- Windows

- create main directories: $HOME\vimfiles\autoload, $HOME\vimfiles\bundle  
    mkdir -p ~\vimfiles\autoload ~\vimfiles\bundle
- save pathogen to '$HOME\vimfiles\bundle' directory  
    save https://raw.githubusercontent.com/tpope/vim-pathogen/master/autoload/pathogen.vim to $HOME\vimfiles\autoload
- install ack (via chocolatey plugin manager)  
    choco install ack 
- follow methods (zip, git with and git without submodules) to install plugins  
    https://gist.github.com/romainl/9970697
- download zip method

- download bundles from https://github.com/spf13/spf13-vim/blob/3.0/.vimrc.bundles and unzip to $HOME\vimfiles\bundle

- scrooloose/nerdtree
- altercation/vim-colors-solarized
- spf13/vim-colors (copy to colors folder under vim81/colors folder
- tpope/vim-surround
- tpope/vim-repeat
- rhysd/conflict-marker.vim
- jiangmiao/auto-pairs
- ctrlpvim/ctrlp.vim
- tacahiroy/ctrlp-funky
- terryma/vim-multiple-cursors
- vim-scripts/sessionman.vim
- matchit
- Lokaltog/powerline
- powerline/fonts (use the powershell script to install fonts)
- bling/vim-bufferline
- jistr/vim-nerdtree-tabs
- flazz/vim-colorschemes
- mbbill/undotree
- nathanaelkane/vim-indent-guides
- tpope/vim-abolish.git
- osyo-manga/vim-over
- gcmt/wildfire.vim
- scrooloose/syntastic
- vim-scripts/EasyClip
- mhinz/vim-signify
- Valloric/YouCompleteMe

- .vimrc  
    execute pathogen#infect()

- filetype plugin indent on
- syntax on
- " Modeline and Notes {
- " vim: set sw=4 ts=4 sts=4 et tw=78 foldmarker={,} foldlevel=0 foldmethod=marker spell:
- "
- "                    __ _ _____              _
- "         ___ _ __  / _/ |___ /      __   __(_)_ __ ___
- "        / __| '_ \| |_| | |_ \ _____\ \ / /| | '_ ` _ \
- "        \__ \ |_) |  _| |___) |_____|\ V / | | | | | | |
- "        |___/ .__/|_| |_|____/        \_/  |_|_| |_| |_|
- "            |_|
- "
- "   This is the personal .vimrc file of Steve Francia.
- "   While much of it is beneficial for general use, I would
- "   recommend picking out the parts you want and understand.
- "
- "   You can find me at http://spf13.com
- "
- "   Copyright 2014 Steve Francia
- "
- "   Licensed under the Apache License, Version 2.0 (the "License");
- "   you may not use this file except in compliance with the License.
- "   You may obtain a copy of the License at
- "
- "       http://www.apache.org/licenses/LICENSE-2.0
- "
- "   Unless required by applicable law or agreed to in writing, software
- "   distributed under the License is distributed on an "AS IS" BASIS,
- "   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
- "   See the License for the specific language governing permissions and
- "   limitations under the License.
- " }

- " Environment {

-     " Identify platform {
-         silent function! OSX()
-             return has('macunix')
-         endfunction
-         silent function! LINUX()
-             return has('unix') && !has('macunix') && !has('win32unix')
-         endfunction
-         silent function! WINDOWS()
-             return  (has('win32') || has('win64'))
-         endfunction
-     " }

-     " Basics {
-         set nocompatible        " Must be first line
-         if !WINDOWS()
-             set shell=/bin/sh
-         endif
-     " }

-     " Windows Compatible {
-         " On Windows, also use '.vim' instead of 'vimfiles'; this makes synchronization
-         " across (heterogeneous) systems easier.
-         if WINDOWS()
-           set runtimepath=$HOME/.vim,$VIM/vimfiles,$VIMRUNTIME,$VIM/vimfiles/after,$HOME/.vim/after
-         endif
-     " }

-     " Arrow Key Fix {
-         " https://github.com/spf13/spf13-vim/issues/780
-         if &term[:4] == "xterm" || &term[:5] == 'screen' || &term[:3] == 'rxvt'
-             inoremap <silent> <C-[>OC <RIGHT>
-         endif
-     " }

- " }

- " Use before config if available {
-     if filereadable(expand("~/.vimrc.before"))
-         source ~/.vimrc.before
-     endif
- " }

- " Use bundles config {
-     if filereadable(expand("~/.vimrc.bundles"))
-         source ~/.vimrc.bundles
-     endif
- " }

- " General {

-     set background=dark         " Assume a dark background

-     " Allow to trigger background
-     function! ToggleBG()
-         let s:tbg = &background
-         " Inversion
-         if s:tbg == "dark"
-             set background=light
-         else
-             set background=dark
-         endif
-     endfunction
-     noremap <leader>bg :call ToggleBG()<CR>

-     " if !has('gui')
-         "set term=$TERM          " Make arrow and other keys work
-     " endif
-     filetype plugin indent on   " Automatically detect file types.
-     syntax on                   " Syntax highlighting
-     set mouse=a                 " Automatically enable mouse usage
-     set mousehide               " Hide the mouse cursor while typing
-     scriptencoding utf-8

-     if has('clipboard')
-         if has('unnamedplus')  " When possible use + register for copy-paste
-             set clipboard=unnamed,unnamedplus
-         else         " On mac and Windows, use * register for copy-paste
-             set clipboard=unnamed
-         endif
-     endif

-     " Most prefer to automatically switch to the current file directory when
-     " a new buffer is opened; to prevent this behavior, add the following to
-     " your .vimrc.before.local file:
-     "   let g:spf13_no_autochdir = 1
-     if !exists('g:spf13_no_autochdir')
-         autocmd BufEnter * if bufname("") !~ "^\[A-Za-z0-9\]*://" | lcd %:p:h | endif
-         " Always switch to the current file directory
-     endif

-     "set autowrite                       " Automatically write a file when leaving a modified buffer
-     set shortmess+=filmnrxoOtT          " Abbrev. of messages (avoids 'hit enter')
-     set viewoptions=folds,options,cursor,unix,slash " Better Unix / Windows compatibility
-     set virtualedit=onemore             " Allow for cursor beyond last character
-     set history=1000                    " Store a ton of history (default is 20)
-     set spell                           " Spell checking on
-     set hidden                          " Allow buffer switching without saving
-     set iskeyword-=.                    " '.' is an end of word designator
-     set iskeyword-=#                    " '#' is an end of word designator
-     set iskeyword-=-                    " '-' is an end of word designator

-     " Instead of reverting the cursor to the last position in the buffer, we
-     " set it to the first line when editing a git commit message
-     au FileType gitcommit au! BufEnter COMMIT_EDITMSG call setpos('.', [0, 1, 1, 0])

-     " http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session
-     " Restore cursor to file position in previous editing session
-     " To disable this, add the following to your .vimrc.before.local file:
-     "   let g:spf13_no_restore_cursor = 1
-     if !exists('g:spf13_no_restore_cursor')
-         function! ResCur()
-             if line("'\"") <= line("$")
-                 silent! normal! g`"
-                 return 1
-             endif
-         endfunction

-         augroup resCur
-             autocmd!
-             autocmd BufWinEnter * call ResCur()
-         augroup END
-     endif

-     " Setting up the directories {
-         set backup                  " Backups are nice ...
-         if has('persistent_undo')
-             set undofile                " So is persistent undo ...
-             set undolevels=1000         " Maximum number of changes that can be undone
-             set undoreload=10000        " Maximum number lines to save for undo on a buffer reload
-         endif

-     " }

- " }

- " Vim UI {

-     if !exists('g:override_spf13_bundles') && filereadable(expand("~/.vim/bundle/vim-colors-solarized/colors/solarized.vim"))
-         let g:solarized_termcolors=256
-         let g:solarized_termtrans=1
-         let g:solarized_contrast="normal"
-         let g:solarized_visibility="normal"
-         color solarized             " Load a colorscheme
-         syntax enable
-         set background=dark
-         colorscheme=solarized
-     endif

-     color solarized             " Load a colorscheme
-     syntax enable
-     set background=dark

-     set tabpagemax=15               " Only show 15 tabs
-     set showmode                    " Display the current mode

-     set cursorline                  " Highlight current line

-     highlight clear SignColumn      " SignColumn should match background
-     highlight clear LineNr          " Current line number row will have same background color in relative mode
-     "highlight clear CursorLineNr    " Remove highlight color from current line number

-     if has('cmdline_info')
-         set ruler                   " Show the ruler
-         set rulerformat=%30(%=\:b%n%y%m%r%w\ %l,%c%V\ %P%) " A ruler on steroids
-         set showcmd                 " Show partial commands in status line and
-                                     " Selected characters/lines in visual mode
-     endif

-     if has('statusline')
-         set laststatus=2

-         " Broken down into easily includeable segments
-         set statusline=%<%f\                     " Filename
-         set statusline+=%w%h%m%r                 " Options
-         set statusline+=\ [%{&ff}/%Y]            " Filetype
-         set statusline+=\ [%{getcwd()}]          " Current dir
-         set statusline+=%=%-14.(%l,%c%V%)\ %p%%  " Right aligned file nav info
-     endif

-     set backspace=indent,eol,start  " Backspace for dummies
-     set linespace=0                 " No extra spaces between rows
-     set number                      " Line numbers on
-     set showmatch                   " Show matching brackets/parenthesis
-     set incsearch                   " Find as you type search
-     set hlsearch                    " Highlight search terms
-     set winminheight=0              " Windows can be 0 line high
-     set ignorecase                  " Case insensitive search
-     set smartcase                   " Case sensitive when uc present
-     set wildmenu                    " Show list instead of just completing
-     set wildmode=list:longest,full  " Command <Tab> completion, list matches, then longest common part, then all.
-     set whichwrap=b,s,h,l,<,>,[,]   " Backspace and cursor keys wrap too
-     set scrolljump=5                " Lines to scroll when cursor leaves screen
-     set scrolloff=3                 " Minimum lines to keep above and below cursor
-     set foldenable                  " Auto fold code
-     set list
-     set listchars=tab:›\ ,trail:•,extends:#,nbsp:. " Highlight problematic whitespace

- " }

- " Formatting {

-     set nowrap                      " Do not wrap long lines
-     set autoindent                  " Indent at the same level of the previous line
-     set shiftwidth=4                " Use indents of 4 spaces
-     set expandtab                   " Tabs are spaces, not tabs
-     set tabstop=4                   " An indentation every four columns
-     set softtabstop=4               " Let backspace delete indent
-     set nojoinspaces                " Prevents inserting two spaces after punctuation on a join (J)
-     set splitright                  " Puts new vsplit windows to the right of the current
-     set splitbelow                  " Puts new split windows to the bottom of the current
-     "set matchpairs+=<:>             " Match, to be used with %
-     set pastetoggle=<F12>           " pastetoggle (sane indentation on pastes)
-     "set comments=sl:/*,mb:*,elx:*/  " auto format comment blocks
-     " Remove trailing whitespaces and ^M chars
-     " To disable the stripping of whitespace, add the following to your
-     " .vimrc.before.local file:
-     "   let g:spf13_keep_trailing_whitespace = 1
-     autocmd FileType c,cpp,java,go,php,javascript,puppet,python,rust,twig,xml,yml,perl,sql autocmd BufWritePre <buffer> if !exists('g:spf13_keep_trailing_whitespace') | call StripTrailingWhitespace() | endif
-     "autocmd FileType go autocmd BufWritePre <buffer> Fmt
-     autocmd BufNewFile,BufRead *.html.twig set filetype=html.twig
-     autocmd FileType haskell,puppet,ruby,yml setlocal expandtab shiftwidth=2 softtabstop=2
-     " preceding line best in a plugin but here for now.

-     autocmd BufNewFile,BufRead *.coffee set filetype=coffee

-     " Workaround vim-commentary for Haskell
-     autocmd FileType haskell setlocal commentstring=--\ %s
-     " Workaround broken colour highlighting in Haskell
-     autocmd FileType haskell,rust setlocal nospell

- " }

- " Key (re)Mappings {

-     " The default leader is '\', but many people prefer ',' as it's in a standard
-     " location. To override this behavior and set it back to '\' (or any other
-     " character) add the following to your .vimrc.before.local file:
-     "   let g:spf13_leader='\'
-     if !exists('g:spf13_leader')
-         let mapleader = ','
-     else
-         let mapleader=g:spf13_leader
-     endif
-     if !exists('g:spf13_localleader')
-         let maplocalleader = '_'
-     else
-         let maplocalleader=g:spf13_localleader
-     endif

-     " The default mappings for editing and applying the spf13 configuration
-     " are <leader>ev and <leader>sv respectively. Change them to your preference
-     " by adding the following to your .vimrc.before.local file:
-     "   let g:spf13_edit_config_mapping='<leader>ec'
-     "   let g:spf13_apply_config_mapping='<leader>sc'
-     if !exists('g:spf13_edit_config_mapping')
-         let s:spf13_edit_config_mapping = '<leader>ev'
-     else
-         let s:spf13_edit_config_mapping = g:spf13_edit_config_mapping
-     endif
-     if !exists('g:spf13_apply_config_mapping')
-         let s:spf13_apply_config_mapping = '<leader>sv'
-     else
-         let s:spf13_apply_config_mapping = g:spf13_apply_config_mapping
-     endif

-     " Easier moving in tabs and windows
-     " The lines conflict with the default digraph mapping of <C-K>
-     " If you prefer that functionality, add the following to your
-     " .vimrc.before.local file:
-     "   let g:spf13_no_easyWindows = 1
-     if !exists('g:spf13_no_easyWindows')
-         map <C-J> <C-W>j<C-W>_
-         map <C-K> <C-W>k<C-W>_
-         map <C-L> <C-W>l<C-W>_
-         map <C-H> <C-W>h<C-W>_
-     endif

-     " Wrapped lines goes down/up to next row, rather than next line in file.
-     noremap j gj
-     noremap k gk

-     " End/Start of line motion keys act relative to row/wrap width in the
-     " presence of `:set wrap`, and relative to line for `:set nowrap`.
-     " Default vim behaviour is to act relative to text line in both cases
-     " If you prefer the default behaviour, add the following to your
-     " .vimrc.before.local file:
-     "   let g:spf13_no_wrapRelMotion = 1
-     if !exists('g:spf13_no_wrapRelMotion')
-         " Same for 0, home, end, etc
-         function! WrapRelativeMotion(key, ...)
-             let vis_sel=""
-             if a:0
-                 let vis_sel="gv"
-             endif
-             if &wrap
-                 execute "normal!" vis_sel . "g" . a:key
-             else
-                 execute "normal!" vis_sel . a:key
-             endif
-         endfunction

-         " Map g* keys in Normal, Operator-pending, and Visual+select
-         noremap $ :call WrapRelativeMotion("$")<CR>
-         noremap <End> :call WrapRelativeMotion("$")<CR>
-         noremap 0 :call WrapRelativeMotion("0")<CR>
-         noremap <Home> :call WrapRelativeMotion("0")<CR>
-         noremap ^ :call WrapRelativeMotion("^")<CR>
-         " Overwrite the operator pending $/<End> mappings from above
-         " to force inclusive motion with :execute normal!
-         onoremap $ v:call WrapRelativeMotion("$")<CR>
-         onoremap <End> v:call WrapRelativeMotion("$")<CR>
-         " Overwrite the Visual+select mode mappings from above
-         " to ensure the correct vis_sel flag is passed to function
-         vnoremap $ :<C-U>call WrapRelativeMotion("$", 1)<CR>
-         vnoremap <End> :<C-U>call WrapRelativeMotion("$", 1)<CR>
-         vnoremap 0 :<C-U>call WrapRelativeMotion("0", 1)<CR>
-         vnoremap <Home> :<C-U>call WrapRelativeMotion("0", 1)<CR>
-         vnoremap ^ :<C-U>call WrapRelativeMotion("^", 1)<CR>
-     endif

-     " The following two lines conflict with moving to top and
-     " bottom of the screen
-     " If you prefer that functionality, add the following to your
-     " .vimrc.before.local file:
-     "   let g:spf13_no_fastTabs = 1
-     if !exists('g:spf13_no_fastTabs')
-         map <S-H> gT
-         map <S-L> gt
-     endif

-     " Stupid shift key fixes
-     if !exists('g:spf13_no_keyfixes')
-         if has("user_commands")
-             command! -bang -nargs=* -complete=file E e<bang> <args>
-             command! -bang -nargs=* -complete=file W w<bang> <args>
-             command! -bang -nargs=* -complete=file Wq wq<bang> <args>
-             command! -bang -nargs=* -complete=file WQ wq<bang> <args>
-             command! -bang Wa wa<bang>
-             command! -bang WA wa<bang>
-             command! -bang Q q<bang>
-             command! -bang QA qa<bang>
-             command! -bang Qa qa<bang>
-         endif

-         cmap Tabe tabe
-     endif

-     " Yank from the cursor to the end of the line, to be consistent with C and D.
-     nnoremap Y y$

-     " Code folding options
-     nmap <leader>f0 :set foldlevel=0<CR>
-     nmap <leader>f1 :set foldlevel=1<CR>
-     nmap <leader>f2 :set foldlevel=2<CR>
-     nmap <leader>f3 :set foldlevel=3<CR>
-     nmap <leader>f4 :set foldlevel=4<CR>
-     nmap <leader>f5 :set foldlevel=5<CR>
-     nmap <leader>f6 :set foldlevel=6<CR>
-     nmap <leader>f7 :set foldlevel=7<CR>
-     nmap <leader>f8 :set foldlevel=8<CR>
-     nmap <leader>f9 :set foldlevel=9<CR>

-     " Most prefer to toggle search highlighting rather than clear the current
-     " search results. To clear search highlighting rather than toggle it on
-     " and off, add the following to your .vimrc.before.local file:
-     "   let g:spf13_clear_search_highlight = 1
-     if exists('g:spf13_clear_search_highlight')
-         nmap <silent> <leader>/ :nohlsearch<CR>
-     else
-         nmap <silent> <leader>/ :set invhlsearch<CR>
-     endif

-     " Find merge conflict markers
-     map <leader>fc /\v^[<\|=>]{7}( .*\|$)<CR>

-     " Shortcuts
-     " Change Working Directory to that of the current file
-     cmap cwd lcd %:p:h
-     cmap cd. lcd %:p:h

-     " Visual shifting (does not exit Visual mode)
-     vnoremap < <gv
-     vnoremap > >gv

-     " Allow using the repeat operator with a visual selection (!)
-     " http://stackoverflow.com/a/8064607/127816
-     vnoremap . :normal .<CR>

-     " For when you forget to sudo.. Really Write the file.
-     cmap w!! w !sudo tee % >/dev/null

-     " Some helpers to edit mode
-     " http://vimcasts.org/e/14
-     cnoremap %% <C-R>=fnameescape(expand('%:h')).'/'<cr>
-     map <leader>ew :e %%
-     map <leader>es :sp %%
-     map <leader>ev :vsp %%
-     map <leader>et :tabe %%

-     " Adjust viewports to the same size
-     map <Leader>= <C-w>=

-     " Map <Leader>ff to display all lines with keyword under cursor
-     " and ask which one to jump to
-     nmap <Leader>ff [I:let nr = input("Which one: ")<Bar>exe "normal " . nr ."[\t"<CR>

-     " Easier horizontal scrolling
-     map zl zL
-     map zh zH

-     " Easier formatting
-     nnoremap <silent> <leader>q gwip

-     " FIXME: Revert this f70be548
-     " fullscreen mode for GVIM and Terminal, need 'wmctrl' in you PATH
-     map <silent> <F11> :call system("wmctrl -ir " . v:windowid . " -b toggle,fullscreen")<CR>

- " }

- " Plugins {

-     " Misc {
-         if isdirectory(expand("~/.vim/bundle/nerdtree"))
-             let g:NERDShutUp=1
-         endif
-         if isdirectory(expand("~/.vim/bundle/matchit.zip"))
-             let b:match_ignorecase = 1
-         endif
-     " }

-     " OmniComplete {
-         " To disable omni complete, add the following to your .vimrc.before.local file:
-         "   let g:spf13_no_omni_complete = 1
-         if !exists('g:spf13_no_omni_complete')
-             if has("autocmd") && exists("+omnifunc")
-                 autocmd Filetype *
-                     \if &omnifunc == "" |
-                     \setlocal omnifunc=syntaxcomplete#Complete |
-                     \endif
-             endif

-             hi Pmenu  guifg=#000000 guibg=#F8F8F8 ctermfg=black ctermbg=Lightgray
-             hi PmenuSbar  guifg=#8A95A7 guibg=#F8F8F8 gui=NONE ctermfg=darkcyan ctermbg=lightgray cterm=NONE
-             hi PmenuThumb  guifg=#F8F8F8 guibg=#8A95A7 gui=NONE ctermfg=lightgray ctermbg=darkcyan cterm=NONE

-             " Some convenient mappings
-             "inoremap <expr> <Esc>      pumvisible() ? "\<C-e>" : "\<Esc>"
-             if exists('g:spf13_map_cr_omni_complete')
-                 inoremap <expr> <CR>     pumvisible() ? "\<C-y>" : "\<CR>"
-             endif
-             inoremap <expr> <Down>     pumvisible() ? "\<C-n>" : "\<Down>"
-             inoremap <expr> <Up>       pumvisible() ? "\<C-p>" : "\<Up>"
-             inoremap <expr> <C-d>      pumvisible() ? "\<PageDown>\<C-p>\<C-n>" : "\<C-d>"
-             inoremap <expr> <C-u>      pumvisible() ? "\<PageUp>\<C-p>\<C-n>" : "\<C-u>"

-             " Automatically open and close the popup menu / preview window
-             au CursorMovedI,InsertLeave * if pumvisible() == 0|silent! pclose|endif
-             set completeopt=menu,preview,longest
-         endif
-     " }

-     " Ctags {
-         set tags=./tags;/,~/.vimtags

-         " Make tags placed in .git/tags file available in all levels of a repository
-         let gitroot = substitute(system('git rev-parse --show-toplevel'), '[\n\r]', '', 'g')
-         if gitroot != ''
-             let &tags = &tags . ',' . gitroot . '/.git/tags'
-         endif
-     " }

-     " AutoCloseTag {
-         " Make it so AutoCloseTag works for xml and xhtml files as well
-         au FileType xhtml,xml ru ftplugin/html/autoclosetag.vim
-         nmap <Leader>ac <Plug>ToggleAutoCloseMappings
-     " }

-     " SnipMate {
-         " Setting the author var
-         " If forking, please overwrite in your .vimrc.local file
-         let g:snips_author = 'Steve Francia <[steve.francia@gmail.com](mailto:steve.francia@gmail.com)>'
-     " }

-     " NerdTree {
-         if isdirectory(expand("~/.vim/bundle/nerdtree"))
-             map <C-e> <plug>NERDTreeTabsToggle<CR>
-             map <leader>e :NERDTreeFind<CR>
-             nmap <leader>nt :NERDTreeFind<CR>

-             let NERDTreeShowBookmarks=1
-             let NERDTreeIgnore=['\.py[cd]$', '\~$', '\.swo$', '\.swp$', '^\.git$', '^\.hg$', '^\.svn$', '\.bzr$']
-             let NERDTreeChDirMode=0
-             let NERDTreeQuitOnOpen=1
-             let NERDTreeMouseMode=2
-             let NERDTreeShowHidden=1
-             let NERDTreeKeepTreeInNewTab=1
-             let g:nerdtree_tabs_open_on_gui_startup=0
-         endif
-     " }

-     " Tabularize {
-         if isdirectory(expand("~/.vim/bundle/tabular"))
-             nmap <Leader>a& :Tabularize /&<CR>
-             vmap <Leader>a& :Tabularize /&<CR>
-             nmap <Leader>a= :Tabularize /^[^=]*\zs=<CR>
-             vmap <Leader>a= :Tabularize /^[^=]*\zs=<CR>
-             nmap <Leader>a=> :Tabularize /=><CR>
-             vmap <Leader>a=> :Tabularize /=><CR>
-             nmap <Leader>a: :Tabularize /:<CR>
-             vmap <Leader>a: :Tabularize /:<CR>
-             nmap <Leader>a:: :Tabularize /:\zs<CR>
-             vmap <Leader>a:: :Tabularize /:\zs<CR>
-             nmap <Leader>a, :Tabularize /,<CR>
-             vmap <Leader>a, :Tabularize /,<CR>
-             nmap <Leader>a,, :Tabularize /,\zs<CR>
-             vmap <Leader>a,, :Tabularize /,\zs<CR>
-             nmap <Leader>a<Bar> :Tabularize /<Bar><CR>
-             vmap <Leader>a<Bar> :Tabularize /<Bar><CR>
-         endif
-     " }

-     " Session List {
-         set sessionoptions=blank,buffers,curdir,folds,tabpages,winsize
-         if isdirectory(expand("~/.vim/bundle/sessionman.vim/"))
-             nmap <leader>sl :SessionList<CR>
-             nmap <leader>ss :SessionSave<CR>
-             nmap <leader>sc :SessionClose<CR>
-         endif
-     " }

-     " JSON {
-         nmap <leader>jt <Esc>:%!python -m json.tool<CR><Esc>:set filetype=json<CR>
-         let g:vim_json_syntax_conceal = 0
-     " }

-     " PyMode {
-         " Disable if python support not present
-         if !has('python') && !has('python3')
-             let g:pymode = 0
-         endif

-         if isdirectory(expand("~/.vim/bundle/python-mode"))
-             let g:pymode_lint_checkers = ['pyflakes']
-             let g:pymode_trim_whitespaces = 0
-             let g:pymode_options = 0
-             let g:pymode_rope = 0
-         endif
-     " }

-     " ctrlp {
-         if isdirectory(expand("~/.vim/bundle/ctrlp.vim/"))
-             let g:ctrlp_working_path_mode = 'ra'
-             nnoremap <silent> <D-t> :CtrlP<CR>
-             nnoremap <silent> <D-r> :CtrlPMRU<CR>
-             let g:ctrlp_custom_ignore = {
-                 \ 'dir':  '\.git$\|\.hg$\|\.svn$',
-                 \ 'file': '\.exe$\|\.so$\|\.dll$\|\.pyc$' }

-             if executable('ag')
-                 let s:ctrlp_fallback = 'ag %s --nocolor -l -g ""'
-             elseif executable('ack-grep')
-                 let s:ctrlp_fallback = 'ack-grep %s --nocolor -f'
-             elseif executable('ack')
-                 let s:ctrlp_fallback = 'ack %s --nocolor -f'
-             " On Windows use "dir" as fallback command.
-             elseif WINDOWS()
-                 let s:ctrlp_fallback = 'dir %s /-n /b /s /a-d'
-             else
-                 let s:ctrlp_fallback = 'find %s -type f'
-             endif
-             if exists("g:ctrlp_user_command")
-                 unlet g:ctrlp_user_command
-             endif
-             let g:ctrlp_user_command = {
-                 \ 'types': {
-                     \ 1: ['.git', 'cd %s && git ls-files . --cached --exclude-standard --others'],
-                     \ 2: ['.hg', 'hg --cwd %s locate -I .'],
-                 \ },
-                 \ 'fallback': s:ctrlp_fallback
-             \ }

-             if isdirectory(expand("~/.vim/bundle/ctrlp-funky/"))
-                 " CtrlP extensions
-                 let g:ctrlp_extensions = ['funky']

-                 "funky
-                 nnoremap <Leader>fu :CtrlPFunky<Cr>
-             endif
-         endif
-     "}

-     " TagBar {
-         if isdirectory(expand("~/.vim/bundle/tagbar/"))
-             nnoremap <silent> <leader>tt :TagbarToggle<CR>
-         endif
-     "}

-     " Rainbow {
-         if isdirectory(expand("~/.vim/bundle/rainbow/"))
-             let g:rainbow_active = 1 "0 if you want to enable it later via :RainbowToggle
-         endif
-     "}

-     " YouCompleteMe {
-             let g:acp_enableAtStartup = 0

-             " enable completion from tags
-             let g:ycm_collect_identifiers_from_tags_files = 1

-             " remap Ultisnips for compatibility for YCM
-             let g:UltiSnipsExpandTrigger = '<C-j>'
-             let g:UltiSnipsJumpForwardTrigger = '<C-j>'
-             let g:UltiSnipsJumpBackwardTrigger = '<C-k>'

-             " Enable omni completion.
-             autocmd FileType css setlocal omnifunc=csscomplete#CompleteCSS
-             autocmd FileType html,markdown setlocal omnifunc=htmlcomplete#CompleteTags
-             autocmd FileType javascript setlocal omnifunc=javascriptcomplete#CompleteJS
-             autocmd FileType python setlocal omnifunc=pythoncomplete#Complete
-             autocmd FileType xml setlocal omnifunc=xmlcomplete#CompleteTags
-             autocmd FileType ruby setlocal omnifunc=rubycomplete#Complete
-             autocmd FileType haskell setlocal omnifunc=necoghc#omnifunc

-             " Haskell post write lint and check with ghcmod
-             " $ `cabal install ghcmod` if missing and ensure
-             " ~/.cabal/bin is in your $PATH.
-             if !executable("ghcmod")
-                 autocmd BufWritePost *.hs GhcModCheckAndLintAsync
-             endif

-             " For snippet_complete marker.
-             if !exists("g:spf13_no_conceal")
-                 if has('conceal')
-                     set conceallevel=2 concealcursor=i
-                 endif
-             endif

-             " Disable the neosnippet preview candidate window
-             " When enabled, there can be too much visual noise
-             " especially when splits are used.
-             set completeopt-=preview
-     " }

-     " neocomplete {
-             let g:acp_enableAtStartup = 0
-             let g:neocomplete#enable_at_startup = 1
-             let g:neocomplete#enable_smart_case = 1
-             let g:neocomplete#enable_auto_delimiter = 1
-             let g:neocomplete#max_list = 15
-             let g:neocomplete#force_overwrite_completefunc = 1

-             " Define dictionary.
-             let g:neocomplete#sources#dictionary#dictionaries = {
-                         \ 'default' : '',
-                         \ 'vimshell' : $HOME.'/.vimshell_hist',
-                         \ 'scheme' : $HOME.'/.gosh_completions'
-                         \ }

-             " Define keyword.
-             if !exists('g:neocomplete#keyword_patterns')
-                 let g:neocomplete#keyword_patterns = {}
-             endif
-             let g:neocomplete#keyword_patterns['default'] = '\h\w*'

-             " Plugin key-mappings {
-                 " These two lines conflict with the default digraph mapping of <C-K>
-                 if !exists('g:spf13_no_neosnippet_expand')
-                     imap <C-k> <Plug>(neosnippet_expand_or_jump)
-                     smap <C-k> <Plug>(neosnippet_expand_or_jump)
-                 endif
-                 if exists('g:spf13_noninvasive_completion')
-                     inoremap <CR> <CR>
-                     " <ESC> takes you out of insert mode
-                     inoremap <expr> <Esc>   pumvisible() ? "\<C-y>\<Esc>" : "\<Esc>"
-                     " <CR> accepts first, then sends the <CR>
-                     inoremap <expr> <CR>    pumvisible() ? "\<C-y>\<CR>" : "\<CR>"
-                     " <Down> and <Up> cycle like <Tab> and <S-Tab>
-                     inoremap <expr> <Down>  pumvisible() ? "\<C-n>" : "\<Down>"
-                     inoremap <expr> <Up>    pumvisible() ? "\<C-p>" : "\<Up>"
-                     " Jump up and down the list
-                     inoremap <expr> <C-d>   pumvisible() ? "\<PageDown>\<C-p>\<C-n>" : "\<C-d>"
-                     inoremap <expr> <C-u>   pumvisible() ? "\<PageUp>\<C-p>\<C-n>" : "\<C-u>"
-                 else
-                     " <C-k> Complete Snippet
-                     " <C-k> Jump to next snippet point
-                     imap <silent><expr><C-k> neosnippet#expandable() ?
-                                 \ "\<Plug>(neosnippet_expand_or_jump)" : (pumvisible() ?
-                                 \ "\<C-e>" : "\<Plug>(neosnippet_expand_or_jump)")
-                     smap <TAB> <Right><Plug>(neosnippet_jump_or_expand)

-                     inoremap <expr><C-g> neocomplete#undo_completion()
-                     inoremap <expr><C-l> neocomplete#complete_common_string()
-                     "inoremap <expr><CR> neocomplete#complete_common_string()

-                     " <CR>: close popup
-                     " <s-CR>: close popup and save indent.
-                     inoremap <expr><s-CR> pumvisible() ? neocomplete#smart_close_popup()."\<CR>" : "\<CR>"

-                     function! CleverCr()
-                         if pumvisible()
-                             if neosnippet#expandable()
-                                 let exp = "\<Plug>(neosnippet_expand)"
-                                 return exp . neocomplete#smart_close_popup()
-                             else
-                                 return neocomplete#smart_close_popup()
-                             endif
-                         else
-                             return "\<CR>"
-                         endif
-                     endfunction

-                     " <CR> close popup and save indent or expand snippet
-                     imap <expr> <CR> CleverCr()
-                     " <C-h>, <BS>: close popup and delete backword char.
-                     inoremap <expr><BS> neocomplete#smart_close_popup()."\<C-h>"
-                     inoremap <expr><C-y> neocomplete#smart_close_popup()
-                 endif
-                 " <TAB>: completion.
-                 inoremap <expr><TAB> pumvisible() ? "\<C-n>" : "\<TAB>"
-                 inoremap <expr><S-TAB> pumvisible() ? "\<C-p>" : "\<TAB>"

-                 " Courtesy of Matteo Cavalleri

-                 function! CleverTab()
-                     if pumvisible()
-                         return "\<C-n>"
-                     endif
-                     let substr = strpart(getline('.'), 0, col('.') - 1)
-                     let substr = matchstr(substr, '[^ \t]*$')
-                     if strlen(substr) == 0
-                         " nothing to match on empty string
-                         return "\<Tab>"
-                     else
-                         " existing text matching
-                         if neosnippet#expandable_or_jumpable()
-                             return "\<Plug>(neosnippet_expand_or_jump)"
-                         else
-                             return neocomplete#start_manual_complete()
-                         endif
-                     endif
-                 endfunction

-                 imap <expr> <Tab> CleverTab()
-             " }

-             " Enable heavy omni completion.
-             if !exists('g:neocomplete#sources#omni#input_patterns')
-                 let g:neocomplete#sources#omni#input_patterns = {}
-             endif
-             let g:neocomplete#sources#omni#input_patterns.php = '[^. \t]->\h\w*\|\h\w*::'
-             let g:neocomplete#sources#omni#input_patterns.perl = '\h\w*->\h\w*\|\h\w*::'
-             let g:neocomplete#sources#omni#input_patterns.c = '[^.[:digit:] *\t]\%(\.\|->\)'
-             let g:neocomplete#sources#omni#input_patterns.cpp = '[^.[:digit:] *\t]\%(\.\|->\)\|\h\w*::'
-             let g:neocomplete#sources#omni#input_patterns.ruby = '[^. *\t]\.\h\w*\|\h\w*::'
-     " }

-     " FIXME: Isn't this for Syntastic to handle?
-     " Haskell post write lint and check with ghcmod
-     " $ `cabal install ghcmod` if missing and ensure
-     " ~/.cabal/bin is in your $PATH.
-     if !executable("ghcmod")
-         autocmd BufWritePost *.hs GhcModCheckAndLintAsync
-     endif

-     " UndoTree {
-         if isdirectory(expand("~/.vim/bundle/undotree/"))
-             nnoremap <Leader>u :UndotreeToggle<CR>
-             " If undotree is opened, it is likely one wants to interact with it.
-             let g:undotree_SetFocusWhenToggle=1
-         endif
-     " }

-     " indent_guides {
-         if isdirectory(expand("~/.vim/bundle/vim-indent-guides/"))
-             let g:indent_guides_start_level = 2
-             let g:indent_guides_guide_size = 1
-             let g:indent_guides_enable_on_vim_startup = 1
-         endif
-     " }

-     " Wildfire {
-     let g:wildfire_objects = {
-                 \ "*" : ["i'", 'i"', "i)", "i]", "i}", "ip"],
-                 \ "html,xml" : ["at"],
-                 \ }
-     " }

-     " vim-airline {
-         " Set configuration options for the statusline plugin vim-airline.
-         " Use the powerline theme and optionally enable powerline symbols.
-         " To use the symbols ?, ?, ?, ?, ?, ?, and ?.in the statusline
-         " segments add the following to your .vimrc.before.local file:
-         "   let g:airline_powerline_fonts=1
-         " If the previous symbols do not render for you then install a
-         " powerline enabled font.

-         " See `:echo g:airline_theme_map` for some more choices
-         " Default in terminal vim is 'dark'
-         if isdirectory(expand("~/.vim/bundle/vim-airline-themes/"))
-             if !exists('g:airline_theme')
-                 let g:airline_theme = 'solarized'
-             endif
-             if !exists('g:airline_powerline_fonts')
-                 " Use the default set of separators with a few customizations
-                 let g:airline_left_sep='›'  " Slightly fancier than '>'
-                 let g:airline_right_sep='‹' " Slightly fancier than '<'
-             endif
-         endif
-     " }

- " }

- " GUI Settings {

-     " GVIM- (here instead of .gvimrc)
-     if has('gui_running')
-         set guioptions-=T           " Remove the toolbar
-         set lines=40                " 40 lines of text instead of 24
-         if !exists("g:spf13_no_big_font")
-             if LINUX() && has("gui_running")
-                 set guifont=Andale\ Mono\ Regular\ 12,Menlo\ Regular\ 11,Consolas\ Regular\ 12,Courier\ New\ Regular\ 14
-             elseif OSX() && has("gui_running")
-                 set guifont=Andale\ Mono\ Regular:h12,Menlo\ Regular:h11,Consolas\ Regular:h12,Courier\ New\ Regular:h14
-             elseif WINDOWS() && has("gui_running")
-                 set guifont=Andale_Mono:h10,Menlo:h10,Consolas:h10,Courier_New:h10
-             endif
-         endif
-     else
-         if &term == 'xterm' || &term == 'screen'
-             set t_Co=256            " Enable 256 colors to stop the CSApprox warning and make xterm vim shine
-         endif
-         "set term=builtin_ansi       " Make arrow and other keys work
-     endif

- " }

- " Functions {

-     " Initialize directories {
-     function! InitializeDirectories()
-         let parent = $HOME
-         let prefix = 'vim'
-         let dir_list = {
-                     \ 'backup': 'backupdir',
-                     \ 'views': 'viewdir',
-                     \ 'swap': 'directory' }

-         if has('persistent_undo')
-             let dir_list['undo'] = 'undodir'
-         endif

-         " To specify a different directory in which to place the vimbackup,
-         " vimviews, vimundo, and vimswap files/directories, add the following to
-         " your .vimrc.before.local file:
-         "   let g:spf13_consolidated_directory = <full path to desired directory>
-         "   eg: let g:spf13_consolidated_directory = $HOME . '/.vim/'
-         if exists('g:spf13_consolidated_directory')
-             let common_dir = g:spf13_consolidated_directory . prefix
-         else
-             let common_dir = parent . '/.' . prefix
-         endif

-         for [dirname, settingname] in items(dir_list)
-             let directory = common_dir . dirname . '/'
-             if exists("*mkdir")
-                 if !isdirectory(directory)
-                     call mkdir(directory)
-                 endif
-             endif
-             if !isdirectory(directory)
-                 echo "Warning: Unable to create backup directory: " . directory
-                 echo "Try: mkdir -p " . directory
-             else
-                 let directory = substitute(directory, " ", "\\\\ ", "g")
-                 exec "set " . settingname . "=" . directory
-             endif
-         endfor
-     endfunction
-     call InitializeDirectories()
-     " }

-     " Initialize NERDTree as needed {
-     function! NERDTreeInitAsNeeded()
-         redir => bufoutput
-         buffers!
-         redir END
-         let idx = stridx(bufoutput, "NERD_tree")
-         if idx > -1
-             NERDTreeMirror
-             NERDTreeFind
-             wincmd l
-         endif
-     endfunction
-     " }

-     " Strip whitespace {
-     function! StripTrailingWhitespace()
-         " Preparation: save last search, and cursor position.
-         let _s=@/
-         let l = line(".")
-         let c = col(".")
-         " do the business:
-         %s/\s\+$//e
-         " clean up: restore previous search history, and cursor position
-         let @/=_s
-         call cursor(l, c)
-     endfunction
-     " }

-     " Shell command {
-     function! s:RunShellCommand(cmdline)
-         botright new

-         setlocal buftype=nofile
-         setlocal bufhidden=delete
-         setlocal nobuflisted
-         setlocal noswapfile
-         setlocal nowrap
-         setlocal filetype=shell
-         setlocal syntax=shell

-         call setline(1, a:cmdline)
-         call setline(2, substitute(a:cmdline, '.', '=', 'g'))
-         execute 'silent $read !' . escape(a:cmdline, '%#')
-         setlocal nomodifiable
-         1
-     endfunction

-     command! -complete=file -nargs=+ Shell call s:RunShellCommand(<q-args>)
-     " e.g. Grep current file for <search_term>: Shell grep -Hn <search_term> %
-     " }

-     function! s:IsSpf13Fork()
-         let s:is_fork = 0
-         let s:fork_files = ["~/.vimrc.fork", "~/.vimrc.before.fork", "~/.vimrc.bundles.fork"]
-         for fork_file in s:fork_files
-             if filereadable(expand(fork_file, ":p"))
-                 let s:is_fork = 1
-                 break
-             endif
-         endfor
-         return s:is_fork
-     endfunction

-     function! s:ExpandFilenameAndExecute(command, file)
-         execute a:command . " " . expand(a:file, ":p")
-     endfunction

-     function! s:EditSpf13Config()
-         call <SID>ExpandFilenameAndExecute("tabedit", "~/.vimrc")
-         call <SID>ExpandFilenameAndExecute("vsplit", "~/.vimrc.before")
-         call <SID>ExpandFilenameAndExecute("vsplit", "~/.vimrc.bundles")

-         execute bufwinnr(".vimrc") . "wincmd w"
-         call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.local")
-         wincmd l
-         call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.before.local")
-         wincmd l
-         call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.bundles.local")

-         if <SID>IsSpf13Fork()
-             execute bufwinnr(".vimrc") . "wincmd w"
-             call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.fork")
-             wincmd l
-             call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.before.fork")
-             wincmd l
-             call <SID>ExpandFilenameAndExecute("split", "~/.vimrc.bundles.fork")
-         endif

-         execute bufwinnr(".vimrc.local") . "wincmd w"
-     endfunction

-     execute "noremap " . s:spf13_edit_config_mapping " :call <SID>EditSpf13Config()<CR>"
-     execute "noremap " . s:spf13_apply_config_mapping . " :source ~/.vimrc<CR>"
- " }

- " Use fork vimrc if available {
-     if filereadable(expand("~/.vimrc.fork"))
-         source ~/.vimrc.fork
-     endif
- " }

- " Use local vimrc if available {
-     if filereadable(expand("~/.vimrc.local"))
-         source ~/.vimrc.local
-     endif
- " }

- " Use local gvimrc if available and gui is running {
-     if has('gui_running')
-         if filereadable(expand("~/.gvimrc.local"))
-             source ~/.gvimrc.local
-         endif
-     endif
- " }
- .gitignore  
    .DS_Store
- *.pyc
- *._*
- .vim/
- .vimrc.before  
    " Modeline and Notes {
- " vim: set sw=4 ts=4 sts=4 et tw=78 foldmarker={,} foldlevel=0 foldmethod=marker:
- "
- "                    __ _ _____              _
- "         ___ _ __  / _/ |___ /      __   __(_)_ __ ___
- "        / __| '_ \| |_| | |_ \ _____\ \ / /| | '_ ` _ \
- "        \__ \ |_) |  _| |___) |_____|\ V / | | | | | | |
- "        |___/ .__/|_| |_|____/        \_/  |_|_| |_| |_|
- "            |_|
- "
- "   This is the personal .vimrc.before file of Steve Francia.
- "   While much of it is beneficial for general use, I would
- "   recommend picking out the parts you want and understand.
- "
- "   This file is for options which must be set *before* plugins
- "   are loaded and the main .vimrc config is run. Most of these
- "   are for preventing mappings or commands from being created.
- "
- "   You can find me at http://spf13.com
- " }

- " spf13 options {

-     " Prevent automatically changing to open file directory
-     "   let g:spf13_no_autochdir = 1

-     " Disable views
-     "   let g:spf13_no_views = 1

-     " Leader keys
-     "   let g:spf13_leader='\'
-     "   let g:spf13_localleader='_'

-     " Disable easier moving in tabs and windows
-     "   let g:spf13_no_easyWindows = 1

-     " Disable wrap relative motion for start/end line motions
-     "   let g:spf13_no_wrapRelMotion = 1

-     " Disable fast tab navigation
-     "   let g:spf13_no_fastTabs = 1

-     " Clear search highlighting
-     "   let g:spf13_clear_search_highlight = 1

-     " Disable neosnippet expansion
-     " This maps over <C-k> and does some Supertab
-     " emulation with snippets
-     "   let g:spf13_no_neosnippet_expand = 1

-     " Disable whitespace stripping
-     "   let g:spf13_keep_trailing_whitespace = 1

-     " Enable powerline symbols
-     "   let g:airline_powerline_fonts = 1

-     " vim files directory
-     "   let g:spf13_consolidated_directory = <full path to desired directory>
-     "   eg: let g:spf13_consolidated_directory = $HOME . '/.vim/'

-     " This makes the completion popup strictly passive.
-     " Keypresses acts normally. <ESC> takes you of insert mode, words don't
-     " automatically complete, pressing <CR> inserts a newline, etc. Iff the
-     " menu is open, tab will cycle through it. If a snippet is selected, <C-k>
-     " expands it and jumps between fields.
-     "   let g:spf13_noninvasive_completion = 1

-     " Don't turn conceallevel or concealcursor
-     "   let g:spf13_no_conceal = 1

-     " For some colorschemes, autocolor will not work (eg: 'desert', 'ir_black')
-     " Indent guides will attempt to set your colors smartly. If you
-     " want to control them yourself, do it here.
-     "   let g:indent_guides_auto_colors = 0
-     "   autocmd VimEnter,Colorscheme * :hi IndentGuidesOdd  guibg=#212121 ctermbg=233
-     "   autocmd VimEnter,Colorscheme * :hi IndentGuidesEven guibg=#404040 ctermbg=234

-     " Leave the default font and size in GVim
-     " To set your own font, do it from ~/.vimrc.local
-     "   let g:spf13_no_big_font = 1

-     " Disable  omni complete
-     "   let g:spf13_no_omni_complete = 1

-     " Don't create default mappings for multicursors
-     " See :help multiple-cursors-mappings
-     "   let g:multi_cursor_use_default_mapping=0
-     "   let g:multi_cursor_next_key='<C-n>'
-     "   let g:multi_cursor_prev_key='<C-p>'
-     "   let g:multi_cursor_skip_key='<C-x>'
-     "   let g:multi_cursor_quit_key='<Esc>'
-     " Require a special keypress to enter multiple cursors mode
-     "   let g:multi_cursor_start_key='+'

-     " Mappings for editing/applying spf13 config
-     "   let g:spf13_edit_config_mapping='<leader>ev'
-     "   let g:spf13_apply_config_mapping='<leader>sv'

- " }

- " Use fork before if available {
-     if filereadable(expand("~/.vimrc.before.fork"))
-         source ~/.vimrc.before.fork
-     endif
- " }

- " Use local before if available {
-     if filereadable(expand("~/.vimrc.before.local"))
-         source ~/.vimrc.before.local
-     endif
- " }
- Copy solarized vim to vim\color  
    C:\Program Files (x86)\Vim\vim81\colors

- :g

- The :global command is your friend - learn it well. It lets you run arbitrary :ex commands on every line that matches a regex. It abbreviates to :g.
- To delete all lines that match "George Bush":

- :g/George Bush/ d

- The command that follows can have its own address/range prefix, which will be relative to the matched line. So to delete the 5th line after George Bush:

- :g/George Bush/ .+5 d

- To delete the DEBUG log entries:

- :g/DEBUG/ .,+10 d

- If you knew the stack trace was variable length but always ended at a blank line (or other regex):

- :g/DEBUG/ .,/^$/ d

- You can also execute a command on every line that does NOT match with :g!. e.g. to replace "Bush" with "Obama" on every line that does not contain the word "sucks":

- :g!/sucks/ s/Bush/Obama/

- The default command is to print the line to the message window. e.g. to list every line marked TODO:

- :g/TODO

- This is also useful for checking the regex matches the lines you expect before you do something destructive.
- You can chain multiple commands using "|". e.g. to change Bush to Obama AND George to Barack on every line that does not contain "sucks":

- :g!/sucks/ s/Bush/Obama/g | s/George/Barack/g

- Navigation

- H (high) M (middle) L (low) to jump to that part on the screen
- Screen

- Move current line

- Center of screen: zz z.
- Top of screen: zt
- Bottom of screen: zb

- Move screens

- Half: Down: Ctrl + d & Up: Ctrl + u
- Single line: Down: Ctrl + e & Up:Ctrl + y
- Full: Down: Ctrl + f & Up: Ctrl + b

- Line

- Begin of line:0
- End of line:$
- First non blank character on line:^
- Last non blank character on line:g_

- Percentage of file:n% e.g. 50% will move you to 50% of file
- By Search

- Next occurrence of word:*
- Previous occurrence of word:#
- Search for lines not containing pattern and other helpful searches  
    http://vim.wikia.com/wiki/Search_for_lines_not_containing_pattern_and_other_helpful_searches
- Last occurrence of 

- GN (if you are already searching for something)

- go to end, then N gives last occurrence

- G?searchterm<CR>

- go to end, then search backwards

- By Mark

- Set a mark:ma where a is the name of register
- Go to mark:’a

- Code brackets (curly,round,square):%

- Deletion

- delete a word, which is composed of symbols such as period, hyphen etc: dW
- Delete text including character (say ,): df,
- Delete text up to character (say ,): dt,
- Delete all lines matching search term :g/searchterm/d

- Search

- Count number of matches :%s/pattern//gn
- Find matching brach **%**

- How-To

- Locate vimrc

- :version  
    You will get output like: 
- system vimrc file: "$VIM/vimrc"
-     user vimrc file: "$HOME/.vimrc"
-       user exrc file: "$HOME/.exrc"
-   system gvimrc file: "$VIM/gvimrc"
-     user gvimrc file: "$HOME/.gvimrc"
-     system menu file: "$VIMRUNTIME/menu.vim"
- his is where vim looks for vimrcs, it doesn't mean they exist.

- You can check the full path of your vimrc with

- :echo $MYVIMRC
- :echo $MYVIMRC  
    If the output is empty, then your vim doesn't use a user vimrc (just create it if you wish).

- Plugin folder hierarchy  
    [https://learnvimscriptthehardway.stevelosh.com/chapters/42.html](https://learnvimscriptthehardway.stevelosh.com/chapters/42.html)

- Plugin Layout in the Dark Ages

- The first thing we need to talk about is how to structure our plugin. In the past this was a messy affair, but now there's a tool that makes the process of installing Vim plugins much, much saner.

- We need to go over the basic layout first, then we'll talk about how to restore our sanity.

- Basic Layout

- Vanilla Vim supports splitting plugins into multiple files. There are a number of different directories you can create under ~/.vim that mean various things.
- We'll cover the most important directories now, but don't stress out too much about them. We'll go over them one at a time as we create our Potion plugin.
- Before we continue we need to talk about some vocabulary.
- I've been using the word "plugin" to mean "a big ol' hunk of Vimscript that does a bunch of related stuff". Vim has a more specific meaning of "plugin", which is "a file in ~/.vim/plugin/".
- Most of the time I'll be using the first definition. I'll try to be clear when I mean the second.

- ~/.vim/colors/

- Files inside ~/.vim/colors/ are treated as color schemes. For example: if you run :color mycolors Vim will look for a file at ~/.vim/colors/mycolors.vim and run it. That file should contain all the Vimscript commands necessary to generate your color scheme.
- We're not going to cover color schemes in this book. If you want to create your own you should copy an existing scheme and modify it. Remember that :help is your friend.

- ~/.vim/plugin/

- Files inside ~/.vim/plugin/ will each be run once every time Vim starts. These files are meant to contain code that you always want loaded whenever you start Vim.

- ~/.vim/ftdetect/

- Any files in ~/.vim/ftdetect/ will also be run every time you start Vim.
- ftdetect stands for "filetype detection". The files in this directory should set up autocommands that detect and set the filetype of files, and nothing else. This means they should never be more than one or two lines long.

- ~/.vim/ftplugin/

- Files in ~/.vim/ftplugin/ are different.
- The naming of these files matters! When Vim sets a buffer's filetype to a value it then looks for a file in ~/.vim/ftplugin/ that matches. For example: if you run set filetype=derp Vim will look for ~/.vim/ftplugin/derp.vim. If that file exists, it will run it.
- Vim also supports directories inside ~/.vim/ftplugin/. To continue our example: set filetype=derp will also make Vim run any and all *.vim files inside ~/.vim/ftplugin/derp/. This lets you split up your plugin's ftplugin files into logical groups.
- Because these files are run every time a buffer's filetype is set they must only set buffer-local options! If they set options globally they would overwrite them for all open buffers!

- ~/.vim/indent/

- Files in ~/.vim/indent/ are a lot like ftplugin files. They get loaded based on their names.
- indent files should set options related to indentation for their filetypes, and those options should be buffer-local.
- Yes, you could simply put this code in the ftplugin files, but it's better to separate it out so other Vim users will understand what you're doing. It's just a convention, but please be a considerate plugin author and follow it.

- ~/.vim/compiler/

- Files in ~/.vim/compiler/ work exactly like indent files. They should set compiler-related options in the current buffer based on their names.
- Don't worry about what "compiler-related options" means right now. We'll cover that later.

- ~/.vim/after/

- The ~/.vim/after/ directory is a bit of a hack. Files in this directory will be loaded every time Vim starts, but after the files in ~/.vim/plugin/.
- This allows you to override Vim's internal files. In practice you'll rarely need this, so don't worry about it until you find yourself thinking "Vim itself sets option x, but I want something different".

- ~/.vim/autoload/

- The ~/.vim/autoload/ directory is an incredibly important hack. It sounds a lot more complicated than it actually is.
- In a nutshell: autoload is a way to delay the loading of your plugin's code until it's actually needed. We'll cover this in more detail later when we refactor our plugin's code to take advantage of it.

- ~/.vim/doc/

- Finally, the ~/.vim/doc/ directory is where you can add documentation for your plugin. Vim has a huge focus on documentation (as evidenced by all the :help commands we've been running) so it's important to document your plugins.

- VIMRC  
    :e $MYVIMRC

- My Current Setup  
    " BASIC SETUP:

- set nocompatible

- " enter the current millenium

- syntax enable

- filetype plugin on

- " FINDING FILES:
- "
- " Search down into subfolders
- " Provides tab-completion for all file-related tasks

- " Display all matching files whe we tab complete

- set wildmenu

- " NOW WE CAN:
- "  - Hit tab to :find by partial match
- "  - Use * to make it fuzzy

- " THINGS TO CONSIDER:
- " - :b lets you autocomplete any open buffer

- " TAG JUMPING:
- "
- " Crete the 'tags' file (may need to install ctags first)

- command! MakeTags !ctags -R .

- " NOW WE CAN:
- " - Use ^] to jump to tag under cursor
- " - Use g^] for ambiguous tags
- " - Use ^t to jump back up the tag stack

- " THINGS TO CONSIDER:
- " - This dosen't help if you want a visual list of tags
- " set tag+=/Users/sandeepdivekar/Documents/GitHub/LeetCode

- " AUTOCOMPLETE:
- " The good stuff is documented in |ins-completion|
- " HIGHLIGHTS:
- " - ^x^n for JUST this file
- " - ^x^f for filenames (works with our path trick!)
- " - ^x^] for tags only
- " - ^n for anything specified by the 'complete' option

- " NOW WE CAN:
- " - Use ^n and ^p to go back and forth in the suggestion list

- " FILE BROWSING:
- "
- " Tweaks for browsing:
- let g:netrw_banner=0 "disable annoying banner
- let g:netrw_browse_split=4 "open in prior window
- let g:netrw_altv=1 "open splits to the right
- let g:netrw_liststyle=3 "tree view
- let g:netrw_list_hide=netrw_gitignore#Hide()
- let g:netrw_list_hide.=',\(^\|\s\s\)\zs\.\S\+'

- " NOW WE CAN:
- " - :edit a folder to open a file browser
- " - <CR>/v/t to open in an h-split/v-split/tab
- " - check |netrw-browse-maps| for more mappings

- " SNIPPETS:
- " Read an empty HTML template and move cursor to title

- nnoremap ,html :-1read $HOME/.vim/.skeleton.html<CR>3jwf>a
- nnoremap ,class :-1read $HOME/.vim/.class.cs<CR>3jwf>a

- " NOW WE CAN:
- " add snippets

- " BUILD INTEGRATION:
- " Steal Mr. Bradley's formatter and add it to our spec_helper
- " http://philipbradley.net/rspec-into-vim-with-quickfix
- "
- " Configure the 'make' command to run RSpec
- "set makeprg=bundle\ exec\ rspec\ -f\ QuickfixFormatter
- " NOW WE CAN:
- " - Run :make to run RSpec
- " - :cl to list errors
- " - :cc# to jump to error by number
- " - :cn and :cp to navigate forward and back
- Nouns in VIM

- iw => inner word
- it => inner tag (like html tag)
- i" => inner quote
- ip => inner paragraph
- as => a sentence
- f,F => 'find' the next character
- t,T => 'find' the next character
- /   => search up to the next match

- Primer  
    https://danielmiessler.com/study/vim/
- plugins

- sensible.vim  
    https://github.com/tpope/vim-sensible
- scriptease.vim  
    https://github.com/tpope/vim-scriptease
- repeat.vim  
    https://github.com/tpope/vim-repeat
- surround.vim  
    https://github.com/tpope/vim-surround
- speeddating.vim  
    https://github.com/tpope/vim-speeddating
- commentary.vim  
    https://github.com/tpope/vim-commentary

- Automate OmniSharpInstall & github  
    omnisharp-manager.ps1 file in .vim/bundles/...

- # OmniSharp-roslyn Management tool
- #
- # Works on: Microsoft Windows

- # Options:
- # -v | version to use (otherwise use latest)
- # -l | where to install the server
- # -u | help / usage info
- # -H | install the HTTP version of the server

- [CmdletBinding()]
- param(
-     [Parameter()][Alias('v')][string]$version,
-     [Parameter()][Alias('l')][string]$location = "$($Env:USERPROFILE)\.omnisharp\",
-     [Parameter()][Alias('u')][Switch]$usage,
-     [Parameter()][Alias('H')][Switch]$http_check
- )

- if ($usage) {
-     Write-Host "usage:" $MyInvocation.MyCommand.Name "[-Hu] [-v version] [-l location]"
-     exit
- }

- [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

- $Token = '0de33114c97c6c53b1e895155977e70b0297e7f9'
- $Base64Token = [System.Convert]::ToBase64String([char[]]$Token);

- $Headers = @{
- Authorization = 'Basic {0}' -f $Base64Token;
- }
- function get_latest_version() {
-     $response = Invoke-RestMethod -Headers $Headers -Uri "https://api.github.com/repos/OmniSharp/omnisharp-roslyn/releases/latest"
-     return $response.tag_name
- }

- if ([string]::IsNullOrEmpty($version)) {
-     $version = get_latest_version
- }

- if ($http_check) {
-     $http = ".http"
- } else {
-     $http = ""
- }

- if ([Environment]::Is64BitOperatingSystem) {
-     $machine = "x64"
- } else {
-     $machine = "x86"
- }

- $url = "https://github.com/OmniSharp/omnisharp-roslyn/releases/download/$($version)/omnisharp$($http)-win-$($machine).zip"
- $out = "$($location)\omnisharp$($http)-win-$($machine).zip"

- if (Test-Path -Path $location) {
-     Remove-Item $location -Force -Recurse
- }

- New-Item -ItemType Directory -Force -Path $location | Out-Null

- Invoke-WebRequest -Uri $url -OutFile $out

- # Run Expand-Archive in versions that support it
- if ($PSVersionTable.PSVersion.Major -gt 4) {
-     Expand-Archive $out $location -Force
- } else {
-     Add-Type -AssemblyName System.IO.Compression.FileSystem
-     [System.IO.Compression.ZipFile]::ExtractToDirectory($out, $location)
- }

- # Check for file to confirm download and unzip were successful
- if (Test-Path -Path "$($location)\OmniSharp.Roslyn.dll") {
-     Set-Content -Path "$($location)\OmniSharpInstall-version.txt" -Value "OmniSharp $($version)"
-     exit 0
- } else {
-     exit 1
- }

- Reload vimrc **:so $MYVIMRC**
- Install vim on Ubuntu  
    [https://www.vim.org/git.php](https://www.vim.org/git.php)
- [https://phoenixnap.com/kb/how-to-install-vim-ubuntu](https://phoenixnap.com/kb/how-to-install-vim-ubuntu)

- sudo apt-get install libncurses5-dev libncursesw5-dev
- sudo apt install build-essential
- git clone [https://github.com/vim/vim.git](https://github.com/vim/vim.git)
- cd vim/src
- make
- sudo make install

- Move current line to top/middle/bottom  
    zt/zz/zb
- Move cursor to beginning of function, from within a function  
    [+[ i.e. two [

- Current .vimrc  
      
- " ============================================================================
- " .vimrc of SANDEEP Divekar
- " ============================================================================

- "In older versions of Vim, not loading a vimrc file activates vi compatible mode, which causes many useful features to be disabled. The -N flag prevents this by setting the ‘nocompatible’ option. Since version 8.0 of Vim, the ‘nocompatible’ option is set by default, making the -N flag unnecessary."
- set nocompatible

- "With Vim’s built-in plugins enabled, you’ll be able to use features such as netrw (Tip 44) and omni-completion (Tip 119), as well as many others."

- filetype indent plugin on
- " ============================================================================
- " VIM-PLUG BLOCK
- " ============================================================================

- " Specify a directory for plugins
- " - For Neovim: stdpath('data') . '/plugged'
- " - Avoid using standard Vim directory names like 'plugin'
- call plug#begin('~/.vim/plugged')

- Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
- Plug 'preservim/nerdtree' |
- \ Plug 'Xuyuanp/nerdtree-git-plugin' |
- \ Plug 'ryanoasis/vim-devicons' |
- \ Plug 'scrooloose/nerdtree-project-plugin' |
- \ Plug 'PhilRunninger/nerdtree-visual-selection'
- Plug 'tpope/vim-repeat'
- Plug 'tpope/vim-surround'
- Plug 'tpope/vim-fugitive'
- Plug 'vim-scripts/AutoClose'
- Plug 'vim-utils/vim-man'
- Plug 'mhinz/vim-startify'
- Plug 'brglng/vim-sidebar-manager'
- Plug 'preservim/nerdcommenter'
- Plug 'OmniSharp/omnisharp-vim'
- Plug 'nickspoons/vim-sharpenup'
- Plug 'w0rp/ale'
- Plug 'morhetz/gruvbox'
- Plug 'vim-airline/vim-airline'
- Plug 'vim-airline/vim-airline-themes'
- Plug 'prabirshrestha/asyncomplete.vim'
- Plug 'natebosch/vim-lsc'
- "try below later for use with omnisharp vim"
- "Plug 'SirVer/utilsnips'
- "Plug 'honza/vim-snippets'
- Plug 'mbbill/undotree'
- Plug 'jremmen/vim-ripgrep'

- " Initialize plugin system
- call plug#end()
- " ============================================================================
- " Basic settings
- " ============================================================================

- "set spell

- " enter the current millenium

- syntax enable

- filetype plugin on

- "set lines=50 columns=100
- " FINDING FILES:
- "
- " Search down into subfolders
- " Provides tab-completion for all file-related tasks

- " Display all matching files whe we tab complete

- set wildmenu

- " NOW WE CAN:
- "  - Hit tab to :find by partial match
- "  - Use * to make it fuzzy

- "Persistent undo
- set undofile

- "First create a directory for holding undofile
- "mkdir ~/.vim/undodir

- set undodir=~/.vim/undodir

- "//
- set number

- "Search
- set hlsearch
- set ignorecase
- set incsearch
- set smartcase

- set ruler
- set showcmd
- set history=50

- set ttyfast                " Faster redrawing.
- set lazyredraw             " Only redraw when necessary.

- set splitbelow             " Open new windows below the current window.
- set splitright             " Open new windows right of the current window.

- set cursorline             " Find the current line quickly.
- set cursorcolumn
- set wrapscan               " Searches wrap around end-of-file.

- set hidden                 " Switch between buffers without having to save first.
- set laststatus  =2         " Always show statusline.
- set display     =lastline  " Show as much as possible of the last line.

- set nowrap

- set autoindent             " Indent according to previous line.
- set noexpandtab            " Use tabs instead of spaces.
- set softtabstop =0         " Tab key indents by 0 spaces.
- set shiftwidth  =4         " >> indents by 4 spaces.
- set shiftround             " >> indents to next multiple of 'shiftwidth'.
- set copyindent
- set tabstop     =4
- set autoread

- " turn hybrid line numbers on
- :set number relativenumber

- " turn hybrid line numbers off
- ":set nonumber norelativenumber
- ":set nonu nornu

- " toggle hybrid line numbers
- ":set number! relativenumber!
- ":set nu! rnu!

- set colorcolumn=80
- highlight ColorColumn ctermbg=0 guibg=lightgrey

- " session management
- let g:startify_session_autoload = 1
- let g:startify_session_persistence = 1

- "split window
- nnoremap <C-H> <C-W><C-H>
- nnoremap <C-J> <C-W><C-J>
- nnoremap <C-K> <C-W><C-K>
- nnoremap <C-L> <C-W><C-L>

- " open NERDTree automatically
- "autocmd StdinReadPre * let s:std_in=1
- "autocmd VimEnter * NERDTree

- let g:NERDTreeGitStatusWithFlags = 1
- let g:WebDevIconsUnicodeDecorateFolderNodes = 1
- let g:NERDTreeGitStatusNodeColorization = 1
- let g:NERDTreeColorMapCustom = {
-     \ "Staged"    : "#0ee375",  
-     \ "Modified"  : "#d9bf91",  
-     \ "Renamed"   : "#51C9FC",  
-     \ "Untracked" : "#FCE77C",  
-     \ "Unmerged"  : "#FC51E6",  
-     \ "Dirty"     : "#FFBD61",  
-     \ "Clean"     : "#87939A",   
-     \ "Ignored"   : "#808080"   
-     \ }       

- colorscheme gruvbox
- set bg=dark

- " sync open file with NERDTree
- " " Check if NERDTree is open or active
- function! IsNERDTreeOpen()        
-   return exists("t:NERDTreeBufName") && (bufwinnr(t:NERDTreeBufName) != -1)
- endfunction

- " Call NERDTreeFind iff NERDTree is active, current window contains a modifiable
- " file, and we're not in vimdiff
- function! SyncTree()
-   if &modifiable && IsNERDTreeOpen() && strlen(expand('%')) > 0 && !&diff
-     NERDTreeFind
-     wincmd p
-   endif
- endfunction

- " Highlight currently open buffer in NERDTree

- map <C-o> :NERDTreeToggle<CR>

- "OmniSharp
- let g:OmniSharp_highlighting = 3
- let g:OmniSharp_selector_ui = 'fzf'    " Use fzf.vim
- let g:OmniSharp_selector_findusages = 'fzf'    " Use fzf.vim

- " Use the stdio OmniSharp-roslyn server
- let g:OmniSharp_server_stdio = 1

- " Set the type lookup function to use the preview window instead of echoing it
- let g:OmniSharp_typeLookupInPreview = 1

- " Timeout in seconds to wait for a response from the server
- let g:OmniSharp_timeout = 5

- " Don't autoselect first omnicomplete option, show options even if there is only
- " one (so the preview documentation is accessible). Remove 'preview' if you
- " don't want to see any documentation whatsoever.
- set completeopt=longest,menuone,preview

- " Fetch full documentation during omnicomplete requests.
- " By default, only Type/Method signatures are fetched. Full documentation can
- " still be fetched when you need it with the :OmniSharpDocumentation command.
- "let g:omnicomplete_fetch_full_documentation = 1

- " Set desired preview window height for viewing documentation.
- " You might also want to look at the echodoc plugin.
- set previewheight=5

- " Tell ALE to use OmniSharp for linting C# files, and no other linters.
- let g:ale_linters = { 'cs': ['OmniSharp'] }

- " Update semantic highlighting after all text changes
- let g:OmniSharp_highlight_types = 3
- " Update semantic highlighting on BufEnter and InsertLeave
- " let g:OmniSharp_highlight_types = 2

- augroup omnisharp_commands
-     autocmd!

-     " Show type information automatically when the cursor stops moving.
-     " Note that the type is echoed to the Vim command line, and will overwrite
-     " any other messages in this space including e.g. ALE linting messages.
-     autocmd CursorHold *.cs OmniSharpTypeLookup

-     " The following commands are contextual, based on the cursor position.
-     autocmd FileType cs nnoremap <buffer> gd :OmniSharpGotoDefinition<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fi :OmniSharpFindImplementations<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fs :OmniSharpFindSymbol<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>fu :OmniSharpFindUsages<CR>

-     " Finds members in the current buffer
-     autocmd FileType cs nnoremap <buffer> <Leader>fm :OmniSharpFindMembers<CR>

-     autocmd FileType cs nnoremap <buffer> <Leader>fx :OmniSharpFixUsings<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>tt :OmniSharpTypeLookup<CR>
-     autocmd FileType cs nnoremap <buffer> <Leader>dc :OmniSharpDocumentation<CR>
-     autocmd FileType cs nnoremap <buffer> <C-\> :OmniSharpSignatureHelp<CR>
-     autocmd FileType cs inoremap <buffer> <C-\> <C-o>:OmniSharpSignatureHelp<CR>

-     " Navigate up and down by method/property/field
-     autocmd FileType cs nnoremap <buffer> <C-k> :OmniSharpNavigateUp<CR>
-     autocmd FileType cs nnoremap <buffer> <C-j> :OmniSharpNavigateDown<CR>

-     " Find all code errors/warnings for the current solution and populate the quickfix window
-     autocmd FileType cs nnoremap <buffer> <Leader>cc :OmniSharpGlobalCodeCheck<CR>
- augroup END

- " Contextual code actions (uses fzf, CtrlP or unite.vim when available)
- nnoremap <Leader><Space> :OmniSharpGetCodeActions<CR>
- " Run code actions with text selected in visual mode to extract method
- xnoremap <Leader><Space> :call OmniSharp#GetCodeActions('visual')<CR>

- " Rename with dialog
- nnoremap <Leader>nm :OmniSharpRename<CR>
- nnoremap <F2> :OmniSharpRename<CR>
- " Rename without dialog - with cursor on the symbol to rename: `:Rename newname`
- command! -nargs=1 Rename :call OmniSharp#RenameTo("<args>")

- nnoremap <Leader>cf :OmniSharpCodeFormat<CR>

- " Start the omnisharp server for the current solution
- nnoremap <Leader>ss :OmniSharpStartServer<CR>
- nnoremap <Leader>sp :OmniSharpStopServer<CR>

- " Enable snippet completion
- " let g:OmniSharp_want_snippet=1

- "omnisharp popup styling
- let g:OmniSharp_popup_options = {
- \ 'highlight': 'Normal',
- \ 'padding': [1],
- \ 'border': [1]
- \}

- "asyncomplete lsp
- inoremap <expr> <Tab>   pumvisible() ? "\<C-n>" : "\<Tab>"
- inoremap <expr> <S-Tab> pumvisible() ? "\<C-p>" : "\<S-Tab>"
- inoremap <expr> <cr>    pumvisible() ? "\<C-y>" : "\<cr>"

- imap <c-space> <Plug>(asyncomplete_force_refresh)

- " allow modifying the completeopt variable, or it will
- " be overridden all the time
- let g:asyncomplete_auto_completeopt = 0

- set completeopt=menuone,noinsert,noselect,preview
- autocmd! CompleteDone * if pumvisible() == 0 | pclose | endif

- "git"
- if executable('rg')
- let g:rg_derive_root='true'
- endif

- "leader"
- let mapleader = " "

- let g:netrw_browse_split=2
- "let g:netrw_banner=0"
- let g:netrw_winsize = 25

- nnoremap <leader>h :wincmd h<CR>
- nnoremap <leader>j :wincmd j<CR>
- nnoremap <leader>k :wincmd k<CR>
- nnoremap <leader>l :wincmd l<CR>
- nnoremap <leader>u :UndotreeShow<CR>
- nnoremap <leader>pv :wincmd v<bar> :Ex <bar> :vertical resize 30<CR>
- nnoremap <leader>ps :Rg<SPACE>
- nnoremap <silent> <leader>+ :vertical resize +5<CR>
- nnoremap <silent> <leader>- :vertical resize -5<CR>

-   
    " session
- set sessionoptions=blank,buffers,curdir,folds,tabpages,winsize

- " ---------------
- " ShortCut config {
- " ---------------

- " <Leader>s Session manipulation {
- nmap <leader>sl :SessionList<CR>
- nmap <leader>ss :SSave<CR>
- nmap <leader>sc :SessionClose<CR>
- " } Config ShortCut End

- " [http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session](http://vim.wikia.com/wiki/Restore_cursor_to_file_position_in_previous_editing_session)
- " Restore cursor to file position in previous editing session
- function! ResCur()
- if line("'\"") <= line("$")
- normal! g`"
- return 1
- endif
- endfunction
- augroup resCur
- autocmd!
- autocmd BufWinEnter * call ResCur()
- augroup END

- Current .vsvimrc  
    "//
- set number

- "Search
- set hlsearch
- set ignorecase
- set incsearch
- set smartcase

- set showcmd
- set history=50

- set cursorline             " Find the current line quickly.
- set wrapscan               " Searches wrap around end-of-file.

- set nowrap

- set autoindent             " Indent according to previous line.
- set noexpandtab            " Use tabs instead of spaces.

- " turn hybrid line numbers on
- :set number relativenumber

- " turn hybrid line numbers off
- ":set nonumber norelativenumber
- ":set nonu nornu

- " toggle hybrid line numbers
- ":set number! relativenumber!
- ":set nu! rnu!
- Plugin manager [vim-plug](https://github.com/junegunn/vim-plug) command  
    **Unix**
- curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
-     [https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)

- **Win Powershell**
- iwr -useb [https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) |`
-     ni $HOME/vimfiles/autoload/plug.vim -Force
- Reference VIMRC

- vim plug author .vimrc  
    [https://github.com/junegunn/dotfiles/blob/8646aae3aec418662d667b36444e771041ad0d23/vimrc#L12-L91](https://github.com/junegunn/dotfiles/blob/8646aae3aec418662d667b36444e771041ad0d23/vimrc#L12-L91)
- Awesome vimrc - like spf13 vimrc  
    [https://gist.github.com/cmizony/ad7efafb44b32d1d44d0](https://gist.github.com/cmizony/ad7efafb44b32d1d44d0)

- fold a csharp region: add below in cs.vim in syntax folder inside vimruntime  
    let b:match_words = '\s*#\s*region.*$:\s*#\s*endregion'
- CSHARP C# DEVELOPMENT IN VIM

- add Plug to .vimrc
- from vim run. - :OmniSharpInstall

- Practical VIM

- Search

- f finds the next char, for e.g. f+ finds '+' char
- ; takes you to next match, for the previous search criteria used in f+
- * executes a search for the word under cursor

- Edit

- In Insert Mode

- Ctrl + h deletes one char back
- Ctrl + w deletes one word back
- Ctrl + u deletes back to start of line

- In Normal Mode

- >G increases the indentation from the current line until the end of the file

- Move

- zz brings current line to center of screen

- Copy Paste

- y = yank into register
- yt, = yank till comma
- Ctrl + r 0 = paste text that was just yanked from register 0

- This command puts back text one char at a time, and can be slow

- Ctrl + r Ctrl + p 0 will put entire text immediately and apply indentation as needed.

- Switching Modes

- Esc
- Ctrl + [

- Calculate

- <Ctrl + r>=6*25<CR> calculates 6*25 and enters the result

- Char Set

- to find the numeric code of a char, place cursor on that char, then trigger- ga
- the numeric, hex and octal codes for this char will be printed on the bottom bar
- to enter a char via numeric code use

- Ctrl + v followed by decimal number 065 for A
- Ctrl + v followed by u and then number gives Hex code

- Compound Commands v/s longhand

- Compound

- C
- s
- S
- I
- A
- o
- O

- Longhand

- c$
- cl
- ^C
- ^i
- $a
- A<CR>
- ko

- Repeatable Actions and how to reverse them

- Intent

- Make a change
- Scan line for next char
- Scan line for prev char
- Scan doc for pattern
- Scan doc for prev match
- Perform substitution
- Execute a sequence of chg
- Ex commands
- :substitue - also an Ex command

- Act

- {edit}
- f{char}/t{char}
- F{char}/T{char}
- /pattern<CR>
- ?pattern<CR>
- :s/target/re-placement
- qx{changes}q

- Repeat

- .
- ;
- ;
- n
- n
- &
- @x
- @:
- &

- Reverse

- u
- ,
- ,
- N
- N
- u
- u

- C++ Development in VIM

- Checkout vim source and make it
- Install Plug for vim
- Add vimrc stuff
- Install python3
- Setup youcompleteme stuff from [https://www.ovenproof-linux.com/2018/03/installing-youcompleteme-for-c.html](https://www.ovenproof-linux.com/2018/03/installing-youcompleteme-for-c.html)