# UBUNTU-SETUP-101
Ok, let's go! Ce répo va me permettre de me rappeler de la configuration de mon Ubuntu :v: :heart: :heavy_plus_sign:

## Contenu à ajouter

- [x] Configuration de mon GRUB
- [ ] Confiration de mon terminal
- [ ] Configuration de mon theme Sweet Dark
- [x] Configuration de neovim
- [x] Rock'n'roll

## Table des matières

<!-- MarkdownTOC -->

- [Les choses à faire après avoir installé Ubuntu 18.10](#les-choses-à-faire-après-avoir-installé-ubuntu-1810)
- [Sublime Text 3 :heart:](#sublime-text-3-heart)
    - [Les paquets faciles à installer :trollface:](#les-paquets-faciles-à-installer-trollface)
    - [Les paquets difficiles à installer :rage3:](#les-paquets-difficiles-à-installer-rage3)
- [Git 101](#git-101)
- [Configurer un LAMP](#configurer-un-lamp)
- [Configurer Neovim](#configurer-neovim)
- [Configuration de mon terminal](#configuration-de-mon-terminal)

<!-- /MarkdownTOC -->

## Les choses à faire après avoir installé Ubuntu 18.10

- Mettre à jour le système

![Update][Update_img]

Yup bro ! Voici la commande pour installer les dernières mises à jours
```bash
sudo apt  update && sudo apt upgrade
```
- Installer les codecs vidéos

![Codecs][Codecs_img]

Si tu as oublié d'installer les codecs comme le montre la capture ci-dessous, pas de panique car vous pouvez les installer grâce à ce lien :arrow_right: [CODECS](apt://ubuntu-restricted-extras) :arrow_left:
- Afficher le niveau de la batterie

![Battery_level][Battery_img]

Ok bruh! Si tu veux afficher le niveau de la batterie (pourcentage), rien de plus simple. Il suffit juste de taper cette commande dans votre terminal :arrow_down:
```bash
gsettings set org.gnome.desktop.interface show-battery-percentage true
```

## Sublime Text 3 :heart:

__The best of the best of the best. I'm tellin' you man.__
OK, tout d'abord il faut ajouter le paquet dans le 'dev channel apt' de Ubuntu
```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
Maintenant que c'est fait, nous pouvons installer sublime text sur notre système
```bash
sudo apt-get update
sudo apt-get install sublime-text
```

### Les paquets faciles à installer :trollface:

Rappel : Si par hasard tu as oublié comment on fait (weird flex, but ok) ; les paquets sont à installer dans le Package Control de Sublime Text. 

Liste des paquets à installer :
- __BracketHighlighter__
- __DocBlockr__
- __GitGutter__
- __Djaneiro__
- __Emmet__
- __Terminus__
- __Material Theme__

Dans mon installation, j'utilise la police **Fira Code**. Donc si tu veux l'utiliser, il te suffit de la télécharger
```bash
sudo apt install fonts-firacode
```

### Les paquets difficiles à installer :rage3:

Yup dans cette section je montre comment installer ces paquets qui peuvent vraiment faire mal à la tête aux premiers abords.

- __Markdown Preview__

Pour créer un raccourci-clavier afin de visualiser l'apercu Markdown, rien de plus simple. Il suffit juste de coller ce code dans le fichier
Preferences -> Key Bindings (dans la partie pour User)
```json
[
    {
        "keys": ["alt+m"],
        "command": "markdown_preview",
        "args": {"target": "browser", "parser":"markdown"}
    }
]
```
- __MarkdownTOC__

Ce plugin permet de générer une table de matière pour nos fichiers markdown. Donc après installation du plugin, tu vas dans Preferences -> Package Settings -> MarkdownTOC -> Settings-User
```json
{
  "defaults": {
    "autolink": true,
    "uri_encoding": false,
    "markdown_preview": false
  }
}

```
- __Predawn (Color Theme) & Material Theme(Theme)__

(voir la fin du fichier [setting_user.json](setting_user.json))

- __SublimeLinter__

Permet de vérifier si notre code n'a pas d'erreurs (NB : tu auras besoin d'installer nodejs & pear).  

| Nom du paquet | Description | Pré-requis |
|    :---       |   :---:     |   ---:     |
| SublimeLinter  | Paquet Mère | N/A |
| SublimeLinter-phpcs | Lint for php | ```sudo pear install PHP_CodeSniffer``` |
| SublimeLinter-jshint | Lint for JavaScript | ```sudo npm install -g jshint``` |

- __Anaconda :snake:__

Now we're talking bruh. Mais d'abord il faut installer python3.7 (si tu l'as pas dans ton système)  
```bash
sudo apt install python3.7
```
Maintenant on télécharge le script permettant d'installer _anaconda_. Voici le [lien](https://repo.anaconda.com/archive/Anaconda3-2018.12-Linux-x86_64.sh) de téléchargement. Après téléchargement, on exécute le script un mode user normal

```bash
bash ~/Downloads/Anaconda3-2018.12-Linux-x86_64.sh
```
Suivre les instructions du script pour la configuration.  
De retour dans Sublime Text 3, on installe le package ```Anaconda```. Dans les paramètres de votre projet coller le code ci-dessous
```json
{
    "build_systems":
    [
        {
            "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
            "name": "Anaconda Python Builder",
            "selector": "source.python",
            "shell_cmd": "\"~/anaconda3/bin/python3.7\" -u \"$file\""
        }
    ],
    "folders":
    [
        {
            "path": "/home/ndoy3m4n/Documents/LEARNING_PYTHON"
        }
    ],
    "settings":
    {
        "anaconda_linting": true,
        "anaconda_linting_behaviour": "always",
        "pep257": false,
        "python_interpreter": "~/anaconda3/bin/python3.7",
        "use_pylint": false,
        "enable_docstrings_tooltip": true,
        "anaconda_tooltip_theme": "popup",
        "disable_anaconda_completion": false
    }
}
```
Voilà c'est terminé. Feel the power of the __ANACONDA__

- __View in Browser__

Permet de visualiser le résultat d'un code PHP (par exemple) sur votre navigateur. Après installation du paquet, il faut donner à Sublime Text l'accès à ```/var/www/html``` grâce à la commande suivante :
```bash
sudo chown -R nom_user_simple:nom_user_simple /var/www/html
```
Maintenant il ne reste plus qu'à modifier quelques lignes sur la configuration de notre projet : __Project->Edit Project__
```json
{
    "folders":
    [
        {
            "path": "/var/www/html"
        }
    ],
    "sublime-view-in-browser":
    {
        "baseUrl": "http://localhost",
        "basePath": "/var/www/html"
    }
}
```
Pour afficher votre code sur le navigateur, il suffit juste de taper la manip suivante ```ctrl+alt+v```.  
And now YOU are ready to go or fly. Fly little bird, fly. Buzz little bee, buzz.

## Git 101

- Pour l'installation :
```bash
sudo apt install git
```
- Configuration :
```bash
git config --global user.name "NDOY3M4N"
git config --global user.email pa.ndoye@outlook.fr
```
- Quelques commandes utiles :
```bash
git init # A taper sur un répertoire pour créer un REPO local
git add . #  Pour ajouter les fichiers/dossiers dans notre REPO local
git add -p # Ajoute les fichiers modifiés
git commmit -m "message" # Pour confirm les modifs qu l'on vient de faire
git remote add origin https://github.com/NDOY3M4N/UBUNTU-SETUP-101.git # Connexion à un REPO distant
git push -u origin master # LOCAL vers SERVEUR GITHUB
git pull -u origin master # SERVEUR GITHUB vers LOCAL
```

## Configurer un LAMP

LAMP est l'acronyme de Linux Apache MySQL PHP. Pour l'installation ? Easy
```bash
sudo apt install apache2
sudo apt install php7
sudo apt install mysql-server
sudo apt install phpmyadmin
```
__NB : Il se peut que MySQL pose quelques problèmes, KEEP CALM, YOLO. Suit juste ce lien bruh :arrow_right: [MYSQL](https://linuxconfig.org/how-to-reset-root-mysql-password-on-ubuntu-18-04-bionic-beaver-linux).__

## Configurer Neovim

Neovim est une alternative à VIM. Pour plus d'infos, va sur leur site (fainéant).
Donc, pour l'installation :
```bash
sudo apt install neovim
sudo apt install fonts-powerline
```
Après, il faut créer un fichier de configuration
```bash
mkdir ~/.config/nvim
touch init.vim
```
La plupart des config de Neovim seront dans ce fichier. Une des raisons pour laquelle VIM est spuer puissant est à cause des son système de plugins. Donc nous allons tout de suite installer un système de plugin pour notre neovim. On va utiliser *vim-plug*.
```bash
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
Après l'installation, on édite le fichier de configuration *init.vim*
```
call plug#begin('~/.local/share/nvim/plugged')

Plug 'airblade/vim-gitgutter'
Plug 'editorconfig/editorconfig-vim'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'cocopon/iceberg.vim'
Plug 'junegunn/fzf'
Plug 'junegunn/fzf.vim'
Plug 'mattn/emmet-vim'
Plug 'scrooloose/nerdtree'
Plug 'terryma/vim-multiple-cursors'
Plug 'tpope/vim-eunuch'
Plug 'tpope/vim-surround'
Plug 'w0rp/ale'
Plug 'noahfrederick/vim-noctu'
Plug 'morhetz/gruvbox'
Plug 'ctrlpvim/ctrlp.vim'
Plug 'Yggdroot/indentLine'

call plug#end()
filetype plugin indent on    " required

" Mes Raccourcis
map <C-o> :NERDTreeToggle<CR>

" custom settings for me
set mouse=a
set number
set encoding=utf-8
set backspace=indent,eol,start
set cursorline
set guioptions=
syntax on

" indent for global
set expandtab
set shiftwidth=4
set softtabstop=4
set autoindent

" indent for special file
autocmd FileType c,cpp setlocal expandtab shiftwidth=2 softtabstop=2 cindent 
autocmd FileType python setlocal expandtab shiftwidth=4 softtabstop=4 autoindent

" setup for gruvbox
set t_Co=256
set background=dark
colorscheme iceberg
" colorscheme gruvbox
" let g:gruvbox_contrast_dark = 'soft'

" setup for ctrlp
let g:ctrlp_map = '<c-p>'
let g:ctrlp_cmd = 'CtrlP'
let g:ctrlp_working_path_mode = 'ra'
let g:ctrlp_custom_ignore = '\v[\/]\.(git|hg|svn)$'
let g:ctrlp_custom_ignore = {
  \ 'dir':  '\v[\/]\.(git|hg|svn)$',
  \ 'file': '\v\.(exe|so|dll)$',
  \ 'link': 'some_bad_symbolic_links',
  \ }
set wildignore+=*/tmp/*,*.so,*.swp,*.zip
let g:ctrlp_user_command = ['.git', 'cd %s && git ls-files -co --exclude-standard']

" setup for indent line
let g:indentLine_char = '|'
set tags=./tags,tags;$HOME

" Powerline Fonts
let g:airline_powerline_fonts = 1
```
Après avoir enregistrer et fermer le fichier, on lance nvim et on y tape la commande
```bash
:PlugInstall
```
Cela va installer les plugins qui se trouvent dans notre fichier de configration.

## Configuration de mon terminal

Pour l'instant va sur ces liens
- https://www.youtube.com/watch?v=s-9wo2v3tsk
- https://www.youtube.com/watch?v=iwH1XqVjZOE
- https://www.youtube.com/watch?v=UsKd9Y42Mo0

[Update_img]: img/install_update.png
[Codecs_img]: img/codecs.png
[Battery_img]: img/battery_info.png
