---
layout: post
title: Semantic Versioning
---

<p class="meta">{{ page.date | date: "%-d %b %Y" }}</p>
{{ page.title }}
================

[Semantic Versioning](http://semver.org/), usually abbreviated as **semver**, is a software versioning scheme that uses the format:
```MAJOR.MINOR.PATCH```.

If you are using a library with the semver version ```1.4.2```, the next patch version should be ```1.4.3```, the next minor version should be ```1.5.0```, and the next major version should be ```2.0.0```.

A **patch version** should only contain bug fixes and remain backwards compatible.

A **minor version** contains new features, but remains backwards compatible.

A **major version** can contain new features that break backward compatibility.

When your projects dependend on semantically versioned packages, you need to specify the version ranges you are willing to accept. For example, if you have a [npm](https://www.npmjs.com/) project that depends on lodash, you can declare the dependecy in your ```package.json``` file:

- ```"lodash": "3.9.3"```, to accept only this specific version
- ```"lodash": "~3.9.3"``` or ```"lodash": "3.9.x"```, to accept all patch releases after 3.9.3
- ```"lodash": "^3.9.3"``` or ```"lodash": "3.x"```, to accept all minor releases after 3.9.3
- ```"lodash": "*"``` or ```"lodash": "x"```, to accept all versions

{% highlight json %}
{% endhighlight %}
