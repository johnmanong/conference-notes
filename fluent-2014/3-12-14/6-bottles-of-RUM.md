# 6 Bottles of RUM: Surprising Stories of Mobile Behavior in the Real World (5:15pm)
## Peter McLachlan (Mobify)

# why mobile performance?
- 20-30% of traffic coming in from mobile
- another 20-30% of traffic from tablet
- when people are waiting for things, you're wasting their lives
- "1 second delay in page resonse results in a 7% reduciton in conversions"
- mobile speeds (Mbps):
  - 3G = 3
  - HSPA+ = 40
  - ...
- as bw increases, page load time plateaus around 5-6 mpbs
- page load latency does go down linearly

# so what can we do?
- common best practices
- some performance patterns are anti-patterns
  - e.g. local website and non-local cdn
- *if you are not measuring, you cannot optimize*
- instrument areas of interest
- key advantages
  - more scale than synthetic testing
  - more comprehensive results

# RUM results
- mobile speed: state of the union (cold connection)
  - how long to get 0 bytes of data
  - header only
  - create new domain so no cookies
- median times:
  - 250 ms in most cases
  - much worse in others (india)
- [Google says](https://developers.google.com/speed/articles/web-metrics)
  - top sites have 42.16 resources
    - ...
- test for warm connection
  - response times are almost 1/3 of cold connection time
- ISP breakdown for 6.7 lb image
  - verizon, at&t, t-mobile, sprint
  - not dramatic difference

## cookies increase the size of the header
- max 4kb of cookies
- large payloads are fragmented into several packets
- each packet gets header info
- cannot process response until all packets recieved
- 2-10% increase in response time due to cookies (0-4kb)
  - google says: < 400 bytes of cookies (1% slowdown)
  - affects warm connections more (but are still much faster)

## parallelism
- http1.1 max 2 requests per hostname
  - modern browsers do not respec this
- mobile browsers do no respect this (4-6)
- domain sharding to get more parallel connections
  - e.g. 2x and 4x sharding
  - up to 24 parralel connections
  - not much of a performance increatse (< 5%)
  - probably not worth adding
  - HTTP 2.0 allow to multiplex a single connection
    - multiple objects over same tcp connection
    - no need for sharding

# "materialize" an image
- how long to raster (no get from server or cache)
- three ways:
  - img src
  - img src int64
  - background-img + data uri
- sprites are almost twice as fast data uri's

# conversions and carousels
- two e-commerce sites
  - demographics: 18-30 and 30-50
  - 18-30 carousel
    - tap to zoom (whole target)
    - tap arrow
    - thumbnails
    - carousel is swipable
  - 30-50 carousel
    - pops to inidcate state
    - swipe
    - tap to zoom button
    - larger arrows to scroll
  - 18-30
    - use the icon bar
    - arrow and swipe were not used nearly as much as icon
    - chrome was the swipiest
    - android least
  - 30-40
    - large arrows were most popular
    - iphone did more interaction (and swiping)
  - average interaction before conversion
    - younger had more interaction, android most engaged
    - older had less and more consistent accross type

# css (performance considerations)
- [Steve Souders experiment](http://www.stevesouders.com/blog/2009/03/10/performance-impact-of-css-selectors/)
- 2000 anchors and 2000 rules
- predicted performance based on selector complexity
- result showed it was a micro optimization

## what about mobile?
- very similar results
  - firefox was by far the fastest

## too early to say "don't worry about it"
- sass (and anything that generates code)
  - nesting caused generated code to create 10 page selector
  - make sure its a little bit sane
  - some properties can cause problems
    - e.g. -webkit-backface-visibility applied to '*'

# Summary
- latency is a real issue and not going anywhere any time soon
- use "just enough" connection
  - good server values for connection timeouts
- < 400 bytes of cookies
- ideally cookie free domain for static assets
- domain sharding bad
- sprites are good
- dont worry about css selectors
- swipe is not that popular
- very little data published about this


