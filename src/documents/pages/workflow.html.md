---
title: Workflow
layout: page
tags: [page']
pageOrder: 2
---
One of the benefits of code standards is that it makes it easier for team members to jump into another developer's project and immediately begin working. We enforce a common development platform and workflow across the organization for a similar reason. If you have ever tried to help another developer only to be completely lost in their development environment, you can understand the benefit to be gained.

## IDE ##

### Sublime Text ###

Sublime Text has quickly grown to be an industry-favorite IDE. It offers many helpful options and plugins to help you code more efficiently and with greater precision. It is more powerful than a simple text editor such as Notepad++, but without the bloat of an IDE commonly used to develop back-end code such as Eclipse or Visual Studio.

<h4>Plugins</h4>

We recommend several plugins for use in Sublime Text. Some of these carry a strong recommendation as they help you meet code standards as you code&mdash;before running a lint or validation tool. Others are optional, but are plugins that we have found to help coding efficiency.

<h5>Strongly Recommended</h5>


* [Package Control](http://wbond.net/sublime_packages/package_control) - Sublime Text's Package Control manager. This is used to install all other plugins.
* [BracketHighlighter](http://github.com/facelessuser/BracketHighlighter) - Highlights opening and closing brackets and HTML tags for the block your cursor is currently in.
* [Emmet](http://docs.emmet.io) - formerly known as Zen Coding, this plugin can speed up your HTML and CSS writing by automatically creating closing tags, and following simple macros to programatically create code.
* [jQuery](http://github.com/SublimeText/jQuery) - adds jQuery syntax recognition to Sublime Text
* [LineEndings](http://github.com/SublimeText/LineEndings) - adds line ending and space/tab information and commands to the Sublime status bar.
* [Sass](http://github.com/nathos/sass-textmate-bundle) - adds syntax highlighting and code completion for SASS/SCSS
* [SideBarEnhancements](http://github.com/titoBouzout/SideBarEnhancements) - adds useful commands to the right-click context menu in the Sublime Sidebar. Includes "Open With," "Delete," "Move," "Rename," and enhanced "Find" options.
* [SublimeLinter](http://github.com/SublimeLinter/SublimeLinter) - Lint support for many languages - including HTML tidy, JSHint, and CSSLint.


<h4>User Settings</h4>

User settings in Sublime Text are JavaScript objects. You can alter these to change the behavior of your environment. Again, some of these will help you conform to the standards automatically, and so are required. Others are optional, but recommended to help your coding efficiency.

## Browser ##

Front-end development requires a reliable web browser to run and test your code. We recommend initially writing your code to be work in a modern standards-compliant browser and then back-testing into the legacy browsers you need to support. Both Firefox and Chrome are modern browsers that offer robust development tools for only inspecting and debugging your code. In addition, Chrome's Dev Tools include tools for monitoring performance and memory usage, and so carries the highest recommendation, but you are free to choose either Firefox or Chrome.

### Chrome ###

Chrome's Dev Tools are constantly improved and updated. The links below include both introductory information as well as some advanced tutorials. NETTUTS+ has been running a series of in-depth tutorials of the Chrome Dev Tools since late 2012. We have listed some of those tutorials below.


* [Google Chrome Developer Tools](https://developers.google.com/chrome-developer-tools/) - An introduction to the Developer Tools by Google
* [Chrome Dev Tools: Markup and Style](http://net.tutsplus.com/tutorials/tools-and-tips/chrome-dev-tools-markup-and-style/) - NETTUTS+, October 2, 2012
* [Chrome Dev Tools: Networking and the Console](http://net.tutsplus.com/tutorials/chrome-dev-tools-networking-and-the-console/) - NETTUTS+, November 27, 2012
* [Chrome Dev Tools: JavaScript and Performance](http://net.tutsplus.com/tutorials/tools-and-tips/chrome-dev-tools-javascript-and-performance/) - NETTUTS+, February 4, 2013


### Firefox ###

Firefox is also a modern browser, supporting most advanced features of HTML5 and CSS3. For a long time, developer tools in Firefox were limited to those in the [Firebug addon](http://getfirebug.com/). Firefox now implements its own native developer tools, but Firebug is still around for those things that aren't yet in the native tools.

## Preprocessors ##

When we talk about preprocessors, we are usually referring to meta-languages that go through some sort of compilation process to output standard CSS or JavaScript. In our case, we're talking about using SASS/SCSS to generate CSS.

### SASS/SCSS and Compass ###

SASS/SCSS is a meta-language that compiles down to CSS. It offers a number of features that make writing styles faster, easier, and less error-prone. These include variables and functions, mixins, nesting, and inheritance.

More information can be found on the [SASS website](http://sass-lang.com/) and on the site for [Compass](http://compass-style.org/), a mixin and utility library for SASS.

## JS Frameworks ##

JavaScript frameworks are a necessary part of modern web development. Browser differences still plague us, and the DOM API isn't easy to navigate. Libraries extract much of the compatability and complexity issues, and give us a stable base on which to build our projects. In addition, many libraries implement commonly-used functionality many developers find useful.

### jQuery ###

jQuery is, at its heart, a DOM library that provides a cross-browser layer of abstraction between sensible code the DOM API. It also offers visual effects and AJAX modules. In addition, many popular JavaScript plugins are built around jQuery and extend the jQuery object. jQuery's own sister projects jQuery UI and jQuery Mobile are only two examples of these.

### Underscore ###

Underscore is a utility library that adds programming support to JavaScript, particularly around the manipulation of objects and arrays. It is a hard dependency of Backbone.js.

### Backbone ###

Backbone.js is a lightweight library that provides MVC/MVVM/MV* separation for front-end web applications. It is equally suited to single page and multi-page applications.

## Linting and Validation ##

Linting is the process of validating the semantics of a language. It can't tell you whether or not your program will work, but it can tell you if you used the language correctly. The strictness of linting increased so that it not only reports language errors, but also warnings for style rules. We will use some of these strict options to ensure universal implementation of our coding standards.

### JSHint ###

JSHint is based off of Douglas Crockford's [JSLint program](http://www.jslint.com/). JSLint is very opinionated. JSHint is less so, and offers options to strengthen or weaken many of its default settings.

### CSSLint ###

CSSLint was developed by Nicole Sullivan and Nicholas Zakas. It validates the selector choices and styles in your CSS and issues warnings based on best practices.

### SublimeLinter ###

SublimeLinter is a plugin for Sublime Text that runs JSHint and CSSLint automatically each time you save your file, and highlights errors and warnings. This integration directly into the IDE speeds up development since you don't have to run a build process just to see your linting errors.

## Build ##

An automated build process is an integral part of modern web development. Concatenation, minification, and compression of static assets improves performance of web sites and applications more than any other enhancement.

### Grunt ###

Grunt is a JavaScript-based build tool. Though still in beta, it offers a number of modules for tasks such as compiling SASS, compressing images, building Require.js web applications with r.js, and more. It also offers a "watch" task that monitors your filesystem for changes, and runs custom tasks depending on the file changed.

### ANT ###

ANT is a Java-based build tool. It is likely familiar to anyone who has done enterprise application development. It is stable, and has years of experience behind it. That said, it is significantly slower than the js-based Grunt, and uses a syntax that will be less familiar to front-end developers. Concerns about Grunt's changing API as it progresses out of beta, will likely force this to be the build tool of choice for the time being.

## Version Control ##

Version Control is a requirement for any team project. It's even a good idea if you're working alone. It provides a way to modify code without worry. If things go awry, you can always revert back to an earlier version. Most version control systems also allow release tagging to mark official release versions of code.

### SVN ###

SVN is a non-distributed version control system. There is a single central canonical code repository. Users check code out of the repository, modify it, and commit their changes back into the repository where it then becomes available for other users to check out.

SVN tracks each file separately. You can make a series of changes to a number of files, and then choose which files to send to the repository on an atomic level.

### Git ###

In contrast to SVN, Git is a distributed version control system. While there is a central master branch, users clone a copy of the entire repository to their local system. They can then change, commit, and roll back changes locally, only sending changes back to the master when they are satisfied. This allows the user to work completely disconnected from the network.

Repository administrators can have greater control over Git repositories than SVN. The repository administrator can choose what to merge and from whom. Of course, multiple people can be given administrative access, but this is unlike SVN, which has a strict on/off commit access.

### ClearCase ###

<!-- TODO: Needs content -->

## Testing ##

The rigorous testing of software has long been a part of enterprise-level development. Testing has only recently received its due emphasis in front-end development, but many tools are already available to the savvy developer.

### Unit Testing ###

Unlike some server-side languages like Java or C#, JavaScript does not directly support unit testing. Various libraries introduce unit testing to JavaScript, and can run either in the browser or on a Node server. Our testing suite is as follows:

<h4>Mocha</h4>

Mocha is a unit-testing framework for JavaScript. It runs on either the browser or a Node server. It does not include an assertion library, but allows the user to choose one they may prefer.

The main reasons we choose Mocha are that it allows us to choose our own assertion library, and its first-class support for asynchronous testing. Since JavaScript is by nature asynchronous, and we may often need to test asynchronous code, this is a big deal.

<h4>Chai</h4>

Chai is our assertion library of choice. Chai allows either TDD (`assert()`)or BDD-style (`expect()`/`should()`) assertions. For readability and to match our development workflow, we prefer the BDD-style. Due to compatability issues with Internet Explorer, we prefer the `expect()` syntax to the `should()` syntax.

<h4>Sinon</h4>

Sinon is a library that offers spies, stubs, and mocks for unit testing. This basically means it offers several ways to simulate methods and track when they're called.

Sinon has no dependencies, and will work with any unit-testing framework.

### Continuous Integration ###

Continuous integration is the process by which automated testing is done each time the project source is modified, giving immediate feedback about whether the code builds, and where any errors might be located.

<h4>Travis CI</h4>

Travis CI is a continuous integration server for open-source projects. If your project has a public GitHub repository, you can easily integrate Travis CI.

### Other Testing ###

The tools here are less about automated testing, and more about smoke tests and testing within development.

<h4>Adobe Edge Inspect</h4>

Adobe Edge Inspect runs a server from your development machine that a number of mobile devices can connect to. The devices stay in sync with the page currently rendered by the development machine's browser. The development machine can then use its own dev tools to remotely inspect any of these devices, debug, and take screenshots.

## Optional ##

The following tools are all optional in that we don't force you to use these specific things. We find that they assist our development process, so we recommend you use them or a similar equivalent.

### General ###

#### LiveReload ####

[LiveReload](http://livereload.com/) is a program that monitors your filesystem. Anytime you change a file, it is preprocessed. In addition, LiveReload refreshes the browser for you, so you never have to switch out of your IDE.

LiveReload has a stable OS X release, and currently has an alpha release for Windows.

### Mac OS X ###

#### zsh ####

zsh is a replacement for the standard bash shell that ships with OS X. It has much of the same functionality, but with some useful additions. You can see an argument for using zsh here: <http://friedcpu.wordpress.com/2007/07/24/zsh-the-last-shell-youll-ever-need/>.

A useful addition to zsh is [prezto](https://github.com/bobholt/prezto), which is a fork of [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh). This is a library of "dotfiles" that offers additional functionality to make your terminal use more efficient.

#### iTerm2 ####

[iTerm 2](http://www.iterm2.com/) is a terminal replacement program for Mac OS X. If you spend any time in the terminal, you will likely find iTerm 2's features to be useful.

## Resources ##

* [<cite>James Lutley: My 2012 front-end web development workflow</cite>](http://jameslutley.com/my-2012-front-end-web-development-workflow/)


<a class="btn" href="general-guidelines.html">Previous: General Guidelines</a>
<a class="btn" href="html.html">Next: HTML</a>
