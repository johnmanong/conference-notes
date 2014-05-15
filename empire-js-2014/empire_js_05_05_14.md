# Empire JS | 05.05.2014
--------------------------------

---

## Sorting Algorithms | Jenn Schiffer (9am)
- computer science !== web development
- material from talk: "Introduction to Algorithms" (cormen)
- algorithm: anything that takes an input and produces an output
- (?) algorithm vs. process?
- sorting joke:

    myArray = [10, 7, 1];
    myArray.sort();   // [1, 10, 7]

  - js sort is lexicographical (dictionary sort)

- Array.prototype.sort() ?
  - no ecma script sort spec, must take compare function
- numeric sort

    myArray = [10, 7, 1];
    myArray.sort( function(a, b) { return a-b } );   // [1, 7, 10]

- stability: maintains order of items with "equal" value
- runtime analysis:
  - terrible interview question...(tybg)
  - Big-O: worst case
  - Big-Omega: best case 
  - Big-Theta: average case
- how much space, how much time, what kind of data? No "best" sort for all situations
- Big-0
  - O(1), O(log N), O(N), O(N log N), O(N^2), O(N^3)
  - O(log N) usually leverages recursion

### Sorting algorithms
- Three algorithms today: insertion, bubble, merge
  - ff uses merge sort?

