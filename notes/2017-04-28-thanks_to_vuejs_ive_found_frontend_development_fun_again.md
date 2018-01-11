title: Thanks to Vue.js I’ve found front-end development fun again
date: 2017-04-28
tags: Vue.js, JavaScript, programming, webdev, front-end, web development, front-end development

> Vue.js is a progressive, incrementally-adoptable JavaScript framework for building UI on the web.

Couple days ago I’ve decided to check Vue.js out. And it ended with a deep dive. After couple hours with documentation, I totally fell in love with this framework.

The last time I’ve been feeling so much fun during coding sessions was when I was learning Meteor.js. It feels refreshing, it brings fun, it makes development fun again.

But why? To be honest, I don’t know -  the whole architecture of this tool suits me very well - and that’s maybe because I’ve found it very similar to my own idea when I was trying to develop my very own JavaScript framework :)

## Single File Components

![sfc.gif](/public/1514935708675-sfc.gif)

When I first saw this simple idea, I was just amazed why I haven’t seen earlier such clean and simple approach of developing web apps.

So, what’s so great about it? Just take a look at an example below:

<pre><code class="no-highlight">&lt;template&gt;
  &lt;div&gt;
    &lt;h1&gt;{{ title }}&lt;/h1&gt;
    &lt;h3&gt;{{ subtitle }}&lt;/h3&gt;
    &lt;p&gt;Current state of the counter is: {{ counter }}&lt;/p&gt;
    &lt;button @click=&quot;increaseCounter&quot;&gt;Increase Counter!&lt;/button&gt;
  &lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  export default {
    data: function(){
      title: &quot;Hello Everybody&quot;,
      subtitle: &quot;Just an example&quot;,
      counter: 0
    },
    methods: {
      increaseCounter() {
        this.counter++;
        console.log(&#39;Counter increased!&#39;);
      }
    }
  }
&lt;/script&gt;
&lt;style scoped&gt;
  h1 {
    color: red;
    text-decoration: underline;
  }
  h3 {
    font-weight: 900;
  }
&lt;/style&gt;
</code></pre>

With couple lines of code we have a working Vue.js component, ready to re-use in various places of our code.

I love the idea of defining the component’s structure in one file, but divided by 3 sections:

- HTML template, with some extra Vue.js directives and custom props (AngularJS inspired? ). I’m really happy that this is a default — I really can’t stand JSX’s syntax (but You can use it anyway with Vue.js),
- JavaScript code, which handles all the component’s behavior and data (logic),
- Style block, which can be scoped or not.

I suppose that other frameworks out there also supports this approach, but IMHO they’re not popularized it so much as Vue. Okay, You can say that React.js has its render method, but I really don’t like jsx syntax  -  I want good old HTML. And okay no. 2  -  You can use good old HTML instead of jsx, but it is not recommended way of developing React apps.

## Flexibility

You can use Vue.js with Your favorite jQuery libraries and ES5 syntax (just include Vue.js source file in the document  -  no bundlers needed!). You can also use ES6, with importing / exporting modules and other new JavaScript features as well. Even server-side rendering is not a problem.

You can build just a simple widget for Your website, or spread functionality into multiple Single File Components, or use vue-router and vuex to create rich Single Page Application! There are also rumors that Vue’s alternative to React Native is almost ready — feel free to check out a [WEEX project](https://github.com/alibaba/weex).

## Sugar Syntax

For the long time I was thinking why exactly Angular 1, 2, React or Ember doesn’t suit me at all. Was it a problem of level of additional abstraction? Amount of creating unnecessary boilerplate code?

No.

The way how Vue.js solves creating Single Page Applications (or Web Interfaces) with such intuitive syntax is just a pure magic for me. Everything seems be polished to serve best experience for developer working with it. I’ll repeat myself again, but the last time I’ve felt something like this was when I was learning Meteor.js — so much stuff has been done under the hood, but this magic is fully understandable — You know why it works like this or why Vue.js core devs has solved this like that.

Maybe calling it *very suitable naming conventions and architecture* is a very good summary of what I really wanted to explain here ;)

## Learning curve

What can I say here? Learning Vue.js is like learning jQuery — it’s THAT simple, yet powerful.

## Ending words

The purpose of this article is not to convince anyone to use Vue.js right now. Watching on the current market interest in Europe, there is a lot work to do to promote Vue. As far as I know, the main Vue valley is in the Eastern globe (Asia) - I hope that trend / hype on Vue.js will come as fast as possible here.

-- mrmnmly