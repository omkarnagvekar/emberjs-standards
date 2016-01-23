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
    const obj = { lukeSkywalker: lukeSkywalker, };  
    // good  
    const obj = { lukeSkywalker, }; 
    Group your shorthand properties at the beginning of your object declaration. 
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

