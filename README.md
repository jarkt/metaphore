metaphore
=========

PHP cache slam defense using (memcached) semaphore to prevent dogpile effect (aka clobbering updates or stampending herd).

Problem
-------

Too many requests hit your website at the same time to regenerate same content slamming your database.

More reading:

* https://code.google.com/p/memcached/wiki/NewProgrammingTricks#Avoiding_stampeding_herd
* http://www.php.net/manual/en/mysqlnd-qc.slam-defense.php
* https://www.varnish-cache.org/trac/wiki/VCLExampleGrace

Solution
--------

First request generates new content while all the subsequent requests get (stale) content from cache until new one is re-generated.

Similar solutions:

* [Varnish - Grace](https://www.varnish-cache.org/trac/wiki/VCLExampleGrace)
* [LSDCache](https://github.com/gsmlabs/LSDCache) - this lib is lightweight version of lsdcache (imho lsdcache grew too big into multi-purpose cache library while metaphore strives to be simple to do just one thing and to do it well)

Usage
-----

``` php
use Metaphore\Cache;

$cache = new Cache($memcached);
$cache->cache($key, function(){
    // generate content
}, $ttl);
```
