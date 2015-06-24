---
layout: post
title: Using echo to serve a static files folder
---

<p class="meta">26 Jun 2015</p>

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
