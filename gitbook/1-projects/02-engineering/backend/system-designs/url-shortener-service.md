
"Design a URL shortening service like bit.ly"

**Use cases**
1. Shortening : take a url -> return a much shorter url 
2. Redirection: take a short url -> redirect to the original url
3. Custom URL 
4. Highly available


**Out of scope**
1. Analytics
2. Automated link expiration
3. Manual Link removal 
4. UI vs API 


**Back of the envelope calculations**
Amount of traffic system should handle 
Amount of data system should deal with


New URLs : 100M 
1B requests per month
10% from shortening and 90% from redirection

 Requests per second  = 1BN/24h/3600s
			       = 400 requests per second. 
			       = (40 shortens + 360 redirects)


 Total URL (5 years ) = 5 yrs * 12 mths * 100M  =  6 billion URLs

Average length = 500 char = 500 bytes per URL
6 bytes per short url (per hash)  (A-Z, a-z, 0-9)

Storage :   for all URLs, 36GB for all hashes (over 5 years)

New data written per second = 40 * (500+6) bytes = 20K
Data read per second = 360 * (500 + 6) bytes = 180K
 

**Abstract Design:**

 1. Application Service Layer (serves the requests)
	 1. Shortening Service
	 2. Redirection Service
 2. Data Storage Layer (Keeps track of hash to URL mappings)
	 - Acts like a big hash table, stores mappings and  returns a value when presented with a key

hashed_url = convert_to_base62(hash(original url + random_salt)).take(6) 


Bottlenecks:

- Traffic is probably not going to be very hard
- data - more interesting


Scalable design:
1.  App service layer can start with 1 machine. 
	- Measure how far it takes us with load testing.
	- add a load balancer with a cluster of machines over time : Auto scaling with Amazon Elastic load balancer to deal with spike-y traffic, to increase availablity,
2. Data Storage layer
	- Billions of objects 
	- Each object is fairly small (<1KB)
	- There are no relationship between the objects
	- Reads are 9X more than the write operation (360 reads per second 40 writes per second)
	- 3TBs of URL, 36GB of hash



MySQL 
- Widely used
- Mature tech
- Clear scaling paradigms (Sharding, master-slave replication, master-master replication)
- Used by big players
- Index lookups are fast


mappings
1. hash: varchar(6)
2. original_url : varchar(512)

- Use one mysql table with two var_char fields
- Create a unique index on the hash (36GB) - keep it in memory to speed up look ups.
- Vertical scaling (mysql machine)
- Eventually, Partition the data : 5 partitions, 600 GB of data, 8 GB of index 
- Master-slave : reading from slave, writes to master
- 


1 machine is needed. 
but 2 will split 

---

How do short URLs services work? - Stack Overflow](https://stackoverflow.com/questions/1562367/how-do-short-urls-services-work)

No, they don't use files. When you click on a link like that, an HTTP request is send to their server with the full URL, like [http://bit.ly/duSk8wK](http://bit.ly/duSk8wK) (links to this question). They read the path part (here `duSk8wK`), which maps to their database. In the database, they find a description (sometimes), your name (sometimes) and the real URL. Then they issue a redirect, which is a HTTP 302 response and the target URL in the header.

This direct redirect is important. If you were to use files or first load HTML and then redirect, the browser would add TinyUrl to the history, which is not what you want. Also, the site that is redirected to will see the referrer (the site that you originally come from) as being the site the TinyUrl link is on (i.e., twitter.com, your own site, wherever the link is). This is just as important, so that site owners can see where people are coming from. This too, would not work if a page gets loaded that redirects.

PS: there are more types of redirect. HTTP 301 means: redirect permanent. If that would happen, the browser will not request the bit.ly or TinyUrl site anymore and those sites want to count the hits. That's why HTTP 302 is used, which is a temporary redirect. The browser will ask TinyUrl.com or bit.ly each time again, which makes it possible to count the hits for you (some tiny url services offer this).