title: Handling notifications after email sending.
date: 2015-01-29
tags: Meteor.js, Node.js, JavaScript, programming, webdev, web development, fullstack

## Tangling email sending & notifications together

Today I wanted to implement contact form with validation and (alert) notification system. However, I encountered a problem with session variables.

My idea was to set Session variable which stores information about unseen alert notification and get that value after rendered template callback:

Template event:

<pre><code class="no-highlight">Template.myContactTemplate.template{(
  &#39;click .submitButton&#39;: function(e){
    var dataText = $(e.currentTarget).find(&#39;.dataText&#39;).val();	
    Session.set(&#39;alertMessage&#39;, [&#39;Email has been sent&#39;, &#39;success&#39;]);
    Meteor.call(&#39;sendEmail&#39;, dataText);
  }
)};
</code></pre>

My e-mail sending method:

<pre><code class="no-highlight">Meteor.methods({
  sendEmail: function(text){
    check([text], [String]);
    this.unblock();
    Email.send({
      to: &#39;xyz@xyz.com&#39;,
      from: &#39;contactForm@xyz.com&#39;,
      subject: &#39;New message from contact form&#39;,
      text: text
    });
  }
});
</code></pre>

Rendered callback:

```
Template.contactFormTemplate.rendered = function(){
  Meteor.defer(function(){
    var a = Session.get('alertMessage');
    if(a){
      throwAlert(a[0], a[1]);	//my custom method for alerts
      Session.set('alertMessage', null);		
    }
  });
}
```

The code above will not work. I have noticed that email sending method somehow flush/resets our `alertMessage` session variable. To prevent from such behaviour and keep all variables saved let's add [persistent-session](https://github.com/okgrow/meteor-persistent-session) package:

```
meteor add u2622:persistent-session
```

And that's it. Now our session variables are stored in the browser's localstorage (so we prevent from unwanted variable flushes).

You can discuss about this problem at [this stackoverflow thread](https://stackoverflow.com/questions/28084160/session-variable-unset-after-sending-email).

-- mrmnmly
















