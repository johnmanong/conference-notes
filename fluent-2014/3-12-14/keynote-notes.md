# Speed, Performance, and Human Perception (10:35am)
## Ilya Grigorik (Google)

- performance is important at all layers
  - parsers, lexers, render ...
  - gpu acceleration, multicore, ram ...
  - latency, bw, protocols ...
  - js speed, gc perf ...
  - selector matching, layout, painting ...
  - visis, enagement, conversions ...

- context specific
  - in a game, 10ms can be crutial
  - on an ecommerce site, 10ms is not a big deal

- perfomance tends to be focused on the hardware
- wetware (brain) has its own interpretation of perfomance and quirks
  - 0   - 100ms  : instant
  - 100 - 300ms  : slight delay
  - 300 - 1000ms : task focus, noticable
- vision
  - 24 fps (~40ms) : minimum for stutter free
  - 60 fps (~16ms) : silky smooth
- audio
  - 1+ ms jitter
  - dropping packets is ok in this case

- perceived performance
  - actual performance (hardware/software)
  - expected performance (wetware)
  - ux (glue)

- hacker news
  - technically fast
  - < 500ms render
  - small assets
  - user experience sucks
    - need to zoom to read
    - takes 5 - 10s to actually accomplish the task

- *What are the primary user tasks for your applicaition? What is the time to task completion?*
  - not just page load time
  - how long until its *useful*

- early day of blogger
  - time to create blog was really fast
  - user *expected* this task to take a long time
  - percieved as a lot of work by user (user spent time and commit)
  - users thought it was broken bc it happend too fast
  - added spinner and did nothing for a bit
  - user satisfaction goes up!

- simple example: users to query db
  - some queries fast (indexed)
  - some queries slow
  - random wait times are frustrating
  - can provide meaningful feedback to user

- Precieved Performance = f(Expected Performance, UX, Actual Performance)
- Experience = f(Preceived Performance, Task Completion)

- steps
  - what is the user trying to do?
  - what is the expected performance?
  - what are the techical performance issues?



# The Humble Border-Radius (10:15am)
## Lea Verou (independent)

- border-radius is cool
- value specifies the radius of each corner
- can specify each corner seperately
- what happens when the corder radius > height, width?
  - the browser keeps the *ratios* of the border-radii the same
  - can make circles
- can you make an elipse?
  - no cannot make it out of parts of circles
  - can specify ratio in value of border-radius
    - e.g. 270px / 210px -> elipse
  - not very scalable
  - can also specify ratio
    - e.g. 50%
  - half of elpise
    - 50% / 100% 100% 0 0
  quarter
    - 100% 0 0 0
- can make lots of shapes with border radius
- can animate border radius
- text wrapping does not follow border radius
  - can add padding
  - no solution other than this
  - future: shape-inside: content-box
- js reporting values
  - firefox: reads actual values
  - others: assigned value
  - ems converted to pixel
- corner-shape is proposed
  - allows a lot more shapes possible
  - e.g. bevel -> polygons
  - can emulate with linear gradient for bevel
  - radial gradient can emulate "scoop"


# Virtual Machines, Javascript, and Assembler (9:45am)
## Scott Hanselman (Microsoft)

- neckbeard: when you do anything for 40 years
  - how do you explain the web to someone who has strong programming background, but no web
- "I think there is a world market for maybe five computers" -Thomas J. Watson
- virtual machine: lie about the hardware and move it around
  - infrastructure as a service
- Microsoft Azure
  - a little behind
  - has ascii art
  - open source and on github
- web site > cloud app > virtual machine
  - can't have house party, but you can trash our hotel room every night
- cloud
  - elastic, easy to scale
  - any language
- netflix cheif arch at netflix
  - "...we pushed a button and then we were in europe" --Netflix CTO
  - kid starts talking about ssd reliability
  - "I don't care, I'm renting them"
- history of the web
  - world wide web 25 years ago
  - java vm, microsoft silverlight, adobe flash
  - really want traditional os arch in browser
  - why do we want these vms?
  - javascript
    - limited usefulness...
    - commadore 64 basic vm in browser
    - virtual machines in browser
    - js is an os
- Atwood's Law: any application which can be written in javascript will be written in javascript
- html is the structure
- css is the stylin
- js is everything else
- "js is the assembly language of the web" -Scott Hanselman
- "no one writes javascript anymore, they write jQuery" -Jake Weary
- use the vms in the server and the phone


# Reading, Writing, Arithmetic ... and JavaScript (9:25am)
## Pamela Fox (Khan Academy)

- works for Khan academy
- teaches using JS and processing.js
- visual programming

- first challenge stats
  - why do younger students not complete the first challenge?
  - 13 year olds ~82% completion (89% max)
  - require spacial reasoning

- first logic challenge
  - bouncing ball demo
  - much fewer young students (~50 8 year olds)
  - concepts got harder?
  - conditionals and comparators
  - temporal and spacial reasoning
  - 13 year olds ~73% completion rate

- a reasonable conclusion
  - 13 year olds can learn JS and processingJS
  - start with simple programming , games?
  - can use js to learn other subjects (lit, phyics, etc)
  - go on to do computer science, other areas and apply skills, or just be a more productive human being


# Javascript: Taking the high and low roads (9:05am)
## Brendan Eich (Mozilla) 

- low level changes
  - int64, 32 bit float
  - SIMD (parallel computing)

- high level changes
  - shouldn't need libraries

- [Extensible Web Manifesto](http://extensiblewebmanifesto.org/)