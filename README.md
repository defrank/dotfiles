[![Tasks Ready](https://badge.waffle.io/defrank/dotfiles.svg?label=ready&title=Ready)](http://waffle.io/defrank/dotfiles?label=ready)
[![Tasks in Progress](https://badge.waffle.io/defrank/dotfiles.svg?label=wip&title=WIP)](http://waffle.io/defrank/dotfiles?label=wip)

# holman does dotfiles

Your dotfiles are how you personalize your system. These are mine.

I was a little tired of having long alias files and everything strewn about
(which is extremely common on other dotfiles projects, too). That led to this
project being much more topic-centric. I realized I could split a lot of things
up into the main areas I used (Ruby, git, system libraries, and so on), so I
structured the project accordingly.

If you're interested in the philosophy behind why projects like these are
awesome, you might want to [read my post on the
subject](http://zachholman.com/2010/08/dotfiles-are-meant-to-be-forked/).

The supported shell for these dotfiles is Zsh.  Consider reading the
[guide](http://zsh.sourceforge.net/Guide/zshguide.html) if you are
unfamiliar with it.

## topical

Everything's built around topic areas. If you're adding a new area to your
forked dotfiles — say, "Java" — you can simply add a `java` directory and put
files in there. Anything with an extension of `.zsh` will get automatically
included into your shell. Anything with an extension of `.symlink` will get
symlinked without extension into `$HOME` when you run `script/bootstrap`.

## what's inside

A lot of stuff. Seriously, a lot of stuff. Check them out in the file browser
above and see what components may mesh up with you.
[Fork it](https://github.com/holman/dotfiles/fork), remove what you don't
use, and build on what you do use.

## components

There's a few special files in the hierarchy.

- **bin/**: Anything in `bin/` will get added to your `$PATH` and be made
  available everywhere.
- **Brewfile**: This is a list of applications for
  [Homebrew Cask](http://caskroom.io) to install: things like Chrome and
  1Password and Adium and stuff. Might want to edit this file before
  running any initial setup.
- **topic/\*.zsh**: configuration files
    - Environment configuration (i.e., `.zshenv`)
        - **topic/\*path.zsh**: Any file ending with `path.zsh` (except
          those ending with `fpath.zsh`) is loaded first and is expected
          to setup `$PATH` or similar.
        - **topic/\*env.zsh**: Any file ending with `env.zsh` is loaded
          second and is expected to setup any additional environment
          (e.g., shell options).
    - Interactive configuration (i.e., `.zshrc`)
        - **topic/\*fpath.zsh**: Any file ending with `fpath.zsh` is
          loaded for interactive shells only.  They are expected to
          populate `$fpath`.
        - **topic/\*.zsh**: Any files ending in `.zsh` (except those
          specified elsewhere) are loaded for interactive shells only.
          Interactive configuration can include aliases, color output,
          prompt configuration, or anything else that should only be
          loaded when a user is interacting with Zsh.
        - **topic/\*completion.zsh**: Any file ending with
          `completion.zsh` is loaded last for interactive shells only.
          They are expected to setup autocomplete.
    - Login configuration (i.e., `.zprofile`, `.zlogin`, `.zlogout`)
        - **topic/\*profile.zsh**: Any file ending with `profile.zsh` is
          loaded for login shells only.  Unlike `.zlogin`, these files
          are loaded before the interactive files above are loaded.
        - **topic/\*login.zsh**: Any file ending in `login.zsh` is
          loaded for login shells only.  Unlike `.zprofile`, they are
          loaded after your interactive files are loaded above.  This is
          the ideal place to put anything you want to see when you start
          up a new login shell (e.g., cowsay, date, todo, fortune).
        - **topic/\*logout.zsh**: Any file ending in `logout.zsh` is
          loaded for login shells only and only when you exit/logout the
          shell.
- **topic/\*.symlink**: Any files ending in `*.symlink` get symlinked into
  your `$HOME`. This is so you can keep all of those versioned in your dotfiles
  but still keep those autoloaded files in your home directory. These get
  symlinked in when you run `script/bootstrap`.

## install

Run this:

```sh
git clone https://github.com/holman/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
script/bootstrap
```

This will symlink the appropriate files in `.dotfiles` to your home directory.
Everything is configured and tweaked within `~/.dotfiles`.

The main file you'll want to change right off the bat is
`zsh/zshenv.symlink`, which sets up a few paths that'll be different on
your particular machine.

`dot` is a simple script that installs some dependencies, sets sane macOS
defaults, and so on. Tweak this script, and occasionally run `dot` from
time to time to keep your environment fresh and up-to-date. You can find
this script in `bin/`.

## test

Because you don't want to necessarily ruin your local environment
everytime you make a change, let's use Docker.

**Note:** you can only test the pieces of your dotfiles that will work
in a Linux environment.  macOS specifics cannot be tested.

### dependencies

#### docker

Be sure Docker is installed.

##### macOS

    brew cask install docker

### run

    ./test/run.sh

## bugs

I want this to work for everyone; that means when you clone it down it should
work for you even though you may not have `rbenv` installed, for example. That
said, I do use this as *my* dotfiles, so there's a good chance I may break
something if I forget to make a check for a dependency.

If you're brand-new to the project and run into any blockers, please
[open an issue](https://github.com/holman/dotfiles/issues) on this repository
and I'd love to get it fixed for you!

## thanks

I forked [Ryan Bates](http://github.com/ryanb)' excellent
[dotfiles](http://github.com/ryanb/dotfiles) for a couple years before the
weight of my changes and tweaks inspired me to finally roll my own. But Ryan's
dotfiles were an easy way to get into bash customization, and then to jump ship
to zsh a bit later. A decent amount of the code in these dotfiles stem or are
inspired from Ryan's original project.
