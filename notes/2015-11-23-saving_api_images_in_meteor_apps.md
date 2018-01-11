title: Saving API images in Meteor apps
date: 2015-11-23
tags: Meteor.js, Node.js, JavaScript, js, programming, webdev, web development, fullstack

## Today I would like to share the knowledge about saving image files from external APIs.

Consider this scenario: You have to develop an mobile app, that downloads some data and files from external API and saves those files locally to work offline if necessary.

## Packages

First, we need to install proper Meteor.js plugins which enables to interact with files ([more info](https://atmospherejs.com/cfs/standard-packages)):

<pre><code class="no-highlight">meteor add cfs:standard-packages
</code></pre>

This is the main set of packages, that will help us dealing with files - I'm very happy that someone did such great job and solved file management problems in really painful way.

Also, we have to install a storage adapter package - my favorite is [gridfs](https://atmospherejs.com/cfs/gridfs). If You're using newest Meteor version then You should have it merged into Meteor's core - on the other case You have to install it:

<pre><code class="no-highlight">meteor add cfs:gridfs
</code></pre>

## Collection

Okay, so we have all necessary tools, now we have to define our file / media collections:

<pre><code class="no-highlight">/* lib/models.js */
Media = new FS.Collection(&quot;media&quot;, {
  stores: [new FS.Store.GridFS(&quot;media&quot;)]
});
</code></pre>

Thanks to `/lib/` file path, our collection definition will be available both on the server and the client side of the app.

<pre><code class="no-highlight">## Cross-Origin Resource Sharing (CORS)
</code></pre>

In this step, we will make sure that we don't get a [CORS](https://www.w3.org/TR/cors/) error. To ensure this, we have to add adequate header to our request:

<pre><code class="no-highlight">/* server/private_helpers.js */
Meteor.startup(function(){
  WebApp.connectHandlers.use(function(req, res, next) {
    res.setHeader(&quot;Access-Control-Allow-Origin&quot;, &quot;*&quot;);
    return next();
  });
});
</code></pre>

## Getting file via API

Now it's time to get the file path via our API. You can do this in couple ways - e.g. via Meteor's [HTTP package](https://atmospherejs.com/meteor/http) (`meteor add http`) or classically - via ajax request.

Personally, I decided to go classy and used jQuery (❤promises):

<pre><code class="no-highlight">/* client/public_helpers.js  */

var imageArr = [];
var getApiFiles = function(){
  var dfd = new $.Deferred();
  $.ajax({
    url: PATH_TO_REMOTE_API,
    dataType: &#39;json&#39;
  }).done(function(data){
    imageArr = data;
    dfd.resolve(imageArr);
  }).error(function(error){
    console.log(&#39;getImage error&#39;);
  });
  return dfd.promise();
};
</code></pre>

Let's assume that the response (in our case imageArr) will look like this:

<pre><code class="no-highlight">[
  {
    id: 1,
    photo: &quot;/media/image1.jpg&quot;,
    default: false
  },
  {
    id: 2,
    photo: &quot;/media/image2.jpg&quot;,
    default: false
  },
    id: 3,
    photo: &quot;/media/image3.jpg&quot;,
    default: true
  }
]
</code></pre>

## File downloading Meteor method

To make everything work, we have to add server side file downloading method:

<pre><code class="no-highlight">/* server/private_helpers.js  */
Meteor.methods({
  saveFile: function(filePath){
    var file = new FS.File();
    file.attachData(filePath, function(err){
      if(err){
        throw err;
      }
      Media.insert(file, function(err, fileObj){
        return fileObj._id;
      });
    });
  }
});
</code></pre>

## Final function

In the last step, we have to execute our methods properly:

<pre><code class="no-highlight">/* client/helpers.js */
$.when(getApiFiles()).done(function(){
  for(var img in imageArr){
    var img_id = Meteor.call(&#39;saveFile&#39;, &quot;http://remote-domain.xyz&quot; + imageArr[img].photo);

    /* here You can process additional features, e.g. attaching img_id to another collection etc. */
  }
});
</code></pre>

And that's it! Now You can use Your saved files in Your Meteor.js application locally, even without internet connection.

I've read couple comments that FS package should not be used in production, but in my opinion it just do the job perfectly. Until Meteor Core Development Team provide an official solution to handle file management You can be sure that I'll be using these packages - and therefore You should ;)

If You have any questions or suggestions, feel free to [contact](/about/).

-- mrmnmly