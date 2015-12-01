---
layout: post
title: Bratton Camera - Twitter Streaming and File Upload on Heroku
category: Physical Computing
---

<p>In order to ensure the longevity of the project, I wanted most of the computing ( ie: the tweeting, and the scraping ) to occur on a remote server.  By doing this I ensure that photo's will continue to be tweeted even if the camera looses power or is confiscated. The code I am running on my Heroku server does a few things: </p>
<ul>
    <li>Scrapes Twitter in real-time for tweets at my username</li>
    <li>It send the most recent photo in my uploads directory to the original tweeter</li>
    <li>It accepts remote file uploads from my Raspberry Pi</li>
</ul>
<br>
<p>Currently I am tracking tweets at my user name so that I don't reveal the bot until it is ready to go live.</p>

{% highlight javascript %}

var request         =       require('request');
var express         =       require("express");
var multer          =       require('multer');
var app             =       express();
var upload          =       multer({ dest: './uploads/'});
var port = process.env.PORT || 8080;
var Tweeter         =       require('twitter');
var Stream          =       require('node-tweet-stream')
var Keys            =       require('./keys.js')();
var fs              =       require('fs');
{% endhighlight %}

<p> These are my dependencies.  Using Express is a bit of overkill, but I did it because it rules also I realize now that some of this can be refactored as it relates to older versions of the same code. Multer is an awesome library that assists with file uploads. The other variable to pay attention to here is 'Keys'.  I set up a new file that is not tracked by git to add my twitter api keys so that when I push this to github my private information will not be public.</p>

{% highlight javascript %}

var client = new Tweeter({
  consumer_key: Keys.consumer_key,
  consumer_secret: Keys.consumer_secret,
  access_token_key: Keys.access_token_key,
  access_token_secret: Keys.access_token_secret
});

var stream = new Stream({
    consumer_key: Keys.consumer_key,
    consumer_secret: Keys.consumer_secret,
    token: Keys.access_token_key,
    token_secret: Keys.access_token_secret
})
{% endhighlight %}
<p>Here I set up my keys using the Keys requirement above.</p>

{% highlight javascript %}

app.use(express.static('uploads'));
app.use(multer({ dest: './uploads/',
    // I'm keeping this in case I want to rename the file
    rename: function (fieldname, filename) {
        return filename;
    },
    onFileUploadStart: function (file) {
        console.log(file.originalname + ' is starting ...');
    },
    onFileUploadComplete: function (file) {
        console.log(file.fieldname + ' uploaded to  /' + file.name)

    }
}));

{% endhighlight %}

<p>The above code sets up multer. The most important part of this code is the express.static('uploads') bit.  Here I declare the uploads folder as the place to serve static assets.  This way I will be able to see my uploaded photos without explicitly declaring routes. Likely there is a better way to do this.  I also declare the uploads directory to be where uploads are stored.</p>

{% highlight javascript %}
app.post('/api/photo',function(req,res){
    console.log('got photo');
    // upload file
    upload(req,res,function(err) {
        if(err) {
            return res.end("Error uploading file.");
        }
        // this redirect is for testing
        res.redirect('/'+res.req.files.file.name)
    });
});
{% endhighlight %}
<p>This code sets up a post route for the requests from my pi.</p>

{% highlight javascript %}
app.listen(port, function() {
    console.log('Our app is running on http://localhost:' + port);
    // When the stream gets a tweet grab the most recent photo and tweet it back at the user
    stream.on('tweet', function (tweet) {
      console.log('tweet received', tweet)
      var data = require('fs').readFileSync('./uploads/photo.jpg');
      // Make post request on media endpoint. Pass file data as media parameter
      client.post('media/upload', {media: data}, function(error, media, response){
        console.log(error);
        if (!error) {
          var status = {
            status: "Check out this photo @"+tweet.user.screen_name,
            media_ids: media.media_id_string // Pass the media id string
          }
          client.post('statuses/update', status, function(error, tweet, response){
            if (!error) {
              console.log(tweet);
            }
          });
        }
      });
    })
    stream.on('error', function (err) {
      console.log('Oh no')
    })
    // track terms
    console.log('running');
    stream.track('brttncm');
    stream.track('@dmehro');
});
{% endhighlight %}
<p>The above code is the meat of the program.  It sets up the listener on the stream and tweets the photo in my uploads directory at users who tweet at me.</p>