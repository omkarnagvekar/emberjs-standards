# Emberjs Coding Standards
JavaScript Coding Standards - ININ Mumbai

This README outlines JavaScript/ES6 coding standards to be followed in Ember application.

## Javascript/ES6 specific rules:

### 1. Declaration Types(Types, references)


* When you access a primitive type you work directly on its value

    ```js
    const foo = 1;  
    let bar = foo;  
    bar = 9;  
    console.log(foo, bar); // => 1, 9
    ```
    
* When you access a complex type you work on a reference to its value.
   
    ```js
    const foo = [1, 2];  
    const bar = foo;  
    bar[0] = 9;  
    console.log(foo[0], bar[0]); // => 9, 9
    ```
    
* Use const for all of your references; avoid using var
    
    ```js
    // bad  
    var a = 1;  
    var b = 2;  
    // good  
    const a = 1;  
    const b = 2;
    ```
    
* If you must reassign references, use let instead of var.
    
    ```js
    // bad  
    var count = 1;  
    if (true) { 
        count += 1; 
    }  
     
    // good, use the let.  
    let count = 1;  
    if (true) { 
        count += 1; 
    }
    ```
    
* Note that both let and const are block-scoped.
    
    ```js
    // const and let only exist in the blocks they are defined in.  
    { 
     let a = 1; 
     const b = 1;  
    }  
    console.log(a); // ReferenceError  
    console.log(b); // ReferenceError
    ```
    
* All variable declarations should be at the top of block scope with a single let/const


### 2. Objects


* Use the literal syntax for object creation. 

    ```js
    // bad  
    const item = new Object();  
    // good  
    const item = {}; 
    ```

* Don't use reserved words as keys. 

    ```js
    // bad  
    const superman = {  
      default: { clark: 'kent' }, 
      private: true,  
    };  
    // good  
    const batman = { 
      defaults: { bruce: 'wayne' }, 
      hidden: true,  
    }; 
    ```

* Use readable synonyms in place of reserved words. 

    ```js
    // bad  
    const superman = { 
        class: 'alien', 
    };  
    // bad  
    const superman = { 
        klass: 'alien', 
    };  
    // good  
    const superman = { 
        type: 'alien', 
    }; 
    ```

* Use computed property names when creating objects with dynamic property names. 

    ```js
    function getKey(k) { 
     return `a key named ${k}`;  
    }  
    // bad  
    const obj = { 
     id: 5, 
     name: 'San Francisco',  
    };  
    obj[getKey('enabled')] = true;  
    // good const obj = { 
     id: 5, 
     name: 'San Francisco', 
     [getKey('enabled')]: true,  
    }; 
    ```

* Use object method shorthand. 

    ```js
    // bad  
    const atom = { 
     value: 1, 
     addValue: function (value) { 
      return atom.value + value;  
     },  
    };  
    // good  
    const atom = { 
     value: 1, 
     addValue(value) { 
      return atom.value + value; 
     },  
    }; 
    ```

* Use property value shorthand. 

    ```js
    const lukeSkywalker = 'Luke Skywalker';  
    // bad  
    const obj = { 
        lukeSkywalker: lukeSkywalker, 
    };  
    // good  
    const obj = { 
        lukeSkywalker, 
    }; 
    ```

* Group your shorthand properties at the beginning of your object declaration. 

    ```js
    const anakinSkywalker = 'Anakin Skywalker';  
    const lukeSkywalker = 'Luke Skywalker';  
     
    // bad  
    const obj = { 
     episodeOne: 1, 
     twoJediWalkIntoACantina: 2, 
     lukeSkywalker, 
     episodeThree: 3, 
     mayTheFourth: 4, 
     anakinSkywalker,  
    };  
    // good  
    const obj = { 
     lukeSkywalker, 
     anakinSkywalker, 
     episodeOne: 1, 
     twoJediWalkIntoACantina: 2, 
     episodeThree: 3, 
     mayTheFourth: 4,  
    }; 
    ```

* Only quote properties that are invalid identifiers. 

    ```js
    // bad  
    const bad = { 
     'foo': 3, 
     'bar': 4, 
     'data-blah': 5,  
    };  
    // good  
    const good = { 
     foo: 3, 
     bar: 4, 
     'data-blah': 5,  
    }; 
    ```


