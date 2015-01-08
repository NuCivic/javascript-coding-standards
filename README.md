Javascript Style Guide
===============================================================================

Table of Contents
-------------------------------------------------------------------------------
1. [Types](#types)
2. [Objects](#objects)
3. [Arrays](#arrays)
4. [Array and Object initializers](#array-and-object-initializers)
5. [Strings](#strings)
6. [Functions](#functions)
7. [Arguments](#arguments)
8. [Properties](#properties)
9. [Variables](#variables)
10. [Parenthesis](#parenthesis)
11. [Conditional Expressions & Equality](#conditional-expressions-and-equality)
12. [Blocks](#blocks)
13. [Explicit scope](#explicit-scope)
14. [Loops](#loops)
15. [Wrapper objects](#wrapper-objects)
16. [Built-in object prototypes](#built-in-object-prototypes)
17. [Errors and Exceptions](#error-and-exceptions)
18. [Comments](#comments)
19. [Spaces](#spaces)
20. [Commas](#commas)
21. [Semicolons](#semicolons)
22. [Line lenght](#line-lenght)
23. [Type Casting & Coercion](#type-casting-and-coercion)
24. [Naming Conventions](#naming-conventions)
25. [Accessors](#accessors)
26. [Constructors](#constructors)
27. [Events](#events)
28. [Modules](#modules)
29. [jQuery](#jquery)
30. [Underscore / LoDash](#underscore-lodash)
31. [Don't use](#dont-use)
32. [Tools](#tools)
33. [Sublime text plugins](#sublime-text-plugins)
34. [Sources](#sources)
35. [License](#license)

Types
-------------------------------------------------------------------------------
* **Primitives:** When you access a primitive type you work directly on its value.
  - string
  - number
  - boolean
  - null
  - undefined

```javascript
var foo = 1;
var bar = foo;

bar = 9;

console.log(foo, bar); // => 1, 9
```

* **Complex:** When you access a complex type you work on a reference to its value
  - object
  - array
  - function

```javascript
var foo = [1, 2];
var bar = foo;

bar[0] = 9;

console.log(foo[0], bar[0]); // => 9, 9
```


* To check type of primitives use `typeof`:

```javascript
console.log(typeof 'hello' === 'string');
console.log(typeof 1 === 'number');
console.log(typeof 1.0 === 'number');
console.log(typeof true === 'boolean');
```

* To check if a variable type is `undefined`:

```javascript
console.log(typeof variable === 'undefined');
```

* To check if a variable type is `null`:

```javascript
console.log(variable === null);
```

* To check if a variable type is an `Array`:

```javascript
console.log(variable instanceof Array);
console.log(Object.prototype.toString.call(variable) === '[object Array]');
```

* To check if a variable type is an `Object`:

```javascript
console.log(Object.prototype.toString.call(variable) === '[object Object]');
```

* To check if a variable type is an `Object`:

```javascript
console.log(typeof variable === 'function');
```

[⬆ back to top](#)


Objects
-------------------------------------------------------------------------------
* Use the literal syntax for object creation.
```javascript
// bad
var item = new Object();

// good
var item = {};
```

* Don't use reserved word as object keys and variables. 

```javascript
// bad
var superman = {
  default: { clark: 'kent' },
  private: true
};

// good
var superman = {
  defaults: { clark: 'kent' },
  hidden: true
};
```

Arrays
-------------------------------------------------------------------------------
* Use the literal syntax for array creation

```javascript
// bad
var items = new Array();

// good
var items = [];
```

* If you don't know array length use Array#push.

```javascript
var someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
```

* When you need to copy an array use Array#slice

```javascript
var len = items.length;
var itemsCopy = [];
var i;

// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

// good
itemsCopy = items.slice();
```

* To convert an array-like object to an array, use Array#slice

```javascript
function trigger() {
  var args = [].slice.call(arguments);
  ...
}
```

* Never use Array as a map/hash/associative array

```javascript
// bad
var associative = [];
associative['name'] = 'dont do this';

// good
var associative = {};
associative['name'] = 'this is better';

// good for modern browsers
var associative = Object.create(null);
associative['name'] = 'this is better';
```

[⬆ back to top](#)

Array and Object initializers
-------------------------------------------------------------------------------

* Single-line array and object initializers are allowed when they fit on a line.

```javascript
var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
```

* Multiline array initializers and object initializers are indented 2 spaces, with the braces on their own line, just like blocks.

```javascript
// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};
```

[⬆ back to top](#)


Strings
-------------------------------------------------------------------------------
* Use single quotes '' for strings

```javascript
// bad
var name = "Bob Parr";

// good
var name = 'Bob Parr';

// bad
var fullName = "Bob " + this.lastName;

// good
var fullName = 'Bob ' + this.lastName;
```

* Strings longer than 80 characters should be written across multiple lines using string concatenation.

```javascript
// bad
var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// bad
var errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

// good
var errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';
```

* When programmatically building up a string, use Array#join instead of string concatenation. Mostly for IE.

```javascript
var items;
var messages;
var length;
var i;

messages = [{
  state: 'success',
  message: 'This one worked.'
}, {
  state: 'success',
  message: 'This one worked as well.'
}, {
  state: 'error',
  message: 'This one did not work.'
}];

length = messages.length;

// bad
function inbox(messages) {
  items = '<ul>';

  for (i = 0; i < length; i++) {
    items += '<li>' + messages[i].message + '</li>';
  }

  return items + '</ul>';
}

// good
function inbox(messages) {
  items = [];

  for (i = 0; i < length; i++) {
    items[i] = messages[i].message;
  }

  return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
}
```

[⬆ back to top](#)


Functions
-------------------------------------------------------------------------------
* Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.

```javascript
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
var test;
if (currentUser) {
  test = function test() {
    console.log('Yup.');
  };
}
```

* Never name a parameter arguments, this will take precedence over the arguments object that is given to every function scope.

```javascript
// bad
function nope(name, options, arguments) {
  // ...stuff...
}

// good
function yup(name, options, args) {
  // ...stuff...
}
```

* In general, avoid nested functions:

```javascript

// bad
function sayHi(){
  function printHello(){
    console.log('Hello');
  }
  printHello();
}

// good
function sayHi(){
  printHello();
}

function printHello(){
  console.log('Hello');
}
```

[⬆ back to top](#)

Arguments
-------------------------------------------------------------------------------
* If a function takes a lot of arguments, especially if many of those arguments are optional, or several of the arguments are functions, don't try to put all of the arguments in the function's signature. Instead, add a final argument, `options`.

```javascript
var makeCube = function (owner, options) {
  // Provide default values for the options.
  options = _.extend({
    color: 'grey',
    weight: 1.0,
    material: 'aluminum',
    onRender: function () {},
    onDestroy: function () {}
  }, options);

  console.log(owner + ", here is your " + options.color + "cube.");
  options.onRender();
  ...
});
```

[⬆ back to top](#)


Commas
-------------------------------------------------------------------------------

Use trailing commas.

* Keep the most important arguments in the signature (eg, owner above). Ideally, the arguments in the signature are the "cake" (the main substance and structure of the operation), and the options are the "icing" (frills and modifiers).

* When possible, all function arguments should be listed on the same line.

[⬆ back to top](#)


Properties
-------------------------------------------------------------------------------

* Use dot notation when accessing properties.

```javascript
var luke = {
  jedi: true,
  age: 28
};

// bad
var isJedi = luke['jedi'];

// good
var isJedi = luke.jedi;
```

* Use subscript notation [] when accessing properties with a variable.

```javascript
var luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

var isJedi = getProp('jedi');
```

* Use subscript notation [] when accessing properties that has special chars.

```javascript
var luke = {
  jedi: true,
  age: 28
};
luke['view-map'] = 1;

var map = luke['view-map'];
```

[⬆ back to top](#)


Variables
-------------------------------------------------------------------------------


* Declarations with `var`: AlwaysAlways use var to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace.

```javascript
// bad
superPower = new SuperPower();

// good
var superPower = new SuperPower();
```

* Use one `var` declaration per variable. It's easier to add new variable declarations this way, and you never have to worry about swapping out a `;` for a `,` or introducing punctuation-only diffs.

```javascript 
// bad
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// bad
// (compare to above, and try to spot the mistake)
var items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// good
var items = getItems();
var goSportsTeam = true;
var dragonball = 'z';
```

* Declare unassigned variables last.

```javascript
// bad
var i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
var i;
var items = getItems();
var dragonball;
var goSportsTeam = true;
var len;

// good
var items = getItems();
var goSportsTeam = true;
var dragonball;
var length;
var i;
```

* Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

```javascript
// bad
function() {
  test();
  console.log('doing stuff..');

  //..other stuff..

  var name = getName();

  if (name === 'test') {
    return false;
  }

  return name;
}

// good
function() {
  var name = getName();

  test();
  console.log('doing stuff..');

  //..other stuff..

  if (name === 'test') {
    return false;
  }

  return name;
}

// bad
function() {
  var name = getName();

  if (!arguments.length) {
    return false;
  }

  return true;
}

// good
function() {
  if (!arguments.length) {
    return false;
  }

  var name = getName();

  return true;
}
```

[⬆ back to top](#)

Parenthesis
-------------------------------------------------------------------------------
* Only where required. 

```javascript
// bad
function toggle(t){
   return (t === 1) ? 'hello' : 'world';  
}

// good
function toggle(t){
   return t === 1 ? 'hello' : 'world';  
}
```

[⬆ back to top](#)


Conditional Expressions & Equality
-------------------------------------------------------------------------------
* Use `===` and `!==` over `==` and `!=`.
* Use shortcuts.

```javascript 
// bad
if (name !== '') {
  // ...stuff...
}

// good
if (name) {
  // ...stuff...
}

// bad
if (collection.length > 0) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}
```

* `||` for default values. `||` is handy for introducing default values:

```javascript
this.name = this.name || "Anonymous";
_.each(this.items || [], function () { ... });
```
But be careful. This doesn't work if `false` or `0` are valid values.

* `&&` for conditional function calls. `&&` can be handy when conditionally calling a function for its value:

```javascript
// Preferred
return event && handleEvent(event);

// Not preferred
return event ? handleEvent(event) : null;
```

* `a && b || c`. This is an idiom borrowed from Python. It does the same thing as `a ? b : c`, except that if `a` and `b` are both false, it returns `c`. You should use `a && b || c` only where `a ? b : c` won't do the job.

[⬆ back to top](#)


Blocks
-------------------------------------------------------------------------------

* Use braces with all multi-line blocks.

```javascript
// bad
if (test)
  return false;

// good
if (test) return false;

// good
if (test) {
  return false;
}

// bad
function() { return false; }

// good
function() {
  return false;
}
```
* You shouldn't omit curly braces unless whole block fits into a line.

```javascript

// bad
if (aVeryVeryVeryLongVariable)
  return withAVeryLongCondition && (someKindOfVariable + 'some cool string';

// god
if (aVeryVeryVeryLongVariable && withAVeryLongCondition && someKindOfVariable){
  return withAVeryLongCondition && (someKindOfVariable + 'some cool string';
}

// good
if (test) return false;

```

[⬆ back to top](#)


Explicit scope
-------------------------------------------------------------------------------

* Always. For example, don't rely on window being in the scope chain. 

```javascript 

// bad
globalvariable = 1;

// good
window.globalvariable = 1;
```

[⬆ back to top](#)


Loops
-------------------------------------------------------------------------------

* Use for-in loops only for iterating over keys in an object/map/hash
* Use regular loops to iterate over arrays

```javascript
var list = ['a', 'b', 'c'];
var config = {age: 19, color: 'white'};

// bad
for(k in list){
   console.log(list[k]);
}

// good
for(k in config){
   console.log(config[k]);
}

// good
for(var k = 0, l = list.length; k < l ; k++){
   console.log(list[k]);
}
```
* If you loop over a list with a fixed length then set the lenght in the initialization part of the `for` loop. This guarantee lenght property is accessed just once.

```javascript

// bad
for(var k = 0; k < list.length ; k++){
   console.log(list[k]);
}

// good
for(var k = 0, l = list.length; k < l ; k++){
   console.log(list[k]);
}
```

[⬆ back to top](#)

Wrapper Objects
-------------------------------------------------------------------------------

* Avoid to use wrapper objects. Use literals instead.

```javascript
// bad
var mystring = new String('hello');

// bad
var obj = new Object();

// bad
var arr = new Array();

// good
var mystring = 'hello';

// good
var obj = {};

// good
var arr = [];
```

[⬆ back to top](#)


Built-in object prototypes
-------------------------------------------------------------------------------
* Don't modify built-in object prototypes. If you're usign a monkey patch library make sure all the patched prototypes are documented.

```javascript 
// bad
String.prototype.capitalize = function() { /* ... */ };

// good
function capitalize(){ /* ... */};
```

[⬆ back to top](#)


Errors and Exceptions
-------------------------------------------------------------------------------
* All errors that are thrown or passed to callbacks should all be instances of Error.

* Use try-catch stament only if the error is threw by a sync operation like JSON.parse. 

* Use callbacks if the error is the result of an async operation. 

[⬆ back to top](#)


Comments
-------------------------------------------------------------------------------
* Use JSDoc. [See more](http://usejsdoc.org/). Include a description, specify types and values for all parameters and return values.

```javascript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param {String} tag
// @return {Element} element
function make(tag) {

  // ...stuff...

  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param {String} tag
 * @return {Element} element
 */
function make(tag) {

  // ...stuff...

  return element;
}
```

* Use `// FIXME:` to annotate problems

```javascript
function Calculator() {

  // FIXME: shouldn't use a global here
  total = 0;

  return this;
}
```

* Use `// TODO:` to annotate solutions to problems

```javascript
function Calculator() {

  // TODO: total should be configurable by an options param
  this.total = 0;

  return this;
}
```

* Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment and leave an space after `//`.

```javascript
// bad
var active = true;  // is current tab

// good
// is current tab
var active = true;

// bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}

// good
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}
```

* If a function takes more arguments than there are formal parameters (via arguments), comment like so:

```javascript
_.extend(Foo.prototype, {
  myVariadicFunction: function (/* arguments */) { ... },
  anotherVariadicFunction: function (x, y, z, /* arguments */) { ... },
});
```

* When possible, all function arguments should be listed on the same line. If doing so would exceed the 80-column limit, the arguments must be line-wrapped in a readable way.

```javascript

// good
function hello(veryDescriptiveArgumentNumberOne, tableModelEventHandler){

}

// good
function hello(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
}

// bad
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
}

```

[⬆ back to top](#)


Spaces
-------------------------------------------------------------------------------
* Use soft tabs set to 2 spaces. Use only spaces.

```javascript
// bad
function() {
∙∙∙∙var name;
}

// bad
function() {
∙var name;
}

// good
function() {
∙∙var name;
}
```

* Place 1 space before the leading brace.

```javascript
// bad
function test(){
  console.log('test');
}

// good
function test() {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog'
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog'
});
```

* Set off operators with spaces.

```javascript
// bad
var x=y+5;

// good
var x = y + 5;
```

* End files with a single newline character.

```javascript
// bad
(function(global) {
  // ...stuff...
})(this);

```

```javascript
// bad
(function(global) {
  // ...stuff...
})(this);↵
↵
```

```javascript
// good
(function(global) {
  // ...stuff...
})(this);↵
```

[⬆ back to top](#)


Commas
-------------------------------------------------------------------------------
* Leading commas: **Nope**.

```javascript
// bad
var story = [
    once
  , upon
  , aTime
];

// good
var story = [
  once,
  upon,
  aTime
];

// bad
var hero = {
    firstName: 'Bob'
  , lastName: 'Parr'
  , heroName: 'Mr. Incredible'
  , superPower: 'strength'
};

// good
var hero = {
  firstName: 'Bob',
  lastName: 'Parr',
  heroName: 'Mr. Incredible',
  superPower: 'strength'
};
```
** Additional trailing comma: **Nope**.

```javascript
  // bad
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn',
  };

  var heroes = [
    'Batman',
    'Superman',
  ];

  // good
  var hero = {
    firstName: 'Kevin',
    lastName: 'Flynn'
  };

  var heroes = [
    'Batman',
    'Superman'
  ];
```

[⬆ back to top](#)


Semicolons
-------------------------------------------------------------------------------

* Always

```javascript
// bad
(function() {
  var name = 'Skywalker'
  return name
})()

// good
(function() {
  var name = 'Skywalker';
  return name;
})();

// good (guards against the function becoming an argument when two files with IIFEs are concatenated)
;(function() {
  var name = 'Skywalker';
  return name;
})();
```

[⬆ back to top](#)

Line lenght
-------------------------------------------------------------------------------

* 80 characters is the maximum. It's OK to occasionally go over 80 characters if it substantially improves later indentation, or if there is no good way to break the line.

[⬆ back to top](#)


Type Casting & Coercion
-------------------------------------------------------------------------------
Use object wrappers to coerce values. For example:

```javascript

// bad
var x = '' + unknowTypeValue;

// bad
var x = new String(unknowTypeValue);

// good
var x = String(unknowTypeValue);
```
Note that String wrapper is being called without `new` keyword.

**Exceptions** 
You could use `!!` to coerce boolean values.

```javascript
var age = 0;

// bad
var hasAge = new Boolean(age);

// good
var hasAge = Boolean(age);

// good
var hasAge = !!age;
```

[⬆ back to top](#)


Naming Conventions
-------------------------------------------------------------------------------

* Avoid single letter names. Be descriptive with your naming.

```javascript
// bad
function q() {
  // ...stuff...
}

// good
function query() {
  // ..stuff..
}
```

* Use camelCase when naming objects, functions, and instances

```javascript
// bad
var OBJEcttsssss = {};
var this_is_my_object = {};
function c() {}
var u = new user({
  name: 'Bob Parr'
});

// good
var thisIsMyObject = {};
function thisIsMyFunction() {}
var user = new User({
  name: 'Bob Parr'
});
```

* Use PascalCase when naming constructors or classes

```javascript
// bad
function user(options) {
  this.name = options.name;
}

var bad = new user({
  name: 'nope'
});

// good
function User(options) {
  this.name = options.name;
}

var good = new User({
  name: 'yup'
});
```

* Use a leading underscore _ when naming private properties. It's a private implementation detail and shouldn't be used from outside the module where it is defined. It could disappear or change at any time.

```javascript
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// good
this._firstName = 'Panda';
```

* When saving a reference to this use self.

```javascript

// bad
function() {
  var that = this;
  return function() {
    console.log(that);
  };
}

// bad
function() {
  var _this = this;
  return function() {
    console.log(_this);
  };
}

// good
function() {
  var self = this;
  return function() {
    console.log(self);
  };
}
```

* Name your functions. This is helpful for stack traces.

```javascript
// bad
var log = function(msg) {
  console.log(msg);
};

// good
var log = function log(msg) {
  console.log(msg);
};
```

* Use NAMES_LIKE_THIS for constant values.

* In summary, use functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis, EnumNamesLikeThis, methodNamesLikeThis, CONSTANT_VALUES_LIKE_THIS, foo.namespaceNamesLikeThis.bar, and file.names.like.this.js.

[⬆ back to top](#)


Accessors
-------------------------------------------------------------------------------

* Accessor functions for properties are not required

* If you do make accessor functions use getVal() and setVal('hello')

```javascript
// bad
dragon.age();

// good
dragon.getAge();

// bad
dragon.age(25);

// good
dragon.setAge(25);
```

* If the property is a boolean, use isVal() or hasVal()

```javascript
// bad
if (!dragon.age()) {
  return false;
}

// good
if (!dragon.hasAge()) {
  return false;
}
```

[⬆ back to top](#)


Constructors
-------------------------------------------------------------------------------

* Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

```javascript
function Jedi() {
  console.log('new jedi');
}

// bad
Jedi.prototype = {
  fight: function fight() {
    console.log('fighting');
  },

  block: function block() {
    console.log('blocking');
  }
};

// good
Jedi.prototype.fight = function fight() {
  console.log('fighting');
};

Jedi.prototype.block = function block() {
  console.log('blocking');
};
```

* Methods can return this to help with method chaining.

```javascript
// bad
Jedi.prototype.jump = function() {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
};

var luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

// good
Jedi.prototype.jump = function() {
  this.jumping = true;
  return this;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
  return this;
};

var luke = new Jedi();

luke.jump()
  .setHeight(20);
```

* It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

```javascript
function Jedi(options) {
  options || (options = {});
  this.name = options.name || 'no name';
}

Jedi.prototype.getName = function getName() {
  return this.name;
};

Jedi.prototype.toString = function toString() {
  return 'Jedi - ' + this.getName();
};
```

[⬆ back to top](#)


Events
-------------------------------------------------------------------------------

* When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

```javascript
// bad
$(this).trigger('listingUpdated', listing.id);

...

$(this).on('listingUpdated', function(e, listingId) {
  // do something with listingId
});
```

prefer:

```javascript
// good
$(this).trigger('listingUpdated', { listingId : listing.id });

...

$(this).on('listingUpdated', function(e, data) {
  // do something with data.listingId
});
```

[⬆ back to top](#)


Modules
-------------------------------------------------------------------------------
* The module should start with a `;`. This ensures that if a malformed module forgets to include a final semicolon there aren't errors in production when the scripts get concatenated.

* The file should be named with dots, live in a folder with the same name, and match the name of the single export converted to camel-case.

lodash.data (folder)
.
|--lodash.data.js

```javascript
;(function(global){
  function LodashData(){
    ...
  }
  global.LodashData = LodashData;
})(this);
```

* Always declare 'use strict'; at the top of the module.

```javascript
;(function(global){
  function LodashData(){
    'use strict';
    ...
  }
  global.LodashData = LodashData;
})(this);
```

jQuery
-------------------------------------------------------------------------------

* Prefix jQuery object variables with a $.

```javascript
// bad
var sidebar = $('.sidebar');

// good
var $sidebar = $('.sidebar');
```

* Cache jQuery lookups.

```javascript
// bad
function setSidebar() {
  $('.sidebar').hide();

  // ...stuff...

  $('.sidebar').css({
    'background-color': 'pink'
  });
}

// good
function setSidebar() {
  var $sidebar = $('.sidebar');
  $sidebar.hide();

  // ...stuff...

  $sidebar.css({
    'background-color': 'pink'
  });
}
```

* For DOM queries use Cascading $('.sidebar ul') or parent > child $('.sidebar > ul').

* Use find with scoped jQuery object queries.

```javascript
// bad
$('ul', '.sidebar').hide();

// bad
$('.sidebar').find('ul').hide();

// good
$('.sidebar ul').hide();

// good
$('.sidebar > ul').hide();

// good
$sidebar.find('ul').hide();
```

[⬆ back to top](#)

Underscore / LoDash
-------------------------------------------------------------------------------

* Prefer LoDash over underscore

* Use mixins if you want to extend base functionality


```javascript
_.mixin({
  capitalize: function(string) {
    return string.charAt(0).toUpperCase() + string.substring(1).toLowerCase();
  }
});
_("fabio").capitalize();
```
 
* Use functional style

```javascript

// bad
_([1, 2, 3]).map(function(n){ return n * 2; });

// good
_.map([1, 2, 3], function(n){ return n * 2; });
```

* When underscore is present use it to iterate over list and transform data over for and for-in loops.

[⬆ back to top](#)


Don't use
-------------------------------------------------------------------------------

* `eval()`. Using eval could be dangerous. 
* `with(){}`. The with statement is deprecated. It is forbidden in strict mode.
* `__proto__`. While support for Object.prototype.__proto__ already exists today in most browsers, its behavior has only been standardized recently in the new ECMAScript 6 specification. `Object.getPrototypeOf` be used instead.
* `caller`. This feature is non-standard and is not on a standards track. Do not use it on production sites facing the Web: it will not work for every user. There may also be large incompatibilities between implementations and the behavior may change in the future.
* `callee`.  The 5th edition of ECMAScript (ES5) forbids use of arguments.callee() in strict mode. Avoid using arguments.callee() by either giving function expressions a name or use a function declaration where a function must call itself.

[⬆ back to top](#)


Tools
------------------------------------------------------------------------------
(JsHint) [http://jshint.com/]
(Sublime Text)[www.sublimetext.com/3] or you prefered editor.
(Grunt)[http://gruntjs.com/]

[⬆ back to top](#)


Sublime text plugins
------------------------------------------------------------------------------
(Dockblockr)[https://github.com/spadgos/sublime-jsdocs]

[⬆ back to top](#)


Sources
------------------------------------------------------------------------------
https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
https://github.com/airbnb/javascript
https://github.com/meteor/meteor/wiki/Meteor-Style-Guide

[⬆ back to top](#)

License
-------------------------------------------------------------------------------

(The MIT License)

Copyright (c) 2014 NuCivic

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

[⬆ back to top](#)