#### Insertion sort 
- [fiddle](http://jsfiddle.net/v4CXh/2/)
- nested for loops

  // for each item n
    // for each item before index i
      // if item is less than previous item
        // swap those items

- can be ok if nearly sorted, terminates early
- [3,2,1] -> order N in THIS case
- stable sort
- O(n^2)

#### Bubble sort
- O(n^2)
- non-stable
- similar to insertion sort
- Donald Knuth "The Art of Programming"
- just don't use it

#### merge sort
- O(N log N)
- uses recursion to sort sub arrays
  - split until read to merge (1 item)
- multi branch recursion
- fast and (hella) stable
- takes up memory for temp arrays and recursive calls

#### other sorts
- shell, quick, cocktail, heap, counting, comb, bucket, radix, shear, shuttle, lucky, etc.
- "how can we use this increase our SEO?" -> "yes"

---

## Anatomy of a Successful Module | Trevor Landau (9:45am)

### | beyond a big idea
- open source
- stability
- explorable
- community
- outreach

### | Open Source

#### Github
- website to store git repositories
- issue tracking
- allows others to fork/contribute

#### NPM
- for node js developers, can take it a step further
- modules for node projects
- usage statistics for module
- dependencies listed
- check out the author

#### Browserify
- allows you to create node modules
- allows module to be used in browser (augments window)

#### Bower
- used for module management

### | Stability

#### JSHint
- static code analyzer
- provides feedback on code style and best practices

#### Mocha
- provides unit tests for node

#### Coninuous Integration
- **Travis CI**
- can watch github repo
- hook into merge

- **Instanbul**
  - js tool to instrument code to test coverage

### Explorable
- badge from Travis for stability
- various levels of documentation
  - short Readme
  - hook into github wiki (e.g. d3)
  - host a site (e.g. underscore)
  - video tutorials (e.g. Ember.js)
  - blog to follow activity (e.g. React)
  - working examples (e.g. React)

### | Community
- Twitter account to communicate
- get people to contribute
- public changelog: bug fixes, improvements, etc
- Github has milestones
  - link issues to release milestones

### | Outreach
- announcement on Twitter
  - use hashtags! (e.g. #nodejs #javascript)
  - can explicitly ask for help promoting (e.g. "help me promote by RTing")
- talk to the press
  - jsut email them!
  - e.g. js weekly
- IRC
  - free node server dedicated to opensource
  - annouce your stuff there

### | Present at a Conference
- Pete Hunt @ Facebook/React has been doing this a lot

---

## Final Frontier | Domenic Denicola (10:15am)
- no star wars future :(
- "The Singularity Trilogy" by Hertling
  - discuss the rise of ai
  - starts with traditional computers
  - smart phones become main computing platform
  - last book is implants and cyborgs

### Smart Phones and mobile
- personal devices
- presenting on a windows tablet
- hasn't used traditional laptop in 6 months
- can dock for more traditional setup

### Instagram
- lanched on a single closed platform in 2010
- acq by fb for $1b
- THEN launched a webapp
- firmly planted in Apple's walled garden, with no api in place
- what went so wrong?
  - IMO: uploading photos is annoying, upload from where i take it, and android cameras suck (quality upper bond), needs to generate buzz, apple is already a "club" (NODA)

### why web apps?
- no installation step
- no approval needed
- can easily push updates
- first class mobile experience: have to build an app

### Future of Web Apps
  1. you visit a URL
  2. sometimes you bookmark the url
  3. ... (there is no step three)

- no middle man
- no app store

### Leveling up the Web
- need to upgrade the web platform to get it up to par
- what is left to achieve parity? Three roles which need leveling up
  - user engagement
  - user experience
  - developer experience

### User Engagement
- web not engaging as apps
- offline is a big problem for web
- potential solution: *Service worker*
  - between network and app layer
  - app can respond to network requests
  - can have fallbacks, pull from local if offline, etc
  - background thread/processing
- push messages (from the server)
  - have small things link toast
  - chats, replies, breaking news
  - need something that work 
  - can use service worker
- payments
  - app stores take cut from developers and charge users through account
  - *request autocomplete*: one set of cc credentials

### User Experience
- speed
  - load time too long
  - 300ms touch delay
  - garbage collection
  - janky scrolling
  - blink team 2014 goal: improving local performance
  - azure @ mozilla: compile js
- responsiveness
  - one app for all devices
- storage
  - let apps take up storage
  - now: popup asks for permission
  - maybe evict based on inverse of frequency of use
- system integration
  - need access to homescreen, task manager, notification center, etc.

### Developer Experience
- better base primitives
  - mutation observers on the dom, and obj observe in js
  - shadow dom, better encapsulation
  - animation interface
- powerful application frameworks
  - e.g. Angular: better html for webapps
  - e.g. Ember: based on Coco, which is tried and true
- modern layout techniques
  - flexbox, grid ... duh
  - shouldn't need clearfix, display none, and other hax
  - maybe render stream and doc stream completely decoupled
- more hardware access
  - control your robots from your computerphone
  - geolocation is there, but geo fencing is not
  - Mozilla, FF OS is a step in the right direction

### Conclusion
- we need to defend against closed app ecosystems
- web is open and collaborative

---

## BeagleBone Black: The versatile JS underdog | Kassandra Perch (10:50am)
- open source hardware platform
- similar to rasberry pi but ...
  - can ssh irectly
  - analog output 8x
  - accessble pru microcontroller
- js is a first class citizen
  - node is pre-installed (cloud 9 on port 8000)
- libraries
  - bonescript: procedural
  - beaglebone-io: johnny-five wrapper, evented, new 

### downsides
  - hard to get ahold of (adafruit?)
  - non-js community side of things is not as strong
  - johnny-five + arduino

### But I don't know electronics
- inputs: 3 wires, input, groud and power
- outputs: 3 wires, input, groud and power
- *Fritzing diagrams*
  - cad tool
  - lookup components

### DEMO!
- npm module for open pixel control/LED scape
- programatically set a frame/pixels

### What's next?
- angstrom -> debian
- Beaglebone-IO under development
- open-pixed-control underdevelopment

### Conclusion
- you can do robots too!
- good starting point: arduino + Johnny-Five

---

## Siphoning Energy from the Pocket Universe in JS | Drew Petersen (11:20am)
- [github for demo](https://github.com/kirbysayshi/multithreaded-game-example)
- 60 fps === 16.667ms/frame
  - original NES was 60fps
- don't jank out
- Ideal Game loop
  - hardware says go
  - update everything
  - draw everything
- loop in the browser
  - browser stuff
  - process input
  - update (minor GC)
  - draw everything (message only)
  - more browser stuff (layout, etc.)
- Current state: Compromise
  - make games less complex
  - implicit exclusion of users on low and mid range hw

- making a game is like creating a whole new world...but how?

### Web Workers
- HW threads in Js
- high level api
- not guaranteed to get one
- register worker nad listen to events from worker
  - no dom
  - lacks percision

- example threads
  - broswer thread
    - process broswer
    - dispatch input worker
    - listen to events

  - worker thread
    - update world
    - handle collisions
    - update physics
    - ai

### DEMO! : single vs double threads
- single ~ 40 fps, double ~ 60fps
  - rendering + work
  - work is slightly different (send message or not)
  - renering code is the same!
- browserify + workerify: isomorphic!
- Entity system
  - factory for stuff
  - messaging between app and worker
- snapshot
  - read/write entities
  - do not need custom data struct, serializing an obj
  - e.g. corgi!
  - create snapshots, collect, and send em out to the world
  - not a lot of worker messages over bus
  - one big message better
- when render code recieves message (web workers async), enque handling of it

### render + worker
- web worker emits snapshots only every 33ms
- render loops every 16ms
- does render draw everything twice?
- Demo: 16ms render + 33ms worker = jitter!
  - interpolation!
  - hang onto last two snap shots
  - compute an intermediate step
  - renders one step behind, but visibly smoother

### Another Demo: why?
- now with 2000 circles
  - single threaded: 14 second to compute for physics
  - double threaded: 4 second to compute for physics
  - blocking prevents controls until compute finished
  - async keeps browser responsive

---

## LUNCH

---

## Road to Web Components | Tom Dale (1:30pm)
- etymology of "Web Components"
  - web: internet
  - com: serial ports for windows
  - ents: tree people from LOTR
- web components allow you to declare your own html tags
  - appearance: html + css
  - behavior: js

### What Components Are Not
- "With React, angular and ember aren't needed, they're zombies anyways" -HN

#### Polymer
- Google project
- polyfill for building web components
- "build anything"
- "hype cycle"
  - technology trigger
  - peak of inflated expectations *Web Components are here*
  - trough of disillusionment
  - slope of enlightenment
  - plateau of productivity
- web app = Models + State + [components]

#### defending routing in the client
- "flows are just as important as individual screens are" - Ryan Singer (Basecamp)
- can move away from server only routing (Rails, Django, etc)
- web app = modles + [states] + [components]    // many models and many states to manage
  - many states and many components 
- components don't handle flow between components

#### URLs
- urls allow access to any point of application
- need to preserve state?

#### Conclusion
- **Great way to build components, but just that**


### Benefits of Components
- why it is good
  - Reusable
  - Isolated
  - use HTML
  - Reduce development time 99%
  - Google pays $10 per Web Component in app (*BEES!*)
- [Extensible Web Manifesto](http://extensiblewebmanifesto.org/)
- Data-bound elements
  - HTML is the og data bound object
- Bridge components
- Inter-operability
  - Promises/A+
  - shared test suite
  - Q, RSVP, Sparrow | Promises/A | DOM Promises | Q.async Task.js | async function
- Bridge Ecosystems

### Using Components Today (in Ember)
- Super Easy
- Amazing Tooling

#### DEMO
- ember cli
- add to component/, same name as component (handle bars)
- apache ssi
- components support two way binding out of the box
- no javascript!
- es6 modules, js file by the same name
- Chrome, Firefox extension for tooling: Ember Inspector
  - can change data on obj and state of page will reach

---

## Backbone.Marionette and RequireJS | Daniel Cousineau (~2:10pm)
- ...
- factories for building ui
- rendering modules is self contained
- single page app
- single package javascript function
- unified controller system
- *idempotent*
  - method with zero side effects
  - can be called repeatedly and always gets same results
- good idea to build idempotent modules 
  - Don't do this: `$('.some_class').doStuff()`
  - use View's element to do work and bind events
- preload data to prevent Flash of Unstyled Content
- almond js: require.js without async loading?
  - just defines "requires", "define"
- small-ish js file prevents flicker
  - js (1.3 Mb) -> min + gzip -> js (120 kb)
  - minimal flicker
  - after first page load, hits cache
  - single page app is maintainable, quick, and useful!

### Refs
- [Books by David Sulc](https://leanpub.com/u/davidsulc)

---

## The No Build System Build System | Peter Müller (2:35pm)

### Development Lifecycle
- old cycle
  - development iteration
  - deployment with FTP

- new cycle
  - boilerplate / bootstrapping
    - yeoman
    - html5 boiler plate
  - development iteration
  - package management
    - bower
  - build & optimization (*build system*)
  - deployment

### Development Loop
- editor
- authoring abstractions
- livereload
- browser

### Why a build system?
- Transport
  - *bandwidth*: compress assets
  - *latency*: bundle assets
- performance is necessary first step for a good user experience
- dev code !== production code
  - human readable vs computer readable
- No build system (in development step)

### Automation
- **Grunt**
  - task runner
  - combine tasks to create a build system
  - tasks configured in parallel
  - lots of configuration, each io is specified
- **Gulp**
  - takes input, pipes to next task
  - less file io
  - input >> step >> step >> output
- unix tool wrappers
  - make
  - jake
  - rake
  - ant
  - maven
- treats files independently out of context
- A website is a dependency graphy
  - does not work well with paradigm of stream of files

### Problems 
- Discovery
  - generally write a manifest
  - write dependencies as a list and manually maintained...not good
- Coherence
  - incoherent dependency graph
  - leaking details of transport into development
  - file renaming, bundling, spriting, compression
  - Sass imports don't do not explicitly declare includes per file

### Not Provided: build system has to act like browser
- asset graph: website in, website out
- graph model which attempts to map all sites assets
- each asset is stored in memory
- solves problem of discovery
  - resolves dependencies and relationships
- solves problem of coherence
  - manage files through graph functions
  - updates references
- once you build a graph from your website, serialize output

### How can we use this?
- do it yourself
  - asset graph is extremely abstract
  - difficult, new paradigm
  - difficult, lacking documentation
- use our tools
  - assetgraph-builder
  - very opinionated: how to build spa
  - grunt wrapper: `grunt-reduce`

### Promise
- don't need to configure
- works out of the box, like a broswer

### TODO MVC Challenge
- [page](http://mntr.dk/todomvc-challenge/)
- based on Tastejs [TODO MVC](https://github.com/tastejs/todomvc)
- trying to use assetgraph with Addy Osmani TODO MVC examples
- 40% success rate with zero config other than pointing at index.html
- tracking bugs and iterating
- current status: 80% sucess!

### YABS?
- just make it work in the browser

### DEMO
- build and host an mvc demo
- build visual representation (force directed graph) of asset graph
- ???
- expush
  - express middleware
  - spdy-push


---

## Greenfields and Front-end Style Guides | Mark Wunsch (3:30pm)
- this is a people and an organization
- works at Rent the Runway
  - halfway between ecommerce and "hotel"

### Prelude
- documentation is dead, long live documentation
  - "old style" is not maintainable
  - living document
  - warning: JSLint will hurt your feelings
  - Design Linter?
- Vulcan: Roman god of Neck Beards
  - "Apollo in the forge or Vulcan"
- Need some Tooling

### Surverying
- Greenfield Work
  - no work before
- Brownfield Work
  - land used previously for industrial purposes

#### The DOM holds the truth
- Demo js
  - walks dom
  - copies node
  - gets and applies computed styles
- Demo coffeescript
  - takes url
  - uses phantom js
  - remove from parent node context
  - render and show markup to get demo
- simple audit shows discrepencies
  - same data shown 3 different ways

### Collaborating
- you are the styleguide
  - lead them through the hell that is web development
- photoshop
  - BANE of every developers' existence
  - worth of that artifact approaches zero as code makes it production
  - great for presenting to executives
  - not so great of developers, who have to build the UI
- designers should not have to know about SEO and CSS box models
- styleguide is a contract between designers and developers

### Scaffolding
- "The Living Document"
- this is the product of this effort
- goes back to the DOM, since everything will be rendered as a DOM node
- *Encapsulation*
  - missing from OOCSS
  - e.g.
      <div class="wrapper">
        <div class="ui-shibboleth clrfix">
          <div class="hidden"></div>
        </div>
      </div>
  - markup has style info littered all over it
- Web Components
  - allow for encapsulationn for components
  - Polymer
  - suited for styleguides
  - expose interface w/o exposing implementation details
- Polymer
  - build custom web components
  - can rely on elements instead of a living document

### Conclusion
- styleguides are not enough
- the contract is the elements, not a guide
- living libraries

### Questions
- performance, Steve Sounders on Web Components?
- cross browser compatability?
  - FROM DOCS: only target IE10+, NO IE8 support due to insufficient DOM api
- performance on page load?
- how does it fit into build process?

### Appendix
- brad frost: atomic web
- 24 ways front end style guide
- 24 ways design systems
- a list apart creating style guides
- OOCSS, SMACSS

---

## Gadgets for Holistic Web Detection | Eric Shepherd (4:10pm)
- 2006 example of mobile web 
  - unminified script in the head
  - moo effects
  - sending down to palm pilot
  - seems naive but we still do some of this
  - web fonts, heavy sites etc

### Device Detection
- you're on a phone, let's send you to m.
- you're on a tablet, let's send you to t. ??
- you're on a desktop, let's send you to the site we actually put all our time and money into
- feature detection
- use all of these detections: device / feature / resolution

### Resolution detection
- breakpoints
  - they use max / min
- needs buy in accross entire workflow
- make sure names match what they are
  - good: wide, med, small
  - bad: tablet, iphone, desktop
- design to smallest design
- IE 7/8 does not support breakpoints
  - polyfills!
  - respondJS
    - cross origin concerns
    - loads css as text/only applies styles with JS
  - picturefill
- Preprocessor: DRY vs DOY
  - Don't Repeat Yourself vs Don't Override Yourself
  - Nesting is an antipattern
  - Mixins === bricks, media queries === frame
- (?) can overriding create the same or more amount of css as repeating and isolating

### Device Detection
- perpendicular to resolution and features
- its about *power*
  - how powerful is the device
  - want breakpoints same as styling

#### Breakpoints for Devices
- "Target Experiences"
  - Minimal: baseline, IE7, unknown, mobile
  - Intermediate: ipad, tablet, IE8
  - Full: desktop browsers
- What do we send to browsers
  - html
  - css/fonts
  - javascript
- HTML
  - wrap dom in a conditional block in template
- CSS
  - send it all down the wire
  - use target experience as a class identifier
  - might not include heavy styling (transforms, transistions, etc)
- JS
  - smaller bundlers
  - AMD modules

#### JS: Expectations for Minimal
- simple utility - be identical
- complex utility - do less
- third-party code - should not wire up
- DOM component - nice fallback
- e.g. Carousel
  - dom fallback is div with overflow scroll
  - remove 1000 lines of code for minimal
- augment define to take a fourth argument, which specifies which target experience
- What happens
  - lazy loading
  - create 3 bundles
    - main.full, main.intermediate, main.minimal

### Feature Detection
- only using it for what it is meant for
- granular control
- modernizer
  - css classes
  - js

### Combining
- resolution and detection: 4 x 3
- many more when considering features as well

### thoughts
- only browser can resize
- maybe targeted CSS is not bad, granted you provided a good mixin


---

## Lesser Known Debugging Techniques | Amjad Masad

### How far have we come?
- started with VBA scripting, which provided a console
- `document.write("hello world");` ... and nothing
- 'Done' Icon...maybe it will tell me something
  - cryptic message
  - a lot of frustration

### Code that is easier to debug
- lambdas are fun, but hard to debug
- closures hide their state really well
  - can use a class, but can inspect from the outside
  - closure method, cannot see or change internals
  - can't monkey patch closures
  - can also use lambda calculus to compute: increment + counter functions
- make classes and objects are accessable from console
  - start things from the console
  - quickly set breakpoints and monkey patch


### Tips and Tricks
- always be debugging
  - have the program in a runnable state
  - split big changes into small steps and validate as you go
  - breadth first > depth first
  - keep the momentum going, b/c it's rarely broken
- change and break things
  - take bold steps
  - change things in the debugger, learn as much as possible
  - lean on tools
- live edit
  - fix mistakes without reloading
  - implement features without reloading
  - add conditional debugging

#### setting up traps
- in large apps, hard to track what does what
- can step debug all code
- need a way to break into actions
- break on method calls
  - can't set a breakpoint on native method calls...no access to source
  - need to know source for the method...can be hard to find
- break on custom events
  - monitor events on an element: `monitorEvents(elem)`
  - on change -> debug
- break on property access
  - WTF changes
  - setters and getters
- break on callbacks
  - similar to custom events
- break on DOM Mutation Events
  - can be done from devTools (rt click)
  - no fine grained control (e.g. cannot break when node added)
  - async callstack (no callstack, except chrome canary)
- break on Object Mutation
  - in canary under a flag
  - `Object.observe`
  - break on property add, delete, change
  - async callstack isn't quite working yet

### The Tools
- The command line api
  - `$0` : current element
  - `$(selector)`: get access to elements
  - `monitorEvents(elem)`: watch events
  - `getElementEvents(elem)`: get all event listeners for an element
- undocumented apis
  - `debug(fn)` : break when function is called
  - `monitor(fn)` : log when function is called
- debug utils
  - $duv(object, event)
  - $dug(object, prop)
  - $dus(object, prop)      // setting
  - $dum(object, function)  // nextime
- Problems with live edit
  - not flexible
  - doesn't support remote file systems
  - does not allow build step (e.g. coffeescript)

### introducing *flo*
- open src from fb
- live edit js, css, images
  - does not refresh the page when recompiling
- supports build step
- ??
- why *flo*
  - lots of js goodness
  - reloading and geting to the user flow takes a long time (load, click, click...)
  - complex dev env
- how?
  - server and client components
  - server is npm module
  - client component is a chrome extension
  - [link](facebook.github.com/fb-flo)

### questions
- setup intended for dev only?


---

## Code Memes | David Byrd (5:15pm)
- Meme
  - "An idea, behvior or style that spreads from person to person within a culture"
- Goodwin's Law
  - length of discussion proportional to probability of Nazi/Hitler reference
- Github issue
  - grows longer, debate about syntax
- JavaScript has weird shit
  - any group of unicode chars can be function name
  - nothing is really true

### Weird -> Cool
- example: jQuery
  - $('*').loves().chaining().and().not().worrying().about().ie()
  - $tyle : we can do a lot of jQuery in JS
- no `.contains()`
  - `[1,2,3].indexOf(2) !== -1`
  - all numbers are 16 bits
  - -1 turns into 0, only number to do so
  - `~[1,2,3].indexOf(x)`
  - `~`: bitwise not
- JS is so ghetto, we can make stuff up
- "The Wheel"
  - `if(x) y()`
  - default: `var name = x || "David"`
  - safeguard: `x && x.y()`
- `"a".concat("b")`: works but slow
  - `"a" + "b"` : this doesn't make any sense
  - `["a", "b"].join("")` : better

### The future
- "javascript is too important to be left to the experts" --someone
- make more memes with javascript




