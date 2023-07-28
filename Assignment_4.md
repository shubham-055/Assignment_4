```
                    ##JAVASCRIPT ASSESSMENT 4
```

1. How does the JS engine work?

A JavaScript engine is a software program that interprets and executes JavaScript code. It is responsible for translating the JavaScript code into machine code that can be executed by the computer's CPU.

The JavaScript engine works in several stages:

Parsing: The first stage is parsing, which is the process of breaking down the JavaScript code into its constituent parts. This includes identifying the different tokens in the code, such as keywords, variables, and operators.

AST construction: The second stage is AST construction, which is the process of creating an abstract syntax tree (AST) for the JavaScript code. The AST is a hierarchical representation of the code that makes it easier for the JavaScript engine to understand.

Just-in-Time (JIT) Compilation:
JIT compilation involves creating machine code during runtime, instead of ahead of time like traditional compilation. The intermediate code generated during the compilation phase is not written to a binary file but is executed immediately. This technique allows JavaScript engines to optimize the code based on runtime information and make it more efficient.

Optimization Process:
To fully optimize JavaScript code, the engine first generates an unoptimized version of the machine code that can be executed immediately. While the code is running, the engine continues to re-optimize and recompile the code in the background, using information gathered during execution. This iterative optimization process helps produce the most optimized version of the code.

Garbage collection: The JavaScript engine performs garbage collection, which is the process of removing objects from memory that are no longer being used.

 

2. What is the output & Why?

``` js
    let timerId = setInterval(function() {
    alert('tick');
    }, 2000);
    setTimeout(function(){
    clearInterval(timerId);
    alert('stop');
    }, 5000);

    Output :
    tick
    tick
    stop
```


The setInterval() function creates a timer that will call the function passed to it every 2000 milliseconds. The setTimeout() function creates a timer that will call the function passed to it after 5000 milliseconds. So after giving alert 2 times in 4000ms when timer reach 5000ms it invokes setTimeout function that will clear the setInterval() timer, so the setInterval() function will no longer be called. The last alert will be "stop".


3. Write printAnimals() in such a way that it prints all animals in the object below.

``` js
   const animals = [ { species: 'Lion', name: 'King' },
{ species: 'Whale', name: 'Queen' } ];

function printAnimals(i) {
this.print = function() {
console.log('#' + i + ' ' + this.species + ': ' + this.name);
}
this.print();
}
for(let i = 1;i<=animals.length;i++) {
    printAnimals.call(animals[i-1],i);
}

Output : 
#1 Lion: King
#2 Whale: Queen
```

4. What is the output & Why?

``` js
    function sumOfNumbers() {
    var total = 0;
    for (var i = 0; i < arguments.length; i++) {
    total += arguments[i];
    }
    return total;
    }
    var numbers = [1, 2, 3];
    var sum = sumOfNumbers.apply(null, numbers);
    console.log(sum);

    Output :
    6
```
The sumOfNumbers() function is basically just calculating sum of all the arguments passed to it and then return the sum, Although the function doesn't define any parameters but The function uses the arguments object(inbuilt prototype), which is an array-like object that holds all the arguments passed to the function when it is invoked. The apply() method allows us to call a function with an array of arguments as if the arguments were passed to the function directly. When the apply method is called with a null or undefined reference as the first argument, the value of 'this' inside the function being invoked will point to the global object.

5. What is the output & Why?

``` js
    "use strict";
    var person = {
    name : "Jack",
    prop : {
    name : "Daniel",
    getName : function() {
        return this.name;
        }
      }
    }
    var name = person.prop.getName.bind(person);
    console.log(name());
    var name = person.prop.getName();
    console.log(name);
```
The given code creates an object person with a nested object prop containing a method getName. The getName method returns the 'name' property of the object it belongs to(using this keyword). Here, the bind method is used to create a new function and assigned the new function to variable 'name'. Now the name function is copy of getname and this keyword inside the name function will always refer to the 'person' object, regardless of how the function is called.

Please note that there is no change in any of original objects(person or person.prop).

when we console.log(name()), The name function is called. Since this keyword of name function will point to the person object. Therefore, it will return the name property of the person object, which is "Jack".

