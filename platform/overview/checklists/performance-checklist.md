---
description: Checklist for a better web application performance
---

# Performance Checklist

Performance is crucial in today's web applications. A slow app feels buggy to the users and makes them flee it. Although performance is such an important topic, there are so many optimization vectors that it's easy to forget some of them. The intent of this checklist is to gather performance practices to apply when developing a web application.

While we apply these practices, we should always keep the following rules in mind:

* Don't optimize too early
* Don't let performance ruin productivity
* Always check an optimization is efficient by measuring performance before and after it

## Objectives

* [x] &#x20;Define the **performance metrics and objectives**
  * The [RAIL model](https://developers.google.com/web/fundamentals/performance/rail) is generally a good model to start with.
  * If speed is an advantage we want to have against competitors, know that users usually will feel we are faster if we are at least 20% faster than them.
* [x] &#x20;Plan out a **loading sequence**; this way we can define early what is important in the content, what to load first and what to load later
* [x] &#x20;Make a **performance budget**
  * The [performance budget calculator](http://www.performancebudget.io/) is useful to estimate the budget depending on the performance we want to obtain. [This one](https://codepen.io/bradfrost/full/EPQVBp) is nice too.
  * Remember that this budget takes compression into account.
  * Currently, the recommended budget is [max. 170kb gzipped, 130kb if JS heavy](https://infrequently.org/2017/10/can-you-afford-it-real-world-web-performance-budgets/), but it depends mostly on the user-centric objectives

## Frontend

* [ ] &#x20;If choosing between SPA frameworks, **take in account features like server side rendering**; these features will be hard to add later
* [ ] &#x20;Take in account **how much every library / framework will take on the performance budget**; don't use too much of them
  * [Bundlephobia](https://bundlephobia.com/) can help we estimate the size of a new dependency.
* [ ] &#x20;**Make sure we need custom fonts** before using them
  * [This article](https://hackernoon.com/web-fonts-when-you-need-them-when-you-dont-a3b4b39fe0ae) can help
* [ ] &#x20;Consider technologies like [**AMP**](https://www.ampproject.org/fr/) and [**Instant Articles**](https://instantarticles.fb.com/), but be aware of their pros and cons
  * Keep also in mind these solutions are not mandatory to obtain correct performance

#### Optimize images

Images represent in average \~60% of a page's weight, thus it's an important part to optimize.

* [ ] &#x20;Use **WebP compression** format for browsers that accept it
* [ ] &#x20;Use **responsive images** with `img`'s' `srcset` and `size` attributes
* [ ] &#x20;**Optimize** manually **important images** or script their optimization
* [ ] &#x20;**Lazy load** images
* [ ] &#x20;Replacing animated **gifs by videos** can reduce their size dramatically (details [here](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/replace-animated-gifs-with-video/))

#### Reduce code size

* [ ] &#x20;**Minimize** the source code
* [ ] &#x20;Use **tree shaking** (e.g. with [webpack](https://webpack.js.org/)) to remove unused code
* [ ] &#x20;If the bundled code file is too big, use **code splitting** to load only what's needed first and lazy load the rest
* [ ] &#x20;Serving **ES2015 code to browsers supporting it** and ES5 code to browsers that don't, using `type="module"` and `nomodule`, can improve the bundle size and parsing time (details [here](https://philipwalton.com/articles/deploying-es2015-code-in-production-today/))

#### Reduce number of requests

* [ ] &#x20;Replace third parties components (like sharing buttons, maps...) by **static components**
  * Tools like the [Simple sharing buttons generator](https://simplesharingbuttons.com/) can help.
* [ ] &#x20;Cache requests client side using **service workers**
* [ ] &#x20;Bundle common images using **CSS sprites**

#### Prepare next requests

We can use prefetching to prepare the browser to next requests and make them faster or even instant. [This article](https://css-tricks.com/prefetching-preloading-prebrowsing/) is a few old but explains well the following techniques.

* [ ] &#x20;Use **dns-prefetch** to resolve the domain of services we may need
* [ ] &#x20;Use **preconnect** to do DNS lookup, TCP handshake and TLS negotiation with services we know we will need soon
* [ ] &#x20;Use **prefetch** to request specific resources that are likely to be needed soon, like images and scripts
  * This technique makes an especially good combination with lazy loading.
* [ ] &#x20;Use **preload** to request specific resources that will be needed in the current page, e.g. `<script>` tags at the end of the body
  * The difference between `prefetch` and `preload` is explained [here](https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf).
* [ ] &#x20;Use **prerender** to request and prerender pages that are very likely to be visited soon, like homepage or user dashboard
  * Be aware that this technique is quite heavy, make sure we know what we are doing before applying it.

#### Optimize time to rendering

Ideally the critical code should fit in 14KB in order to be server in the first TCP roundtrip ([why 14KB?](https://tylercipriani.com/blog/2016/09/25/the-14kb-in-the-tcp-initial-window/)). These techniques help to achieve this goal.

* [ ] &#x20;**Inline critical CSS** in the `<head>` of the pages
  * Tools like [CriticalCSS](https://github.com/filamentgroup/criticalCSS) and [critical](https://github.com/addyosmani/critical) can help defining the site's critical CSS
* [ ] &#x20;If critical CSS is inlined, we can then **defer the CSS files loading**
  * [loadCSS](https://github.com/filamentgroup/loadCSS) can help achieving that
* [ ] &#x20;When the CSS files are loaded, **set a cookie to avoid using inlined critical CSS anymore**; this way it will benefit from browser cache
  * More explanations on this technique [here](https://gomakethings.com/inlining-critical-css-for-better-web-performance/#what-about-browser-caching)
* [ ] &#x20;**Defer scripts execution**, especially social media buttons and ads
* [ ] &#x20;**Defer fonts loading**; the technique is explained [here](https://www.sitepoint.com/improving-font-performance-subsetting-local-storage/)
* [ ] &#x20;Use **server side rendering** if making an SPA

#### Optimize fonts

* [ ] &#x20;**Subset the fonts** using [Font Squirrel's font generator](https://www.fontsquirrel.com/tools/webfont-generator)
* [ ] &#x20;Use **WOFF2** with fallback to WOFF and OTF

#### Make animations smooth

* [ ] &#x20;Prefer animating using CSS' **transform** and **opacity**; more explanations [here](https://www.html5rocks.com/en/tutorials/speed/high-performance-animations/)
* [ ] &#x20;If animating with JS, use **requestAnimationFrame** instead of `setInterval`
* [ ] &#x20;**Avoid animating during high network activity**; for example, wait till the page is fully loaded

#### User perceived performance

User-perceived performance is often disregarded but can be more important than actual performance. These techniques allow us to improve it.

* [ ] &#x20;We should use a **loader only on "long" / "heavy" tasks**, i.e. tasks the user can imagine they are heavy (e.g. account creation)
* [ ] &#x20;Instead, we can use **animations** to illustrate the transitions following the user's action, for example, the transition from one page to another
* [ ] &#x20;Show **app shell before content** if needed; more explanations [here](https://developers.google.com/web/fundamentals/architecture/app-shell)
* [ ] &#x20;If using JPG images, we can use **progressive JPGs** to improve their loading perception
* [ ] &#x20;If not using especially JPG, we can **replace the images by cheaper components** until they are loaded
  * We can replace an image with a canvas filled with its main colour.
  * We can replace an image with a very lightweight, blurred version of it. This efficient technique is explained in [this article](https://code.facebook.com/posts/991252547593574/the-technology-behind-preview-photos/) from Facebook.
  * We can also simply use a low-quality version of it.
* [ ] &#x20;Make an **optimistic UI** to make some interactions feel instant; a quick explanation can be found [here](https://uxplanet.org/optimistic-1000-34d9eefe4c05)

## Backend

* [ ] &#x20;When choosing a web framework/library/language, take into account the following points:
  * How **fast** is the library / underlying language (but be aware that benchmarks are usually biased)?
  * How easy will it be to handle **concurrency**?
  * Does it allow **efficient resource management**, e.g. using a connections pool or an event loop?

General

* &#x20;Provide **batch queries/transactions** instead of making the client send multiple requests
* &#x20;**Identify & optimize** slow resources
* &#x20;**Parallelize** slow tasks
* &#x20;Use relevant **data structures**
* &#x20;Don't overuse **serialization**
* &#x20;**Generate static content when deploying** so that it will be computed only once
* &#x20;If possible, use [jemalloc](http://jemalloc.net/) to improve memory allocation

Cache

* [ ] &#x20;Use **HTTP cache**; the different caching techniques are explained in [this guide](https://developer.mozilla.org/docs/Web/HTTP/Caching)
* [ ] &#x20;Consider using **ESI** if the app is not a SPA
* [ ] &#x20;**Cache calls to other services** using Redis, a reverse proxy...
* [ ] &#x20;**Cache data** slow to compute and **memoize** slow functions

#### Don’t loose time with non-urgent tasks

* [ ] &#x20;**Defer tasks** to workers using a queue or use event-based patterns like Event Sourcing
* [ ] &#x20;Use **UDP** for immediate but not vital tasks like logging

#### Don’t lose time with errors

* [ ] &#x20;**Fail fast** by validating request inputs as soon as possible
* [ ] &#x20;Use the **circuit breaker** pattern to avoid waiting for timeout when needing another service
* [ ] &#x20;On sensible resources, **detect suspicious requests as attacks before actually handling them**; attacks can cause heavy resources consumption
  * For example, detect a login request as part of a brute force attack before fetching user data from the database

## Database

* [ ] &#x20;Make sure we **use the right DBMS** for the needs
  * Usually, a relational database will cover most needs, but in some cases, a NoSQL database may be a better fit.
  * If hesitating between NoSQL solutions, [this comparison](https://kkovacs.eu/cassandra-vs-mongodb-vs-couchdb-vs-redis) may help us.
* [ ] &#x20;First, use **indexes** smartly
  * [Use the Index, Luke](http://use-the-index-luke.com/) provides a complete guide on this subject for common RDBMS. [here](http://use-the-index-luke.com/sql/partial-results/fetch-next-page)
* [ ] &#x20;**Tune** the DB; tools like [MySQLTuner](https://github.com/major/MySQLTuner-perl) and the experimental [OtterTune](https://github.com/cmu-db/ottertune) can help
* [ ] &#x20;**Identify & optimize critical and slow queries** (e.g. code that produces n+1 queries)
  * In most SQL databases, `EXPLAIN` can help by showing the execution plan for a query
  * In PostgreSQL, `EXPLAIN ANALYZE` can help further by executing the explained query
* [ ] &#x20;If using pagination, **use the last row instead of `offset`** as a starting point; more explanations [here](http://use-the-index-luke.com/)
* [ ] &#x20;Once we are sure the used DBMS is the good one for our needs, **take advantage of its advanced features** (e.g. materialized views in Oracle, hyperloglogs in Redis...)
* [ ] &#x20;**Don’t use ORM for complex queries**, unless you know what you’re doing
* [ ] &#x20;If possible, **defer heavy tasks** to moments of the day when there is less load on the database (at night for example) to save resources when needed
* [ ] &#x20;If possible, enable [jemalloc](http://jemalloc.net/) to improve memory allocation
* [ ] &#x20;If using UUIDs, reorder them before storing them; more explanations [here](https://www.percona.com/blog/2014/12/19/store-uuid-optimized-way/)
* [ ] &#x20;Try different storage engines
  * On many DBMSs [RocksDB](http://rocksdb.org/) often gives interesting results.

## Network and Infrastructure

* [ ] &#x20;Serve static content using a **CDN** to shorten the distance between the client and the server
  * When using the CDN take into consideration features like HTTP/2 support, compression...
* [ ] &#x20;Deploy the app on **several datacenters**, also to shorten the distance between the client and the server
* [ ] &#x20;Serve resources compressed using **Brotli** if it's supported, **Gzip** otherwise
* [ ] &#x20;Compress resources that are rarely changed using **Zopfli**
* [ ] &#x20;Use **HTTP/2** and its features like **server push** and enable **HPACK** to compress HTTP headers
* [ ] &#x20;Use **OCSP stapling** to fasten TLS shaking
* [ ] &#x20;Use [**0-RTT resumption**](https://blog.cloudflare.com/introducing-0-rtt/) to avoid round trips during TLS negotiations
* [ ] &#x20;**Avoid redirects** as they increase the number of needed requests
* [ ] &#x20;If using a microservices architecture, **bring services needing each other often closer**, ideally in the same machine
  * Kubernetes' pods can help achieve this goal

## Measuring

* [ ] &#x20;Measure **server-side** performance; this is usually already done by the web framework
* [ ] &#x20;Measure **client-side** performance; tools like [Web Page Test](http://www.webpagetest.org/) can help
* [ ] &#x20;Measure client-side performance **by country**; results may hugely differ from one to another
* [ ] &#x20;Use tools like [Lighthouse](https://developers.google.com/web/tools/lighthouse/) to **audit** the site
* [ ] &#x20;**Load test** the servers as they probably won't have the same perfs under 10rps and 1000rps
  * [Gatling](https://gatling.io/) and [Locust](https://locust.io/) are good tools to perform these tests.
* [ ] &#x20;Keep track of **queries to the databases** to ease slow queries discovery

## Misc

* [ ] &#x20;Keep the **dependencies up-to-date** as their performance is often improved by their maintainers
* [ ] &#x20;Take into account the [**`Save-Data`**](https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/save-data/) request header to serve lighter assets to clients with limited resources
