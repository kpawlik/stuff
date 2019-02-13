* [File path (current)](#file-path-current)                             
* [Comment](#comment)                                                   
* [Search word under cursor](#search-word-under-cursor)                 
  * [Replace  WebApps by HELL](#replace--webapps-by-hell)               
  * [Cleas search results](#cleas-search-results)                       
  * [Show tabs](#show-tabs)                                             
  * [Next tab](#next-tab)                                               
* [Windows](#windows)                                                   
  * [Split window](#split-window)                                       
  * [Switch window](#switch-window)                                     
* [show line numbers](#show-line-numbers)                               
* [Show whitespace](#show-whitespace)                                   
* [SESSION](#session)                                                   
  * [save](#save)                                                       
  * [load](#load)               
* [CRONTAB](#crontab)
* [PASTE](#paste)

```sh
sshpass -p'A!!min3' scp -r ~/.vim  catl0dlas10012:~/
sshpass -p'A!!min3' scp -r ~/.vimrc  catl0dlas10012:~/

sshpass -p'A!!min3' scp -r ~/.vim  catl0dlas10014:~/
sshpass -p'A!!min3' scp -r ~/.vimrc  catl0dlas10014:~/
```
# File path (current)

[Get_the_name_of_the_current_file](http://vim.wikia.com/wiki/Get_the_name_of_the_current_file)

```
:echo @% 
```

# Comment 
```
:map cl 0i//<Esc>
:map ucl 02x

:map cl 0i#<Esc>
:map ucl 01x
```
# Search word under cursor
```
*
```
#Incremental search
```
:set incsearch
```
#Replace 
## Replace  WebApps by HELL
```
:%s@WebApps@HEL
```
##Replace /WebApps/ by --HELL--/
```
:%s@\/WebApps\/@--HELL--/
```
## Cleas search results
```
:noh
```
#Tabs

## Show tabs
```
:tab ball
```
## Next tab
```
gt
```
#Edit file/folder
```
:edit <path>
```
# Windows

## Split window
```
Ctrl+w v
```
## Switch window
```
Ctrl+w Ctrl+w
```
# show line numbers
```
:set number
```
# Show whitespace
```
:set list
:set nolist
```
# SESSION
## save
```
:mksession ~/path
```

## load 
```
:source ~/path
```
# CRONTAB
```
edit:
~/.bash_profile

and set:

EDITOR=/usr/bin/vim
export EDITOR
```

# PASTE
## turn off auto intend
```
:set paste
```

