(Looking for the old version? Check out the [version2](https://github.com/mroth/bootstrapper/tree/version2) branch!)

# Bootstrapper
Scripts and walkthroughs to bootstrap my new Macs when I get them.  This doesn't happen all too often, but in between home, work, desktops, laptops, catastrophic hardware failures, etc., it happens more often than I'd like!

The main things this handles (thus far):

 - RVM and Ruby 1.9.x
 - Node.js and NPM, with global CoffeeScript
 - Other handy CLI stuff: homebrew, git, ack, ssh-copy-id, etc...
 - Common libraries: XQuartz, ImageMagick
 - zsh shell with oh-my-zsh and syntax highlighting
 - Installs a bunch of common applications for dev types: Chrome, Firefox, MacVim, TextMate, SublimeText, Dropbox, VirtualBox/Vagrant, SizeUp...
 - Easy dotfile management via [homesick](https://github.com/technicalpickles/homesick)
 - A macro-update task to update *everything* for us OCD-compulsives. 
 - Everything should easily customizeable

This is still a bit of a mess, but getting cleaned up over time, and is approaching the point where it could be easily customized for your own usage.


## Philosophy
Tasks should be runnable at any time, creating/repairing installations when needed, ignoring stuff if already exists.

## Version 3
Moved to using chef recipes for software installation.  Trying to backport all my needed installs into `pivotal_workstation` project so they can benefit others!

## Installation
Make sure you have Apple Dev tools installed because life is impossible on a Mac otherwise (shame this part can't be automated).

Do `sudo gem install bundler; bundle install` in this repo directory.  This will get all your pre-dependencies going.

### Bootstrap
Just do `rake bootstrap`

To just do software installation (in case you don't have a dotfile repo), you can do bootstrap:software which will get the entire environment up and going but won't mess with configuration management.

## Doing stuff manually instead
Tasks can be run invidually if needed.

### Main software installation

Once bundle dependencies are installed, can be run via `cookbooks:converge`.

Want to modify what gets installed?  You can edit the list of recipes in `soloistrc`.

### Other software setup (Rake tasks)
There are a few for things that haven't been backported into chef recipes in pivotal_workstation yet.

  * install coffeescript `node:coffee_install`
  * zsh syntax highlighting `zsh:syntax_highlighting_install`
  * install macvim and janus `vim:install`

TODO: All of these can be done via task `:extras`

### Configuration management
#### Dotfiles
User dotfiles are now managed via homesick.  Do `rake dotfiles:install` to get things going.
By default, we look for `$USERNAME/dotfiles` on Github, and we try to infer your GitHub username from system environment.  To manually override, you can set `DOTFILES_GITHUB_USERNAME` and/or `DOTFILES_REPO_NAME`, like so `DOTFILES_GITHUB_USERNAME=johndoe rake dotfiles:setup`
Alternately, you can simply do it manually by following the instructions on the homesick page (or not).

#### SublimeText user folder
To link... TODO DESC

### Updating ALL THE THINGS
Since we're OCD, we need a script update everything.  TODO rewrite for new system
