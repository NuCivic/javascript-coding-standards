# Javascript Style Guide

## JavaScript Language Rules

### var
Declarations with **var**: Always

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

### Explicit scope
Always. For example, don't rely on window being in the scope chain. 

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

**Bad**
```javascript 
	globalvariable = 1;
```

**Good**
```javascript 
	window.globalvariable = 1;
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

### Omit curly braces
No. You shouldn't omit curly braces unless whole block fits into a line.

### Parentheses
Only where required. 

### Strings
Prefer `'` over `"`.

### Comments
Use JSDoc.

### Signature comment for arguments
If a function takes more arguments than there are formal parameters (via arguments), comment like so:

```javascript
_.extend(Foo.prototype, {
  myVariadicFunction: function (/* arguments */) { ... },
  anotherVariadicFunction: function (x, y, z, /* arguments */) { ... },
});
```

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


### Equality testing
Prefer `===` over `==`. 

### `||` for default values
`||` is handy for introducing default values:

```javascript
this.name = this.name || "Anonymous";
_.each(this.items || [], function () { ... });
```

But be careful. This doesn't work if `false` or 0 are valid values.



