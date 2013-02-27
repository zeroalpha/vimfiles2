namespace :vim do
  desc "Install Dependencies for Ubuntu/Debian"
  task :dep do
    sh <<-SH
      sudo apt-get install libncurses-dev  libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev ruby-dev python-dev git-core
    SH
  end
  desc "download and compile vim"
  task :compile do
    sh <<-SH
      mkdir ~/.src -p
      cd ~/.src
      wget ftp://ftp.vim.org/pub/vim/unix/vim-7.3.tar.bz2
      tar jxf vim-7.3.tar.bz2
      cd vim73/
      ./configure --with-features=huge --enable-gui=gnome2 --enable-rubyinterp --enable-pythoninterp
      make
      sudo make install
    SH
  end
end
desc "Install dependencies, download and compile vim"
task :vim => ["vim:dep", "vim:compile"]

namespace :powerline do
  desc "install powerline"
  task :install do
    sh <<-CMD
      pip install --user git+git://github.com/Lokaltog/powerline
    CMD
  end
  desc "install powerline fonts"
  task :font do
    sh <<-CMD
      mkdir -p ~/.fonts
      wget https://github.com/Lokaltog/powerline/raw/develop/font/PowerlineSymbols.otf -O ~/.fonts/PowerlineSymbols.otf
      fc-cache -vf ~/.fonts
      mkdir -p ~/.config/fontconfig/conf.d/
      wget https://github.com/Lokaltog/powerline/raw/develop/font/10-powerline-symbols.conf -P ~/.config/fontconfig/conf.d/10-powerline-symbols.conf
      echo "Fonts installed, restart terminal"
    CMD
  end
end
task :powerline => ["powerline:font", "powerline:install"]

desc "Symlink vimrc/gvimrc"
task :symlink do
  sh <<-SH
  ln -s ~/.vim/vimrc ~/.vimrc
  ln -s ~/.vim/gvimrc ~/.gvimrc
  SH
end

namespace :bundle do
  desc "Install Vundle" 
  task :clone do
    sh <<-SH
    mkdir -p ~/.vim/bundle
    git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle
    SH
  end

  desc "Install Vundle packages"
  task :install do
    sh <<-CMD
    vim +BundleInstall +qall
    CMD
  end
end
task :bundle => ["bundle:install"]
task :all => [:symlink, "bundle:clone", "bundle:install", :powerline]
