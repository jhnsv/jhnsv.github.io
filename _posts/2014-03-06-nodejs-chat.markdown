---
layout: post
title: "A dead crappy simple node.js chat with telnet"
date: 2014-03-06 20:37:00
categories: nodejs
published: true
---


#A dead crappy simple node.js chat with telnet

Stolen from http://www.youtube.com/watch?v=jo_B4LTHi3I

Prerequisite: node.js installed

Usage: 

1. create chat.js (with the code from down under)
2. type node chat.js in the terminal
3. open a new terminal-window
4. telnet 127.0.0.1 8000
5. chat away

Bonus: on a local company net? get your IP (ifconfig) and telnet into that, share it with your friends. 

{% highlight javascript %}
var net = require('net')

var sockets = [];

var server = net.createServer(function(socket) {
 
  sockets.push(socket); 
    
  socket.on('data', function(d) {
    for (var i = 0; i < sockets.length; i++) {
      if (sockets[i] == socket) continue;
      sockets[i].write(d);   
    }
   
  });
  
  socket.on('end', function(d) {
    var i = sockets.indexOf(socket);
    sockets.splice(i,1);
  });
  
});

server.listen(8000);
{% endhighlight %}