### 3. Arrays 

* Use the literal syntax for array creation. 

    ```js
    // bad  
    const items = new Array();  
    // good  
    const items = []; 
    ```

* Use Array#push instead of direct assignment to add items to an array. 

    ```js
    const someStack = [];  
    // bad  
    someStack[someStack.length] = 'abracadabra';  
    // good  
    someStack.push('abracadabra'); 
    ```

* for-loops: define length before loop 

* Use array spreads ... to copy arrays. 

    ```js
    // bad  
    const len = items.length;  
    const itemsCopy = [];  
    let i;  
    for (i = 0; i < len; i++) { 
     itemsCopy[i] = items[i];  
    }  
    // good  
    const itemsCopy = [...items]; 
    ```


### 4. Destructuring 

* Use object destructuring when accessing and using multiple properties of an object. 

```js
// bad  
function getFullName(user) { 
 const firstName = user.firstName; 
 const lastName = user.lastName; 
 return `${firstName} ${lastName}`;  
}  
// good  
function getFullName(user) { 
 const { firstName, lastName } = user; 
 return `${firstName} ${lastName}`;  
}  
// best  
function getFullName({ firstName, lastName }) { 
 return `${firstName} ${lastName}`;  
} 
```

* Use array destructuring. 

```js
const arr = [1, 2, 3, 4];  
// bad  
const first = arr[0];  
const second = arr[1];  
// good  
const [first, second] = arr; 
```

* Use object destructuring for multiple return values, not array destructuring. 

```js
// bad  
function processInput(input) {  
 // then a miracle occurs  
 return [left, right, top, bottom];  
}  
// the caller needs to think about the order of return data  
const [left, __, top] = processInput(input);  
// good  
function processInput(input) { 
 // then a miracle occurs 
 return { left, right, top, bottom };  
}  
// the caller selects only the data they need  
const { left, right } = processInput(input); 
```

 
### 5. Strings 

* Use single quotes '' for strings. 

```js
// bad  
const name = "Capt. Janeway";  
// good  
const name = 'Capt. Janeway'; 
```

* Strings that cause the line to go over 100 characters should be written across multiple lines using string concatenation. However long strings with concatenation could impact performance. 

```js
getVal() 
.getName().getId() 
```

* When programmatically building up strings, use template strings instead of concatenation. 

```js
// bad  
function sayHi(name) { 
 return 'How are you, ' + name + '?';  
}  
// bad  
function sayHi(name) { 
 return ['How are you, ', name, '?'].join();  
}  
// good  
function sayHi(name) { 
 return `How are you, ${name}?`;  
} 
```
 
### 6. Functions 

* Use function declarations instead of function expressions. 

```js
// bad  
const foo = function () {  
};  
// good  
function foo() {  
} 
```

* Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently. 

```js
var a = function() {};  
for (var i=10; i; i--) { a(); } 
 for (var i=10; i; i--) { 
 var a = function() {}; 
 // OK, no references to variables in the  outer scopes. a();  
}  
for (let i=10; i; i--) { 
 var a = function() { return i; }; 
 // OK, all references are referring to block scoped variable  in the loop. a();  
} 
```

* Never name a parameter arguments. This will take precedence over the arguments object that is given to every function scope. 

```js
// bad  
function nope(name, options, arguments) { 
 // ...stuff...  
}  
// good  
function yup(name, options, args) { 
 // ...stuff...  
} 
```

* Never use arguments, opt to use rest syntax ... instead. 

```js
// bad  
function concatenateAll() { 
 const args = Array.prototype.slice.call(arguments); 
 return args.join('');  
}  
// good  
function concatenateAll(...args) { 
 return args.join('');  
} 
```

* Use default parameter syntax rather than mutating function arguments. 

```js
// really bad  
function handleThings(opts) { 
 // No! We shouldn't mutate function arguments. 
 // Double bad: if opts is falsy it'll be set to an object which  may 
 // be what you want but it can introduce subtle bugs. 
 opts = opts || {}; 
 // ...  
}  
// still bad  
function handleThings(opts) { 
 if (opts === void 0) { 
  opts = {}; 
 } 
 // ...  
}  
// good  
function handleThings(opts = {}) { 
 // ...  
} 
```

