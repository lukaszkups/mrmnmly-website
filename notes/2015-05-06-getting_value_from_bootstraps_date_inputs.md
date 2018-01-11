title: Getting value from bootstrap's date inputs
date: 2015-05-06
tags: jQuery, JavaScript, bootstrap, HTML5, programming, webdev, web development, front-end, front-end development, js

Today my friend asked me how to get the value (date) from bootstrap's date input. My first thought was like:

<pre><code class="no-highlight">var myDate = $(&#39;input&#39;).val();
</code></pre>

But instead of value I've got `""` (an empty string). I've inspected the input element in DOM and it was actually right behavior - that input had no value.

Luckily, after quick search I've found the solution:

<pre><code class="no-highlight">var myDate = $(&#39;input&#39;).data(&#39;date&#39;);
</code></pre>

And that's it - enjoy!

-- mrmnmly