title: Delegated vs direct jQuery event binding
date: 2015-01-08
tags: jQuery, JavaScript, programming, front-end, webdev, web development

## Delegated vs direct jQuery event binding

Today I would like to show the difference between two event binding methods (as a example I will take .on() method):

- direct:

<pre><code class="no-highlight">$(&#39;div span&#39;).on(&#39;click&#39;, function(){
  console.log(&#39;clicked!&#39;);
});
</code></pre>

- and delegated one:

<pre><code class="no-highlight">$(&#39;div&#39;).on(&#39;click&#39;, &#39;span&#39;, function(){
  console.log(&#39;clicked!&#39;);
});
</code></pre>

The difference in code is very subtle, but in functionality (spoiler alert) delegated version of the code is far more flexible and universal.

## Delgated vs direct === Dynamic vs static

Direct version of jQuery `.on()` method allows You to bind the event to actually added elements in the document.

On the other side, dynamic version of jQuery `.on()` method allows You to bind events to all elements that will match the query - also those added dynamically (e.g. added by other jQuery methods).

So, if we have a HTML like this:

<pre><code class="no-highlight">&lt;ul id=&quot;exampleList&quot;&gt;
  &lt;li&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

..and we'll bind the events to `<li>` elements:

<pre><code class="no-highlight">//first solution:
$(&#39;ul#exampleList li&#39;).on(&#39;click&#39;, function(){
  console.log(&#39;clicked!&#39;);
});

//second solution:
$(&#39;ul#exampleList&#39;).on(&#39;click&#39;, &#39;li&#39;, function(){
  console.log(&#39;clicked!&#39;);
});
</code></pre>

And then we're add dynamically couple new `<li>` elements:

<pre><code class="no-highlight">for(var i=0; i&lt;3; i++){
  $(&#39;ul#exampleList&#39;).append(&#39;&lt;li&gt;&lt;/li&gt;&#39;);
}
</code></pre>

..we will have something like this:

<pre><code class="no-highlight">&lt;ul id=&quot;exampleList&quot;&gt;
  &lt;li&gt;&lt;/li&gt;
  &lt;li&gt;&lt;/li&gt;
  &lt;li&gt;&lt;/li&gt;
  &lt;li&gt;&lt;/li&gt;
&lt;/ul&gt;
</code></pre>

Using first solution of event binding, the click event will work only for first `<li>` element - the one that existed before code execution.

The second solution provides event binding support for elements, which exists during event binding code execution and those which will be dynamically added later.

So, if You want to work with dynamically loaded elements, use the second (*Delegated*) solution of event binding.

-- mrmnmly
