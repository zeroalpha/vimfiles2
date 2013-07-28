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
desc "Install dependencies (sudo), download and compile vim (on ~/.src)"
task :vim => ["vim:dep", "vim:compile"]

desc "Symlink vimrc/gvimrc"
task :symlink do
  sh <<-SH
  ln -s ~/.vim/vimrc ~/.vimrc
  ln -s ~/.vim/gvimrc ~/.gvimrc
  SH
end

namespace :bundle do
  desc "Install Vundle"
  task :vundle do
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
task :all => [:symlink, "bundle:clone", "bundle:install"]
