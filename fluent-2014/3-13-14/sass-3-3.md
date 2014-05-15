# The mindblowing power of sass 3.3 (12:00pm)
## Chris Eppstein (LinkedIn)

## New SASS Features
- Sass 3.3 was released last Friday!
- features
  - source maps
  - string functions
  - map data struct
  - meta scripting
  - extended use of & in selectors
  - @at-root
  - variable scoping

### source maps
- additional file which maps from generated code to source
- pass flag to sass or set "sourcemap = true" in compass config
- set up workspaces
  - ad folder
  - rt-click and set map
  - point at .css (not .scss)
  - live edit in chrome
    - saves to disk
    - can set watcher to recompile
    - chrome can act like live reload
- source maps are just json files

### string manipulation functions
- is quoted, length, lcation, insert, slice, upcase, downcase
- e.g. function to capitalize, camel case

### map data structure
- syntax = (key1: value1, key2: value2)
- functions
  - map-merge()     // overwrites pre-exisiting keys
  - map-keys()
  - map-values()
  - map-get()
  - length()        // number of keys in the map
  - nth()
- maps are ordered
  - order set when first inserted
- e.g. can hold breakpoints in map
- can use media queries in extend
  - @at-root selector

### metascripting
- can use call(fn name, args)
  - can store funciton in theme map
  - all functions which variable name

### expanding the use of &
- can use & to string concat selector
  - e.g. .module { &-header: {} } -> .module-header
- can be used to dry up SMACS style

### @at-root directive
- takes you out of context

### variable scoping
- before 3.3, only global scope
- variables in mixin will shadow global var
  - can still overwrite the global appending "!global"
- will give you a warning right now

## New Compass Features
- compass features
  - compass prefixing

### compass prefixing
- graceful usage threshold: 0.1%
- debug browser support: false