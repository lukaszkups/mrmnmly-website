title: Things to do after installing Elementary OS
date: 2015-05-24
tags: Elementary OS, eOS, linux, ubuntu, system, operating system, installation

> Couple days ago I was upgrading my system (from Elementary OS beta to stable version). Unfortunately it is related with system reinstallation.

For those who do not know this linux distribution I'll refer to check [this link](https://elementary.io/). In short, it is the most polished and beautiful linux distro ever made.

Some people accuse that elementary developers are copying apple's OSX design guidelines. Personally, as a past OSX user I think it is not definitely copying, but inspiration is visible.

## Step I: first thing first

If You haven't checked it during installation, update all the system packages to newest version:

<pre><code class="no-highlight">sudo apt-get update
sudo apt-get upgrade
</code></pre>

Next, let's install all necessary development tools:

<pre><code class="no-highlight">// add required package repositories
sudo apt-add-repository ppa:ubuntu-mozilla-daily/ppa
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-add-repository ppa:cordova-ubuntu/ppa
sudo apt-get update
sudo apt-get install firefox
sudo apt-get install sublime-text-installer
// installing ruby &amp; rails
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
curl -L https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.2.2
rvm use 2.2.2 --default
echo &quot;gem: --no-ri --no-rdoc&quot; &gt; ~/.gemrc
sudo apt-get install rubygems-update
gem install nanoc
gem install kramdown
gem install haml
gem install bundler
gem install rails -v 4.2.1
// installing meteorjs
sudo apt-get install npm
curl https://install.meteor.com/ | sh
sudo apt-get install cordova-cli
// installing python &amp; django
sudo apt-get install sqlite
sudo apt-get install python-pip
sudo apt-get install python-setuptools
sudo apt-get install python3-setuptools
sudo apt-get install python-django
// preparing stuff for my custom .vimrc settings
touch ~/.vimrc
mkdir ~/.vim/swap
mkdir ~/.vim/swap/tmp
mkdir ~/.vim/backups
mkdir ~/.vim/backups/tmp
export LC_ALL=en_CA.UTF-8
export LANG=en_CA.UTF-8
// git setup
git config --global user.email &quot;&lt;youremail&gt;&quot;
git config --global user.name &quot;&lt;yourusername&gt;&quot;
</code></pre>

And that should be enough for starting point.

## Step II: D-d-d-d-d-drop the base!

This is my worst nightmare every time I reinstall the OS - installing Postgres datatabse.

I've decided to give it separate paragraph because it's a bit longer than couple lines of simple terminal commands (in fact it is, but I want to store this information somewhere, to prevent from googling it every freaking time).

First, install postgres packages:

<pre><code class="no-highlight">sudo apt-get install postgresql postgresql-contrib
</code></pre>

Next, create database cluster:

<pre><code class="no-highlight">sudo pg_createcluster 9.3 main --start
</code></pre>

Now, lets create new user for our system database:

<pre><code class="no-highlight">createuser --interactive
</code></pre>

You will be asked couple yes/no questions - easy peasy. After that, we need to set a password for our new user:

<pre><code class="no-highlight">sudo -i -u postgres
alter user &lt;username&gt; with password &quot;&lt;your password&gt;&quot;;
</code></pre>

Now we can create new database, and set its access settings:

<pre><code class="no-highlight">\q
createdb &lt;dbname&gt;
psql
grant all privileges on database &lt;dbname&gt; to &lt;username&gt;;
</code></pre>

(heavy breathing) and that's it.

## Step III: personalization

If You want to Elementary even more beautiful, try custom icons and themes, for example:

<pre><code class="no-highlight">sudo apt-add-repository ppa:mpstark/elementary-tweaks-daily
sudo apt-get install elementary-tweaks
sudo add-apt-repository ppa:numix/ppa
sudo apt-get install numix-icon-theme-circle
</code></pre>

Now You can access a new submenu in Your system settings app called tweaks, where You can customize Your system design (`numix-circle` icons are my favorite!).

In addition, You can also take a look at keyboard submenu and bind key shortcuts that suits You best (it's worth to mention, that Elementary OS default ones are pretty intuitive).

And that's all folks! This setup should be a fine starter for development. If You have any improvements/suggestions, feel free to [tweet to me](http://twitter.com/mrmnmly) about it.

-- mrmnmly
