# Setting up a Development Environment on Mac OSX

How-to for dummies (aka designers like me).


## Xcode

1. Get [Xcode](https://developer.apple.com/xcode/) from the Mac App Store.
Why would you need Apple’s SDK when you’re developing for the Web only? Because you’re on OSX and Apple want you to eat their dog food — all of it. Before OSX v.9 “Mavericks”, you needed to install Xcode and (separately!) also install the Command Line tools. It seems with Mavericks you can have the Command Line tools, _without_ Xcode. Any how, once the Command Line tools are being installed, you already have lots in the tool belt. For one: git.


## Git

1. Check if Git is installed, and which version you have:
```Batchfile
	$ git version
```
It’s unlikely you’ll need to upgrade. If you do, [here](http://stackoverflow.com/questions/8957862/how-to-upgrade-git-to-latest-version-on-mac-osx-lion) is how.

2. Get Atlassian’s **[SourceTree](http://www.sourcetreeapp.com/)**. (Note: The version in the Mac App Store is deprecated.) Okay, that’s an app, as in: has a GUI. It’s a Git client with a decent graphical interface: you’ll prefer using that over memorizing all those git commands, especially when you start committing separate chunks of edits.


## ssh

ssh is making life a lot easier: let your computer login with your credentials.

1. Let’s see if you have some public keys already:
```batch
$ cd .ssh
```
```batch
$ ls -la
```
`ls` lists the contents of the directory, while `-la` will show everything in there.
```batch
$ cat id_rsa.pub
```
`cat` shows the contents of a file; `id_rsa_pub` is a common filename for a default key, created on your machine (using ras algorithm)

2. copy/paste in Github; import in in Bitbucket

3. Not unlikely you still connect to some repo’s over the https protocol, requiring you to give you password, on each single occasion you need to connect. Let’s free ourselves from that burden and change the connection to ssh:

```batch
$ git remote set-url origin [the repo’s url]
```
e.g. 
$ git remote set-url origin git@bitbucket.org:username/reponame.git


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

4. On a side note: suppose you’re a terminal n00b like me, then you probably look for help and type in `$ node help`. Alas, but the Node prompt gives you shit, like `module.js:340 throw err; ^ Error: Cannot find module` etc. Don’t worry: that just means there is no “help” command for Node. The one you’re looking for is `$ node --help`, showing you all available commands, that do exist. We can only conclude, once again, that the UX of the command line interface isn’t all too great. If someone is looking for help, you shouldn’t throw and error. Never. Ever.


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

$ sudo gem install compass
$ compass --version

$ gem install compass-animate 


## Docpad

Static site generator. But you do have the option to deploy dynamic apps as well. Docpad runs on Node.js. Best of all: it’s all file based; no database needed! Docpad’s lead developer has an [installation guide](http://docpad.org/docs/install).

1. As Docpad runs on Node.js, you’ll need to have Node installed (see above). We do want to check if we’re running the latest and greatest:
```Batchfile
$ node -version
```
[![NPM version](https://badge.fury.io/js/docpad.png)](http://badge.fury.io/js/docpad)


2. We do the same for npm (the Node package manager):
```Batchfile
$ npm install -g npm
``` 
→ starts re-installing npm?! It’s sort of an update procedure.

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


## Grunt


http://gruntjs.com/installing-grunt

1. Make Grunt globally available on our machine by installing its command line interface (CLI). As the [official “Getting Started” tutorial](http://gruntjs.com/getting-started) explains, this will install the CLI, not the Grunt task runner (since we want that to be specific to a particular project folder):
```Batchfile
$ npm install -g grunt-cli
```

2. We now have Grunt globally available, but still need to setup a project form scratch (and along with that setup, have the Grunt task runner installed). We could do that manually (by creating a `package.json` and Grunfile, but will use (and first install) the Grunt project initialization command. (More info is [here](http://gruntjs.com/project-scaffolding).) Install as follows, and test if all went well:
```
$ npm install -g grunt-init
```
```
$ grunt-init --help
```
Once the `grunt-init` command is installed, we will still have to add a Grunt project template, so that the command can use it. There are several dozens of templates available, but we will start with the [basic Gruntfile creation template](https://github.com/gruntjs/grunt-init-gruntfile), which we install as follows (using git clone):
```
$ git clone https://github.com/gruntjs/grunt-init-gruntfile.git ~/.grunt-init/gruntfile
```

3. Now navigate (`cd`) to the folder where you want to create your new Grunt project, and from there, run `grunt-init gruntfile`:
```
$ cd path/to/project
project $ grunt-init gruntfile
```
You will be prompted to answer a few questions. after that, a `Gruntfile.js` will have been created in your project folder’s root.

4. As we used the basic Gruntfile template, `grunt-init` didn’t create a `package.json`, too. For that, we will use [npm’s own `init`command](https://npmjs.org/doc/init.html):
```
project $ npm init
```
Again, you’ll go through a dialog of Q&A: answer the questions asked and the script will create the `package.json` file in your project folder’s root (alongside the `Gruntfile.js` we already have).

5. Still, Grunt itself is not installed. But with both the `Gruntfile.js` and node `package.json` files in place, we can finally install Grunt _per se_ into our project:
```
project $ npm install grunt --save-dev
```
After running, there will now be a `node_modules` folder in your project’s parent folder, containing grunt. At last!

6. Install a grunt plugin. We will install the [compass grunt plugin](https://github.com/gruntjs/grunt-contrib-compass). As follows:
```
project $ npm install grunt-contrib-compass --save-dev
```

project $ npm install grunt-contrib-concat --save-dev
project $ npm install grunt-contrib-uglify --save-dev
project $ npm install grunt-contrib-nodeunit --save-dev
project $ npm install grunt-contrib-jshint --save-dev
project $ npm install grunt-contrib-watch --save-dev

project $ npm uninstall grunt-contrib-concat
project $ npm uninstall grunt-contrib-uglify
project $ npm uninstall grunt-contrib-nodeunit
project $ npm uninstall grunt-contrib-jshint
project $ npm uninstall grunt-contrib-watch

## Meteor

[Meteor](http://docs.meteor.com)

1. Check if you have `curl` (should be pre-installed by Xcode). 

$ curl --version

2. With the curl command, we will be running an install script (= shell script van Meteor downloaden):

$ curl https://install.meteor.com | /bin/sh

3. Check if all went well:

$ meteor --version


Install [**Meteorite**](https://github.com/oortcloud/meteorite/). For time being is de facto standard package manager for Meteor (next to npm); voor thrid party meteor packages

4. $ npm install -g meteorite

5.  $ mrt --version

6. Start Meteor: $ meteor

7. Installeer packages voor een project: $ mrt install


	## MongoDB

Meteor comes with MongoDB, but you’ll be wanting to run Mongo apart from Meteor, separate instances. Thus install separately.

- http://docs.mongodb.org/manual/tutorial/install-mongodb-on-os-x/

1. $ brew update

2. $ brew install mongodb

fans spinning like mad!!!

```
==> Caveats
To have launchd start mongodb at login:
    ln -sfv /usr/local/opt/mongodb/*.plist ~/Library/LaunchAgents
Then to load mongodb now:
    launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mongodb.plist
Or, if you don't want/need launchctl, you can just run:
    mongod
==> Summary
🍺  /usr/local/Cellar/mongodb/2.4.7: 18 files, 271M, built in 3.4 minutes
```

3. Install GUI voor Mongo: [Genghis](http://genghisapp.com):

	$ sudo gem install genghisapp

4. Opstarten: $ genghisapp

“all kinds of weirdness” ipv sudo: via RVM

MongoDB driver C extension not found.
Install this extension for better performance: gem install bson_ext -v 1.9.0

$ sudo gem install bson_ext -v 1.9.0


# Python

OSX comes with Python pre-installed. But you need to upgrade, because the pre-installed version is 2.7.x, as you can see:

```batch 
$ python
Python 2.7.5 (default, Sep 12 2013, 21:33:34) 
```

The official python.org website, has a [section on installing/upgrading on OSX](http://docs.python.org/3/using/mac.html#getting-and-installing-macpython). It isn’t very helpful, though. It basically says that you should upgrade to Python 3, but keep the OSX pre-installed v.2.7.x, because OSX itself needs that one — sigh. You’ll end up having two versions; quite disturbing. No word or link on an actual install guide. Confusingly, there’s yet [another page](http://www.python.org/getit/mac/) on the same website, saying more or less the same. Well, the _download page_ you’re actually look for, is [here](http://www.python.org/download/).

1. Download the “Python 3.3.2 Mac OS X 64-bit/32-bit x86-64/i386 Installer” packaged in `python-3.3.2-macosx10.6.dmg`; open that file by double-clicking.

2. Run the install scripts: Right click the “Python” installer package icon. Then select “Open using ... Installer”. (Some pedantic OSX warning pops up: ignore that, and proceed. If you’d wanna know why: read the ReadMe.txt in the package’s unpacked folder.) Follow the instructions in the dialogues. Click, click, click, and you got Python 3 installed!

3. Check your Applications folder: there’s a Python 3.x folder now. In there, there’s a Python Launcher.