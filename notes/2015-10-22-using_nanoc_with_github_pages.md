title: Using nanoc with github pages
date: 2015-10-22
tags: nanoc, nanoc3, github, git, ruby, static site, static site generator, devops, hosting

> This guide is based on the originally posted article at [Schmurfy's blog](http://schmurfy.github.io/2011/05/06/create_your_github_user_page_with_nanoc.html) - I've modified it for current github pages flow.

Let's get it started.

First, clone Your nanoc page repository to local disk and enter it:

<pre><code class="no-highlight">git clone yourRepoCloneUrl
cd yourRepoFolder
</code></pre>

Now, if You don't have `output` folder yet create it, then clone Your repo again into that directory:

<pre><code class="no-highlight">mkdir output
git clone yourRepoCloneUrl output
</code></pre>

Let's enter this folder and create isolated (orphan) branch, `gh-pages`:

<pre><code class="no-highlight">cd output
git checkout --orphan gh-pages
</code></pre>

Next we have to clean all the contents from our `output` folder's git track:

<pre><code class="no-highlight">git rm -rf .
</code></pre>

Now re-check if You are on `gh-pages` branch - there's possibility that You're now on detached state - if so then type:

<pre><code class="no-highlight">git checkout gh-pages
</code></pre>

To avoid problems in the future, remove the master branch from the `output` folder:

<pre><code class="no-highlight">git branch -d master
</code></pre>

Everything should be set here, so now enter the main project folder and try to compile it:

<pre><code class="no-highlight">cd ..
nanoc aco
</code></pre>

And that's it! Everything that is outside the `output` folder belongs to Your master branch (so You should push every change You want to keep.

If You want to publicize Your nanoc page, compile the project, enter the output folder (you should be switched automatically to `gh-pages` branch) then commit and push Your changes to Your `gh-pages` repo branch.

And that's it! If You ever need any help with nanoc and `gh-pages` - let me know on [twitter](http://twitter.com/mrmnmly).

-- mrmnmly
