---
layout: post
title: A quick webapp project template
---

<p class="meta">{{ page.date | date: "%-d %b %Y" }}</p>
{{ page.title }}
================

Let's create a minimal working webapp project template,
using [Bootstrap](http://getbootstrap.com/),
[React](http://facebook.github.io/react/),
[React Router](http://rackt.github.io/react-router/),
[NPM](https://www.npmjs.com/),
and [Webpack](http://webpack.github.io/).

The directory layout looks like this:

```
js/
    about.jsx
    app.jsx
    home.jsx
index.html
package.json
webpack.config.json
```

All the code is pretty much self explanatory, but let's briefly describe each file separately.

```js/about.jsx``` and ```js/home.jsx``` are two React (Router) pages.
In this trivial example, each of them renders a heading:

{% highlight javascript %}
import React from "react/addons";
import Router from "react-router";

export default React.createClass({
    mixins: [Router.State],

    render: function() {
        return (<h1>About</h1>);
    }
});
{% endhighlight %}


```js/app.jx``` is the entry point of the application.
It renders the website structure and configures the routes.
The active page will be rendered in the place of the ```<RouteHandler/>``` component.

{% highlight javascript %}
import React from 'react/addons';
import Router from 'react-router';
import {Route, Redirect, RouteHandler, Link} from 'react-router';

import Home  from './home.jsx'
import About from './about.jsx'

var pages = [
  { id: "home",  path: "/home",  title: "Home",  handler: Home  },
  { id: "about", path: "/about", title: "About", handler: About }
];

// hold the current active path
// used to identify which bootstrap's navbar <li> element
// should be declared with the "active" class
var activePath;

var App = React.createClass({
  render: function() {
    return (
      <div>
        <nav className="navbar navbar-default navbar-fixed-top">
          <div className="container">
            <div className="navbar-header">
              <button type="button" className="navbar-toggle collapsed"
                data-toggle="collapse"
                data-target="#navbar"
                aria-expanded="false" aria-controls="navbar">
                <span className="sr-only">Toggle navigation</span>
                <span className="glyphicon glyphicon-menu-hamburger"></span>
              </button>
              <a className="navbar-brand" href="/">App</a>
            </div>
            <div id="navbar" className="collapse navbar-collapse">
              <ul className="nav navbar-nav">
                {pages.map(function(page, i) {
                  var className = (activePath === page.path) ? "active" : "";
                  return (
                    <li key={i} className={className}>
                      <Link to={page.path}>{page.title}</Link>
                    </li>
                  );
                })}
              </ul>
            </div>
          </div>
        </nav>
        <div className="container">
          <div style={{marginTop: "70px"}} >
            <RouteHandler/>
          </div>
        </div>
      </div>
    )
  }
});

var routes = (
  <Route handler={App}>
    {pages.map(function(page, i) {
      return (
          <Route key={i}
            name={page.id}
            path={page.path}
            handler={page.handler}/>
      );
    })};
    <Redirect from="/" to="home" />
  </Route>
);

Router.run(routes, Router.HashLocation, function(Handler, state) {
  activePath = state.path.split("?")[0];
  React.render(<Handler />, document.getElementById('app'));
});
{% endhighlight %}


The ```webpack.config.json``` configuration file tells webpack to build
```js/app.jsx``` and all its dependencies into a ```bundle.js``` file.
Webpack uses loaders to compile jsx, css, and scss files into ```bundle.js```.
Although in this minimal project template we haven't created any css (or scss) file,
it is a good idea to have the build system ready for them.

{% highlight javascript %}
var config = {
  entry: ['./js/app.jsx'],
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders: [{
      test: [/\.jsx?$/],
      loaders: ['babel']
    }, {
      test: [/\.css$/, /\.scss$/],
      loader: 'style!css!sass'
    }]
  }
};

module.exports = config;
{% endhighlight %}


In ```package.json``` we declare our production dependencies (React and React Router)
and our development dependencies (Webpack's loaders).

{% highlight json %}
{
  "name": "quick-webapp-template",
  "version": "0.0.1",
  "dependencies": {
    "react": "*",
    "react-router": "*"
  },
  "devDependencies": {
    "babel-loader": "*",
    "style-loader": "*",
    "css-loader": "*",
    "sass-loader": "*"
  }
}
{% endhighlight %}


Finally, the ```index.html``` page loads twitter bootstrap and our own ```bundle.js```.
Bootstrap depends on jquery, so we need to load it too.

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>App</title>
  <link href="/bootstrap.min.css" rel="stylesheet">
  <!--[if lt IE 9]>
  <script src="/html5shiv.min.js"></script>
  <script src="/respond.min.js"></script>
  <![endif]-->
</head>
<body>
  <div id="app"></div>
  <script src="/jquery.min.js"></script>
  <script src="/bootstrap.min.js"></script>
  <script src="/bundle.js"></script>
</body>
</html>
{% endhighlight %}

If you remember ```js/app.jsx```, you'll recognize that our app will be rendered inside the
```<div id="app">``` element.

Assuming you have NPM and Webpack installed in your system, you can run:

- ```npm install``` to install all the dependencies
- ```webpack``` to build ```bundle.js```
- ```webback -w``` to build ```bundle.js``` and keep building it each time a source file is changed
- ```webpack -p``` to build an optimized version of ```bundle.js```, which is appropriate to be used in production

To see the resulting website running, you should serve the project directory in a webserver.

A common way to do this is to run:

{% highlight bash %}
cd <project_dir>
python -m SimpleHTTPServer 3000
{% endhighlight %}
and then visit [http://localhost:3000/](http://localhost:3000/)


As an alternative, you can create your own static web server using Go, as explained
[here](http://dfreire.github.io/2015/06/24/using-echo-to-serve-a-static-files-folder.html).


You can find and use the source code for this template
[here](https://github.com/dfreire/quick-webapp-template).
