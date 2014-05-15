# Inside JavaScript Execution (4:30pm)
## Chase Douglas (New Relic)

# focus
- when to optimize
- object specs
- function optimizations
- primitives

# when should I worry about optimizations?
- code execution frequency
- "hot" code paths

# plain olde objects
- key/value pairs are string literals
- properties and values stored as hashmap
  - "propName" >> hash() >> index >> array[index]
- what happens when you get a key collision in hash function
  - linked list in array

# array objects
- `var myObj = [5, "a", "two"]`
- values are stored as a linear list in memory*
  - *converted to a hash map when values are far away
  - `var myObj = [5, "a", "two"] myObj[1000000] = "ooopsies"`
  - keeps memory footprint under control
  - performance takes a hit

# objects with arrays and properties
- `var myObj = [5, "a", "two"]; myObj.prop1="hello"`
- *Hashmaps stink!*
- want arbitrary properties, but don't want overhead of hashmap

# object classes
- declare function with class name

    function MyClass(x,y) {
      this.x = x;
      this.y = y;
    }

- instantiate via: `var myObj = new MyClass(5, "baz")`
- engine will allocate memory for class and properties
- but we can arbitrarily add properties
  - `myObj.z = "Oh noes"`
  - would not be found when looking up MyClass object
  - still adds it, but it keeps track that it's different (MyClass*)

# runtime optimizations
- repetitive invocations of simple function with different arg type
  - optimize when called for the same arg type
  - deopt when a different type is detected

# polymorphism is bad!
- always send same types into functions (Monomorphic functions)
- engine has to track MyClass and MyClass* differently

# objects vs primitives
- objs stored in memory as pointer
- primatives are stored directly in memory (faster access)
- primitives:
  - strings
  - booleans
  - numbers (sometimes)
- "boxing primitives"
  - `var a  = "str"; a.x = 5`
  - js can add properties to do anything
  - now it has to track a pointer to string and property
  - *be kind to your primitives*
  - **don't do this**

# numbers
- sometimes they are primitives
- all numbers are double-precision floating-point values
- 53 bits (top 11 bits are 0)
  - otherwise 'NaN'
- x86-64 memory address up to 48 bits
- 2^64 - 2^48 > 2^53
- can fit both numbers and properties side-by-side
- 'NaN-boxing'
  - if first 11 bits are 1, it's a number
  - if first 11 bits are 0, it's a pointer to an object
- 'Nun-boxing'
  - if first 11 bits are 0, it's a number
  - if first 11 bits are 1, it's a pointer to an object
- adding the '1's in front has cost, choose which would be accessed more to assign 0 or 1s in front
- what about v8?
  - 'crankshaft'
  - performs optimizations at runtime
    - type inference
    - loads values into registers
    - ...