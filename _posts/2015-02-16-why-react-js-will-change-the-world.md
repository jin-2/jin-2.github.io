---
layout: post-sidebar
date: 2015-02-10
title: "Why React JS Will Change the World"
categories: coding js
author_name : Dan Robberts
author_url : /author/dan
author_avatar: dan
show_avatar : true
read_time : 22
feature_image: feature-water
show_related_posts: true
square_related: recommend-spain
published: false
---

React components implement a `render()` method that takes input data and returns what to display. This example uses an XML-like syntax called JSX. Input data that is passed into the component can be accessed by `render()` via `this.props`.

{% highlight HTML %}
<!DOCTYPE html>
<html>
  <head>
    <script src="build/react.js"></script>
    <script src="build/JSXTransformer.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/jsx">
      React.render(
        <h1>Hello, world!</h1>,
        document.getElementById('example')
      );
    </script>
  </body>
</html>
{% endhighlight %}

## Want CommonJS?
If you want to use React with browserify, webpack, or another CommonJS-compatible module system, just use the react npm package. In addition, the jsx build tool can be integrated into most packaging systems (not just CommonJS) quite easily.

![Fire image]({{site.url}}/{{site.baseurl}}img/post-assets/fire.jpg)

## Next Steps
Check out the tutorial and the other examples in the starter kit's examples directory to learn more.

Jekyll also offers powerful support for code snippets:

{% highlight javascript %}
{
  "name": "my-project-name",
  "version": "0.1.0",
  "devDependencies": {
    "grunt": "~0.4.5",
    "grunt-contrib-jshint": "~0.10.0",
    "grunt-contrib-nodeunit": "~0.4.1",
    "grunt-contrib-uglify": "~0.5.0"
  }
}
{% endhighlight %}

We also have a wiki where the community contributes with workflows, UI-components, routing, data management etc.

Good luck, and welcome!
