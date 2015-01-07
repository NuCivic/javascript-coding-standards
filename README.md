# Javascript Style Guide

## JavaScript Language Rules

### var
Declarations with `var`: Always. Use one var declaration per variable. 

**Bad**

```javascript
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
```
**Good**

```javascript
var items = getItems();
var goSportsTeam = true;
var dragonball = 'z';
```
Declare unassigned variables last.

**Bad**

```javascript
var i;
var items = getItems();
var dragonball;
var goSportsTeam = true;
var len;
```
**Good**

```javascript
var items = getItems();
var goSportsTeam = true;
var dragonball;
var length;
var i;
```

Assign variables at the top of their scope. This helps avoid issues with variable declaration and assignment hoisting related issues.

**Bad**
```javascript
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
```
**Good**
```javascript
  var name = getName();

  test();
  console.log('doing stuff..');

  //..other stuff..

  if (name === 'test') {
    return false;
  }

  return name;
```

**Bad**
```javascript
function() {
  var name = getName();

  if (!arguments.length) {
    return false;
  }

  return true;
}

```
**Good**
```javascript
function() {
  if (!arguments.length) {
    return false;
  }

  var name = getName();

  return true;
}
```


### Constants
* Use NAMES_LIKE_THIS for constant values.

### Semicolons
Always use semicolons.

### Exceptions
Yes.

### Custom exceptions
Yes.

### Wrapper Objects
Never use wrapper objects. Always use literal way.

**Bad**

```javascript
var mylist = new Array();
```
**Good**

```javascript
var mylist = [];
```

### Nested functions
No.

### eval()
No. Use eval could be dangerous. 

### with() {}
No. Use "with" could introduce scope bugs hard to detect.

### for-in loop
Only for iterating over keys in an object/map/hash

### Associative Arrays
Never use Array as a map/hash/associative array

### Multiline string literals
No.

### Modifying prototypes of builtin objects
No.


## JavaScript Style Rules

### Naming
In general, use functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis, EnumNamesLikeThis, methodNamesLikeThis, CONSTANT_VALUES_LIKE_THIS, foo.namespaceNamesLikeThis.bar, and file.names.like.this.js.

Avoid single letters names.

Name your functions. This is helpful for stack traces:

**Bad**

```javascript
var log = function(msg) {
  console.log(msg);
};

```

**Good**
```javascript
var log = function log(msg) {
  console.log(msg);
};
```

### Explicit scope
Always. For example, don't rely on window being in the scope chain. 

**Bad**

```javascript 
  globalvariable = 1;
```

**Good**

```javascript 
  window.globalvariable = 1;
```

### Preserve scope
Use a variable named "self" at the top of the scope you want to preserve.

```javascript
function MyConstructorThing(){
	var self = this;

	self.sayHi = function(){
		//preserved scope
		console.log(self);
	};
}
```

### Line Length
80 characters is the maximum. It's OK to occasionally go over 80 characters if it substantially improves later indentation, or if there is no good way to break the line.

### Spaces vs. Tabs
Use only spaces, and indent 2 spaces at a time.

### Curly Braces
Always start your curly braces on the same line as whatever they're opening. Use this brace style:
```javascript 
if (a < 0) {
  console.log("a is negative");
  handleNegativeA();
} else if (a > 0) {
  console.log("a is positive");
  handlePositiveA();
} else {
  console.log("a is zero or NaN");
  handleOtherA();
}
```

### Array and Object initializers
Single-line array and object initializers are allowed when they fit on a line.

```javascript
var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
```
Multiline array initializers and object initializers are indented 2 spaces, with the braces on their own line, just like blocks.
```javascript
// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};
```
### Function Arguments
When possible, all function arguments should be listed on the same line.

### Blank lines
Use blank lines to group lo

### Space between tokens

`a = b + 1`, not `a=b+1`

`function (a, b, c) { return 1; }`, not `function(a,b,c) {return 1;}`

`for (i = 0; i < 3; i++)`, not `for(i=0;i<3;i++)`

`a(1, 2, 3)`, not `a(1,2,3)`

`{a: 1, b: 2}`, not `{a:1,b:2}`

`if (a)`, not `if(a)`

`if (!a)`, not `if (! a)`

`a++`, not `a ++`

`--b`, not `-- b`

When functions or objects fit entirely on a single line, put a space inside the enclosing braces:

`stack.push({parent: node, red: true})`, not `stack.push({parent:node, red:true})`

`samples.concat([1, 2, 3])`, not `samples.concat([ 1, 2, 3 ])`

### Private identifiers
If a method or property name starts with _, it's a private implementation detail and shouldn't be used from outside the module where it is defined. It could disappear or change at any time.

### Blocks
You shouldn't omit curly braces unless whole block fits into a line.



### Parentheses
Only where required. 

### Strings
Prefer `'` over `"`.