* Always put default parameters last. 

```js
// bad  
function handleThings(opts = {}, name) { 
 // ...  
}  
// good  
function handleThings(name, opts = {}) { 
 // ...  
} 
```

* Spacing in a function signature. 

```js
// bad  
const f = function(){};  
const g = function (){};  
const h = function() {};  
// good  
const x = function () {};  
const y = function a() {}; 
```

* Never mutate parameters. 

```js
// bad function f1(obj) { obj.key = 1; };  
// good function f2(obj) {  
const key = obj.key ? obj.key : 1;  
}; 
```

* Never reassign parameters. 

```js
// bad  
function f1(a) { a = 1; }  
function f2(a) { if (!a) { a = 1; } }  
// good  
function f3(a) { const b = a || 1; }  
function f4(a = 1) { } 
```

* When you must use function expressions (as when passing an anonymous function), use arrow function notation. 

```js
// bad  
[1, 2, 3].map(function (x) { const y = x + 1; return x * y; });  
// good  
[1, 2, 3].map((x) => { const y = x + 1; return x * y; }); 
```

* If the function body consists of a single expression, omit the braces and use the implicit return. Otherwise, keep the braces and use a return statement. 

```js
// good  
[1, 2, 3].map(number => `A string containing the ${number}.`);  
// bad  
[1, 2, 3].map(number => { const nextNumber = number + 1; `A string containing the ${nextNumber}.`; });  
// good  
[1, 2, 3].map(number => { const nextNumber = number + 1; return `A string containing the ${nextNumber}.`; }); 
```

* In case the expression spans over multiple lines, wrap it in parentheses for better readability. 

```js
// bad  
[1, 2, 3].map(number => 'As time went by, the string containing the ' + `${number} became much longer. So we needed to break it over multiple ` + 'lines.' );  
// good  
[1, 2, 3].map(number => ( `As time went by, the string containing the ${number} became much ` + 'longer. So we needed to break it over multiple lines.' )); 
```

* If your function takes a single argument and doesn’t use braces, omit the parentheses. Otherwise, always include parentheses around arguments. 

```js
// bad  
[1, 2, 3].map((x) => x * x);  
// good  
[1, 2, 3].map(x => x * x);  
// good  
[1, 2, 3].map(number => ( `A long string with the ${number}. It’s so long that we’ve broken it ` + 'over multiple lines!' ));  
// bad  
[1, 2, 3].map(x => { const y = x + 1; return x * y; });  
// good  
[1, 2, 3].map((x) => { const y = x + 1; return x * y; }); 
```


### 7. Modules 

* Always use modules (import/export) over a non-standard module system. You can always transpile to your preferred module system. 

```js
// bad  
const AirbnbStyleGuide = require('./AirbnbStyleGuide'); module.exports = AirbnbStyleGuide.es6;  
// ok  
import AirbnbStyleGuide from './AirbnbStyleGuide'; export default AirbnbStyleGuide.es6;  
// best  
import { es6 } from './AirbnbStyleGuide'; export default es6; 
```

* Do not use wildcard imports. 

```js
// bad  
import * as AirbnbStyleGuide from './AirbnbStyleGuide';  
// good  
import AirbnbStyleGuide from './AirbnbStyleGuide'; 
```

* And do not export directly from an import. 

```js
// bad // filename es6.js  
export { es6 as default } from './airbnbStyleGuide';  
// good // filename es6.js  
import { es6 } from './AirbnbStyleGuide'; export default es6; 
```


### 8. Properties 

* Use dot notation when accessing properties. 

```js
const luke = { jedi: true, age: 28, };  
// bad const isJedi = luke['jedi'];  
// good const isJedi = luke.jedi; 
```

* Use subscript notation [] when accessing properties with a variable. 

```js
const luke = { jedi: true, age: 28, };  
function getProp(prop) { return luke[prop]; }  
const isJedi = getProp('jedi');
```


### 9. Variables 

* Use one const declaration per variable. 

```js
// bad  
const items = getItems(),  
goSportsTeam = true,  
dragonball = 'z';  
// bad // (compare to above, and try to spot the mistake) const items = getItems(),  
goSportsTeam = true;  
dragonball = 'z';  
// good  
const items = getItems();  
const goSportsTeam = true;  
const dragonball = 'z'; 
```

