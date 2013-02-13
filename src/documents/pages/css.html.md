---
title: CSS
layout: page
tags: [page']
pageOrder: 4
---

The second component of a web page is the presentation information contained in the Cascading Style Sheet (CSS.) Web browsers successful implementation of CSS has given a whole generation of web authors site-wide control over the look and feel of their web sites.

Just as the information on a web page is semantically described in the HTML markup, CSS describes all presentation aspects of the page via a description of its visual properties. CSS is powerful in that these properties are mixed and matched via identifiers to control the page's layout and visual characteristics through the layering of style rules (the "cascade").

Many of our CSS rules are drawn from the default rules for [CSS Lint](http://csslint.net/). These are a collection of best practices from people who have built very large modular web applications. We have augmented them with additional recommendations.

## Files and Placement ##

Your CSS should be in external files, linked to from the HEAD of the document using `<link>` elements (not @import rules).

## Resets ##

Reset files allow more consistent styling across browsers. Solutions range from the more invasive to the looser, depending on how much of the browser defaults to come through.

We generally recommend normalize.css, which ships with the [HTML5 Boilerplate](http://html5boilerplate.com/), and offers sensible defaults.

## Formatting ##

CSS selectors should each be on their own line. Each property should also be on its own line, and indented, like so:

    .my-selector {
        color: #333;
        margin: 2px;
    }

Single-line CSS should be avoided at all costs, because it is a version-control nightmare. Changing one property causes the entire style to be flagged as a change. Your automated build process will take care of minifying your CSS for you.

## Semantics ##

For a long time, there has been a push for semantic class names on web pages, meaning an element's class should describe what it is, not what it looks like. While there is some merit to this, we don't enforce it dogmatically. Sometimes a non-semantic classname just makes sense, especially when we're talking about pre-made components with a specific use case.

## Parsing Errors ##

Validate your CSS. Invalid CSS has the possibility of dropping a property or an entire rule. If you think this rule is in effect, but actually isn't, you'll be quickly frustrated. Linting your CSS removes this concern.

## Hacks ##

In the long history of CSS, several "hacks" were discovered that selectively loaded styles in certain browsers. These include the "star hack" and the "underscore hack" to load styles only into IE < 8 and IE < 7, respectively. The usage of such hacks is considered bad practice, and should not be used. Instead, use IE conditional comments to load over-riding styles for those browsers.

## !important ##

The occasional use of `!important` can be necessary; for example, when overriding a third-party widget (such as [Twitter](http://dev.twitter.com/) or [Disqus](http://disqus.com/)) that dynamically loads in its own !important styles. Outside of this example, however, the `!important` declaration is usually a sign of poorly-formed CSS. When backed into using the `!important` declaration, it is likely more advantageous for you to refactor your CSS immediately than to use it.

## Vendor Prefixes ##

Experimental CSS properties often require vendor prefixes to work in certain browsers. While browser vendors such as Chrome are working as quickly as possible to support these properties without the prefix, they remain an important part of writing CSS.

Some developers only use the -webkit prefix on experimental properties. As this excludes the sizable population that uses a Mozilla, Presto, or Microsoft browser engine, we should use all vendor prefixes required by a property. Additionally, don't forget to use the non-prefixed property, which will future-proof your site for when browsers drop the prefix.

Luckily for us, if we use SASS with Compass, the pre-made [Compass CSS3 prefixes mixin](http://compass-style.org/reference/compass/css3/) will take care of this for us.

## Accessibility ##

We mention accessibility a few times in this document, but here are some additional considerations.

### Focus Outlines ###

Never use `outline: 0` or `outline: none;` on focusable elements. The most important accessibility feature is keyboard navigation, and removing focus outlines makes this next-to-impossible for sighted keyboard users.

Another quick pointer is that whenever you declare a :hover style, you should also declare a :focus style for keyboard navigation. These can often be the same style, which makes it easy to do.

## Pixels vs. Ems ##

The jury's still out!

## Box-Sizing ##

The traditional CSS box model is frustrating at best. In the traditional model, an element with 100px width, 5px of padding, and 1px of border would come out to be 112px wide. Even worse, with percentages, we can't use width 100% with padding or border, because our element breaks out of the flow. When we design a layout, especially a responsive one, we would like the width we set to be the actual final width.

`box-sizing: border-box` to the rescue.

If you apply box-sizing: border box to an element, its padding and border are deducted from the width instead of added to it. Seems sensible, right? This doesn't work in IE6 or IE7, but there's a [reasonable polyfill](https://github.com/Schepp/box-sizing-polyfill) for the functionality. Mozilla and older versions of Android require vendor prefixes.

Border-box can be appied on an element-by-element basis, or to the entire site using the universal selector, `*`. The performance of the `*` selector is not a concern, as it's just as fast as using any element selector like `h1`.

So use `box-sizing: border-box` with all new development, particularly responsive designs. Components for the component library should have this applied to the outermost element, and new sites should have this applied universally.

The full syntax with vendor prefixes follows:

    /* apply a natural box layout model to all elements */
    * {
        -moz-box-sizing: border-box;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
    }

For more information: [* { box-sizing: border-box } FTW](http://paulirish.com/2012/box-sizing-border-box-ftw/) - Paul Irish

## Shorthand Properties ##

Some styles such as margin, padding, background, border, and font allow shorthand versions of their declarations. So, instead of typing out margin-top, margin-right, margin-bottom, and margin-left, you can and should use the shorthand: `margin: 1px 2px 3px 4px;`.

In general, CSS shorthand is preferred because of its terseness, and the ability to later go back and add in values that are already present, such as the case with margin and padding. Developers should be aware of the TRBL acronym, denoting the order in which the sides of an element are defined, in a clock-wise manner: Top, Right, Bottom, Left. If bottom is undefined, it inherits its value from top. Likewise, if left is undefined, it inherits its value from right. If only the top value is defined, all sides inherit from that one declaration.

## Image Replacement ##

Image replacement a CSS technique used when you want to replace existing page text with an image, but still leave the text available for screen readers. A common example is the site logo.

There have been a number of techniques put forward for image replacement over the years, and new techniques come out every few months.. Each has its own set of drawbacks. We recommend using the latest HTML5 Boilerplate on each new project, as this includes the current state-of-the-art image replacement technique. As of December 2012, the technique used is as follows:

    /*
    * Image replacement
    */

    .ir {
        background-color: transparent;
        border: 0;
        overflow: hidden;
        /* IE 6/7 fallback */
        *text-indent: -9999px;
    }

    .ir:before {
        content: "";
        display: block;
        width: 0;
        height: 150%;
    }

This technique avoids the -9999px text-indent, which has some unwanted side effects, in all browsers but IE6 and 7. For IE6 and 7, notice that the CSS "star hack" is used, which we said that you shouldn't do. A better solution within your project would be to use IE conditional comments to load this style separately for IE < 8. Using the hack within HTML5 Boilerplate ensures that even users who don't use conditional stylesheets get the fix.

## Inefficient Selectors ##

For the most part, we aren't overly concerned with selector performance. There are many other ways a page can be slow, such as overloading images or web fonts, but there are some selectors to watch out for.

### RegEx Selectors ###

Some selectors utilize a regular expression when being applied to the page, and are significantly slower than other selectors. For the most part, these are used when matching attributes such as:

    a[href*=github.com] {
        color: green;
    }

Selectors to avoid include:


* `*=`
* `|=`
* `^=`
* `$=`
* `~=`


Note that this does not include the plain attribute selector, `a[href]` or the exact equals selector, `a[rel=external]`. These do not have the same regex-related performance hit as the ones listed above.

### The Universal Selector ###

In our discussion of box-sizing, we noted that there is not a performance concern with the universal selector, `*`. This is true when it is used by itself. However, it should never be used as the right-most part of a multi-part selector.

This is fine:

    * {
        /* styles */
    }

But this is not:

    p * {
        /* styles */
    }

Unqualified attribute selectors have the same issue when used as the right-most part of a selector (or even alone).

These are fine:

    input[type=text] {
        /* styles */
    }

    [rel=external] span {
        /* styles */
    }

But this is not:

    div [type=text] {
        /* styles */
    }

    [rel=external] {
        /* styles */
    }

## Useless Properties ##

Depending on the display setting of your element, certain properties have no effect. Including these properties in your style blocks only adds confusion and bloat to your CSS. You can safely delete the following properties depending on your display type:

<dl class="dl-horizontal">
  <dt>`display: inline`</dt>
  <dd>width, height, margin-top, margin-bottom, float</dd>
  <dt>`display: inline-block`</dt>
  <dd>float</dd>
  <dt>`display: block`</dt>
  <dd>vertical-align</dd>
  <dt>`display: table-*`</dt>
  <dd>margin, float</dd>
</dl>

## Web Fonts ##

Web fonts have quickly become a go-to for web design. There are a few things you should watch out for, however.

### The @font-face Declaration ###

Due to a parsing bug in old versions of IE, @font-face should be declared in a very specific way. The IE .eot font face should be declared first, and its url should include a query string.

    @font-face {
        font-family: 'MyFontFamily';
        src: url('myfont-webfont.eot?#iefix') format('embedded-opentype'),
        url('myfont-webfont.woff') format('woff'),
        url('myfont-webfont.ttf')  format('truetype'),
        url('myfont-webfont.svg#svgFontName') format('svg');
    }

This forces IE to see everything after the .eot as one large query string, thus eliminating the 404 error that may otherwise arise.

### Number of Web Fonts ###

Web fonts are great, but they are also huge. H - U - G - E. It's not uncommon to see your font payload hit over 1 MB with just a few faces or weights. In addition, fonts are blocking downloads in some browsers, and keep other page resources from downloading until they are complete.

A recommendation is to use web fonts only for titling or other special purpose. Replacing body text, which can render in Arial, Verdana, or Georgia with a web font that is "like" Arial, Verdana, or Georgia only adds useless weight to your page, and reduces performance.

## Additional Resources ##

* [CSS Lint Rules](https://github.com/stubbornella/csslint/wiki/Rules)

<a class="btn" href="html.html">Previous: HTML</a>
<a class="btn" href="javascript.html">Next: JavaScript</a>
