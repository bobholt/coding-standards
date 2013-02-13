---
title: Appendices
layout: page
tags: [page']
pageOrder: 12
---

## Appendix A: JSHint Options ##

The following options should be set in both your project's JSHint build options and in SublimeText's SublimeLinter plugin user options (Sublime Text 2 > Preferences > Package Settings > SublimeLinter > Settings - User). See "Settings - Default" for the proper formatting (or download a [sample](/files/sublime-text--settings-user.txt)). The jQuery option below can be set to `true` for SublimeText, but should be `false` in your project build.

```none
// Enforcing Options
"bitwise"       : true,     // Prohibits bitwise operators
"camelcase"     : true,     // Forces camelCase or UPPER_CASE variable names
"curly"         : true,     // Requires curly braces around blocks
"eqeqeq"        : true,     // Forces strict equality checks
"forin"         : true,     // Requires own property checks in `for-in` loops
"immed"         : true,     // Requires IIFEs to be wrapped in parentheses
"indent"        : 4,        // Enforces a specific tab width (may not work?)
"latedef"       : true,     // Requires defining a variable before using it
"newcap"        : true,     // Requires constructor functions to be capitalized
"noarg"         : true,     // Prohibits `arguments.caller` & `arguments.callee`
"noempty"       : true,     // Warns about empty code blocks (useless code)
"nonew"         : true,     // Prohibits using constructors for side-effects
"plusplus"      : false,    // Prohibits increment & decrement (`++` & `--`) - DISABLED
"quotmark"      : "single", // Forces single quotes for strings
"regexp"        : true,     // Prohibits the unsafe `.` selector in regular expressions
"undef"         : true,     // Prohibits using explicitly undeclared variables
"unused"        : true,     // Warns on unused variables
"strict"        : true,     // Forces strict mode in functional scope
"trailing"      : true,     // Makes trailing whitespace an error
"maxparams"     : 4,        // Sets the maximum number of arguments allowed in a fn
"maxdepth"      : 3,        // Sets the maximum number of nested blocks
"maxstatements" : 30,       // Sets the maximum number of statements allowed in a fn
"maxcomplexity" : 10,       // Sets cyclomatic complexity
"maxlen"        : 150,      // Sets the maximum line length

// Relaxing Options
"asi"           : false,    // Allows missing semicolons
"boss"          : false,    // Allows using assignment `=` where comparison `===` is expected
"debug"         : false,    // Allows `debugger` statements
"eqnull"        : true,     // Allows `==` when comparing with null - ENABLED
"es5"           : false,    // Allows ES5 features which may not be supported in all browsers
"esnext"        : false,    // Allows ES6 features which are not yet finalized
"evil"          : false,    // Allows the use of `eval()`
"expr"          : false,    // Allows the use of expressions where assignments or fn calls are expected
"funcscope"     : false,    // Allows declaring variables inside control structures
"globalstrict"  : false,    // Allows global strict mode, which can break third-party plugins
"iterator"      : false,    // Allows using the `__iterator__` property
"lastsemic"     : false,    // Allows no semicolons on the last statement in a 1-line block
"laxbreak"      : false,    // Allows potentially-unsafe line breaks
"laxcomma"      : false,    // Allows comma-first coding style
"loopfunc"      : false,    // Allows fn definition inside loops
"multistr"      : false,    // Allows multi-line strings
"onecase"       : false,    // Allows single-case switches.
"proto"         : false,    // Allows using the `__proto__` property
"regexdash"     : false,    // Allows unescaped `-` at the end of regular expressions
"scripturl"     : false,    // Allows `javascript:` urls
"smarttabs"     : false,    // Allows mixed tabs & spaces
"shadow"        : false,    // Allows variable shadowing
"sub"           : false,    // Allows `[]` notation when dot notation is available.
"supernew"      : false,    // Allows "weird" constructors
"validthis"     : false,    // Allows possible strict violations of `this`.

// Environments
"browser"       : true,     // Pre-defines browser globals such as `document` and `navigator`
"couch"         : false,    // Pre-defines CouchDB globals
"devel"         : false,    // Pre-defines `console` and `alert` globals
"dojo"          : false,    // Pre-defines Dojo globals
"jquery"        : false,    // Pre-defines jQuery globals - Enable in SublimeText Options
"mootools"      : false,    // Pre-defines MooTools globals
"node"          : false,    // Pre-defines Node.js globals
"nonstandard"   : false,    // Pre-defines non-standard globals like `escape` and `unescape`
"prototypejs"   : false,    // Pre-defines Prototype globals
"rhino"         : false,    // Pre-defines Rhino globals
"worker"        : false,    // Pre-defines Web Worker globals
"wsh"           : false,    // Pre-defines Windows Script Host globals
"yui"           : false,    // Pre-defines YUI globals

// Legacy
// These options are legacy from JSLint.
// Aside from bug fixes they will not be improved in any way and might be removed.
"nomen"         : false,    // Prohibits the dangling `_` in variables
"onevar"        : false,    // Forces one `var` statement per fn
"passfail"      : false,    // Forces JSHint to stop on the first error
"white"         : false,    // Checks against Douglas Crockford's whitespace rules
```

The following options should not be included in project linting, but can be added to Sublime Text's SublimeLinter User Options so it doesn't yell at you for your test suite.

```none
// Pre-defined globals
"predef"        : [
    "after",        // Chai BDD Assertions
    "afterEach",    // Chai BDD Assertions
    "before",       // Chai BDD Assertions
    "beforeEach",   // Chai BDD Assertions
    "define",       // Require.js AMD definition
    "describe",     // Chai BDD Assertions
    "expect",       // Chai BDD Assertions
    "it",           // Chai BDD Assertions
    "require",      // Require.js AMD definition
    "sinon"         // Sinon mock/stub/spy framework global
]
```

## Appendix B: Sublime Text User Settings ##

The following settings are recommended for SublimeText. You can copy this directly into your User Settings (Sublime Text > Preferences > Settings - User) if it is empty, or edit it to include the following:

```none
{
    // The number of spaces a tab is considered equal to
    // Required by our standards
    "tab_size": 4,

    // Set to true to insert spaces when tab is pressed
    // Default to soft-tabs. Required by our standards
    "translate_tabs_to_spaces": true,

    // Set to true to removing trailing white space on save
    // Required by our standards
    "trim_trailing_white_space_on_save": true

    // Determines what character(s) are used to terminate each line in new files.
    // Valid values are 'system' (whatever the OS uses), 'windows' (CRLF) and
    // 'unix' (LF only).
    // Required by our standards
    "default_line_ending": "unix",

    // List any packages to ignore here. When removing entries from this list,
    // a restart may be required if the package contains plugins.
    // Vintage puts SublimeText in VI mode.
    "ignored_packages": [
        "Vintage"
    ]
}
```

There are plenty of other options you can choose from. Refer to the Default Settings file for explanations, but some we find useful are:

```none
// Completely Optional
{
    // Spacing between the gutter and the text
    // Reduces space in the IDE
    "margin": 0,

    // Columns in which to display vertical rulers
    // Adds a line at our JSHint-set right text limit
    "rulers": [150],

    // Set to true to turn spell checking on by default
    "spell_check": true,

    // Makes auto indent a little smarter, e.g., by indenting the next line
    // after an if statement in C. Requires auto_indent to be enabled.
    // This seems to have additional side-effects. Set to false.
    "smart_indent": false,

    // Set to true to draw a border around the visible rectangle on the minimap.
    // The color of the border will be determined by the "minimapBorder" key in
    // the color scheme
    // Makes it easier to see the visible rectangle in some color schemes
    "draw_minimap_border": true,

    // Set to false to disable scrolling past the end of the buffer.
    // On OS X, this value is overridden in the platform specific settings, so
    // you'll need to place this line in your user settings to override it.
    // Makes the right-side mini-map scroll more intuitively
    "scroll_past_end": false,

    // By default, auto complete will commit the current completion on enter.
    // This setting can be used to make it complete on tab instead.
    // Completing on tab is generally a superior option, as it removes
    // ambiguity between committing the completion and inserting a newline.
    "auto_complete_commit_on_tab": true,

    // Makes tabs with modified files more visible
    "highlight_modified_tabs": true,

    // Show folders in the side bar in bold
    "bold_folder_labels": true
}
```

<a class="btn" href="code-reviews.html">Previous: Code Reviews</a>