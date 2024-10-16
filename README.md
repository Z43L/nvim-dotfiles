# vim
```
" Iniciar gestión de plugins
call plug#begin()

" Plugins para Vim
Plug 'nvim-lua/plenary.nvim' " Utilidades esenciales
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } } " Fuzzy finder (similar a Telescope para Vim)
Plug 'preservim/nerdtree' " Explorador de archivos NERDTree
Plug 'itchyny/lightline.vim' " Barra de estado ligera
Plug 'neoclide/coc.nvim', {'branch': 'release'} " COC.nvim para autocompletado y LSP
Plug 'morhetz/gruvbox' " Tema de colores Gruvbox
Plug 'dracula/vim', { 'as': 'dracula' } " Tema Dracula
" Finalizar gestión de plugins
call plug#end()

" Configuración de Coc.nvim (autocompletado y LSP)
let g:coc_global_extensions = ['coc-tsserver', 'coc-pyright', 'coc-json', 'coc-html', 'coc-css', 'coc-lua']

" Atajos de teclado útiles para Coc.nvim
inoremap <silent><expr> <CR> pumvisible() ? coc#pum#confirm() : "\<CR>"
inoremap <silent><expr> <S-Tab> pumvisible() ? "\<C-p>" : "\<S-Tab>"
nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gr <Plug>(coc-references)
nmap <silent> gi <Plug>(coc-implementation)

" Configuración de lightline (barra de estado)
" let g:lightline = {
"      \ 'colorscheme': 'dracula',
"      \ }

" Configuración de NERDTree (explorador de archivos)
map <C-n> :NERDTreeToggle<CR>

" Opciones generales de Vim
set number " Mostrar números de línea
set relativenumber " Números de línea relativos
set tabstop=4 " Tamaño del tabulador
set shiftwidth=4 " Tamaño de la indentación
set expandtab " Convertir tabs en espacios
" set termguicolors " Colores verdaderos
" set termguicolors

" Aplicar el tema Dracula
syntax enable
set background=dark
colorscheme dracula

" Atajos útiles
nnoremap <C-p> :Files<CR> " Usar FZF para encontrar archivos
nnoremap <C-f> :Rg<CR> " Usar FZF para buscar texto en el proyecto


```

# nvim-dotfiles
```
" Iniciar gestión de plugins
call plug#begin()

Plug 'nvim-lua/plenary.nvim' " Utilidades esenciales
Plug 'nvim-telescope/telescope.nvim' " Fuzzy finder poderoso
Plug 'nvim-treesitter/nvim-treesitter', {'do': ':TSUpdate'} " Resaltado de sintaxis avanzado
Plug 'neovim/nvim-lspconfig' " Cliente LSP para autocompletado y diagnósticos
Plug 'hrsh7th/nvim-cmp' " Autocompletado moderno
Plug 'hrsh7th/cmp-nvim-lsp' " Fuente LSP para nvim-cmp
Plug 'L3MON4D3/LuaSnip' " Snippets
Plug 'saadparwaiz1/cmp_luasnip' " Snippets para nvim-cmp
Plug 'nvim-lualine/lualine.nvim' " Barra de estado atractiva
Plug 'kyazdani42/nvim-web-devicons' " Iconos de archivos
Plug 'kyazdani42/nvim-tree.lua' " Explorador de archivos
Plug 'folke/tokyonight.nvim' " Tema de colores Tokyo Night
Plug 'akinsho/nvim-bufferline.lua' " Línea de buffers múltiples
Plug 'neoclide/coc.nvim', {'branch': 'release'} " COC.nvim para intellisense

" Terminar gestión de plugins
call plug#end()

" Configuración de Treesitter
lua <<EOF
require('nvim-treesitter.configs').setup {
  ensure_installed = {"c", "lua", "python", "javascript", "html", "css"},
  highlight = {
    enable = true,
  },
}
EOF

" Configuración de LSP
lua <<EOF
local lspconfig = require('lspconfig')
lspconfig.ts_ls.setup{} -- Configuración de TypeScript/JavaScript
lspconfig.pyright.setup{} -- Configuración de Python
lspconfig.lua_ls.setup{} -- Configuración de Lua
EOF

" Configuración de autocompletado
lua <<EOF
local cmp = require'cmp'
cmp.setup {
  snippet = {
    expand = function(args)
      require('luasnip').lsp_expand(args.body)
    end,
  },
  mapping = {
    ['<C-b>'] = cmp.mapping.scroll_docs(-4),
    ['<C-f>'] = cmp.mapping.scroll_docs(4),
    ['<C-Space>'] = cmp.mapping.complete(),
    ['<CR>'] = cmp.mapping.confirm({ select = true }),
  },
  sources = {
    { name = 'nvim_lsp' },
    { name = 'luasnip' },
  },
}
EOF

" Configuración de lualine
lua <<EOF
require('lualine').setup {
  options = {
    theme = 'gruvbox',
    section_separators = {'', ''},
    component_separators = {'', ''},
  }
}
EOF

" Configuración de Nvim Tree
lua <<EOF
require('nvim-tree').setup {
  view = {
    width = 30,
    side = 'left',
  }
}
EOF

" Configuración de Telescope
lua <<EOF
require('telescope').setup{
  defaults = {
    vimgrep_arguments = {
      'rg',
      '--color=never',
      '--no-heading',
      '--with-filename',
      '--line-number',
      '--column',
      '--smart-case'
    },
    prompt_prefix = '🔍 ',
    selection_caret = ' ',
    path_display = {'truncate'},
  }
}
EOF

" Opciones generales de Neovim
set number " Mostrar números de línea
set relativenumber " Números de línea relativos
set tabstop=4 " Tamaño del tabulador
set shiftwidth=4 " Tamaño de la indentación
set expandtab " Convertir tabs en espacios
set termguicolors " Colores verdaderos
colorscheme gruvbox " Aplicar el tema Gruvbox

" Atajos útiles
nnoremap <C-n> :NvimTreeToggle<CR>
nnoremap <C-p> :Telescope find_files<CR>
nnoremap <C-f> :Telescope live_grep<CR>
```
