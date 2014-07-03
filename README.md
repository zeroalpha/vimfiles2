Vimfiles
========

Vim files for Linux and Windows


## One line install
0. \curl -L https://raw.github.com/zeroalpha/vimfiles2/master/install.sh | bash


## Manual Install
1. Clone this repository:

    ```
    $ git clone https://github.com/zeroalpha/vimfiles2.git ~/.vim
    $ cd ~/.vim
    ````


2. Optional: install vim with python and ruby support (needed for some plugins)

    ```
    $ make vim_source
    ```

3. Install Vundle, and Plugins and symlink vimrc to ~/.vimrc

    ````
   $ make install
    ```

#### Credits
Big thanks to [zealot128](https://github.com/zealot128/vimfiles2) for introducing me to vim and providing this glorious set of plugins and settings neatly bundled
