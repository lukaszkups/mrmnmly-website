title: Sending emails with Meteor.js
date: 2015-01-12
tags: JavaScript, Meteor.js, Node.js, programming, backend, mailing, e-mail, webdev, web development, fullstack

## This is my personal wrap-up explanation of the code available in official [Meteor.js documentation](http://docs.meteor.com/).

Today I had to implement contact form for one of my Meteor.js project. At first I've jumped to official Meteor.js documentation and analyse email mechanics.

At the beginning, we have to install `email` package (via terminal):

<pre><code class="no-highlight">meteor add email</code></pre>

Next, we need to declare our email settings - to do that, let's create a `server/smtp.js` file:

<pre><code class="no-highlight">// smtp.js file contents
Meteor.startup(function(){
  process.env.MAIL_URL = &#39;smtp://email_username:email_password@email_host:email_port/&#39;;
});
</code></pre>

Example for gmail:

<pre><code class="no-highlight">Meteor.startup(function(){
  process.env.MAIL_URL = &#39;smtp://boo.foo:superDooperPassword@smtp.gmail.com:587/&#39;;
});
</code></pre>

We can also use custom domain email account:

<pre><code class="no-highlight">Meteor.startup(function(){
  process.env.MAIL_URL = &#39;smtp://boo.foo@awesomedomain.com:superDooperPassword@smtp.gmail.com:587/&#39;;
});
</code></pre>

After everything is set, let's register actual sending method, available for client (but declared on server so place code below somewhere under `server/` folder):

<pre><code class="no-highlight">// In your server code: define a method that the client can call
Meteor.methods({
  sendEmail: function (to, from, subject, text) {
    check([to, from, subject, text], [String]);

    // Let other method calls from the same client start running,
    // without waiting for the email sending to complete.
    this.unblock();

    //actual email sending method
    Email.send({
      to: to,
      from: from,
      subject: subject,
      text: text
    });
  }
});
</code></pre>

Those function arguments are of course optional - we can also add cc, bcc, Reply-To, html or headers.

My example for contact form:

<pre><code class="no-highlight">Meteor.methods({
  sendEmail: function (text) {
    check([text], [String]);

    this.unblock();

    Email.send({
      to: &#39;support@myClientProject.com&#39;,
      from: &#39;contact@myClientProject.com&#39;,
      subject: &#39;New message from contact form&#39;,
      text: text
    });
  }
});
</code></pre>

After we declared our server method, let's create actual sending event:

<pre><code class="no-highlight">Template.contactFormTemplate.events({
  &#39;submit form#contactForm&#39;:function(e){
    var contactForm = $(e.currentTarget),
      fname = contactForm.find(&#39;#firstName&#39;).val(),
      lname = contactForm.find(&#39;#lastName&#39;).val(),
      email = contactForm.find(&#39;#email&#39;).val(),
      phone = contactForm.find(&#39;#phone&#39;).val(),
      message = contactForm.find(&quot;#message&quot;).val();

    //isFilled and isEmail are my helper methods, which checks if variable exists or is email address valid
    if(isFilled(fname) &amp;&amp; isFilled(lname) &amp;&amp; isFilled(email) &amp;&amp; isFilled(phone) &amp;&amp; isFilled(message) &amp;&amp; isEmail(email)){
      var dataText = &quot;Message from: &quot; + fname + &quot; &quot; + lname + &quot;\rEmail: &quot; + email + &quot;\rPhone: &quot; + phone + &quot;\rContent:&quot; + message;

      Meteor.call(&#39;sendEmail&#39;, dataText);
      //throwAlert is my helper method which creates popup with message
      throwAlert(&#39;Email send.&#39;, &#39;success&#39;);
    }else{
      throwAlert(&#39;An error occurred. Sorry&#39;, &#39;error&#39;);
      return false;
    }
  }
});
</code></pre>

Besides of code above, You need of course some html template code:

<pre><code class="no-highlight">&lt;template name=&quot;contactFormTemplate&quot;&gt;
  &lt;form id=&quot;contactForm&quot;&gt;
    &lt;input type=&quot;text&quot; name=&quot;firstName&quot; id=&quot;firstName&quot; placeholder=&quot;First name&quot;&gt;
    &lt;input type=&quot;text&quot; name=&quot;lastName&quot; id=&quot;lastName&quot; placeholder=&quot;last name&quot;&gt;
    &lt;input type=&quot;text&quot; name=&quot;phone&quot; id=&quot;phone&quot; placeholder=&quot;Phone number&quot;&gt;
    &lt;input type=&quot;email&quot; name=&quot;email&quot; id=&quot;email&quot; placeholder=&quot;Your email address&quot;&gt;
    &lt;textarea id=&quot;message&quot;&gt;&lt;/textarea&gt;
    &lt;input type=&quot;submit&quot; value=&quot;Send&quot;&gt;
  &lt;/form&gt;
&lt;/template&gt;
</code></pre>

And that's all - it was THAT easy. You can now add `{{> contactFormTemplate}}` tag to any template You want and enjoy Your awesome contact form.

-- mrmnmly


