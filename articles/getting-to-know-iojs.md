# Getting to know io.js

Last week, Twitter was abuzz about an initial release of [io.js](http://iojs.org). io.js is an npm compatible platform originally based on Node.js and is a fork of Joyent's [Node.js](http://nodejs.org/).

## Why fork Node.js?

The io.js team is made up mostly of the [key contributors](https://github.com/iojs/io.js/blob/v1.x/README.md#current-project-team-members) to Node.js. In August, the team created [Node Forward](http://nodeforward.org/) which was an attempt by the community to help improve Node.js. 

> A broad community effort to improve Node, JavaScript, and their ecosystem through open collaboration.

Here we get a hint at why the community felt compelled to fork nodejs at this point:

> Some problems require broader ownership and contributorship than have traditionally been applied, while others are so dispersed between tiny projects that they require new collaborative space to grow. Node Forward is a place where the collaboration necessary to solve these issues can take place.

Ultimately, the work of the community could not be released under the trademark restrictions of Node, so a fork was made and io.js was born.

[Isaac Schlueter](https://twitter.com/izs) a core contributor, [provides a lot of the backstory behind the decision to fork on his personal blog](http://blog.izs.me/post/104685388058/io-js). One key takeaway, it is the intention of io.js that the two projects will hopefully merge together sometime in the future. 

## What's new in io.js?

First, io.js introduces proper [semantic versioning (semver)](http://semver.org/) by tagging the release 1.0.0 because it's such a divergence from Node.js. jQuery blogged about the importance of using semver in a [recent blog post](http://blog.jquery.com/2014/10/29/jquery-3-0-the-next-generations/):

> One of those best practices is semantic versioning, or semver for short. In a practical sense, semver gives developers (and build tools) an idea of the risk involved in moving to a new version of software. Version numbers are in the form of MAJOR.MINOR.PATCH with each of the three components being an integer. In semver, if the MAJOR number changes it indicates there are breaking changes in the API and thus developers need to beware.

## Latest V8 engine

io.js updated the V8 JavaScript engine up to 3.31.74.1 which is most notable for running ES6 features of the JavaScript spec without using the `--harmony` flag to enable them.

### Available ES6 features

The features listed below are available with io.js without specifying any flag:

*   [Block scoping (`let`, `const`)](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-let-and-const-declarations)
*   Collections ([`Map`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-map-objects), [`WeakMap`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-constructor-properties-of-the-global-object-weakmap), [`Set`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-set-objects), [`WeakSet`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-constructor-properties-of-the-global-object-weakset))
*   [Generators](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-generator-function-definitions)
*   [Binary and Octal literals](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-literals-numeric-literals)
*   [Promises](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-promise-jobs)
*   [New String methods](http://www.sitepoint.com/preparing-ecmascript-6-new-string-methods/)
*   [Symbols](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-ecmascript-language-types-symbol-type)
*   [Template strings](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-static-semantics-templatestrings)

### New modules

io.js comes with new experimental core modules:

*   [smalloc](https://iojs.org/api/smalloc.html): allows you to do external rawmemory allocation/deallocation/copying in JavaScript
*   [v8](https://iojs.org/api/v8.html): exposes events and interfaces specificto the version of V8 build with node

You can review the full list of changes in the [io.js changelog](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md).

## Running io.js

Running a JavaScript node application with io.js is the same as running it with node; the only exception is that the name has changed. 

Node.js

    $ node app.js

io.js

    $ iojs app.js

### Node version manager

[Node version manager (nvm)](https://github.com/creationix/nvm), which is a bash script that allows you to manage multiple versions of Node.js and now supports installing various versions of io.js. If you have nvm installed you can run the following command in your terminal to list the versions of io.js available:

    $ nvm ls-remote v1
        iojs-v1.0.0
        iojs-v1.0.1
        iojs-v1.0.2
        iojs-v1.0.3

Then in your project folder you can install io.js by specifying the latest version listed.

    $ nvm install iojs-v1.0.3

**Note:** At the time of this writing, I'd recommend only installing io.js via nvm. Many early adopters who've installed io.js through the installer on io.js homepage are saying that io.js inserts itself over node by replacing a symlink that links to node to now link to io.js. nvm allows you set a specific version for specific project folders.

## Trying it out

Want to test io.js out in an Atlassian Connect add-on?  You can quickly get a HipChat add-on to run on io.js and utilize an ES6 feature like Generators by following these simple steps:

1.  Go to the [HipChat Add-ons Quick Start guide](https://www.hipchat.com/docs/apiv2/quick_start?utm_source=dac&amp;utm_medium=blog&amp;utm_campaign=getting-to-know-iojs)and follow the instructions to get a add-on up and running with the[atlassianlabs/ac-koa-hipchat](https://bitbucket.org/atlassianlabs/ac-koa-hipchat?utm_source=dac&amp;utm_medium=blog&amp;utm_campaign=getting-to-know-iojs)framework

2.  `vagrant ssh` into the vagrant server you set up in step 1. At the commandprompt you'll need to install nvm by running this command:


    curl https://raw.githubusercontent.com/creationix/nvm/v0.23.0/install.sh | bash


This will install nvm and update your shell. You'll next need to type `exit`at the command prompt to close your ssh session and restart the shell.

3.  Open `package.json` and edit the web script line so it uses io.js insteadof Node.js:

    "scripts": {
     "web": "iojs web.js",
     "web-dev": "nodemon --harmony -e js,json,css,hbs web.js"
    },

4.  Again run `vagrant ssh` to restart the servers shell and run the followingcommand to start the application:

    $ cd project && npm start web

This will start the Koa HipChat add-on server and you can register your add-onwith a HipChat room using the following URL:

     `https://xxxxxxxx.ngrok.com/addon/capabilities`

      where `xxxxxxxx.ngrok.com` is the url specified in the shell after the  server starts up.

If you are able to type `/hello` in the chat field and have the HipChat add-on reply back with "Hi" then congratulations! You are now running an io.js application that utilizes ES6 features such as Generators.

## Should you use io.js?

The all important question you might be asking yourself, can I use io.js in my node add-ons today? Right now io.js is a little more than a week old and the latest version at the time of this writing, v1.0.3, is still listed as "Unstable" on the site. Services like nvm are still working the bugs out. Hosting companies haven't announced support for it. Right now if you're an early adopter and want to see a "Stable" io.js test your add-ons with io.js and file any [issues you find](https://github.com/iojs/io.js/issues). Ultimately, it's too early to switch to io.js but keep an eye on it and maybe it'll become the most popular JavaScript server platform to use.