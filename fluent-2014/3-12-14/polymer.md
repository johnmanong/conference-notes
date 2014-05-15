# Polymer: Web Components in Action
## Eric Bidelman

### the web 10 years ago
- elements were building blocks
- e.g. select element
  - default ui
  - html attributes
    - disabled
    - selected
    - size

- elements are composable
- elements are programmable
- so what happened?
  - 'div soup'
  - tags in the browser are noe expressive enough

### web today
- markup side is behind
- building tab components
  - many ways to do it
  - markup and js
- want to get back to expressive markup
- web components are getting us there

### what are web components
- set of emerging standards
- allow extending HTML
- extend functionality
- web components
  - templates
  - custom elements
  - shadow dom
  - html imports

### what is polymer
- library uses latest web tech to create custom html elements
- layers of polymer
  - Native: already baked into the broswer
  - Platform: web component polyfills for all modern browsers
  - Core: opinionated way to work with Web Components
  - Elements: reusable custom elements (in progress)

### using elements
- 'everything is an element'
- set of ui components
  - cards, accordian, toggle, tabs, etc.
- elements which dont render ui
  - layout: grid, flex
  - view: media query, page
  - services/libs: shared libs
  - data: local storage, xhr
  - ...

### maps demo (video)
- prototyping tool
- data binding feature in polymer
- no js code
- all the work done by elements team

### creating elements
- declarative element registration
- use 'polymer-element' to declare custom element
- style encapsolation
- can include script as well
- the mental model changes when building in components

#### data-binding
- double mustach syntax
- can set data in js
- can publish properties so users can configure elements

#### declaritive events
- 'on-' syntax for event listeners

#### automatic node finding
- use shadow dom to find elements
- can get at things internal to the element

## platform
- build on evolving w3c standards
- set of polyfils which you can use any browsers
- additional features:
  - mutation observers
  - pointer events
  - web animations
- touch for free!
- bower install polymer platform
- `<script src="platform.js"></script>`
- eventually this layer will go away, native will replace

## conclusion
- polymers large molecules made up of monomers
- web apps are a collection of web components with many sub elements

## Questions:
- broswer compatability with polymer
- organizing pattern libs/documentaion
- plays nice with angular?

- including in project
  - bower
- production ready? 
  - yes/no stds are changing, some apps in produciton
  - modern browsers just work
- shadow dom
  - no jquery in components...doesn't make sense
- testing?
  - early days, still exploring end-to-end workflow
  