---
title: HTML
layout: page
tags: [page']
pageOrder: 3
---

HTML is the structure and content of the web. It does not define the look and feel of a document, but its semantic structure. We will define formatting and style rules in raw files that use HTML, including template files.

We will follow the HTML5 markup standard. We don't believe that there is any arguable reason to use XHTML. HTML5 should be the baseline for any new project. Its doctype works in all browsers, and older browsers such as IE6 can be shimmed to support new HTML5 elements.

## HTML5 Boilerplate ##

The [HTML5 Boilerplate](http://html5boilerplate.com/) offers a quick and easy template for any HTML5 site. It is the combined result of many many developers contributing knowledge and best practices. You should strongly consider using it as the basis for any new project.

## Doctype ##

Only doctypes which trigger browser standards modes should be used. Quirks mode is not acceptable. The HTML5 doctype works in all browsers, triggers standards mode, and removes the need to use CDATA blocks for inline JavaScript (which you should avoid in most cases).

`<!DOCTYPE html>`

It's that easy.

## Character Encoding ##

Your HTML should be delivered as UTF-8 for best support of international character sets. The server should ensure this is set in the HTTP header sent with the file, but your markup should also include a `meta` element in the head of the document.

In HTML5:<br>
  `<meta charset="utf-8">`

This element should be placed immediately after the `<head>` element in an attempt to avoid re-rendering in IE. (See <http://support.microsoft.com/kb/928847>.)

When using UTF-8, there is no need to use entity references such as `&mdash;` or `&rdquo;`, assuming the file editors and all team members are also using UTF-8. The remaining exception to this is for characters that have special meaning in HTML such as `&lt;`, `&amp;`, and `&nbsp;`.

For more information: [<cite>W3C: Handling character encodings in HTML and CSS</cite>](http://www.w3.org/International/tutorials/tutorial-char-enc/).

## Viewport Meta Element ##

The viewport meta element should be constructed in this manner:

`<meta name="viewport" content="width=device-width">`

This configuration sets the content to match the width of the device, while still allowing the user to zoom in or out to their preferred level. You may see developers use `maximum-scale=1` or `user-scalable=no`. This prohibits the user from zooming in on a mobile device, and for accessibility, should never be used.

## Validation ##

All HTML markup should be run through the [W3C validator](http://validator.w3.org/). 100% validity is not necessary, but you should understand why your code does not pass, and make a conscious choice for that outcome.

## Comments ##

Commenting HTML is not as important as JavaScript, but it can be useful for delineating sections. A recommended practice is to place an comment on closing tags to indicate which element is being closed. For example:

    <div class="my-div">
        ...
    </div><!-- end div.my-div -->

## Conditional Comments ##

Internet Explorer prior to version 10 recognizes [conditional comments](http://msdn.microsoft.com/en-us/library/ms537512%28v=vs.85%29.aspx), which allows the conditional loading of resources (such as stylesheets or script files) based on the version of IE the client is using.

Every effort should be made to construct a fully-functional and well-rendered site prior to the use of conditional comments. Conditionals should be something of a last resort for browser compatibility.

HTML5 Boilerplate handles this in an interesting way, using conditional comments to add `.ie7`, `.ie8`, or `.ie9` classes to the page, which can then be used in your base stylesheet to specify IE-specific styles. This makes it so IE isn't forced to download an additional stylesheet (a file-transfer penalty).

## Semantic Markup ##

HTML elements should be chosen in such a way as to represent the semantic content of the document. Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons. This is a longer conversation than we will tackle at the present time, but here are a few quick pointers:

* Never ever use tables for page layout. Ever. It is semantically bad, poor for accessibility, and makes for nearly unreadable source code. It has no place in the modern web. Don't do it.
* Use headings elements (`<h1>` - `<h6>`) for headings.
* Use the `<p>` paragraph element for paragraph content. Do not separate paragraphs with multiple `<br>` elements. That would be an example of inserting presentation into your markup.
* Lists of items should always be marked up in a `<dl>`, `<ol>`, or `<ul>`. Never use a series of `<div>` or `<p>` elements for lists.
* Use label fields to label each form field, the `for` attribute should associate itself with the input field, so users can click the labels. `cursor:pointer;` on the label in your CSS is wise, as well.

These pages have some great information:

* [<cite>Adobe Developer Connection: Using semantic HTML</cite><](http://www.adobe.com/devnet/html5/articles/semantic-markup.html)
* [<cite>BBC: Future Media Standards & Guidelines - Semantic Mark-up v1.6</cite>](http://www.bbc.co.uk/guidelines/futuremedia/technical/semantic_markup.shtml)

## Quoting Attributes ##

While the HTML5 specification defines quotes around attributes as optional, for consistency with attributes that accept whitespace, all attributes should be quoted.

    <p class="line note" data-attribute="106">This is my paragraph of special text.</p>

## Style Guidelines ##

### General Formatting ###

Use a new line for every block-level element. If they are children of other block-level elements, they should be indented.

It is acceptable for `<li>` elements to be placed all on one line if the whitespace around them causes display issues (typically seen in horizontal layouts with `display: inline-block;`).

### Protocol-Relative URLs ###

Omit the protocol (`http:`, `https:`) from embedded resources such as images, media files, style sheets, and script files unless the resource is not available over both protocols.

This prevents mixed-content warnings in browsers. In HTML:

    <!-- Not recommended -->
    <script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>

    <!-- Recommended -->
    <script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>

And in CSS:

    /* Not recommended */
    .example {
        background: url(http://www.google.com/images/example);
    }

    /* Recommended */
    .example {
        background: url(//www.google.com/images/example);
    }

### Capitalization ###

Use only lowercase for element names and attributes. HTML5 allows uppercase, but that doesn't read well.

### Void Elements ###

Although fine with HTML, do not close void elements, e.g. write `<br>`, not `<br />`.

### Type attributes ###

`type` attributes for style sheets and scripts can be safely omitted in HTML5 (unless using styles other than CSS or scripts other than JavaScript).

<a class="btn" href="workflow.html">Previous: Workflow</a>
<a class="btn" href="css.html">Next: CSS</a>
