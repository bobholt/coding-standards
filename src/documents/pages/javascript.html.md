---
title: JavaScript
layout: page
tags: [page']
pageOrder: 5
---

## Libraries ##

We primarily develop new applications in [jQuery](http://api.jquery.com/), though the thorough knowledge and wise usage of plain JavaScript is *strongly* recommended.

Additional libraries to be familiar with include:

* [Backbone.js](http://documentcloud.github.com/backbone/)
* [underscore.js](http://documentcloud.github.com/underscore/) (required by Backbone) <mark>(the Underscore compatability build of [Lo-Dash](http://lodash.com/) is currently preferred for its better performance and stability.)</mark>
* [RequireJS](http://requirejs.org/)

## Code Organization ##

99.9% of code should be housed in external javascript files. These files should be included at the END of the BODY tag for maximum page performance. There is no need to use the language or type attributes in the `<script>` tag (unless you're not writing JavaScript). It is the server, not the script tag, that determines the MIME type, and the browser assumes JavaScript by default for script tags.

    <body>

        <!-- page code -->

        <script src="myfile.js"></script>

    </body>

### Third-party Scripts ###

Third-party scrips should be maintained in separate files within a `vendor` directory inside your `js` directory. These will be concatenated and minified as part of the build process. Already-minified scripts should end with the extension `.min.js`

    -app
    -css
    -img
    -js
    app.js
    -vendor
    plugin1.js
    plugin2.min.js

### Application Code ###

**app.js** is meant to hold your site or application code. This isn't always the best solution as larger teams and or larger, more feature rich projects should break application code into module or feature-specific files. In these situations, however, app.js can still be used for your "main" page initialization script. For smaller sites, simpler applications, and initial prototyping, however, a single well-organized app.js file can make sense.

Always include a table of contents at the top of your js files when they combine multiple modules or pieces of functionality. For example:

    // app.js - Complete site code
    // Contents:
    //   MYAPP.common - global functionality used throughout the site
    //   MYAPP.pageOne - functionality unique to myapp.com/pageOne

    var MYAPP = window.MYAPP = window.MYAPP || {};

    MYAPP.common = (function(){&hellip;}());

    MYAPP.pageOne = (function(){&hellip;}());

### Source Code Organization ###

Organize your code using:

* AMD modules loadable through Require.js. This can include the patterns below.
* the [Revealing Module Pattern](http://www.addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript) (preferably using [DOM-based routing](http://paulirish.com/2009/markup-based-unobtrusive-comprehensive-dom-ready-execution/) when no other solution (e.g. Backbone) is applicable)
* [Objects with constructors](http://mckoss.com/jscript/object.htm)

### Configuration Variables ###

Constants or configuration variables (like animation durations, etc.) should be declared at the top of the applicable file and well-commented.

## Modifying Built-ins ##

### Object.prototype ###

Only add methods to Object.prototype if **all three** of the following conditions are met:

1. The method is a shim for methods expected to be supported consistently in future implementations of JavaScript (such as `Object.prototype.keys()`)
2. You check that the method does not already exist in the current implementation.
3. You clearly document the shim.


    // Adding ES5 implementation of Object.keys()
    if ( typeof Object.prototype.keys !== 'function' ) {

        Object.prototype.keys = function() {

            // implementation...

        };

    }

Note that jQuery does not support altering the global object. If you alter the global object and experience jQuery bugs as a result, you will need to consider a different tactic.

## Syntax Best Practices ##

### Functional Programming ###

Create functions which can be generalized, take parameters, and return values. This allows for substantial code reuse and, when combined with includes or external scripts, can reduce the overhead when scripts need to change. For example, instead of hard coding a pop-up window with window size, options, and url, consider creating a function which takes size, url, and options as variables.

When in doubt, return `this`. Returning the context object allows chaining of methods.

### Global Variables ###

Minimize global variables - the fewer globals you create, the better. Generally one, for your application namespace, is a good number. Zero, through using an AMD solution, is even better. When specifying any global variable, clearly identify it by explicitly attaching it to window, so developers after you know that you knew what you were doing.

    window.globalVar = { ... }

Note that after the declaration, you should refer to globals without the `window.` declaration, which actually takes longer to resolve in all current browsers.

All other variables should be declared inside functions using the `var` keyword or as part of an object literal.

### Local Variable Declaration and Assignment ###

Assignments in a declaration should always be on their own line with their own `var` keyword at the top of the function for easier code maintenance (See [this discussion](http://benalman.com/news/2012/05/multiple-var-statements-javascript/)). Declarations that don't have an assignment should be assigned to null. For example:

    var a = null;
    var b = null;
    var c = null;
    var test = true;
    var test2 = false;

### Semicolons ###

Variable assignments should always have a semicolon after them.

Semicolons should always be followed by an endline.

Always use semicolons. Automatic semicolon insertion is intended to fix the **error** of missing semicolons. Relying on ASI can cause subtle, hard-to-debug problems. Don't do it. You're better than that.

### Equality and type checks ###
Strict equality checks (`===`) should always be used in favor of `==` except when checking against null (the loose equality can be useful in this situation, as it will match both null and undefined).

* String: `typeof object === 'string'`
* Number: `typeof object === 'number'`
* Boolean: `typeof object === 'boolean'`
* Object: `typeof object === 'object'`
* Plain Object: `jQuery.isPlainObject(object)`
* Function: `jQuery.isFunction(object)` or `typeof object === 'function'`
* Array: `jQuery.isArray(object)`
* Element: `object.nodeType`
* null: `object === null`
* null or undefined: `object == null`
* undefined:
    * Global Variables: `typeof variable === 'undefined'`
    * Local Variables: `variable === undefined`
    * Properties: `object.prop === undefined`

### RegExp ###

All RegExp operations should be done using `.test()` and `.exec()`. "string".match() should not be used.

### Strings ###
Strings should always use <mark>single-quotes instead of double-quotes. This is helpful when creating strings that include HTML.</mark>

### Loops ###
`for-in` loops are often incorrectly used to loop over the elements in an Array. This is very error prone because it does not loop from 0 to length - 1 but over all the keys present in the object and its prototype chain. Always use normal `for` loops when using arrays.

When using jQuery, it is acceptable to use $.each() to loop over arrays, if you prefer. The performance hit is relatively small.

### document.write() ###
Don't use `document.write()`.

### eval() ###
The `eval` function has historically been the most misused feature of JavaScript. Avoid it.

`eval` has aliases. Do not use the Function constructor. Do not pass strings to `setTimeout` or `setInterval`.

### parseInt() ###
Always specify the radix parameter in `parseInt()`. This avoids unexpected parsing into non-decimal numbers. A common example is when parsing strings from date form fields:

    // With the radix
    parseInt('09', 10) === 9;

    // Without the radix
    // The leading zero forces this into base-8
    parseInt('09') === 0;

## Unit Testing ###

Projects *must* include some form of unit, reference, implementation or functional testing. Use case demonstrations DO NOT QUALIFY as "tests".

Our current preferred unit testing suite is [Mocha](http://visionmedia.github.com/mocha/) with [Sinon](http://sinonjs.org/) and [Chai](http://chaijs.com/).

## Comments and Documentation ##

### Comments ###

Comment your code! It helps reduce time spent troubleshooting JavaScript functions. An occasional nugget of humor might be appreciated. Frustrations and resentments will not.

It is important that comments be kept up-to-date. Erroneous comments can make programs even harder to read and understand.

Make comments meaningful. Focus on what is not immediately visible. Don't waste the reader's time with stuff like this:

    i = 0; // Set i to zero.

Generally use line comments. Save block comments for formal documentation and for commenting out large blocks of quote. Large commented-out blocks of quote should be removed when no longer needed. They only serve to confuse later developers about whether the functionality was permanently removed or planned to be implemented in the future.

Single line comments should always be on their own line and be above the line they reference. Additionally there should be an extra endline above it. For example:

    var some = "stuff";

    // Loop over the first ten elements of the array
    for ( var i = 0; i < 10; i++ ) {}

### Documentation ###

Documentation should follow [YUIDoc](http://yui.github.com/yuidoc/) structure. Style information can be found on [Google's Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml?showone=Comments#Comments) and the [JavaDoc](http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html) style guide is a useful resource on how to write well-formed doc comments. A syntax reference is available on the [YUIDoc site](http://yui.github.com/yuidoc/syntax/index.html).

Avoid sentence fragments in documentation. Start sentences with a properly capitalized word, and end them with punctuation.

## Feature Detection ##

Don't rely on the user-agent string. Do proper feature detection. (More at [Dive Into HTML5: Detection](http://diveintohtml5.org/detect.html) & [jQuery.support docs](http://api.jquery.com/jQuery.support/)).

[Modernizr](http://modernizr.com/) makes this very easy, and a build of it should be in every project, if only to provide HTML5 shimming.

## Deploying to Production ##

All JavaScript is required to pass [JSHint](http://www.jshint.com/) before moving to production. See [Appendix A](appendices.html) for a list of options we include by default.

Use automatic minification. [Google Closure Compiler](https://developers.google.com/closure/compiler/) or [UglifyJS](https://github.com/mishoo/UglifyJS) as part of an automated build process is preferred. Don't manually minify. With the exception of the traditional `i`, etc. in `for` loops, variable names in your code should be long enough to be meaningful.

## Event Delegation ##

When assigning unobtrusive event listeners, it is typically acceptable to assign the event listener directly to the element(s) which will trigger some resulting action. However, occasionally there may be multiple elements which match the criteria for which you are checking, and attaching event listeners to each one might negatively impact performance. In such cases you should use event delegation instead.

jQuery's [`delegate()`](http://api.jquery.com/delegate) (jQuery 1.4) should be used over [`live()`](http://api.jquery.com/live) for performance reasons. As of jQuery 1.7 [`on()`](http://api.jquery.com/on/) and [`off()`](http://api.jquery.com/off/) should be used exclusively.

## Exception Handling ##

Without custom exceptions, returning error information from a function that also returns a value can be tricky, not to mention inelegant. Feel free to throw custom exceptions when appropriate.

    var loadException = function(message) {
        this.message = message;
        this.name = "Load Exception";
    }

    var mightThrow = function() {
        if (something) {
            // ...
        } else if (somethingElse) {
            // ...
        } else {
            throw new loadException("Data Not Loading");
        }
    };

Mitigate errors by handling all possible cases. `try`/`catch` blocks should not be used in performance-critical code, as the catch block executes in an additional context layer.

## Debugging ##

Even with the best of validators, browser quirks will inevitably cause issues. There are several invaluable tools which will help to refine code integrity and loading speed. It is important that you have all of these tools available to you, despite the browser you primarily use for development. We recommend developing for Google Chrome first, then Firefox, Safari, and Opera, with additional tweaks via conditional comments just for Internet Explorer. The following is a list of helpful debuggers and speed analyzers...

* **Firefox**: [Firebug](http://getfirebug.com/), [Page Speed](http://code.google.com/speed/page-speed/), [YSlow](http://developer.yahoo.com/yslow/)
* **Safari**: [Web Inspector](http://developer.apple.com/safari/library/documentation/AppleApplications/Conceptual/Safari_Developer_Guide/UsingtheWebInspector/UsingtheWebInspector.html)
* **Google Chrome**: [Developer Tools](http://google.com/chrome/intl/en/webmasters-faq.html#tools)
* **Opera**: [Dragonfly](http://opera.com/dragonfly/)
* **Internet Explorer 6-7**: [Developer Toolbar](http://microsoft.com/downloads/details.aspx?familyid=E59C3964-672D-4511-BB3E-2D5E1DB91038)
* **Internet Explorer 8-10**: [Developer Tools](http://msdn.microsoft.com/en-us/library/dd565625%28v=VS.85%29.aspx)

## Matters of Style ##

### Naming Conventions ###

Naming Conventions in JavaScript are just that: conventions. There is nothing in JavaScript that requires these conventions, but these have emerged over time as a best practice, and should be observed.

#### Files ####

Filenames should be all lowercase in order to avoid confusion on case-sensitive platforms. Filenames should end in .js, and should contain no punctuation except for - (dash) or _ (underscore) (we prefer dashes to underscores). For example, `myfile.js` or `my-file.js`.

#### Variables and Functions ####

Variables and functions should be lower camel-case. That is, they should start with a lowercase letter, and subsequent words in the name should be capitalized. For example, `myFunction()` or `myReallyLongFunction()`

Name variables and functions logically: For example: `popUpWindowForAd` rather than `myWindow`. All Boolean variables should start with "is". Test for positive conditions.

    isValid = (test.value >= 4 && test.success);

##### Constructors #####

Constructor functions should use upper camel case. JavaScript issues neither a compile-time warning nor a run-time warning if a required new is omitted. Bad things can happen if `new` is not used, so the capitalization convention is the only defense we have.

    var MyConstructor = function(){...};

    var instance = new MyConstructor();

##### Constants #####

Use all-caps separated by underscores for variables you would consider to be constant. Never use the `const` keyword because IE doesn't parse it.

    var DAYS_IN_WEEK = 7;

##### Private variables #####

"Private" variable and function names should start with an underscore. Since JavaScript doesn't have true "private" properties, this is simply an indicator to developers to neither change nor rely on any undocumented behavior of this property.

    var _dontTouchMe = function() {...}

### Whitespace ###

Use **two spaces** to indent your code.

Use liberal spacing in your code for readability. The minification process will take care of removing it.

    // NO:
    if(blah==='foo'){

        foo('bar','baz',{zoo:1});

    }

    // YES:
    if ( blah === 'foo' ) {

        foo( 'bar', 'baz', {zoo: 1} );

    }

### Additional Whitespace Rules ###

Opening braces are always prefixed by a space.

    // NO:
    if (test){

    // YES:
    if (test) {

Commas and colons are always followed by a space.

    // NO:
    var arr = [ 1,2,3 ];

    // YES:
    var arr = [ 1, 2, 3 ];

Don't use tabs inside a line.

    var a = true;

    // yayy
    var c = false;

    // grrr
    var b    = false;

Lines with nothing on them should have no whitespace.

There should be no whitespace at the end of a line. Set your IDE/text editor to trim whitespace at the end of lines.

Always include extra spaces around the arguments.

    foo( true );

    foo( 'blah' );

Exception: no spaces is allowed if you're already inside of another function call.

    // Allowed:
    foo( bar(true) );

Exception: Functions, object literals, and array literals go snug to front and back of the parentheses - but ONLY when it's the only argument.

    // Allowed:
    foo(function() { });

    foo([   ]);

    foo({   });

Exception: *Multi-line* function/object/array literals go snug at end (and at start ONLY if the only argument).

    // NO:
    foo( true, { blah: 'baz' });

    // YES:
    foo( true, {

    blah: "baz"

    });

Empty functions don't need filler spaces.

    foo();

Empty objects and arrays don't need filler spaces.

    []
    {}

### Code Blocks ###
`if`/`else`/`for`/`while`/`try` always have braces and always go on multiple lines.
Braces should always be used on blocks.

    // NO:
    if ( true )
    blah();

    // YES:
    if ( true ) {
        blah();
    }

Don't put statements on the same line as a conditional.

    // NO:
    if ( true ) return;
    if ( true ) blah();

    // YES:
    if ( true ) {
        return;
    }

    if ( true ) {
        blah();
    }

`else`/`else if`/`catch` go on the same line as the brace.

    if ( blah ) {
        baz();
    } else {
        baz2();
    }

Exception: else if is allowed, a else { } is not required

    } else if ( test ) {
        blah();
    }

    // Not needed:
    } else {
        if ( test ) {
            blah();
        }
    }

Don't use ternary operators instead of if/else statements except in object literals.

    // NO:
    someVar = logicalTest ? 'ifTrue' : 'ifFalse';

    // YES:
    if ( logicalTest ) {

        someVar = 'ifTrue';

    } else {

        someVar = 'ifFalse';

    }

    // Acceptable:
    var obj = {

        param: logicalTest ? 'ifTrue' : 'ifFalse'

    };

<a class="btn" href="css.html">Previous: CSS</a>
<a class="btn" href="testing.html">Next: Testing</a>
