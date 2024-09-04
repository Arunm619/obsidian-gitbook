
Nginx - web server that is going to serve web content (typically)


airbnb uses nginx server while meesho uses envoy.


Nginx is a reverse proxy.
it sits before the server to serve the static web content.

 ![[Screenshot 2024-05-05 at 8.27.50 PM.png]]

Nginx can also act as a LB (Load balancer)


Can also used for encryption (HTTP vs HTTPs)


---
Nginx.conf is a configuration file that helps define the server. 

It contains key value pairs called the directives. 

 Blocks are called contexts. Within context, there will be specific directives defining it.


---
Serving static content

put all the website into a folder and setup the config with server and events contexts. 

within server context, we need to fill two directives
- where to listen on - 8080 port
- which files to server - root directory


events block is mandatory.
```nginx.conf
http{
server {
listen 8080;
root /arun/mycoolwebsite;
}
}

events {}
```


**nginx -s reload**
will reload the new site on 8080

---

**Mime Types***

To apply styles in the site, even though its loading up in network tab, we need to configure content type. 
because the content type is always - text/plain



```nginx.conf
http{

types {
text/css css; //extensions
text/html  html; //extensions
}
server {
listen 8080;
root /arun/mycoolwebsite;
}
}

events {}
```

to add default mime types 

`include mime.types;`


Location context 

We have a new fruits index.html inside fruits folder inside the root. How to expose that?

```
location /fruits {
root /arun/mycoolwebsite;
}

```


How to re-use pages with new endpoints?

use alias!

```

location  /carbs {
alias /arun/mycoolwebsite/fruits;
}
```


root will append while alias will not append the location data. 

----

if pages have different names than standard index.html use try_files under location contexts
```
location  /vegetables {
root /arun/mycoolwebsite/vegetables;
try_files /vegatables/veggies.html /index.html =404; 
}
```

try_files is basically fallback mechanism

we can also use regex

```
location  ~* count/[0-9]  {
root /arun/mycoolwebsite;
try_files  /index.html =404; 
}
```


----
  Redirects and rewrites


Redirects 

```
locaiton /crops {
   return 307 /fruits;
}
```

but the problem is URL will change to /fruits as per redirection.


if we don't want that behaviour but are just interested in updating the contents, then the answer is rewrites. 

```
location /veggies { 
# Serve the same content as /fruits when visiting /veggies 
proxy_pass http://example.com/fruits; 
}
```

This is one way. the usual way. 

we can also mix regex. 

```
location /veggies { 
# Rewrite the URI to /fruits and pass it to the fruits location block rewrite ^/veggies(.*)$ /fruits$1 break; 
proxy_pass http://example.com; 

}
```


----

##### The Load balancer

Docker allows to create multiple servers. 

lets initialise npm to install express servers. 

```index.js

const express = require("express")
app.get("/", (req, res) =>  {
res.send("I am an endpoint")
})

app.listen(7777, () => {
  console.log("Listening on port 7777")
})
```

"node index" inside package.json with "start" will start the server.


Dockerfile for express app 


creating the express app as an image 
and then spinning up 4 instances of it in docker with 1111,2222,3333,4444 ports mapped to 7777.

how to round robin among these servers if I hit 8080 of Nginx


default is roundrobin!!!

```

upstream backendserver {
   server 127.0.0.1:1111
   server 127.0.0.1:2222
   server 127.0.0.1:3333
   server 127.0.0.1:4444
}
location / {
   proxy_pass http://backendserver/;
}
```