* Group all your consts and then group all your lets. 

```js
// bad  
let i, len, dragonball, items = getItems(), goSportsTeam = true;  
// bad  
let i; const items = getItems(); let dragonball; const goSportsTeam = true; let len;  
// good  
const goSportsTeam = true; const items = getItems(); let dragonball; let i; let length; 
```

* Assign variables where you need them, but place them in a reasonable place 

```js
// bad - unnecessary function call  
function checkName(hasName) {  
const name = getName();  
if (hasName === 'test') { return false; }  
if (name === 'test') { this.setName(''); return false; }  
return name;  
}  
 
// good function checkName(hasName) {  
if (hasName === 'test') { return false; }  
const name = getName();  
if (name === 'test') { this.setName(''); return false; }  
return name;  
} 
```

* var declarations get hoisted to the top of their scope, their assignment does not. With const and let you get ReferenceError  

```js
function example() { console.log(notDefined); // => throws a ReferenceError } 
 
function example() { console.log(declaredButNotAssigned); // => undefined var declaredButNotAssigned = true; } 
 
function example() { let declaredButNotAssigned; console.log(declaredButNotAssigned); // => undefined declaredButNotAssigned = true; } 
 
// using const and let function example() { console.log(declaredButNotAssigned); // => throws a ReferenceError console.log(typeof declaredButNotAssigned); // => throws a ReferenceError const declaredButNotAssigned = true; } 
```

* Function declarations hoist their name and the function body 

```js
function example() {  
superPower(); // => Flying  
function superPower() { console.log('Flying'); }  
} 
```


### 10. Comparison Operators 

* Use === and !== over == and != 

* Conditional statements such as the if statement evaluate their expression using coercion with the ToBooleanabstract method and always follow these simple rules: 
    __Objects__ evaluate to ```js true ```
    __Undefined__ evaluates to false 
    __Null__ evaluates to false 
    __Booleans__ evaluate to the value of the boolean 
    __Numbers__ evaluate to false if +0, -0, or NaN, otherwise true 
    __Strings__ evaluate to false if an empty string '', otherwise true 

```js
if ([0] && []) {  
// true  
// An array (even an empty one) is an object, objects will evaluate to true  
} 
```

* Use shortcuts 

```js
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


### 11. Blocks 

* Use braces with all multi-line blocks 

```js
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
function () { return false; }  
 
