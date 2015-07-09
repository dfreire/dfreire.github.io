---
layout: post
title: CSS
---

<p class="meta">{{ page.date | date: "%-d %b %Y" }}</p>
{{ page.title }}
================

<iframe width="100%" height="300"
    src="//jsfiddle.net/z7cmf22f/embedded/result,js,html,css/"
    allowfullscreen="allowfullscreen"
    frameborder="0">
</iframe>

## Inline style sheet

```html
<p style="color: green;">This text is green.<p>
```

* You are styling single elements
* This approach is not reusable

## Header style sheet
```html
<html>
    <head>
        <style>
            p { color: green; }
        </style>
    </head>
    <body>
        <p>This text is green.</p>
    </body>
</html>
```

* Not reusable across pages

## Link style sheet
```html
<html>
    <head>
        <link rel="stylesheet" href="style.css">
    </head>
    <body>
        <p>This text is green.</p>
    </body>
</html>
```

```css
p { color: green; }
```