var name = person.prop.getName(); -  This line calls the getName method directly on the prop object. When calling it directly, the context (this) will be the prop object itself. As a result, the this.name will point to the name property of the prop object, which is "Daniel". The value returned from the getName method is stored in the name variable.

6. What is the output & Why?
```js
function makeUser(){
return { name: "John", ref: this };
}
let user = makeUser();
alert( user.ref.name );

Output :
undefined
```
The code defines a function called makeUser that returns an object with two properties: name set to "John" and ref set to the value of this. Then, it calls the makeUser function and assigns the returned object to the variable user. Finally, it tries to access the property 'name' of the ref object (user.ref.name).

However, the this keyword inside the makeUser function points to the global object because the function is called without any explicit context(explicit binding). As a result, the ref property of the returned object points to the global object. Since the global object does not have a property called name, attempting to access user.ref.name results in undefined.

7. What is the output & Why?
```js
const func = (function(a){
delete a; 
return a;
})(5);
console.log(func);
```
The code defines a immediately invoked function with the argument 5. The function takes the parameter a as 5.

Inside the function, there is a delete statement trying to delete the variable a. However, since a is a function parameter, it cannot be deleted. The delete operator can only be used to delete properties of objects and array elements, not variables or function parameters.

After the failed attempt to delete a, the function returns the value of a, which is 5 in this case.The return value of the function (i.e., 5) is assigned to the constant variable func.Finally, console.log(func); which is 5.

8. Create an object `calculator` with three methods: - `read()` prompts for two values and saves them as object properties with names `a` and `b` respectively. - `sum()` returns the sum of saved values. -    `mul() ` multiplies saved values and returns the result.

```js
const calculator = {
    read(){
        this.a = parseFloat(propmt("Enter the value for a"));
        this.b = parseFloat(prompt("Enter the value for b"));
    },
    sum(){
        return this.a + this.b;
    },
    mul(){
        return this.a*this.b;
    }
}

calculator.read();
console.log(calculator.sum()); // Output the sum of 'a' and 'b'
console.log(calculator.mul()); // Output the product of 'a' and 'b'

```

9. What is scope chain and lexical scoping in JS?

Scope Chain: Scope chain is a chain of lexical scopes that are used to resolve the value of a variable. When a variable is declared, it is added to the scope chain. When a function is executed, its local variables and function declarations are stored in an execution context. If a variable or function is not found in the current execution context, JavaScript looks up the scope chain to find the variable or function in its outer (enclosing) function's execution context. This process continues until the global execution context is reached.

Lexical Scoping: Lexical scoping is a Local memory of its execution context along with the lexical environment of parent (inwards to outwards). For example, a variable declared in a function is only accessible within that function and it cannot be accidentally accessed from outside of the function.

10. FEC (Function Execution Context) and GEC (Global Execution Context):

Function Execution Context (FEC): When a function is called, a new execution context is created for that function, known as the function execution context (FEC). It includes the function's arguments, local variables, and a reference to the outer (enclosing) function's scope. The FEC is added to the top of the scope chain for variable lookups. When the function finishes executing, its execution context is removed from the stack. The this keyword refers to the object that the function is executing within.

Global Execution Context (GEC): The global execution context (GEC) is the outermost execution context in a JavaScript program. It is created when the program starts executing and remains active until the program terminates. The GEC contains any global variables and functions defined in the program and serves as the top-level scope for variable lookups.

11. Write a JavaScript program to create a clock.

```js
  function updateClock() {
    const now = new Date();
    const hours = now.getHours()
    const minutes = now.getMinutes()
    const seconds = now.getSeconds()
  
    const clockDisplay = `${hours}:${minutes}:${seconds}`;
    console.log(clockDisplay);
  }
    setInterval(updateClock, 1000);

```

12. Make the following code work
[1, 2, 3, 4, 5, 6].shuffle();

```js
Array.prototype.shuffle = function() {
  for (let i = this.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [this[i], this[j]] = [this[j], this[i]];
  }
  return this;
};
console.log([1, 2, 3, 4, 5, 6].shuffle());

```