# Cloudfront CDN

* CDN (Content Delivery Network) is a network of distributed servers that deliver webpages and other web content to a user based on the geographic location of the user, the origin of the webpage and a content delivery server.
  * Can be used to deliver entire website - static and dynamic content, as well as streams.
  * Can be used with non AWS servers, but optimised for AWS origin servers.
  * Edge locations can handle PUT/POSTs as well as GETs. After PUT/POST received, will be synced to main server.
  * Objects are cached for the life of the TTL (Time to Live). Can clear cached objects early (Invalidation), but will be charged (although first 1,000 per month free).
* When user makes a GET request:
  * Get distribution URL (MIN)
  * Pings edge location, which sees if it has file cached. If not, it pings the main server which returns the file (so not any faster for first user, in fact be be a little slower).
  * Then download the file from edge location. No need to talk to main server for next request for file.
  TTL, distribution URL.
* Terminology:
  * Edge Location: the location where content is cached (not the same as an AWS Region/AZ).
  * Origin: where original files are stored. Can be an S3 bucket, EC2 instance, Elastic Load Balancer or Route53 - or a separate non-AWS server.
  * Distribution: the name given to a CDN which a user creates, consists of a collection of Edge Locations.
  * Web Distribution: used for websites.
  * RTMP (Real-Time Messaging Protocol) Distribution: used for Media Streaming, especially via Flash (but also some other services).

  ## Practical: setting up web distribution

* 'Restrict Bucket Access' means must use CloudFront to access, cannot ping bucket directly. Requires setting up a new Identity to use internally for this.
* TTL settings: minimum/maximum/default don't apply across the board - instead they depend on whether a Cache-Control header is specified on the object. Minimum/maximum will limit the object cache TTL; default will be used if one is not supplied. This is useful as different objects might have different TTLs e.g. static content might be longer.
* 'Restrict Viewer Access' - allows content to be restricted, for example to those who have paid for a service. Uses signed URLs or signed cookies.
* Can link up to WAF (Web Application Firewall).
* Can either use default SSL certificate (URL will be `https://d111111abcdef8.cloudfront.net/logo.jpg`, or a custom one bought through ACM.
 * IPv6 and HTTP/2 now supported.
 * Takes about half an hour to update a distribution.
 * Can add custom behaviours e.g. different caching for specific paths.
 * Can add custom error pages for 4xx or 5xx responses.
 * Can add Geo-Restrictions, either on a whitelist of blacklist basis (remember to have direct bucket access restricted).
 * Invalidations remove objects from caches - do this by specifying paths, including wildcards i.e. can invalidate whole folders.
* Can add tags to help organise distributions.

	d3ixobjcinzm9c.cloudfront.net