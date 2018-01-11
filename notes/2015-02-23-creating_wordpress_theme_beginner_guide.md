title: Creating Wordpress theme beginner guide
date: 2015-02-23
tags: Wordpress, php, webdev, programming, web development, fullstack, cms

> Disclaimer - I'm not a php programmer, I don't like php actually, but I'm getting pretty convinced that not everything made with php can be bad.

Couple days ago I had to prepare & code a Wordpress template for a client. I was mostly avoiding such tasks, because of its php-relation (I don't really like php for its syntax or its outdated standards & assumptions). I've managed to finish this task thanks to Wordpress (codex) documentation & some basic stackoveflow questions about php language.

And here's some basic tips, which helped me a lot during development:

## Starter kit

There is couple raw wordpress templates that gets rid of css stylesheets or unnecessary template customizations. My personal favorite is [BlankSlate](https://wordpress.org/themes/blankslate/) theme. It is a really nice, simple template that has all standard blog page features.

## Base template elements (files)

Your wordpress theme should have at least those template files:

- **home.php** - it is your home page when You don't set particular static page in wordpress settings. If this file will be missing, then wordpress will look after index.php file.
- **search.php** - this template should render search results list.
- **404.php** - page for Page not found error.
- **archive.php** - template for page archive view.
- **footer.php** - part of the template that will contain page footer.
- **header.php** - part of the template that will contain all contents that should be placed in page header.
- **functions.php** - file with special features and functions for current theme.
- **page.php**- template for every page on the website.
- **sidebar.php** - it will contain template sidebar contents.
- **single.php** - template file that shows how to display single entry/blog post on the page.
- **stylesheet.css** - file with css style for website.
- **page-slugOfThePage.php** - file with custom template for specific page (name of the page must be the same as in file name).
- **category-slugOfTheCategory.php** - custom template for specific category.

If we want to create some really custom view, we need to add to our theme folder a file named with convention: `page-nameOfThePage.php` and then add `nameOfThePage` as a page object in its Wordpress admin section - Wordpress engine will link them with each other.

## Code samples for basic page features

Here's some code examples for features that are required in almost every wordpress project:

- When You want to display the post content (with text styling) use the code below:

<pre><code class="no-highlight">&lt;?php
    $var1 = new WP_Query();
    $var1 = get_posts(array(&#39;name&#39;=&gt;&#39;yourPostSlug&#39;));
    if($var1){
        echo apply_filters(&#39;the_content&#39;, $var1[0]-&gt;post_content);
    }
?&gt;
</code></pre>

- If You want to insert direct link to the image:

<pre><code class="no-highlight">&lt;?php
    $var2 = new WP_Query();
    $var2 = get_posts(array(&#39;name&#39;=&gt;&#39;yourPostSlug&#39;));
    if($var2){
        $img = wp_get_attachment_image_src(get_post_thumbnail_id($var2[0]-&gt;ID, &#39;single-post-thumbnail&#39;);
        wp_reset_postdata();
    }
?&gt;
&lt;img src=&quot;&lt;?php echp $img[0]; ?&gt;&quot; alt=&quot;&quot;/&gt;
</code></pre>

- If You want to list all posts from specific category:

<pre><code class="no-highlight">&lt;ul&gt;
    &lt;?php
        query_posts(&#39;cat=yourCategoryId&#39;);
        while(have_posts()): the_post();
    ?&gt;
        &lt;li&gt;&lt;a href=&quot;&lt;?php the_permalink(); ?&gt;&quot;&gt;&lt;?php the_title(); ?&gt;&lt;/li&gt;
    &lt;?php
        endwhile;
    ?&gt;
&lt;/ul&gt;
</code></pre>

## Resetting Wordpress loop

Sometimes, when You want to implement a little more complicated generic view, You'll need to use multiple loops on the single view. To use every loop without problems we need to reset the previous one, and we have several ways to do it:

- `wp_reset_query();` - resets wordpress query after every custom wp query.
- `wp_reset_postdata();` - resets post variable after every custom wp query.
- `rewind_posts();` - rewinds whole custom query to the beginning so we can loop through it once again.

And that's all folks - if You have some other tips for Wordpress beginners please [tweet](http://twitter.com/mrmnmly) about them to me.

-- mrmnmly
