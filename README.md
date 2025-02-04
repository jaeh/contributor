#Contributor [![Build Status](https://travis-ci.org/jakeleboeuf/contributor.svg?branch=master)](https://travis-ci.org/jakeleboeuf/contributor) [![NPM version](https://badge.fury.io/js/contributor.svg)](http://badge.fury.io/js/contributor) [![Stories in Ready](https://badge.waffle.io/jakeleboeuf/contributor.png?label=ready&title=Ready)](https://waffle.io/jakeleboeuf/contributor)

A simple [node](http://nodejs.org) module to grab your project contributors from your github repo and add them to your package.json. You'll also be prompted to generate a Markdown version of your contributors list and save it to `contributors.md`.



## Install from [npm](https://www.npmjs.org/package/contributor)

    $ npm install contributor -g

Or (preferably), add it as one of your projects `package.json` dependencies. Make sure you have a [valid repository property](https://www.npmjs.org/doc/json.html#repository) pointing to your repo... Something like this will do the trick:


```json
{
  ...
  "dependencies": {
    "contributor": "0.1.x"
  },
  "repository" : {
    "type" : "git",
    "url" : "http://github.com/user/repo.git"
  }
  ...
}
```

## Usage

To get a record of your project's contribution info from your github repo, `cd` into the directory containing your `package.json` and run:

	$ contributor

Bingo! Your `package.json` will be appended with something like this:

```json
{
  ...
  "contributors": [
    {
      "name": "Jake LeBoeuf",
      "email": "dev@jakeleboeuf.com",
      "url": "https://github.com/jakeleboeuf",
      "contributions": 20,
      "hireable": true
    }
  ]
}
```

As of [v0.1.12](https://github.com/jakeleboeuf/contributor/releases/tag/v0.1.12), you'll be prompted to optionally `Save to contributors.md? (yes/no)`.

![Prompt](https://raw.github.com/jakeleboeuf/contributor/master/img/mdPrompt.png)


### contributors.md Preview

It should look all spiffy, but unfortunaly I realized after pushing this that github does not support custom text colors and neato things. lame. I'll fix it someday.

<br>
***Example contributors.md***

###### Contributors
[Jake LeBoeuf](https://github.com/jakeleboeuf)
<font color="#dedede"><font color="#999">17 Commits</font> / <font color="#6cc644">133,879++</font> / <font color="#bd3c00"> 227--</font>
<font color="#dedede">95.54%&nbsp;<font color="#dedede">|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||</font><font color="#f4f4f4">||||||||||</font><br><br>
[Drew Smith](https://github.com/jakeleboeuf)
<font color="#999">1 Commits</font> / <font color="#6cc644">79++</font> / <font color="#bd3c00"> 2--</font>
<font color="#dedede">04.46%&nbsp;<font color="#dedede">||||||||||</font><font color="#f4f4f4">|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||</font></font></font><br><br>
###### [Generated](https://github.com/jakeleboeuf/contributor) on Mon Aug 04 2014 14:10:14 GMT-0400 (EDT)

***Screenshot of intended Markdown***

![Preview](https://raw.github.com/jakeleboeuf/contributor/master/img/preview.png)



### Behind the scenes

[Contributor](https://www.npmjs.org/package/contributor) hunts for repository.url in your your `package.json`. If it finds a valid repo url, it requests collaborator info from the github api and adds it to your `package.json`. Super simple. If your repo is private, you'll be prompted for your Github username/password.

`$ contributor` will always make a backup of your original json to `.package.json`, so all your secret codes are safe.


#### Pro tip: Add a git push alias and kill a couple birds.

	$ git config alias.pushc \!git push $1 $2 && contributor

This will simply add the pushc alias to your .git/config file like so:

	[alias]
    	pushc = !git push $1 $2 && contributor

Then you can run `git pushc origin master`, and voila! Give it a try on your next project and let me know what you think!

--
###Examle output


package.json **Before** `$ contributor`:


```json
{
  "author": "Jake LeBoeuf",
  "name": "contributor",
  "description": "Example package.json.",
  "version": "0.1.1",
  "homepage": "https://github.com/jakeleboeuf/contributor",
  "repository": {
    "type": "git",
    "url": "https://github.com/jakeleboeuf/contributor.git"
  },
  "bugs": {
    "url": "https://github.com/jakeleboeuf/contributor/issues"
  },
  "engines": {
    "node": "0.10.x",
    "npm": "1.4.x"
  },
  "dependencies": {
    "request": "2.34.x",
    "ansi-color": "0.2.x",
    "github": "0.1.x",
    "prompt": "0.2.x"
  }
}
```

package.json **After** `$ contributor`:

```json
{
  "author": "Jake LeBoeuf",
  "name": "contributor",
  "description": "Example package.json.",
  "version": "0.1.1",
  "homepage": "https://github.com/jakeleboeuf/contributor",
  "repository": {
    "type": "git",
    "url": "https://github.com/jakeleboeuf/contributor.git"
  },
  "bugs": {
    "url": "https://github.com/jakeleboeuf/contributor/issues"
  },
  "engines": {
    "node": "0.10.x",
    "npm": "1.4.x"
  },
  "dependencies": {
    "request": "2.34.x",
    "ansi-color": "0.2.x",
    "github": "0.1.x",
    "prompt": "0.2.x"
  },
  "contributors": [
    {
      "name": "Jake LeBoeuf",
      "email": "dev@jakeleboeuf.com",
      "url": "https://github.com/jakeleboeuf",
      "contributions": 20,
      "hireable": true
    }
  ]
}
```

[![Support via Gittip](https://rawgithub.com/twolfson/gittip-badge/0.2.0/dist/gittip.png)](https://www.gittip.com/jakeleboeuf/)

[![NPM](https://nodei.co/npm/contributor.png)](https://nodei.co/npm/contributor/)
