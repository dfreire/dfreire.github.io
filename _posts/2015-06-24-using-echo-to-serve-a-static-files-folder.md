---
layout: post
title: Using Echo to serve a static files folder
---

<p class="meta">{{ page.date | date: "%-d %b %Y" }}</p>
{{ page.title }}
================

[Echo](http://echo.labstack.com/) is a micro web framework for go.

Here's a snippet for serving a static files folder:

{% highlight go %}
package main

import (
	"github.com/labstack/echo"
)

func main() {
	e := echo.New()
	e.Static("/", "public") // Echo.Static(path, root string)
	e.Run(":3000")
}
{% endhighlight %}