### Comments
Use JSDoc. [See more](http://usejsdoc.org/)

Use `// FIXME:` to annotate problems

Use `// TODO:` to annotate solutions to problems

Use // for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment and leave an space after `//`.

**Bad**
```javascript
var active = true;  // is current tab
```

**Good**
```javascript
// is current tab
var active = true;
```

**Bad**
```javascript
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}
```

**Good**
```javascript
function getType() {
  console.log('fetching type...');

  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}
```

If a function takes more arguments than there are formal parameters (via arguments), comment like so:

```javascript
_.extend(Foo.prototype, {
  myVariadicFunction: function (/* arguments */) { ... },
  anotherVariadicFunction: function (x, y, z, /* arguments */) { ... },
});
```
###  Commas
Use trailing commas.

### Coercion
Use object wrappers to coerce values. For example:

**Bad**
```javascript
var x = '' + unknowTypeValue;
```
**Good**
```javascript
var x = String(unknowTypeValue);
```
Note that String wrapper is being called without `new` keyword.

**Exceptions** 
You could use `!!` to coerce boolean values.

```javascript
var hasAge = !!age;
```

### Equality testing
Prefer `===` over `==` and  `==` over `!=`. 

### `||` for default values
`||` is handy for introducing default values:

```javascript
this.name = this.name || "Anonymous";
_.each(this.items || [], function () { ... });
```

But be careful. This doesn't work if `false` or 0 are valid values.

### `&&` for conditional function calls
`&&` can be handy when conditionally calling a function for its value:

```javascript
// Preferred
return event && handleEvent(event);

// Not preferred
return event ? handleEvent(event) : null;
```

### `a && b || c`
This is an idiom borrowed from Python. It does the same thing as `a ? b : c`, except that if `a` and `b` are both false, it returns `c`. You should use `a && b || c` only where `a ? b : c` won't do the job.

### Keyword arguments with options
If a function takes a lot of arguments, especially if many of those arguments are optional, or several of the arguments are functions, don't try to put all of the arguments in the function's signature. Instead, add a final argument, `options`.

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

Keep the most important arguments in the signature (eg, owner above). Ideally, the arguments in the signature are the "cake" (the main substance and structure of the operation), and the options are the "icing" (frills and modifiers).

### Error objects
All errors that are thrown or passed to callbacks should all be instances of Error.

### Reserved words
Don't use reserved word as object keys and variables. 

** Exception **
You could override some built in keywords to prevent side effects. For example:

```javascript
var undefined;
```
Thus, we ensure that 'undefined' is really 'undefined';


### Properties
Use dot notation when accessing properties.

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

Use subscript notation [] when accessing properties with a variable or if the property use special chars like '-'.

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

### Accesors
Accessor functions for properties are not required

If you do make accessor functions use getVal() and setVal('hello') 

**Bad**

```javascript
dragon.age();
```

**Good**

```javascript
dragon.getAge();
```

**Bad**

```javascript
dragon.age(25);
```

**Good**

```javascript
dragon.setAge(25);
```

If the property is a boolean, use `isVal()` or `hasVal()`:

**Bad**

```javascript
if (!dragon.age()) {
  return false;
}
```

**Good**

```javascript
if (!dragon.hasAge()) {
  return false;
}
```

### Constructors

Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

**Bad**

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
```

**Bad**
```javascript
Jedi.prototype.fight = function fight() {
  console.log('fighting');
};

Jedi.prototype.block = function block() {
  console.log('blocking');
};
```

Methods can return this to help with method chaining.

It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.


### Modules / Libraries
Always use the (IIFE pattern)[http://en.wikipedia.org/wiki/Immediately-invoked_function_expression] to create a module.

The module should start with a `;`.

Always declare 'use strict'; at the top of the module.
```javascript
;(function(global){

})(this);
```

### jQuery

Prefix jQuery object variables with a `$`.

**Bad**

```javascript
var sidebar = $('.sidebar');
```
**Good**

```javascript
var $sidebar = $('.sidebar');
```

Cache jQuery lookups.

**Bad**

```javascript
function setSidebar() {
  $('.sidebar').hide();

  // ...stuff...

  $('.sidebar').css({
    'background-color': 'pink'
  });
}
```

**Good**

```javascript
function setSidebar() {
  var $sidebar = $('.sidebar');
  $sidebar.hide();

  // ...stuff...

  $sidebar.css({
    'background-color': 'pink'
  });
}
```

## Tools

(JsHint) [http://jshint.com/]
(Sublime Text)[www.sublimetext.com/3] or you prefered editor.
(Grunt)[http://gruntjs.com/]

### Sublime text plugins
(Dockblockr)[https://github.com/spadgos/sublime-jsdocs]

## Sources
https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
https://github.com/airbnb/javascript
https://github.com/meteor/meteor/wiki/Meteor-Style-Guide