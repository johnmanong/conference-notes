# Design Strategies for JavaScript API
## Ariva Hidavat

- "how to design a good api and why it matters"
- "java is not javascript, just like horse is not horseradish"
- modular architecture introduces interface
- nobody reads docs
- code written once and read many times
- readable, consistent, crystal clear (duh)

- strategies for good api
  - static polymorphism
  - dangerous convenience
  - confusing semantics

## static polymorphism
- mixed element form
  - radio -> value
  - checkbox -> option
  - button -> caption
- make them all value
- slider vs progress bar
  - slider has min, max and val
  - indicator has range and progress
- moving shapes
  - point.translate()
  - rect.translateBy()
- defining a rect
  - one constructor takes objs, corner and dimension
  - another takes coordinates of all four corners
  - solution, first two points, second dim
- var x = NaN, isNaN(x) -> true, x === NaN -> false

## convenience and traps
- romeo and juliet are not js developers...names are important
- can create event from one line (true, true, null, null, false, false, 0, 9)
- boolean trap
  - Slider(true) -> horizontal
  - Slider(false) -> vertical
  - easy to write, impossible to read
  - better to create option object with semantic key 'orientation'
- boolean modifier trap
  - adding boolean to params is bad
  - e.g. true/false to animate or not...how is anyone supposed to know?
    - again option obj would be helpful here
- if one boolean is bad, then two is even worse...more is **even** worse

## ambiguitu begets insanity
- double negatives
  - disabled = false or enabled = true
- write about whats there not what isnt
  - translucent 20% <-> opaque 80%
- non-verbal actions
  - status.message()     -> message is a noun and verb
  - status.showMessage() -> better
  - js substr()
    - `'fluentconf2014'.substr(6, 9)` -> 'conf2014'
    - `'fluentconf2014'.substr(9, 6)` -> 'f2014'
    - `'fluentconf2014'.substring(6, 9)` -> 'con'
    - `'fluentconf2014'.substring(9, 6)` -> 'con'
    - `'fluentconf2014'.slice(6, 9)` -> 'con'
    - `'fluentconf2014'.slice(9, 6)` -> ''
  - array extraction
    - splice and slice
    - immutable vs mutuable
- verbal actions
  - point.translate(), s.trim()
  - do these return the new value or change my point/string?
  - trim and trimmed to specify the behaviour

## best practices
- make everything private by default
  - once its public you can't take it back
- justify the need for public
  - write at least 3 examples
- mandatory api review
  - "you'd fail your first two attempts anyway" -Ariva Hidavat
- API tools
  - tools seperate us

## API detective
- TDD, BDD, PDD (ahhh yah)
- need to review the choice of names in api as well
- syntax parser
  - create meta-data, meta-object
  - detect boolean traps
  - blacklist function names
- future api cop
  - call an immutable function and never use return value
  - check the value of something 2000 times and not another time...

## conclusion
- apply static polymorphism
- judge every shortcut
- read aloud and often