// good  
function () { 
 return false;  
} 
```

* If you're using multi-line blocks with if and else, put else on the same line as your if block's closing brace. 

```js
// bad  
if (test) { 
 thing1(); 
 thing2();  
}  
else { 
 thing3();  
}  
// good  
if (test) { 
 thing1(); 
 thing2();  
} else { 
 thing3();  
}
``` 


### 12. Comments 

* Use /** ... */ for multi-line comments. Include a description, specify types and values for all parameters and return values. 

```js
// bad  
// make() returns a new element  
// based on the passed in tag name  
//  
// @param {String} tag  
// @return {Element} element  
function make(tag) { // ...stuff... return element; }  
 
// good  
/**  
* make() returns a new element  
* based on the passed in tag name  
*  
* @param {String} tag  
* @return {Element} element  
*/  
function make(tag) { // ...stuff... return element; } 
```

* Use // for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it's on the first line of a block.c FIXME (to annotate problems) and TODO (to annotate solutions to problems) 

```js
// FIXME: shouldn't use a global here  
or  
// TODO: total should be configurable by an options param 
```


### 13. Whitespace 

* Use soft tabs set to 4 spaces 

* Place 1 space before the leading brace, opening parenthesis of conditionals. 

* Place no space between the argument list and the function name in function calls and declarations. 

* Set off operators with spaces. 

* End files with a single newline character. 

* Use indentation when making long method chains. Use a leading dot, which emphasizes that the line is a method call, not a new statement. 

* Leave a blank line after blocks and before the next statement. 

* Do not pad your blocks with blank lines. 

* Do not add spaces inside parentheses and brackets. 

* Add spaces inside curly braces. 

* Avoid having lines of code that are longer than 100 characters (including whitespace). 


### 14. Punctuation 

* No Leading commas 

* Use additional trailing comma for last declaration inside objects/arrays 

* Use trailing semicolon after each statement. No leading semicolon allowed 


### 15. Type Casting and Coercion 

* Perform type coercion at the beginning of the statement. 

* Strings: 

```js
// => this.reviewScore = 9;  
// bad  
const totalScore = this.reviewScore + '';  
// good  
const totalScore = String(this.reviewScore); 
```

* Numbers: Use Number for type casting and parseInt always with a radix for parsing strings. 

```js
const inputValue = '4';  
 
// bad 
const val = new Number(inputValue);  
const val = +inputValue;  
const val = inputValue >> 0;  
const val = parseInt(inputValue);  
 
// good 
const val = Number(inputValue);  
const val = parseInt(inputValue, 10); 
```

* Booleans: 

```js
const age = 0;  
 
// bad 
const hasAge = new Boolean(age);  
 
// good 
const hasAge = Boolean(age);  
const hasAge = !!age; 
```


### 16. Naming Convention 

* Avoid single letter names. Be descriptive with your naming. 

* Use camelCase when naming objects, functions, and instances. 

* Use PascalCase when naming constructors or classes. 

```js
// bad  
function user(options) { 
 this.name = options.name;  
}  
const bad = new user({ 
 name: 'nope',  
});  
 
// good  
class User { 
 constructor(options) { 
  this.name = options.name;  
 }  
}  
 
const good = new User({ 
 name: 'yup',  
}); 
```

* Use a leading underscore _ when naming private properties. 

```js
// bad  
this.__firstName__ = 'Panda';  
this.firstName_ = 'Panda';  
 
// good  
this._firstName = 'Panda'; 
```

* Don't save references to this. Use arrow functions or Function#bind. 

```js
// bad  
function foo() { 
 const self = this; 
 return function () { 
  console.log(self);  
};  
}  
// bad function foo() { 
 const that = this;  
return function () { 
  console.log(that);  
};  
}  
 
// good  
function foo() { 
 return () => { 
  console.log(this); 
 };  
} 
```

* If your file exports a single class, your filename should be exactly the name of the class. 

* Use camelCase when you export-default a function. Your filename should be identical to your function's name. 

```js
function makeStyleGuide() {  
}  
export default makeStyleGuide; 
```

* Use PascalCase when you export a singleton / function library / bare object. 

```js
const AirbnbStyleGuide = { 
    es6: {  
}  
};  
export default AirbnbStyleGuide; 
```


### 17. Accessors 

* Accessor functions for properties are not required. 

* If you do make accessor functions use getVal() and setVal('hello'). 

* If the property is a boolean, use isVal() or hasVal(). 

* It's okay to create get() and set() functions, but be consistent. 

```js
class Jedi { 
 constructor(options = {}) { 
  const lightsaber = options.lightsaber || 'blue'; 
  this.set('lightsaber', lightsaber);  
}  
 
set(key, val) { 
  this[key] = val;  
} 
  
get(key) { 
  return this[key];  
}  
} 
```


### 18. Events 

* When attaching data payloads to events, pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. 

```js
// bad  
$(this).trigger('listingUpdated', listing.id);  $(this).on('listingUpdated', function (e, listingId) { 
 // do something with listingId  
}); 
 
// good  
$(this).trigger('listingUpdated', { listingId: listing.id });  $(this).on('listingUpdated', function (e, data) { 
 // do something with data.listingId  
}); 
```


### 19. jQuery 

* Prefix jQuery object variables with a $. 

```js
const $sidebarBtn = $('.sidebar-btn'); 
```

* Cache jQuery lookups. 

```js
const $sidebar = $('.sidebar');  
$sidebar.hide();  
// ...stuff...  
$sidebar.css({ 'background-color': 'pink' }); 
```

* For DOM queries use Cascading 

```js 
$('.sidebar ul') or parent > child $('.sidebar > ul'). 
```

* Use find with scoped jQuery object queries. 

```js
// bad  
$('ul', '.sidebar').hide();  
// bad  
$('.sidebar').find('ul').hide();  
 
// good 
$('.sidebar ul').hide();  
$('.sidebar > ul').hide();  
$sidebar.find('ul').hide(); 
```



