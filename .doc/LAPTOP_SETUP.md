# LAPTOP SETUP

1. start the machine

   1. choose all sain settings for your locale
   1. log into **iCould account** even for work laptop
      > this will allow you to save documents and notes to the
      > cloud which may be helpful for transferring to another
      > machine, a backup, accessing from a phone or the web,
      > finding your device, etc.

1. **System Update**

   1. once fully booted
   1. run a system update `System Preferences -> Software Updates`
      > every new machine is likely to be behind on software
      > updates

1. install command line tools

   ```
   xcode-select --install
   ```

1. **using existing .dotfiles**

   ```
   git clone --bare git@github.com:sjalex78/.dotfiles.git $HOME/.dotfiles
   # based on which git
   alias config='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
   config status
   config config --local status.showUntrackedFiles no
   ```

1. **Git**

   1. review your `~/.gitconfig` file using, below, it should be already setup
      ```
      git config --global --edit
      ```
   1. or use the following to set it up
   1. use the default git that comes with mac
   1. create or bring across your ssh key and make sure it's in gitlab
      [Preferences -> User Settings -> SSH
      Keys](https://gitlab.com/-/profile/keys) as per instructions in
      https://docs.gitlab.com/ee/ssh/#rsa-ssh-keys
      ```
      # NEW
      # based on
      #  https://www.keystash.io/guides/how-to-generate-the-best-ssh-keys.html
      ssh-keygen -o -a 100 -t ed25519
      # OLD
      ssh-keygen -t rsa -b 2048 -C "my UNIQUE NAME key"
      ```
   1. setup sane git defaults
      ```
      git config --global pull.rebase true
      git config --global user.name "Sarah Alexander"
      git config --global user.email sjalex78@gmail.com
      git config --global core.editor vi
      # git config --global core.editor "code --wait"
      git config --global --replace-all core.pager "less -F -X"
      git config --global init.defaultBranch main
      git config --global core.excludesfile ~/.gitignore_global
      git config --global commit.template ~/.gitmessage.txt
      ```
   1. setup `~/.gitmessage.txt` file with current pairs (NOTE: this can also
      be done per directory tree or repository)

      ```sh
      cat <<EOF > ~/.gitmessage.txt


      # Co-authored-by: Pair Name <pair-email-id>
      #
      # Co-authored-by: Michael Milewski <saramic@gmail.com>
      EOF
      ```

   1. review your `~/.gitconfig` file using

      ```
      git config --global --edit
      ```

   1. slow directory listing?
      https://stackoverflow.com/a/25864063
      ```
      git config --add oh-my-zsh.hide-status 1
      git config --add oh-my-zsh.hide-dirty 1
      ```

1. **Mandatory Setup**
   these are referenced by the dot files above

   1. **Brew** _(also see below)_
      ```
      /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
      ```
   1. **OhMyZSH** _(also see below)_

      ```
      sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

      # confirm changes and ignore the new .zshrc file
      vimdiff .zshrc .zshrc.pre-oh-my-zsh
      mv .zshrc.pre-oh-my-zsh .zshrc
      ```

   1. **ASDF install**
      ```
      asdf install
      ```

1. **Configure essentials**

   1. **iTerm**
      1. setup zsh with ohmyzsh via https://ohmyz.sh/#install (or
         github - https://github.com/ohmyzsh/ohmyzsh)
      ```
      sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
      ```
      1. iTerm2 -> **make iterm2 default terminal**
      1. iTerm2 -> **install shell integation**
      1. Profiles -> General -> Working Directory: **Reuse previous sessions
         directory**
      1. background color: **#212121**
      1. font: **18**
      1. Profiles -> Terminal -> Scrollback Buffer : **unlimited scrollback**
      1. General -> tmux -> When attaching, resotre windows as: **Native tabs
         in a new window**
      1. Add script to support iterm command click
         `.bin/iterm_command_click`
   1. **VS Code**
      1. install worthwhile plugins (or use a shared `.vscode` file)
         > 1. ensure press and hold key repeat works
         >
         > ```
         > defaults write -g ApplePressAndHoldEnabled -bool false
         > defaults write com.microsoft.VSCode ApplePressAndHoldEnabled -bool false
         > ```

1. **Brew**

   1. use homebrew to manage most dependencies https://brew.sh
   1. following the instructions from above site, in terminal run something
      similar to
      ```
      /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
      ```
   1. don't forget to do the final step of the previous command to add it to your profile

   ```
   echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
   eval "$(/opt/homebrew/bin/brew shellenv)"
   ```

   1.

1. **install ASDF** runtime version manager (JS, Ruby, Python, Postgres, etc)

   1. should have been done using `make update-dev-env`
   1. if `asdf` command does not work maybe you forgot to add `asdf` to `.zshrc`

   ```
   echo '. $HOME/.asdf/asdf.sh' >> ~/.zshrc
   ```

1. **Mac OSX** some sane non standard settings
   1. right click the dock **Turn Hiding On**
   1. Finder
      1. show hidden files `Cmd Shift .`
      1. add useful diredctory shortcuts
         1. in terminal, open 1 below your home directory `open ~/..`
         1. drag your home directory to LHS Favourites
         1. navigate to Projects and drag that to LHS Favourites
   1. System Prefrences -> Keyboard -> Key repeat **fast**
   1. System Prefrences -> Keyboard -> Delay until repeat **short**
   1. System Prefrences -> Trackpad -> **tap to click**
   1. System Prefrences -> Mouse -> **Secondary click**
   1. System Prefrences -> Control Centre -> Bluewtooth -> **Show in Menu Bar**
   1. Power moves (vi users)
      1. System Prefrences -> Keyboard -> Keyboard Shortcuts...
         -> Modifier Keys -> Caps Lock Key -> Escape
