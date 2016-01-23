# emberjs-standards
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


