---
title: Appendices
layout: page
tags: [page']
pageOrder: 12
---

## Appendix A: JSHint Options ##

* `"browser" = true`, `"jquery" = true` - This allows us to use globals variables available in modern browsers and jQuery.
* `"eqeqeq" = true`, `"eqnull" = true` - Almost universally we use `===` or `!==` with the exception of when we're comparing against `null`. It's actually quite useful to do `== null` or `!= null` as it will pass (or fail) if the value is either `null` or `undefined`. If we want to explicitly check for a `null` or `undefined` value we use `=== null` or `=== undefined`.
* `"smarttabs" = true` - This allows us to mix tabs and spaces on the same line, which we only do in comment blocks

<a class="btn" href="code-reviews.html">Previous: Code Reviews</a>