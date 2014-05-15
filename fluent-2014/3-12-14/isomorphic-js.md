# In pursuit of the holy grail: Building Isomorphic Javascript app
## Spike Brehm


# intro
- isomorphic js can be env agnostric
  - no broswer or server specific code
  - e.g. handlebars
- isomorphic js can be shimmed for envs
  - window.location.pathname vs. reg.path
  - e.g. superagent
    - client side request: jQuery ajax
    - server side request: http lib
    - unify these calls

# isomorphic use cases
- templating (gateway drug)
- routing
- l18n (internationalization)
- date and currency formatting
- model validation
- api interactions

# isomorphic libs
- underscore.js
- backbone.js
- handlebars.js
- jQuery
- Moment
- React.js
- polyglot.js (l18n)

# why go to the trouble?
- performance
  - initial page load speed
  - can download html on initial page load
- SEO
  - crawlable spa's
- Maintainability
  - reducing code duplication
- Flexibility
  - run the code where you want

# progression of code org
## old days of the web
- fat server, thin client
## circa 2011
- thin server (api), fat client
## the future
- fat server, fat client

# arch tradeoffs (little bit of sharing vs all shared)
- few abstractions / many abstractions
- simple / complex
- instagram (react) / asana (all js)

# how to isomorphic
- magic is in the build process
- browserify and grunt
- broswerify
  - require() in the browser, resolves
  - package commonjs modules

