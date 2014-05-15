# keynote with Paul Irish (9:10am)

# Delivering the goods
## minimizing page load time and finally answering the page size vs # of requests

## page optimization
-[an engineer's guide to optimization]
  - id area which will change business needle
  - ...
  - what is speed limit
  - approach limit

- what does performance mean to user
- example: twitter
  - page load at 2.4s (nothing on page)
  - activity finished at ~8s
  - The Speed Index
- not about dom ready or page load, its about pixels on the page

## number of requests vs page size
- correlation to speed index does not differentiate between these
- asked Ilya
  - want to be in good health
  - how do you optimize food intake
  - how often do you eat and how much
  - no one would measure a diet this way
  - not all requests, bytes are eual

## bandwidth and latency
- gains diminish at higher bandwidth
- latency has a much more linear relationship
- latency bounds web browsing
- bw bounds streaming media

### tcp
- intitial handshake to open connection
- *tcp slow start*
  - ramps up size of payload
  - 4 >> 8 >> 16 >>32
  - RTT much slower on mobile
  - dns lookup + handshake + content
- tcp optimized for large data stream
- tcp bottleneck is latency

### critical path
- reddit on mobile, duck feeding the fishes
- webpage test on imgur
  - filmstrip view to view how network requests affect what user sees
  - image url isn't in initial html payload
  - make api request for it
  - also blocked by head loading
  - can also create Timeline (chrome dev tools)
- what is critical in css
  - can inline critical css
  - get the rest later
- eliminate any render-clocking js
  - load all async
- minimize render-blocking css
  - inline vs stylesheet
- deliver the goods
  - no redirect for html
  - gzip

- wrapping up
  - pagespeed insights is totally sweet
  - want a really fast mobile page load
    - first 14 kb request should have everything
  - max 200 ms of server response
  - speed index under 1000

# keynote with Jen Simmons (Jen Simmons Design)

- 25 year anniversary of the www
- the internet crushes everything else
- No central authority
- designed to reduce barriers
- [line mode browser] (http://info.cern.ch/LMBrowser.html)
- html as a language
  - declarative
  - simple. flexible. forgiving.
  - simple programming level
  - simplified version of hypertext markup
- html is too hard or too easy?
- html is awesome
- kittens

# understanding your user's experience
## Christine Sotelo (New Relic, Inc)

- new feautres Real User Monitoring
- javascript error reporting
- ajax timing
- roadmap
  - resource timing
  - cdn perf
  - support for angular
  - more


# beyond pushing "play": interactive, data-driven videos for a web-based world
## Susan E McGregor

- video tells stories that other formats cannot
- usually, cut a hole in the page and put a video there
- what about interactive video...
- the wilderness downtown by chris milk, arcade fire, google
- popcorn maker by mozilla
- data visualization usually needs help to be expressive
- video is very communicative
- [data docs](datadocs.org)
  - create div
  - put a video in it
  - put interactive elements in it
  - put controls above
  - targeted to people who aren't hardcore programmers
  - on github

# The Goodness of JavaScript
## Aaron Frost (Domo), Dave Geddes (Domo)

## 50 shades of JavaScript
- terse, expressive, easy lang
  - js: x === y
  - java: x.equalEqualEqual(y)
- flexible can switch paradims
  - functional programming
  - oop
- found in
  - browser
  - server (node.js)
  - ide (brackets, atom)
  - database (mongo, posgres, ...)
  - mobile (ios7, apache cordova, firefox mobile)
  - build tools (grunt, gulp)
- collateral damage
  - don't talk about math
  - ruined Jake Weary's budding music career
  - typeof NaN; // "number", es6 has a chance to change this

## JS === community
### community.next
- be kind
  - [trollcount](trollcount.com)
- be helpful
  - submit a pr
- leave mark

**"The goodness of javascript is not a language, it's you."**


# Keynote with Yehuda Katz and Tom Dale
## Yahuda Katz(Tilde, Inc.), Tom Dale (Tilde, Inc.)

# ember: a framework for building ambitious web applications

## in defense of frameworks
- "You call a library. A framework calls you."
- this is not a fair way to think about it
- ember is a *framework*, angularJS is a *toolset for building a framework*

### flexibility
- what is flexibility?

### dependency injection
- give system classes, system wires up objects
- core part of ember and angularJS
- angular
  - just list dependencies
  - simple, only one primitive
  - maximally flexible
- ember
  - offer guidance for longterm happiness
  - e.g. Route obj does not have access to the views

### observations
- anyone who has built multiple apps, you probably have a framework
- experienced developers can say you're doing it wrong
- toolkits all have "best practices guides"
- clearly, there is a notion of "the right way to do it"
- angular wants you to build a framework for each app

### roles
- frameworks are about defining roles
- ember
  - data flow: route >> controller >> templates >> components
  - event flow: route << controller << templates << components
- maximally flexible primitive, with an api on top which nudges you in the right direction
- good practices feel good, bad practives feel bad
- you can punch through for flexibility, doesn't feel good
- like a firearm safety, provide a bit of friction before you shoot yourself

### components
- angular most people are building compoents
  - need to tweak each time
- ember provides this out of the box, default config to whats popular

### router
- router is the heart and soul of ember
- the router is ember and ember is the router
- ember used to look a lot like react.js
  - unclear whcih objs can talk to eachother
- loading a model for this template
  - what happens if its in the middle of loading or an error
  - agreed convention allows this to get automatically sucked in

### query params
- establish how controller, view, model properties map to query params

### flexible api
- doing the wrong thing feels the same as doing the right thing

### framework
- makes doing the right thing fel good
- build on top of maximally flexible primitvies
- evolves best practices
- feedback loop to iterate on framework

