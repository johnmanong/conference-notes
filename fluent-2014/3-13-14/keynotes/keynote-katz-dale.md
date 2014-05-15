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

