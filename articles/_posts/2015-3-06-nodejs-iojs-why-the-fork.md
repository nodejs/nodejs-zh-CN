---
layout: post
title: Node.js vs io.js: Why the fork?!?
author: Ralph Whitbeck
reference: http://anandmanisankar.com/posts/nodejs-iojs-why-the-fork/#.VO82hE60PVw.twitter
---

After a hiatus of a couple of months, I’m back with a topic that has invaded many technical discussions in the last months.

**Node.js, the popular server-side JavaScript runtime environment, has been forked!**

OK! But then, Node.js has been forked in the past, e.g: [JXcore](http://jxcore.com) which provides a multithreaded flavour of NodeJS. Why is this specific instance of forking so vastly discussed/debated? It was not just forking of the code, but also - so to speak - forking of some of the top contributors to the NodeJS project. Four of [Node’s top 5 contributors](https://github.com/joyent/node/graphs/contributors) are part of the forked project - [io.js](https://iojs.org).

The possibility of forking has been discussed over the last few months, but the official first release of the forked project [io.js](https://iojs.org) came out early January 2015.

## Why the fork?

Over the last year or so, the number of commits on the Node.js repo has been steadily decreasing.

![Node.js commit trend](http://anandmanisankar.com/assets/images/node_commits.png "Node.js commit trend")

Even worse, the number of releases of node drastically reduced in 2014.

![Node.js release trend](http://anandmanisankar.com/assets/images/node_releases.png "Node.js release trend")

But, one of the main reasons for the forking was the discontent over the way in which Joyent was handling the project. This [blog post](https://www.joyent.com/blog/the-power-of-a-pronoun) from Bryan Cantrill should throw some perspective.

> io.js - the forked version of Node.js, is the result of dissatisfaction over Joyent’s stewardship of the Node.js project.

Talk of a possible forking started mid 2014, after some developers became discontented with the role of Joyent as the steward of the Node.js project. Some of the core contributors tried working with Joyent to move the project into a structure where the contributors and community could step in to solve the problems facing Node (some indicated by the graphs above). Some independent  efforts were started by contributors to improve Node and its ecosystem, in the name of ‘[Node Forward](http://nodeforward.org/)’.

But [Fedor Indutny](https://github.com/indutny), one of the core team members, got tired of getting nowhere with the discussion and started the fork that is currently called io.js. Other contributors close to Fedor volunteered and jumped in.

Joyent responded by forming the [Node Advisory Board](https://www.joyent.com/blog/node-js-advisory-board) to set up open governance, but that  seems to have been too little too late.

> We don’t want to have just one person who’s appointed by a company making decisions. We want contributors to have more control, to seek consensus.
> 
> <cite>— Mikeal Rogers, io.js project team member</cite>

The forking only highlights the tension between corporate sponsor of an open source project and the community of developers contributing to it.

But for Joyent CTO Bryan Cantrill, Node is alive and well, despite the slower pace of development.

> You’ve got to look at the quality of contributions, not the quantity.
> 
> <cite>— Bryan Cantrill, CTO, Joyent</cite>

## OK. Let’s talk about the forking facts!

### What you need to know about io.js:

*   Forked out of Joyent’s Node.js v0.12
*   Fully compatible with the npm ecosystem
*   Will be taking new V8 releases as fast as possible

    *   io.js is on V8 v4.1.0.14, while Node is still on V8 v3.28.73
    *   Newer V8 brings in many performance improvements and fixes
    *   Also, brings in additional support for [new ES6 language features](https://iojs.org/en/es6.html)
*   New (experimental) core modules
    *   [V8](https://iojs.org/api/v8.html): interfacing directly with V8 engine
    *   [smalloc](https://iojs.org/api/smalloc.html): managing external raw memory allocation/deallocation in JavaScript
*   Versioning based on semver, starting with v1.0.0
*   Weekly production releases planned
*   Bug fixes cherry-picked from Node into io.js as necessary
*   [Open Governance Model](https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md): More power to contributors

## My take on the fork

io.js has clearly proved that a project can grow much faster with open governance. It has made 10 releases since its first release on 13 Jan 2015!

![io.js commit trend](http://anandmanisankar.com/assets/images/iojs_commits.png "io.js commit trend")

But the situation is still a bit of a yin yang! The duality arises from the fact that for every statement that you make supporting the fork, there could be one made opposing it in the same context.

### Let’s talk about the positives:

*   Open governance, distributed control
*   Faster releases
*   Newer V8
*   ES6 goodness

### The other perspective:

*   Node is fairly stable and production ready. Why switch?
*   The technical delta (newer V8, ES6 support, etc) is not enticing enough for many
*   Not many corporates are complaining about slow releases from Node

If I quote apache web server, hadoop or linux as good examples of foundation driven open source initiatives, someone would respond quoting Ruby on Rails or Docker as successful single corporate driven OSS initiatives. Hence, the yin yang!

Whether io.js gains traction or not would depend on the consumer adoption. Matt Ranney, Chief Systems Architect at Uber, has already tweeted about putting io.js into production.

> I’m one of the first people to put io.js into production at scale.
> — Matt Ranney ([@mranney](https://github.com/mranney)) [December 3, 2014](https://twitter.com/mranney/status/540013975568535553)

<script async="" src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

But, I see this fork only as an exploration by some of the key contributors in the Node core community with the following intent:

*   Accelerate release of latest advancements in JavaScript as fast as the community feels necessary
*   Support an open governance model as against a single corporate stewardship

From a consumer point of view, I believe io.js is currently only solving some first-world problems in Node.js. It does not yet warrant a switch from Node. In fact, it only confuses and forces the consumer into additional decision making.

But from a community/contributors point of view, **I think this is a push in the right direction - if you look at io.js as an experimental showcase to Joyent on how a good open source project should be governed**. This is one of the reasons I like the ‘OPEN Open Source’ model which [Rod Vagg](https://github.com/rvagg) came up with for the [LevelUp project](https://github.com/rvagg/node-levelup) (a node wrapper for LevelDB).

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is more like an open wiki than a standard guarded open source project.

## The Future: Node and io.js will unite

Some things are fairly clear:

*   Nobody wants multiple forks of Node to complicate the decision making process
*   It was never the goal of io.js or node forward to create a second Node.js
*   The effort required to maintain the fork is tremendous

io.js - ‘the friendly fork’, is **not** intended to compete with Node. Someday, the io.js faction will reunite with Node, once there is an agreement on the collaborative decision making process. Infact, the [reconciliation process has already begun](https://medium.com/@iojs/io-js-and-a-node-js-foundation-4e14699fb7be). Joyent CEO Scott Hammond had invited the io.js technical committee to a private meeting to discuss about Node Foundation, and bringing io.js back to node.js project.

The Node Foundation is expected to have two committees: The Foundation Board and the Technical Committee. The technical committee will operate independent of the foundation board, giving it the required freedom to drive the technical growth of the project. Whether the technical committee will have an open governance model like io.js is still not clear. ([William Bert](https://twitter.com/williamjohnbert) has created a [twitter campaign](http://nodegovernance.io/) to spam (read alert) Scott Hammond about the desire of the community to uses the io.js governance model for Node Foundation). The best thing that can happen is a successful reunion leveraging the best of both worlds.

The ball is now in Joyent’s court!

* * *

#### **Update: 27<sup>th</sup> Feb 2015**

[Mikael](https://github.com/mikeal) has created a work-in-progress [‘Reconciliation Proposal’](https://github.com/iojs/io.js/issues/978) that covers topics like technical governance, long-term support, versioning and WG structuring proposals for a future ‘Node’ which re-unites ‘Node.js’ and ‘io.js’.

* * *
