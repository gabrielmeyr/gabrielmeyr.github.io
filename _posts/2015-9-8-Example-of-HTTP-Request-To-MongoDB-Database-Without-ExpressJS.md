---
layout: post
title: Example of HTTP Request to MongoDB Database Without ExpressJS
---
I'm currently building a project without any frameworks as a learning exercise, and trying to query a MongoDB database for blog posts. It can be a lot harder than you would expect.

Here was the problem. When my http requests got to mongodb, the browser logged a "no 'access-control-allow-origin' header" error. It's easy enough to add the proper CORS header if you control the response. But mongoDB was handling responses on its own, so I didn't know how to add that option.

After some investigation on Google, I decided that this sobering answer on [Stack Overflow](http://stackoverflow.com/questions/28522600/modifying-mongodb-to-allow-cross-origin-requests) from CodesInChaos was the proper answer to my dilemma:

>_Your work by concept is having issue._
  1. _Your post method is directly hitting to TCP Protocol here, which should not be._
  2. _You should call some http request based on some Rest API which is to be in Server._
  3. _At server routing, you should handle the CORS (http request) and then the db layer methods should get the data for Update/Select etc._

>_By the way, for Server Routing you can use high level node framework like [expressjs](http://expressjs.com/starter/basic-routing.html)._

>_If you want a complete example for this, you may go through want to look through <a href="https://github.com/piyasde/express4mongoangular" rel="nofollow">this example</a> and the explanation can be found in at <a href="http://www.phloxblog.in/single-page-application-angular-js-node-js-mongodb-mongojs-module-updated-express-4-part-1/" rel="nofollow">Single Page Application with Angular.js, Node.js and MongoDB - phloxblog</a>._

So I'm not even supposed to be making direct http requests at all. I'm avoiding Express and other frameworks for this project, so I had to try to set up some random REST API on my own.

I tried sleepy.mongoose, CREST, restheart, Dream Factory, and then eventually CouchDB. I tried (with varying degrees of success) to install dependencies like Java 8, Python 3.4, Python 2.7, Erlang, and more. I worked with .gz files,  set environment path variables, and googled error messages.

Eventually the heavens parted and I got my solution. My friend Paul recommended the mongojs library to me, which turned out to be the exactly what I needed for interfacing with MongoDB, he also explained the MVC design pattern to me.

This is the code that finally allowed me to query MongoDB from the client (brwoser side) and write the result to the page.

This is the HTML:

```
<div class="content"></div>
var req = new XMLHttpRequest(); req.open("GET", "science", false); req.send(null); console.log(req.responseText); $(document).ready(function(){ $('.content').html(req.responseText); })
```

And this is what went in the request handler file:

```
function science (response){
  console.log("Request handler 'science' was called.");

  var databaseUrl = "ip"; // "username:password@example.com/mydb"
  var collections = ["blogs"]
  var mongoapp = require('mongojs');
  var db = mongoapp(databaseUrl, collections);

  db.blogs.findOne( function(err, found) {
    if( err || !found) console.log("No science found");
    else {
  console.log(found);
  var result = JSON.stringify(found.title);
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end(result);
}});
}
```

_post edited on January 30, 2016_
