---
title: General Guidelines
layout: page
tags: [page']
pageOrder: 1
---

Style guidelines exit in order to have a common vocabulary of coding so other developers can concentrate on what you're saying rather than on how you're saying it. Common code style across an organization helps consistency, readability, and team efficiency.

Several things, such as indentation rules, are choices between two or more equally-valid options. These choices have to be made for project consistency. To steal a phrase from [Douglas Crockford](http://www.crockford.com/), these standards "will hurt your feelings," because no two developers will naturally code in exactly the same way, and it is unlikely you already code in exactly the way these standards define. You may not agree with these choices, but we ask that you abide by them. You are free to code however you like on your own projects.

In some cases, these standards will be enforced through an automated code linting and build process. Coding against the standard will throw errors that will have to be fixed before you will be allowed to commit code.

## On Consistency ##

Be Consistent.

If you're editing code someone else wrote, take a few minutes to look at the code around you and determine its style. If they use spaces around all their arithmetic operators, you should too. If their comments have little boxes of hash marks around them, your comments should have little boxes of hash marks around them too.

We present global style rules here so that we can all know the vocabulary, but local style is also important. If code you add to a file looks drastically different from the existing code around it, it throws readers out of their rhythm when they go to read it. Avoid this.

## Separation of Concerns ##

Front-end development is made up of HTML, CSS, JavaScript, and related technologies. The most basic rule is:

**Separate content, presentation, and behavior.**

<dl class="dl-horizontal">
	<dt><dfn>Content</dfn></dt>
	<dd>HTML markup. This should be structural, semantic, and devoid of presentation or behavioral code.</dd>

	<dt><dfn>Presentation</dfn></dt>
	<dd>CSS styling. It should be separate from your markup.</dd>

	<dt><dfn>Behavior</dfn></dt>
	<dd>JavaScript code. It should be separate from your markup.Y/dd>
</dl>

## Readability vs. Performance ##

Readable, maintainable code is better than unreadable code, no matter the performance gains. Always choose readability. Performance or file-size gains are negligible compared to the cost of maintaining too-clever code. Minification and compression as part of an automated build process reduce these gains even further. Superfluous or poorly-optimized images have a greater impact on performance than any code optimizations you are likely to make.

Whitespace is encouraged to enhance readability, as are comments. Specific whitespace recommendations for each language will be covered in detail in later sections.

## Indentation ##

In all languages, we choose to use **soft tabs**: that is, spaces instead of the tab character. The tab size will be **two (2)** spaces.

## Line Endings ##

Difference in line-endings between different users is a common cause of merge conflicts.

Unix/OS X and Windows use two different standards for line endings. Without going into specifics, choose Unix-style (LF), not Windows-style (CR+LF). There is a setting within SublimeText to ensure this, and [a plugin](http://github.com/SublimeText/LineEndings) to help you manage it.

Remove extra whitespace at the ends of lines of code. Your IDE should be set up to do this automatically. You may choose to 'show invisibles' in your IDE. This will allow you to 'see' the whitespace characters.

<a class="btn" href="index.html">Previous: Home</a>
<a class="btn" href="workflow.html">Next: Workflow</a>
