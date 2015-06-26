---
layout: post
title: Using Direnv to setup a Go project based development environment
---

<p class="meta">{{ page.date | date: "%-d %b %Y" }}</p>
{{ page.title }}
================

Go does not ship with a package management tool,
so the community has come up with a lot of different approaches for managing dependencies.
Some popular ones are: [godep](https://github.com/tools/godep), [gopkg](http://labix.org/gopkg.in),
and [gd](http://getgb.io/).

However, I find that the simple [direnv](http://direnv.net/) tool works for me.

I simply put a ```.envrc``` file like this on my project's root folder and all the go tools work nicely,
```go get``` correctly installs packages on the ```<project_folder>/src```, etc.

{% highlight bash %}
export GOPATH=<project_folder>
export GOBIN=$GOPATH/bin
export GOROOT=/usr/local/opt/go/libexec
export PATH=$GOROOT/bin:$GOPATH/bin:$PATH
{% endhighlight %}

[Direnv](http://direnv.net/) is language agnostic, so it can be used in other situations as well.
