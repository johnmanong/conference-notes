# Unpacking Technical Decisions (3:30pm)
## Sarah Mei (Ministry of Velocity)

# intro
- we don't make large technical decisions often
  - which javascript framework should we be using?
- repetition is important tool for human learning
  - do the action
  - analyze the results
  - change the action
  - see if it changes the outcome
- frequency: lowest to highest
  - languages
  - frameworks
  - libs
  - everyday code decisions
- we'll look at how people eval gems
- e.g. need a gem for http requests, two canidates
    - HTTParty
      - static methods
      - can include
      - add http call functionally to your object
    - Faraday
      - return new obj
      - make calls on obj
      - keep hyyp functionality in a seperate object
- how to eval gems? (ruby)
  - readme (github)
  - frequency/recency of commits (github)
  - number & age of issues (github)
  - comments on issues and pull requests (github)
  - number and recency of tutorials/blog posts (Google)
  - ...

# main themes
  - interface
    - e.g. readme
  - activity
    - e.g. commits, issues, etc
  - popularity
    - e.g. SO, HN, Google
  - Familiarity
    - e.g. look at code

## java and javascript
- java server faces, google web toolkit, dart

### angularJS
- written by java programmers
- dependency injection
- follows similar programming paradigm as java frameworks
- more familiarity, less risk to adoption

## four quadrant model: The Mei System

### interface
- internal
- project

### activity
- external 
- project

### popularity
- external
- people

### familiarity
- internal
- people

- "A chang ein perspective is worth 80 IQ points" - alan kay
- and 5 yrs experience - mei