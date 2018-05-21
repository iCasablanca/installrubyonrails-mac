---
title: Install Ruby on Rails 5.2 · macOS · RailsApps

language_tabs: # must be one of https://git.io/vQNgJ

toc_footers:
  - It's open source
  - Questions? <a href='https://stackoverflow.com/questions/tagged/ruby-on-rails'>Ask on Stack Overflow</a>
  - Have fixes? <a href='https://github.com/RailsApps/installrubyonrails-mac'>Edit the GitHub repo</a>
  - Want more? <a href='http://railsapps.github.io/'>Visit RailsApps</a>


includes:
  - errors

search: true
---

# Install Ruby on Rails 5.2 · macOS

#### by Daniel Kehoe

_Last updated 3 April 2018_

> What is the RailsApps Project?

> This is an article from the RailsApps project. The [RailsApps project](http://railsapps.github.io/) provides [Rails Example Applications](http://railsapps.github.io/) that developers use as starter apps. Rails changes frequently; each application is known to work and serves as your personal "reference implementation."

Install Ruby on Rails 5.2 on macOS High Sierra. Up-to-date and detailed instructions, plus troubleshooting, for the Rails newest release. How to set up and install Rails 5.2, the newest version of Rails, on macOS 10.13 High Sierra.

This is the most complete and up-to-date installation guide for Ruby on Rails on macOS and a favorite of Rails developers. In addition to installing Rails, it explains how to set up a development environment for Rails, the same as used by any professional Rails developer.

If you like the level of detail and explanation in this article, you will like the book [_Learn Ruby on Rails_](http://learn-rails.com/learn-ruby-on-rails.html).

### If You Are New to Rails

To use Rails on macOS, you'll need Ruby (an interpreter for the Ruby programming language) plus gems (software libraries) containing the Rails web application development framework. If you're new to Rails, see [What is Ruby on Rails?](http://railsapps.github.io/what-is-ruby-rails.html).

### Ruby Version Managers

> Don't Use a One-Click Installer

> You may hear about one-click installation programs such as [RailsInstaller](http://railsinstaller.org/), [Cinderella](http://www.atmos.org/cinderella/), and [BitNami RubyStack](http://bitnami.org/stack/rubystack). These installation programs are often outdated. Most developers install from scratch.

MacOS comes with a "system Ruby" pre-installed. MacOS High Sierra includes Ruby 2.0 which is not the newest version. Do not use the system Ruby (see [an article](https://robots.thoughtbot.com/psa-do-not-use-system-ruby) for why). You should install a Ruby version manager and update to the newest Ruby version. You'll find instructions below.

A Ruby version manager makes it easy to switch between Ruby versions. I recommend [Chruby](https://github.com/postmodern/chruby) (and provide instructions here). In the past, [RVM](https://rvm.io/) was popular but its additional features (its gemsets) are no longer necessary and it adds unnecessary complexity. Sam Stephenson's [rbenv](https://github.com/sstephenson/rbenv) is also popular, but requires extra steps (the rehash command) and modifies gems when you install them.

If you are maintaining older Rails applications, you will need a Ruby version manager. And in the future, you will need to install newer Ruby versions as they are released. Even if you are a student only building new Rails applications, you should be prepared to manage multiple versions of Ruby. These are all reasons to use a Ruby version manager such as [Chruby](https://github.com/postmodern/chruby).

You'll need to prepare your computer before installing Ruby on Rails.

## Prepare Your Computer

> A Hosted Development Alternative

> You can use Ruby on Rails without actually installing it on your computer. Hosted development, using a service such as [Cloud9](https://c9.io/), means you get a computer "in the cloud" that you use from your web browser. Any computer can access the hosted development environment, though you'll need a broadband connection. Cloud9 is free for small projects.

> Using a hosted environment means you are no longer dependent on the physical presence of a computer that stores all your files. If your computer crashes or is stolen, you can continue to use your hosted environment from any other computer. Likewise, if you frequently work on more than one computer, a hosted environment eliminates the difficulty of maintaining duplicate development environments. For these reasons some developers prefer to "work in the cloud" using Cloud9. For more on Cloud9, see the article [Ruby on Rails with Cloud9](http://railsapps.github.io/rubyonrails-cloud9.html). Cloud9 is a good option if you have trouble installing Ruby on Rails on your Mac.

These instructions can be used for macOS 10.9 Mavericks, 10.10 Yosemite, or 10.11 El Capitan. However, you should upgrade to macOS 10.13 High Sierra if you can.

### If You Updated to macOS High Sierra

If you updated to High Sierra from an earlier version of macOS (sometimes called an "over the top" installation), and you previously installed a Rails development environment, your earlier installation remains intact. You will need to [install the new version of Xcode Command Line Tools](http://railsapps.github.io/xcode-command-line-tools.html) (full instructions below). Though Rails is still intact after an update, read through this article and take this opportunity to update your development environment.

### Upgrade macOS to 10.13

MacOS High Sierra was released on September 25, 2017. Make sure you have the latest version of macOS. Under the Apple menu, check "About This Mac." It should show "Version 10.13.0" or newer. If you've owned your Mac for several years and haven't updated macOS, be prepared to spend several hours updating the operating system.

If you need to upgrade, see Apple's instructions [How to upgrade to macOS High Sierra](http://www.apple.com/osx/how-to-upgrade/). You can install macOS 10.13 (High Sierra) from the Mac App Store for free. Allow plenty of time for the download and installation (it may take several hours).

### Terminal Application (for Beginners)

> To learn more about Unix shell commands, read [The Command Line Crash Course](https://learnpythonthehardway.org/book/appendixa.html) or [Learn Enough Command Line to Be Dangerous](http://www.learnenough.com/command-line-tutorial).

You'll need to use the Terminal application to install Ruby and develop Rails applications. The [Terminal application](http://en.wikipedia.org/wiki/Terminal.app) or _console_ gives us access to the Unix command line, or _shell_. We call the command line the shell because it is the outer layer of the operating system's internal mechanisms (which we call the kernel). Search for the macOS Terminal application by pressing the Command-Spacebar combination (which Apple calls "Spotlight Search") and searching for "Terminal." Or look in the **Applications/Utilities/** folder for the Terminal application.

Launch the Terminal application. Then try out the terminal application by entering a shell command:

```shell
$ whoami
```

`$ whoami`

Don't type the `$` character. The `$` character is a cue that you should enter a shell command. This is a longtime convention that indicates you should enter a command in the terminal application. The Unix shell command `whoami` returns your username.

Just a reminder to absolute beginners: Press "Enter" after you type the command.

### Is Xcode Already Installed?

You need to install Apple's [Xcode Command Line Tools](http://railsapps.github.io/xcode-command-line-tools.html) to get the Unix tools needed to install Ruby and develop with Rails. Xcode is Apple's software library for macOS developers. You don't need all of Xcode for Rails development. You just need the Xcode Command Line Tools. Only install the full Xcode package if you are doing development of applications for the Apple operating systems.

Check if you have previously installed the full Xcode package:

```
$ xcode-select -p
```


`$ xcode-select -p`

If you see:

`xcode-select: error: unable to get active developer directory...`

The Xcode package is not installed. Jump to the next section and install only the Xcode Command Line Tools.

If you see:

`/Applications/Xcode.app/Contents/Developer`

or

`/Library/Developer/CommandLineTools`

The full Xcode package is already installed. Maybe you or someone else installed it previously.

If Xcode is installed, you will need to update Xcode to the newest version (Xcode 7.1 or newer). Go to the App Store application and check "Updates." After updating Xcode, be sure to launch the Xcode application and accept the Apple license terms.

If you see a file location that contains spaces in the path:

`/Applications/Apple Dev Tools/Xcode.app/Contents/Developer`

you may have problems installing Ruby. You should delete and reinstall Xcode.

### Install Xcode Command Line Tools

The Xcode Command Line Tools provide a C language compiler needed to install Ruby. For many Rails projects, you will need the C language compiler to install gems that use native extensions.

Here's how to install Apple's Xcode Command Line Tools.

MacOS High Sierra will alert you when you enter a command in the terminal that requires Xcode Command Line Tools. For example, you can enter `gcc`, `git`, or `make`.

Try it. Enter:

```shell
$ gcc
```

`$ gcc`

If Xcode Command Line Tools are not installed, you'll see an alert box:

![alert Xcode Command Line Tools is required](http://railsapps.github.io/images/installing-mavericks-popup.png "alert Xcode Command Line Tools is required")

Alternatively, you can use a command to install Xcode Command Line Tools. It will produce a similar alert box. Note the double hyphen:

`$ xcode-select --install`

Click "Install" to download and install Xcode Command Line Tools.

The instructions in the alert box are confusing. You don't need to "Get Xcode" from the App Store. Just click "Install" for the Xcode Command Line Tools. If you have a slow Internet connection, it may take many minutes.

If the download takes a very long time (over an hour) or fails, you can try an alternative. Go to [https://developer.apple.com/downloads/more](https://developer.apple.com/downloads/more)
and enter your Apple ID and password. You'll be asked to agree to the terms of the Apple Developer Program.
  You'll see a list of software packages you can download. Look for the latest version of _Command Line Tools_
and click to download the _.dmg_ file. Downloading the _.dmg_ file is much faster than waiting for
the command-line-based download. Install the _.dmg_ file by clicking on the package icon.

![downloading Xcode Command Line Tools](http://railsapps.github.io/images/installing-mavericks-download.png "downloading Xcode Command Line Tools")

![installed Xcode Command Line Tools](http://railsapps.github.io/images/imstalling-mavericks-installed.png "installed Xcode Command Line Tools")

Verify that you've successfully installed Xcode Command Line Tools.

```
$ xcode-select -p
/Applications/Xcode.app/Contents/Developer
```

`$ xcode-select -p`

The Xcode Command Line Tools must be installed before you go to the next steps. Just to be certain, verify that `gcc` is installed.

```shell
$ gcc --version
Configured with: --prefix=/Library/Developer/CommandLineTools/usr --with-gxx-include-dir=/usr/include/c++/4.2.1
Apple LLVM version 7.0.0 (clang-700.1.76)
Target: x86_64-apple-darwin15.0.0
Thread model: posix
```

`$ gcc --version`

## Configure Git

Before installing Ruby on Rails, you should configure Git. Git is automatically installed as part of the Xcode Command Line Tools.

[Git](http://git-scm.com/) provides a source control repository. Developers use Git to roll back code changes when needed, to collaborate with others, and deploy applications for hosting with a service such as Heroku. As a Rails developer, you'll use Git with a [GitHub](https://github.com/) account for remote backup and collaboration. See the article [Rails with Git and GitHub](http://railsapps.github.io/rails-git.html) for more background.

Before you configure Git, it is a good idea to [create an account on GitHub](https://help.github.com/articles/signing-up-for-a-new-github-account/). It is important to use the same email address for Git and for GitHub. After you create an account on GitHub, follow their instructions to [set up an SSH key](https://help.github.com/articles/connecting-to-github-with-ssh/) so you don't have to enter a username and password every time you connect to GitHub from the Terminal.

```shell
$ git version
git version 2.8.2
```

Check that Git is installed:

`
$ git version
`

You should see `git version 2.8.2` (or newer).

```shell
$ git config -l --global
fatal: unable to read config file '/Users/.../.gitconfig': No such file or directory
$ git config --global user.name "Your Real Name"
$ git config --global user.email me@example.com
$ git config -l --global
user.name=Your Real Name
user.email=me@example.com
```

Configure Git if you haven't used it before. First, list the current settings with the `git config -l --global` command. Then set `user.name` and `user.email` if necessary. Don't just copy and paste the code you see here. Edit it to add your name and the email address you've used for GitHub.

Now you'll be ready to use Git when you need it.

## Install Homebrew

Developers use Homebrew to install various Unix software packages, including [chruby](https://github.com/postmodern/chruby) and [ruby-install](https://github.com/postmodern/ruby-install).

If you did not use a password to log in to your Mac (that is, if your password is blank), you cannot install Homebrew.

```shell
$ brew
-bash: brew: command not found
```

`$ brew`

Check if Homebrew is installed.

If Homebrew is not installed, install it.

```shell
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

`$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

The Homebrew installation script will display a warning and ask you to enter your Mac password.

`WARNING: Improper use of the sudo command could lead to data loss...`

`To proceed, enter your password...`

`Password:`

Ignore the scary warning and enter your Mac password. You won't see the characters as you type. Press enter when you are done.

If you've installed Homebrew, you can check that Homebrew is installed properly.

```shell
$ brew doctor
Your system is ready to brew.
```

`$ brew doctor`

You may notice that we use Ruby to install Homebrew. We use the macOS pre-installed system version of Ruby to install Homebrew. Soon we'll add a newer version of Ruby.

## Install Ruby-install and Chruby

```shell
$ brew install ruby-install chruby
==> Downloading https://homebrew.bintray.com/bottles/ruby-install-0.6.1.sierra.b
######################################################################## 100.0%
==> Pouring ruby-install-0.6.1.sierra.bottle.tar.gz
🍺  /usr/local/Cellar/ruby-install/0.6.1: 27 files, 67.6KB
==> Downloading https://homebrew.bintray.com/bottles/chruby-0.3.9.sierra.bottle.
######################################################################## 100.0%
==> Pouring chruby-0.3.9.sierra.bottle.tar.gz
==> Caveats
Add the following to the ~/.bash_profile or ~/.zshrc file:
  source /usr/local/opt/chruby/share/chruby/chruby.sh

To enable auto-switching of Rubies specified by .ruby-version files,
add the following to ~/.bash_profile or ~/.zshrc:
  source /usr/local/opt/chruby/share/chruby/auto.sh
==> Summary
🍺  /usr/local/Cellar/chruby/0.3.9: 11 files, 50.0KB
```

Use Homebrew to install the [ruby-install](https://github.com/postmodern/ruby-install) utility and the [chruby](https://github.com/postmodern/chruby) Ruby version manager.

`$ brew install ruby-install chruby`

You'll see beer mug emojis (part of the [Emoji 1.0](https://en.wikipedia.org/wiki/Emoji) standard released in 2015).

### Configure Chruby

You must update your Unix *.bash_profile* file so that the chruby program can be found.

The *.bash_profile* file is in your user home folder. It is hidden in the file browser. You can force the Mac to display hidden files by entering the following command in the Terminal application:

```shell
$ defaults write com.apple.finder AppleShowAllFiles TRUE; killall Finder
```

`$ defaults write com.apple.finder AppleShowAllFiles TRUE; killall Finder`

Hidden files will appear in gray in the Finder window.

Use your text editor (typically [Atom](https://atom.io/) or [Sublime](https://www.sublimetext.com/)) to open the *.bash_profile* file.

To open the *.bash_profile* file with Atom:

`$ atom ~/.bash_profile`

In Unix, the squiggle (tilde) character is a shortcut to your user home folder.

Add two lines anywhere in your *.bash_profile* file.

```shell
### ~/.bash_profile
source /usr/local/share/chruby/chruby.sh
source /usr/local/share/chruby/auto.sh
```

`source /usr/local/share/chruby/chruby.sh`

`source /usr/local/share/chruby/auto.sh`

The first line makes the chruby program available in the shell. The second line will automatically switch the current version of Ruby when you change directories if a hidden file indicates a specific Ruby version.

You must close and reopen the Terminal window for the changes to the *.bash_profile* file to be recognized.

Check that each program was installed successfully.

```shell
$ ruby-install -V
ruby-install: 0.6.1
$ chruby -h
usage: chruby [RUBY|VERSION|system] [RUBYOPT...]
```

`$ ruby-install -V`

`$ chruby -h`

Now you can install the newest Ruby version.

## Install Ruby

After installing the ruby-install utility, install the newest version of Ruby.

The Chruby version manager will use your shell to intercept any calls to Ruby. There's no need to remove the system Ruby. The system Ruby will remain on your system and your preferred version will take precedence.

You can check for the current [recommended version of Ruby](http://www.ruby-lang.org/en/downloads/). Tell the ruby-install utility to check for the newest Ruby version.

```shell
$ ruby-install --latest
```

`$ ruby-install --latest`

Then install the newest Ruby version.

```shell
$ ruby-install --latest ruby
```

`$ ruby-install --latest ruby`

Verify that the newest version of Ruby is installed:

```shell
$ ruby -v
ruby 2.5.1...
```

`$ ruby -v`

Now you can update the development environment. It is likely some gems have been updated since the newest version of Ruby was released. It's best if everything is up to date before you start a new project.

## Check the Gem Manager

[RubyGems](https://rubygems.org/gems/rubygems-update) is the package manager in Ruby. We use it to install software packages that add functionality to Ruby.

Check the installed gem manager version. You may see:

```shell
$ gem -v
2.6.14
```

`$ gem -v`

You can check if a [newer RubyGems](https://rubygems.org/gems/rubygems-update) version is available. Use `gem update --system` to upgrade the Ruby gem manager:

```shell
$ gem update --system
```

`$ gem update --system`

## Default Gems

See what gems are installed as part of the standard Ruby installation.

```shell
$ gem list
```

`$ gem list`

A trouble-free development environment requires the newest versions of the default gems.

To get a list of gems that are outdated:

```shell
$ gem outdated
### list not shown for brevity
```

`$ gem outdated`

To update all stale gems:

```shell
$ gem update
### list not shown for brevity
```

`$ gem update`

It will take a few minutes to update all the default gems.

#### Stay Current

You can track updates to gems at the RubyGems.org site by creating an account and visiting your [dashboard](https://rubygems.org/dashboard). Search for each gem you use and "subscribe" to see a feed of updates in the dashboard (an RSS feed is available from the dashboard). After you've built an application and set up a GitHub repository, you can stay informed with [Gemnasium](https://gemnasium.com/) or [VersionEye](https://www.versioneye.com/). These services survey your GitHub repo and send email notifications when gem versions change. Gemnasium and VersionEye are free for public repositories with a premium plan for private repositories.

#### Faster Gem Installation

By default, when you install gems, documentation files will be installed. Developers seldom use gem documentation files (they'll browse the web instead). Installing gem documentation files takes time, so many developers like to toggle the default so no documentation is installed.

Here's how to speed up gem installation by disabling the documentation step:


```shell
$ echo "gem: --no-document" >> ~/.gemrc
```


`$ echo "gem: --no-document" >> ~/.gemrc`

This adds the line `gem: --no-document` to the hidden **.gemrc** file in your home directory.

#### Install Bundler

The [Bundler](https://rubygems.org/gems/bundler) gem is an essential tool for managing gems when developing and running Rails applications. You must install Bundler.

```shell
$ gem install bundler
```

`$ gem install bundler`

With Bundler in place, you can install sets of gems specified in a project Gemfile.

#### Install Nokogiri

[Nokogiri](http://nokogiri.org/) is a gem that is a dependency for many other gems. Nokogiri is a gem that requires compilation for your specific operating system. As such, if your system environment doesn't match Nokogiri's requirements, compilation of Nokogiri will fail. If your system is configured properly, you'll be able to compile Nokogiri. However, compilation takes time. Every time you install the Nokogiri gem, you'll wait (as long as five minutes).

To save time, install the Nokogiri gem in the RVM global gemset:

```shell
$ gem install nokogiri
```

`$ gem install nokogiri`

During installation, Nokogiri will display two lengthy messages in the console. It will also pause without displaying any progress for as long as five minutes. Don't assume installation has failed unless you see an error message or you've waited more than ten minutes.

If installation fails, make sure your system is configured properly (look for help on [Stack Overflow](http://stackoverflow.com/questions/tagged/nokogiri)).

## Install Rails

Check for the [current version of Rails](http://rubygems.org/gems/rails). Rails 5.1 was current and Rails 5.2 was available in beta release when this was written. For an overview of what's changed in each Rails release, see a [Ruby on Rails Release History](http://railsapps.github.io/rails-release-history.html).

You can install Rails into the current Ruby environment.

Here are the options you have for installing Rails.

If you want to install the current stable release:

```shell
$ gem install rails
```

`$ gem install rails`

If you want the newest beta version or release candidate, you can install with `--pre`.

```shell
$ gem install rails --pre
```

`$ gem install rails --pre`

Or you can get a specific version.

For example, if you want the Rails 3.2.18 release:

```shell
$ gem install rails --version=3.2.18
```

`$ gem install rails --version=3.2.18`

Verify that the correct version of Rails is installed:

```shell
$ rails -v
Rails 5.2.0
```

`Rails 5.2.0`

Rails is now installed. If you want, you can close the Terminal window. Everything is installed, so you won't lose anything by closing the Terminal.

Next, try building a Rails application.

## Create a Workspace Folder

You'll need a convenient folder to store your Rails projects. You can give it any name, such as **code/** or **projects/**. For this tutorial, we'll call it **workspace/**.

Create a projects folder and move into the folder:

```shell
$ mkdir workspace
$ cd workspace
```

`$ mkdir workspace`

`$ cd workspace`

This is where you'll create your Rails applications.

## New Rails Application

Here's how to create a new Rails application.

```shell
$ rails new myapp
```

`$ rails new myapp`

We'll name the new application "myapp." Obviously, you can give it any name you like.

The `rails new` command generates the default Rails starter app. If you wish, you can use the [Rails Composer](http://railsapps.github.io/rails-composer/) tool to generate a starter application with a choice of basic features and popular gems.

#### Quick Test

For a "smoke test" to see if everything runs, display a list of Rake tasks.

```shell
$ cd myapp
$ rails -T
```

`$ cd myapp`

`$ rails -T`

Run the application with the Rails server command:

```shell
$ rails server
```

`$ rails server`

Use your web browser to visit the application at [http://localhost:3000/](http://localhost:3000/).

Use Control-c to stop the server.

This concludes the instructions for installing Ruby and Rails. Read on for additional advice and tips.

## Terminal Application and Text Editor

The built-in Apple Terminal application is adequate but many developers install [iTerm 2](http://www.iterm2.com/#/section/home). It has more options for customization.

For examining and writing code, you'll also need a text editor program such as [Sublime](http://www.sublimetext.com/), [Atom](https://atom.io/), or [Visual Studio Code](https://code.visualstudio.com/). Of course, some programmers will suggest you try Vim or Emacs.

## Rails Example Applications

If you'd like to download and play with a complete, working Rails application, choose any of the [RailsApps Example Applications](http://railsapps.github.io/). For example, you can download the application that is built in the book, [_Learn Ruby on Rails_](http://learn-rails.com/learn-ruby-on-rails.html). Make sure you are in your workspace folder, then download from GitHub and install gems using bundler:

`$ cd ~/workspace`

`$ git clone https://github.com/RailsApps/learn-rails.git`

`$ cd learn-rails`

`$ bundle install --without production`

Examine the code or run the application:

`$ rails server`

The server will start and wait for requests from a web browser. You won't see a result or a prompt while it is waiting for a request from a web browser.

Use your web browser to visit the application at [http://localhost:3000/](http://localhost:3000/).

Use Control-c to stop the server.

## Rails Composer

Use the [Rails Composer](http://www.railscomposer.com) tool to build a full-featured Rails starter app.

You'll get a choice of starter applications with basic features and popular gems.

Here's how to generate a new Rails application using the Rails Composer tool.

```shell
$ cd ~/workspace
$ rails new myapp2 -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb
```

`$ cd ~/workspace`

`$ rails new myapp2 -m https://raw.github.com/RailsApps/rails-composer/master/composer.rb`

The `-m` option loads an application template that is hosted on GitHub.

You can add the `-T` flags to skip Test::Unit if you are using RSpec for testing.

You can add the `-O` flags to skip Active Record if you are using a NoSQL datastore such as MongoDB.

If you get an error "OpenSSL certificate verify failed" when you try to generate a new Rails app, see the article [OpenSSL Errors and Rails](http://railsapps.github.io/openssl-certificate-verify-failed.html).

You can run the Rails server to test the application.

## Databases for Rails

Rails uses the [SQLite](http://www.sqlite.org/) database by default. MacOS come with SQLite pre-installed and there's nothing to configure.

Though SQLite is adequate for development (and even some production applications), a new Rails application can be configured for other databases. The command `rails new myapp --database=` will show you a list of supported databases.

`Supported for preconfiguration are: mysql, oracle, postgresql, sqlite3, frontbase, ibm_db, sqlserver, jdbcmysql, jdbcsqlite3, jdbcpostgresql, jdbc.`

### PostgreSQL

Use the easy-to-install macOS [Postgres.app](http://postgresapp.com/) if you'd like to use PostgreSQL.

To create a new Rails application to use [PostgreSQL](http://www.postgresql.org/):

`$ rails new myapp --database=postgresql`

The `--database=postgresql` parameter will add the pg database adapter gem to the Gemfile and create a suitable config/database.yml file.

Don't use the `--database=` argument with the Rails Composer tool. You'll select a database from a menu instead.

## Deployment

If you wish to run your own servers, you can deploy a Rails application using [Capistrano](http://en.wikipedia.org/wiki/Capistrano) deployment scripts. However, unless system administration is a personal passion, it is much easier to deploy your application with a "platform as a service" provider such as Heroku.

### Hosting

For easy deployment, use a "platform as a service" provider such as:

* [Heroku](http://www.heroku.com/)
* [CloudFoundry](http://www.cloudfoundry.com/)
* [EngineYard](http://www.engineyard.com/)
* [OpenShift](https://openshift.redhat.com/app/)

For deployment on Heroku, see the article:

* [Rails on Heroku](http://railsapps.github.io/rails-heroku-tutorial.html)

## Security

By design, Rails encourages practices that avoid common web application vulnerabilities. The Rails security team actively investigates and patches vulnerabilities. If you use the most current version of Rails, you will be protected from known vulnerabilities. See the [Ruby On Rails Security Guide](http://guides.rubyonrails.org/security.html) for an overview of potential issues and watch the [Ruby on Rails Security Mailing List](https://groups.google.com/forum/?fromgroups#!forum/rubyonrails-security) for announcements and discussion.

### Your Application's Secret Token

Rails uses a session store to provide persistence between page requests. The default session store uses cookies. To prevent decoding of cookie data and hijacking a session, Rails encrypts cookie data using a secret key. When you create a new Rails application using the `rails new` command, a unique secret key is generated. If you've used the Rails Composer tool to generate the application, the application's secret token will be unique, just as with any Rails application generated with the `rails new` command.

The file **config/secrets.yml** contains secret tokens for development and production.

Take care to hide the secret token you use in production. Don't expose it in a public GitHub repo, or people could change their session information, and potentially access your site without permission. It's best to set the secret token in a Unix shell variable.

If you need to create a new secret token:

`$ rails secret`

The command `rake secret` generates a new random secret you can use. The command won't install the key; you have to copy the key from the console output to the appropriate file.

## Troubleshooting

#### Problems with "Gem::RemoteFetcher::FetchError: SSL_connect"

Ruby and RubyGems (starting with Ruby 1.9.3p194 and RubyGems 1.8.23) require verification of server SSL certificates when Ruby makes an Internet connection via https. If you run `rails new` and get an error "Gem::RemoteFetcher::FetchError: SSL_connect returned=1 errno=0 state=SSLv3 read server certificate" see this article suggesting solutions: [OpenSSL errors and Rails](http://railsapps.github.io/openssl-certificate-verify-failed.html).

#### Problems with "Certificate Verify Failed"

Are you getting an error "OpenSSL certificate verify failed" when you try to generate a new Rails app from an application template? See this article suggesting solutions: [OpenSSL errors and Rails](http://railsapps.github.io/openssl-certificate-verify-failed.html).

#### Installing in a Second Account

If you've created a second user account on your Mac, and the first user has already installed Homebrew, the first user may have to change permissions for the **/usr/local/bin** and **/usr/local/Cellar** folders:

`$ sudo chmod g+w /usr/local/bin`

`$ sudo chmod g+w /usr/local/Cellar`

The second user account should be given admin privileges using the System Preferences "Users and Groups" setting.

## Where to Get Help

Your best source for online help with problems is [Stack Overflow](http://stackoverflow.com/questions/tagged/ruby-on-rails-3). Your issue may have been encountered and addressed by others.

To find a real person who can help, attend a Ruby meetup in your city. Google for "ruby meetup" with your city name.

## Credits

Daniel Kehoe wrote the article.
