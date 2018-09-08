EczemaScript:

Too Long Did Read of : https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript (a very nice page)

Types:
  Number, String, Boolean, Function, Object, Symbol (ES2015)
  
  Symbol: unique identifer, with description passed, https://javascript.info/symbol
  
  + undefined & null
  
Some descendents of Object: Function, Array, Date, RegExp

& some Error types

Not got any hecking ints. It's 64 bit doubles (but probably not when optmized the jit-ed).
Watch out for all the standard floating heckery.

All stanard mathy stuff.
Math object with functions & constants.
+ parsing crap (parseInt, ect).
or parseInt(string, base)

Because JS is nuts & has type coercion: + '5', is a valid way to parse a string to int.

Strongs:

Unicode (UTF-16 code units).

Other:

js distinguishes between null & undefined

null: deliberate non-value
undefined: not yet defined

Vars:

declared via: let, const or var

let:
  block level scope
  (the for(..) is counted as in the loops block)
  
const: vars that never change

var: variables scope is the function it was declared in (no block scope)
  
  
Operators:

  +, -, *, /, and % (which is remainder not modulo)
  (and the standard ++, --, +=1, ect)
  
  Some like + work on storngs too
  

Comparisons:

  <>, <=, >= (for strings & numbers)
  
  Equality was broken at first: 123 == '123' (true)
  So ===, & !== fix that: 123 === '123' (false)
  
Control structures:

- All you would expect from C
- Also 'of' & 'in' loops
    'of' - iterates over iterables, (listsm strings, arrays, ect)
    'in' - iterates over all non symbol, enumerable properties of an object.

- can short circuit logic like C
- switch also works with strongs

Objects (in JS):

  name value pairs.
  Similar to hash tables, or dicts in parseltongue
  can acess with dot or [] notation
  

Arrays:

  fairly normal
  
  has the new .forEach stuff
  

Functions:

  Normal:
  function add(x,y) {
    return x + y;
  }
  
  Dumb stuff: no void functions, no return just returns undef
  If you provide less or more params it won't care & try to do something.
  Though functions can see all args they were called with via the `arguments` array varible they have.
  

  `arguments` can be renamed by "rest" syntax
  e.g. function avg(...args) { /* stuff */ }
  
  can all a function with an array for it's params by using .apply()
  avg.apply(null, [param1,parm2]) // where avg is a function. (the first arg is prolly some kind of instance).
  or using the spread operator where the function call could be (if you wanted) avg(...[param1, param2])
  
  
  anonymous functions can be created.
  
  `function avg() { ... }` is the same as `var avg = function() { ... }`
  
  
  How to call anonymous functions recursively:
  named IIFEs:
    e.g. var recursive = (function namedRecursiveFunc(stuff) {
                            namedRecursiveFunc(stuff);
                          })([1,2,3]);
  
Custom Objects:
  
  Not class based, prototype based.
  
  Good custom object (with methods) practice.
  
  function Thing(name, crap) {
    this.name = name;
    this.crap = crap;
    this.thingify = function() {
      return this.name + ' is a thing';
    }
  }
  
  `this` keyword: current object? Unless called in an other way than dot or bracket notation.
  
  Making the object e.g. `var myThing = new Thing('A', 'B');`
  This is just sugar. What it does is create a clean object, then call the function Thing with this bound to that object.
  That object is modified by the Thing function, and then `new` (not Thing) returns it.
  
Where the scary `prototype` crap comes in:

  Don't want to create new method functions each time for every object. (werid that it does that, but it is JS(tm)).
  
  So you could just move the functions out:
  
  function thingThingify() {
      return this.name + ' is a thing';
  }
    
  function Thing(name, crap) {
    this.name = name;
    this.crap = crap;
    this.thingify = thingThingify;
  }
  
  or apparently better:
  
  function Thing(name, crap) {
    this.name = name;
    this.crap = crap;
  }
  
  Thing.prototype.thingify = function () {
    return this.name + ' is a thing';
  }
  
  JS will look for any unset values in the `prototype chain`.
  You can mess around with prototypes anytime at runtime.

  
Inner functions:

  same as GCC C inner functions


Closures:

  super simple example:
  
  function makeAdder(a) {
    return function(b) {
      return b + a;
    };
  }

  Will create a function that always adds a to b;
  Even though makeAdder has return is vars still exist (or they are passed onto the child function).
  
  What really is going on. GC stuff.
  When a function is called a scope is created with what is passed to that function.
  The inner function has a reference to that scope so can still use it & it can't be GC-ed.
  (Sounds like it was probably a happy little bug).
  
