# Setting up a Development Environment on Mac OSX

How-to for dummies (aka designers like me).


## Xcode

1. Get [Xcode](https://developer.apple.com/xcode/) from the Mac App Store.
Why would you need Apple’s SDK when you’re developing for the Web only? Because you’re on OSX and Apple want you to eat their dog food — all of it. Before OSX v.9 “Mavericks”, you needed to install Xcode and (separately!) also install the Command Line tools. It seems with Mavericks you can have the Command Line tools, _without_ Xcode. Any how, once the Command Line tools are being installed, you already have lots in the tool belt. For one: git.


## Git

1. Check your version of Git:
```Batchfile
	$ git version
```
[![NPM version](https://badge.fury.io/js/git.png)](http://badge.fury.io/js/git) — git version 1.8.3.4 (Apple Git-47) ?

2. Update if necessary:
http://stackoverflow.com/questions/8957862/how-to-upgrade-git-to-latest-version-on-mac-osx-lion

3. Get Atlassian’s **[SourceTree](http://www.sourcetreeapp.com/)**. (Note: The version in the Mac App Store is deprecated.) Okay, that’s an app, as in: has a GUI. It’s a Git client with a decent graphical interface: you’ll prefer using that over memorizing all those git commands, especially when you start committing separate chunks of edits.


## ssh
To do!


## Node.js & npm

1. [Download](http://nodejs.org/download/) the Node.js `.pkg` Mac OSX Installer package. Open, and follow the instructions: the installer will build your Node distro from the binaries, at `/usr/local/bin/node`. It also installs [npm](https://npmjs.org/), the de facto standard package manager for the Node ecosystem at `/usr/local/bin/npm`.

2. After installation the utility will say to make sure that “ `/usr/local/bin` is in your `$PATH`”. Whatever that means. Another [tutorial](http://bevry.me/learn/node-install) says we should run `$ sudo chown -R $USER /usr/local` in the terminal. So there we go…

3. Check if you’re up-to-date:
```Batchfile
$ node --version
```
[![NPM version](https://badge.fury.io/js/node.png)](http://badge.fury.io/js/node) — v0.10.21 ?
```Batchfile
$ npm version
```
[![NPM version](https://badge.fury.io/js/npm.png)](http://badge.fury.io/js/npm)


## Homebrew

You’ll need [Homebrew](http://brew.sh) to install all sorts of cool stuff.

1. As you installed Xcode, you already have [Ruby](https://www.ruby-lang.org/en/). We’ll be installing Homebrew using Ruby:
```Batchfile
	$ ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"
```

2. Check if everything’s alright:
```Batchfile
	$ brew doctor
```
The prompt should respond: “Your system is ready to brew.”


## Sass & Compass
To do!


## Docpad

1. As Docpad runs on Node.js, you’ll need to have Node installed (see above). We do want to check if we’re running the latest and greatest:
```Batchfile
$ node -version
```
[![NPM version](https://badge.fury.io/js/docpad.png)](http://badge.fury.io/js/docpad)


2. We do the same for npm (the Node package manager):
```Batchfile
$ npm install -g npm
``` 

3. With those two dependencies in place, we can finally install Docpad:
```Batchfile
$ npm install -g docpad@6.54
``` 
`-g` means we will be installing Docpad globally, and make it available for all users of the Mac. The command runs a bunch of downloads via npm.

4. Check the version:
```Batchfile
$ docpad -V
```
This should do it. If you have multiple Docpad plugins installed in a Docpad project, npm should get them as soon as you `$ docpad run`. However, I noticed a problem with the clean urls plugin: 404 not found. So explicitly install the plugin manually:
```Batchfile
$ docpad install cleanurls
```
Also, some dependencies that not came as Docpad plugins, but were installed (and are in in `docpad.coffee`), need to be installed separately. In my project I used [Moment.js](http://momentjs.com/) and [Cheerio](https://github.com/MatthewMueller/cheerio):
```Batchfile
$ npm install --save moment
```
```Batchfile
$ npm install cheerio
```

## Heroku

1. Download the [OSX installer](https://toolbelt.heroku.com/), open, and follow the instructions.

2. Next, in the terminal, as the [quick start guide](https://devcenter.heroku.com/articles/quickstart) explains, login with your Heroku account:
```Batchfile
$ heroku login
```
When you already got an app at Heroku, which you setup from another machine, you’ll need to add an extra ssh key for the new machine:
```Batchfile
$ heroku keys:add
```

## MongoDB
To do!

## Meteor & Meteorite
To do!
