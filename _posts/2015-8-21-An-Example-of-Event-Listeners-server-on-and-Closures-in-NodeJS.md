---
layout: post
title: An Example of Event Listeners, server.on, and Closures in NodeJS
---
I just watched [a nice Tuts+ tutorial](https://www.youtube.com/watch?v=CoyIBRD6p5U) about `server.on`. It's an eventlistener, in that when the server gets a certain event (specified by the first argument), it calls a callback function (specified by the second argument).

If you are listening for a `request` event, be sure to include `res.end();` at the conclusion of your callback function to keep the client from hanging on, endlessly waiting for a request.

.on is a method that the http object inherits from the EventEmitter class.

Here's the sample server I made in this tutorial

```
var http = require('http');

var server = http.createServer();

server.on('request', function(req, res){
  console.log('got a request');
  res.end();
})
server.listen(8000);
```

I can use the node documentation to see what events are emitted for different objects. See the bullets that start with "Event:" on this page, for example: <a href="https://nodejs.org/api/http.html" target="_blank">https://nodejs.org/api/http.html</a>
<h2>Closures</h2>
To include a closure, pass in your function as an argument but wrap it in parentheses. That way it'll call the first function and close over, then call the code again and run the internal function you included in the code.

Example:

```
var events = require('events');
var em = new events.EventEmitter();

// sets up the event listener</em>
em.on('timedEvent', function(interval){
  console.log('Interval: ' + interval);
});

/ /sets up the event emitter
setInterval(function(){
  var i = 0;
  return function(){   <em>//first function layer frozen</em>
    i++;
    em.emit('timedEvent', i);
    }
  })(), 10000)    //note the () calls the first arg

```

I assume the function `setInterval` already exists natively in the environment and just takes a function then an interval as arguments and calls the function every interval. A quick Google-search confirmed my hunch.

So why use a closure here instead of a normal function? I think it's to freeze our i variable into existence in a new, safe namespace.