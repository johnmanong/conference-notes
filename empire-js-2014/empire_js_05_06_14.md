# Empire JS | 05.06.2014
--------------------------------

---

## Javascript apps as a build artifact | Clay Smith (9:10am)
- how to deploy and provision js apps within native apps
- "Javascript Development Workflow" --Paul Irish
- JS Battle Groups
  - "My Framework is better than yours" (2010 - present) [wiki](http://en.wikipedia.org/wiki/Comparison_of_JavaScript_frameworks)
  - "My buildtool" is better than yours" (2011 - present)
  - "I prefer to write in (a) bc it makes (b) better" (2010-present)
    - (a) coffeescript, typescript, clojurescript, dogescript
    - (b) websites, mobile sites, mobile apps
  - "My dependency management tool is better than yours" (2012-present)
    - bower, browserify, ender

#### Page duty app
- essential javascript
  - fastclick, hammer, etc
- essential build
  - gulp, git, etc
- still complex
- mobile web frontier (2007-present)
  - cordova and phonegap
  - single page app in web view

- Attempt #1
  - just put it all in version control
  - Good:
    - well understood (simple commit)
  - bad
    - sub modules
    - merge conflicts

- Attempt #2
  - npm modules
  - don't let end user know about the complexity involved in building js for module
  - tried npm package.json pointing to private git repo
  - sadly this did not get us all the way there

- Simple process: code -> gulp -> production code
- production js app looks like a build artifact
  - needs place to live outside of source control

- Attempt #3 (success!)
  - Github release api (sept 2013)
  - pseudoo-artifact repo
  - release is tag on files in s3
  - *no gulp or grunt integration for github release*

- options for hybrid apps
  - sonatype nexus, bridge to npm
  - private npm/common js repos
  - want static representation of my app

- *Don't check in your *.min.js files!*

---

## Preventing XSS and CSRF | Jeremy Stashewsky (9:45am)
- Trust (with a capital T) is number on value at SalesForce
- prevention > repair
- two common:
  - XSS : Cross Site Scripting
  - CSRF : Cross Site Request forgery

### XSS
#### what is it
- injection attack
- driven by user inputs
- need validation and sanitation
- user can put stuff on the page
  - javascript
  - html
  - etc
- ex: ejs template
  - template gets user.name and site.name
  - what happens if someone puts user.name = </h1><script>window.location="evil.com"</script>

#### how to precent this
- validating input
- sanitize output
- enable ontent-security policy
- new flow
  - take input and validate/clean, store
  - sanitize/escape before rendering output
  - CSP enabled

##### Validation
- best case: white list (allow list)
  - compare against good known values
  - default is closed
- not everything can be enumerated against an allow list
  - ex: names
  - don't allow angle brackets

##### Sanitization
- cannot validate everything (but you should when you can)
- Goal: prevent user controlled data from breaking out of its context
- How: remove markup characters
  - *Entity Encoding*: convert markup chars to escaped characters
  - whitelist is actually pretty small
- ex: ejs template revisited
  - '-' interpolation
  - '=' escaping operator (basic escaping by default)

#### Contextual Filtering
- just html? no!
- 'expression' in css in old browsers
- places to escape
  - css
  - js
  - html style (js + css)
  - html attributes
- cannot just inline json into a script block
  - can stop script block and inject script
- sanitizing js literals
  - things like `<` become `\x3C`
- doesn't save you from `innerHTML`
  - this undoes all the effort of sanitizing

##### Query Param Attack
- interpolate user id param
  - e.g. `{userId: "42&userId=666"}`
  - could get access to other user
- *URI escaping*
  - convert unsafe chars to UTF-8 ocelots

#### Tools
- secure filters (npm)
- phalcon\Escaper (php)
- Angular has strict contextual escaping service
- React and JSX
- Java: OWASP Enterprise Security API
- Go `html/template`
  - based on EcmaScript Harmony "Quasis"
- helment (npm)
- cspbuilder.info

#### wrap up
- should I sanitize inputs...NO!
  - permanently modifies the data
  - fairly cheap, sanitize on way out


#### Content Security Policy
- last line of defense
- pages defines an allow-list of features and origins which are permitted
- served as a HTTP header
- also can use `<meta>` tag
- e.g. can disallow any script block outside of origin and 'unsafe inline'


## CSRF
- exploits the fact that you're logged into another site via a cookie?
- e.g. logged into example, go to evil.com

### how to fix this?
- assert that user intended to do that
  - user was on my website
  - they clicked submit on my form
  - therefore it was not csrf

#### user was on my website
- add anti-csrf token to all forms
  - not the same value as cookie
  - computed from cookie

#### they clicked on my submit form
- actions that change `PUT`, `POST`, `PATCH`, `DELETE`

#### therefore it isnt csrf
- make sure to use https for no sniffing
- if user has cookie and token, should be legit

### how to do it?
- e.g. ejs template
  - form should use POSt
  - add hidden form field with anti-csrf token
- really sensitive
  - re-prompt for password for senstive actions
  - ask for user confirmation

### sumary
  1. verify use intent
  2. good REST citizen
  3. make sure you're using anti-csrf token

#### XSS
  1. validate inputs
  2. sanitize outputs
  3. Content Security Policy

#### CSRF
  1. verify user intent
  2. use the correct REST verb
  3. use anti-CSRF token

### Tools
- senchalabs 'connect' middleware    

- REF
  - reveal js
  - [secure filters](https://www.npmjs.org/package/secure-filters)

---

## Bits of Nodebots.Next | Rick Waldron (10:30am)

### Beaglebone black Demo Redux
- it works!

### intro
- ps3 controller
- [github](https://github.com/rwaldron)

### animating things in javascript
- Dom
  - alerting the appearance of an element by modifying style property at a given interval
- Canvas
  - alerting position by redrawing at a given interval
- CSS 3D
  - alerting the appearance of an element by modifying style property at a given interval

### animating nodebots in javascript
- moving things in the real world similar to moving things in the fake world
- at Empire JS in 2012
  - temporally bound task sequencing
- want: complex, coordinated, servo animations

### coordination
- servo
  - speed is proportional to servo size and voltage applied
- *Frame Constrained Servo Movements*
  - move servo horn incrementally

    last = position
    for each frame:
      delta = percent * (distance / rate)
      delta = eased(delta)
      last = delta + last

### Degrees of Freedom (DOF)
- e.g. hip + knee = 2 DOF
- more freedom, more complexity
- non-node bot example
  - mechanical and software package : very smooth
  - but want to do it for free

#### 3 DOF + 2 legs
- foot + knee + hip
- sensors can give the robot vision

#### 3 DOF + 4 legs
- dancing
- throwing a fit

#### 6 dof + 2 legs
- fully articulated hips

### so what?
- boucoup financed $ intensive parts of this project
- javascript outside of the browser
- BECAUSE WE CAN
- Can you write js animations, you can program robots!

### ref
- xd module for wireless
- intel galileo

---

## Hacking Webforms with Phantom.js | Alyssa Ravasio (11:20am)
- *hipcamp* : help people discover and book campsites
  - CA is closing 70 sites
  - current system is fragmented
  - company in charge of booking is horrible

### no api exists ... no problem
  - phantom.js and selenium for automating broswer
    - selenium: great for "real browswer", cross browser
    - phantom: just funcationality
  - use this for filling in a webform and completing a financial transistion

### phantom js
- headless, scriptable browser
- used to complete the process

#### how it works
- spawn child process
- interact with page
  - fill in credentials and sign in
  - user details and click submit
  - ...
- company uses own credit card
- listens to page events and steps through process

### lessons learned
- node can spawn children
- javascript makes dream come true
- "with great power comes great responsibility"

---

## MyDB | Guillermo Rauch (11:45am)
- ...
- collaborative rich text in real time

### colloboration
#### low latency
- e.g. change string
  - opt 1: delete from pos 7 to 20, d7 20
  - opt 2: insert new text, i7 New York City

#### convergence
- two people start from the same place and edit at the same time
  - who is correct?
  - is either correct?
  - first to server is the one we are going to keep
- "whoever types faster wins"
- can lose some of intention preservation
  - could implement semantic convergence
  - e.g. 'big' is added and 'city' is added, they do not need to clobber

#### intention preservation
- best way to capture what the user wants
- first approach: `conenteditable=true`
  - by default, it is divergent
  - when 'enter' is pressed, diff browers can produce diff results
- even if convergent, event only fired *after* not during DOM transformation
  - needs events before DOM transformation
  - got batched mutation
- Goggle docs
  - to capture everything, they manually do everything themselves
  - no dependency on DOM behavior
- plauged with hacks
  - attach to `keypress` and re-render dom
  - nope!
  - for example, japanese has many keystrokes, popover, and click
  - google docs has an iframe with `contenteditable` next to the 2px pseudo cursor
  - make it very hard to work on mobile devices
- another approach: textarea over paragraphs
- no rich on mobile
- back to `contenteditable`
  - do best to intercept input

##### Paste interception
- when paste occurs, `preventDefault()` and `clipboardData`
  - not all broswers allow you to change default
  - clipboard data not mature
- work around
  - `beforepaste` is triggered when you dont want to safari
- work around for work around
  - detect cmd+v

##### Typing detection
- `selctionchange`
  - does not exist on firefox
  - workaround: capture every mouse event and synthesize it
  - selection change polyfill
- inject `div` to where use clicks
  - initially empty
- cannot focus on empty div
  - inject unicode whitespace into div to allow programatic shift in focus
- ios has rich text in tooltip, but does not fire events

#### Virtual dom
- like React 
- diff VDOM and DOM
- Google's diff-patch-match with Semantic Cleanup

---

## BigPipe | Arnout Kazemier (1:20pm)
- from facebook 4 years ago
- sections rendered and served to the page when ready
- initial response: doc fragment
  - js lib
  - `<noscript>` for users w/o js
  - async load responses
- front-end & render performance
- generation | latency | rendering
- parallellize rendering into pagelets

### *pagelets*
- small re-usable modules of html, css and javascript
- extends pagelet
- define get method, which is called whenever pagelet is used
- support error page per pagelet
- support auth per pagelet
- styling, whatever you want
- managed via npm
  - can install and extend other's modules

### Client
- small frameworks
- event emitter
- dedicated submit module
- can re-render
- rpc
- sandboxing js into pagelets
  - no polluting global namespace
  - iframe??
- async css and js loading

### Page
- extend page to include pagelets property
- view
  - manually include bootstrapping code
- auth
- modes
  - fully async: unordered render
  - pipeline: load in order specified
  - sync: single flush

### createing a big pipe server
- createServer()
  - `pages` directory
  - `dist` directory
- supports redirects
- spdy property
- real time connection for each page via `primus`
- `primus`
  - wrapper around sockets engine
  - flexible, seamless
  - started as wrapper around engine.io


### compiler
- tries to figure out which pages use which pagelets and sorts
- ensures accuracy and avoids redundancy
- status page (e.g. 404)


### plugins
- how to extend Big Pipe
- supports middleware
  - can be proxied directly into primus

### LIVE DEMO
- success!
- browsenpm.org built by BigPipe

### future goals
- 'quicklinking' or Turbolinks
- pagelet & page cache
- recursive and nested pagelets
- streaming and diff-able assets
- more tests
- more benchmarking
- [site](bigpipe.io)

---

## I-Tier: Node.js at Groupon | Sean McCullough (1:55pm)

### how the platform stopped working
- monolithic rails app
- business through hyper growth
- simple-ish site
- international "rip offs"
  - did not have op power to compete head on
  - acquired companies
  - seperate plateforms
- stack was really independent apps
  - rails (us)
  - java/apache (europe & asia)

#### move to mobile
- built out REST api in each stack
- web layer + mobile layer...for each stack

#### business was stuck
- could not build features fast enough
- wanted ot build world wide
- mobile was always playing catchup
- could not change look and feel
- difficult to internationalize

#### platform was broken
- almost all of the site on cdn
  - a/b testing fragmented cdn
- monolith was too slow and hard to break down

#### start with the front end
- unify global look and feel
- REST api for mobile

#### Bakeoff
- Node, Rails, Java/Play, Python+Twisted, PHP
  - not a great way to make a technolgy choice
  - each has pros and cons

### Node was a good choice
- wanted to target front end developers
- not system engineers
- Javascript was the benefit, not Node
- stack
  - coffeescript
  - light-weight express app
  - mustache and custom view engine
  - custom asset pipeline

#### Boundries
- apps can only talk to REST Api and memcached (CSRF validation)
- layout in a seperate application
- shared common asset bundle

#### Design
- simple controllers
- render from server
- skip fancy performance optimizations
- make the api the bottleneck
  - push as much logic into the api
- resilience when services fail
  - even if backend goes down, show something

#### first page: subscribe page
- proof of concept
- didn't look like the rest of the site
- growing pains
  - max sockets
  - breaking infrastructure
  - new deployment processes
- max outgoing http sockets on node is LOW, set it to inifinity

#### next target: browse page
- new problems
  - auth
  - more svc calls
  - more complicated routing
  - more traffic
  - look and feel consisentcy

#### grout
- can route to I-Teir apps
- experiments between different applications on the same url


#### gconfig
- monolith means you can cram it all into yml files
- simple node app to send json data to clients
- can change on the fly

#### layout
- distribute layout as a service
  - returns partially running mustache template
- changes can be shipped without re-deploying all apps
- easy to use in development
- service
  - semantically versioned
  - roll forward with bug fixes
  - stay locked on a specific version
  - enable site-wide experiments

### how we re-wrote it
- get the whole company to move is hard
  - two platforms is hard too
- globl effort
  - 150 devs world wide
- feature freeze


### what didn't go well
- moving to soa is hard
- testing end to end is hard
- changed team workflows
- teams in silos
- code quality changes
- maybe more hand holding


### Next Steps
- better resiliency to outages
- distributed tracing
- international launch (now!)
- Open Source

### tl; dr
- KILL ALL MONOLITHS


---

## Analyzing Japanese Art with Node.js and Computer Vision | John Resig (2:30pm)

### Japanese Woodblock prints
- developed in japan until 1800's
- 1720's Edo was the largest city in the world
- mass produced for consumption by individuals
- depictions of people, stories, actors, etc ...
- 1840's govt banned printing of kabuki actors
  - kabuki actors as cats
- catfish shooting lasers at head-body thing
  - depiction of an earthquake
  - kimono has building supplies, symbolized rebuilding
  - catfish was personifcation of earthquakes

### wanting to own prints
- can buy them at auction
- some auctions know nothing about prints
  - subject matter
  - artists
  - when it was make
  - who made it
  - etc
- doing research
  - time consuming
  - expensive
- learning japanese
  - need to know 1700's japanese
  - calligraphy


### Ukiyo-e.org
- collection of prints, which have been aggreated from univerisities, museums, aucions
- quarter mil
- parsed text
- put under elastic search
- translated Japanese <-> English

#### Tools
- *Node i18n 2*
- does internationalization/translation
- stack
  - digital ocean
    - nginx
    - naught node express
    - mongo db
    - elastic search
    - scrapper
  - amazon cloudfront
    - images
    - js css
  - amazon s3
    - images
    - js css
- scrubber for quick browse of artists' work

#### Collecting wordblock prints
- use phantom.js for crawling
- queue based crawling using PhatomJS
- *stack scraper*

#### Image processing
- image similarity
  - TinEye services
  - wrote node modules
  - ignores images and analyzes the image itself
  - can even work around color/no-color
  - able to find multipanel when incorrectly assembled
- search by image
  - take photograph of a print
  - get results that match print
- sometimes its wrong
  - match color bar, instead of image itself
- *Idyll* mobile image cropping
- David Chester at Shutterstock, looking into auto cropping
- [eratzlabs.com](http://eratzlabs.com)
  - who made this print based on style of print

### Aiding the study of woodblock prints
- image diffing
  - e.g. pattern, face, print, etc
- ownership meant you actually owned the block itself
  - can transer ownership and modify
  - headswap for "new" print
  - different artists signing
- image analysis is unique bc it is different than other meta data
- can find missing data since images are compared


#### correcting print data
- name of artist can appear many different ways
  - need good mapping between languages
  - single representation of japanese congi in english can have many representations
- many-to-many mappings make this extremely difficult
- wrote some modules for this
  - *hepburn* english to japanese
  - *enamadict* look up name to see first or last name
  - *ndla* lookup on japanese govt db of names
  - *romanjiname* combines above 3
  - *yearrange* parse all the weird ways to write dates

### **CODE EVERY DAY**

---

## Web RTC can be Easy | Michelle Bu (3:40pm)
- at stripe primary communication is gchat
- message has to go from SF to datacenter (Dalles, OR) to SF
- why not peer to peer?
- computers behind NAT ip mask
- need secure connection
- tcp is too slow!
- maintains PeerJS

### Web RTC
- peer to peer data, files, video
- Web RealTime Communication
- features
  - transport protocols UDP SCTP
  - end to end security DTLS
  - NAT traversal

### Live Demo...success!

### How did that work?
- purple
  - start RTC peer connection
  - build media and add to stream
  - send offer to blue
- blue
  - recieved offer
  - create connection
  - add media
  - send answer

### getUserMedia
- allows you to take media like webcam and mic and add media output to stream
- [shiny demos](http://shinydemos.com/getusermedia)

### pretty simple, theoretically...
- cross browser, cross platform
- browser support -> iswebrtcready.com

### remember magically send
- blue got purple's offer and purple got blue's purple offer answer
- need *signal server* to connect users
- server IS required, but once its setup you don't need it
- configs are broswer/version dependent
- a lot of magic to get around NAT
- *STUN*, *ICE*, *NAT.TURN*
  - *ICE* used to send around IP

### Resources
- simple WebRTC
- rtc.io
- peerjs

---

## The hidden benefits of static analysis | Kirill Cherkashin and Tsering Shrestha (4:00pm)

### static analysis
- static analysis
  - eval without running code
  - feed to js parser
- query syntax tree
- *grasp*
- sublime-grasp, resharper
- consistent code style is important
  - editor config
  - *EditorConfig*
  - *CodePainter* extends *EditorConfig*

#### JS linting tools
- help detect errors and potential errors
- JSLint, JShunt, Closure Linter, ESLint
- ESLint uses Esprima parser
  - allows for cusomized tools
- what about fixing the result
- *Fixmyjs*
  - fixes JSLint errors

#### code metrics and visualization
- brocoli!

#### removing duplicate code
- duplicate code is bad
- *JScpd*  (JS copy paste detection)


### static and dynamic analysis
- dynamic analysis is analyzing code when code is being run
- *JSCoverage*, *BlanketJS*, *Istanbul*
  - instrument code
  - run tets
  - verify all checkpoints were hit
- *COLT* Live Coding Tool
  - creates static http server
  - parsers
  - can jump to definition
  - Webstorm + COLT

#### adv debugging with spyjs
- used to be stand alone
- now part of webstorm
- how it works
  - create a proxy to http server
  - static analysis to inject code
  - ...
- get history of all events, not just call stack

### did not talk about
- type detection
- refactoring
- static security
- tests and generating tests
- cisualizing source code, graphs and flows

---

## Easing into ECMAScript 6 and Beyond | Ben Newman (Facebook) (4:40pm)
- [how to capitalize titles](titlecapitalization.com)
- ~"We have the opportunity, as technologist, to get rid of problems forever"
- example: comparison with -1
  - [1,2,3].indexOf(x) !== -1 -> ~[1,2,3].indexOf(x)
- *Abstract Syntax Tree*
- *recast*
  - tool for parsing, traverse and modify abstract syntax tree
  - -1 is a unary operator, - is operant and 1 is the input

### recast
- why recast over burrito, or falafel
- how to use it
  - require
  - .parse()
  - transform // whatever you want
  - .print()
- "Non-destructive partial source transformation" --Ariya Hidayat
- only change the parts that matter
  - human readable diff
- can be the laziest programmer
  - just write scripts to make transforms
- gave a talk about this all last month...link in slides

### at facebook
- rewrote 1600+ classes
- 150,000 insertions/deletions
- right tool, and problem goes away

### what to do now?
- just writing and running scripts doesn't fill time
- hard to "fix forward"
- why haven't all python projects on python 3
  - semantics, not just syntax changes

### what about ecma 6
- how to avoid python trap?
- easy into new language by simulating new features
- take things out of the future and use them now
- ex: native sort()
  - [1,2,3].sort((a,b) => a-b)    // ES6
  - [1,2,3].sort(function(a,b) {  // ES5
      return a-b
    }).bind(this)

#### how to use this?
- use recast!
  - print ES5 for ES6 code

#### what about something more complicated, like generators?
- declared with a*
- returns generator
  - has next()
  - has done()
- how to write a transform for this?
  - hoist variables
  - wrap all but var declaration into generator (outer just function)
  - yield turns into return statements
  - switch statement to decide what step you're at
  - runtime function called wrapGenerator, defines context

#### next: async functions
- sweetest of syntactic sugar
- functions return promise
- combines generators and promise
- PR in *regenerator* project [link](https://github.com/facebook/regenerator)
- not planned for EC6 or EC7 ... oh no!

### summary
- as long as there are shiney things, we'll transpile them
- incremental transpilation is the key to avoiding the python 3 trap
- this is how we will know how great the future will be
- still hard!
  - AST transformations don't always play well together
  - not everything can be transpiled
  - things like sourcemaps are needed
  - language specs can change 

---

## Pixel Art and Javascript | Vince Allen (spotify) (5:25pm)
- started with atari
- still playing pixel art games
  - minecraft (100 million uses)
  - radical fishing
  - spirit (future)
- pixel art in art
  - space invader
  - pixelation as a service
- post it note art
  - wrote program to match pixels in image to available poster images
- starting making digital pixel art
- all static
  - wanted it to be animated

### *big block framework*
- swap out class names
- predefine css
- works for small universe
- doesn't scale well
- bottleneck was 1-to-1 dom to pixel

### *bit shadow Machine*
- one dom element, h, w:0
- use boxshadows, which are still visible
  - can have any number of box shadows
  - use offset to position
  - can have blur
  - spread to scale
  - color
  - opacity
- scales to many box shadows
  - 1000! works
  - map velocity to blur, cheap effects
- how many box shadows can we have
  - box shadow fractal generator
  - 29,000!
- tool to capture animation
  - done in photoshop
  - *bit shadow press* to generate code

### how to make movies
- photoshop
  - adobe generator: automate tasks
  - use to create photoshop files
  - combine files to make hd movie
  - every object is a layer
- node to generate and capture each frame
- combine to make a movie!


---
