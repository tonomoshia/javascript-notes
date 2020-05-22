## Scope

### Global Variables

When you create a variable in a file that is not enclosed in a `function`, module or `if` statement, it is a *global variable*.
It can be accessed from any other JavaScript that is running on the page, like a `<script>` tag. Or in the console. 

In the browswer, *global scope* is the `window`.

`var` variables are attached to the `window` object and are global scoped.

`const` and `let` variables declared outside of a code block are also globally scoped but they are not attached.

Making *global variables* is _discouraged_. Is a recipe for a headache in almost all use cases. 

###### Comment on Global Variables
Best Practice:  Try not to create global variables as they can lead to bugs (_unexpected results_) down the road.

### Scope in general
#### Function Scope
Variables created inside of a function are only available inside that function (unless we explicity `return` it and put it into its own variable inside the function). {} are fences that keep the variables in and do not allow them to leak out. They can _leak in_ though. So you can use a global variables inside a function. 


###### [Eloquent JavaScript Chapter 3: Functions (excerpt)][2]
>>Bindings declared with let and const are in fact local to the block that they are declared in, so if you create one of those inside of a loop, the code before and after the loop cannot “see” it. In pre-2015 JavaScript, only functions created new scopes, so old-style bindings, created with the var keyword, are visible throughout the whole function that they appear in—or throughout the global scope, if they are not in a function.

Shadow variables: You can name variable the same thing if they are not in the same scope, however it is not a good idea as it often leads to uncertain results. 

###### [StackOverflow on Variable Shadowing in JavaScript][1]
>>In computer programming, variable shadowing occurs when a variable declared within a certain scope (decision block, method, or inner class) has the same name as a variable declared in an outer scope. This outer variable is said to be shadowed...


If you have a function inside another function - that function will only be able to be invoked inside the parent function. 

#### Block Scope
`{ }` = Code block. Gates that keep variables inside. They are not allowed to leave those gates. 

If you need a variable to be available outside of a block, declare the above the code block and then define it (set it to something) inside the code block. 

![Variable Above A Code Block](variable-above-if-statement.png)

`var` variables are not **block scoped**. They are **function scoped**.

`let` variables are **block scoped**.

#### Scope lookup
Lexical Scoping -> scope lookup happens where functions are _defined_, not where they're run.

--
- [x] TODO: Add some information from [Soumya's Notion Notes][3] on Scope before finalizing notes.

# Soumya's Hoisting Notes

## Scope

Scope answers the question: *"Where are my variables and functions available to me?".*

- **Global Variables**

    Available anywhere. They are created not inside a function, module, if statement etc.

    `<script> const first = 'Soumya'; </script> //here first is a global variable.`

    In the browser, the global scope is called *window.* Methods like `setTimeout, setInterval` are available on the *window* object.

    ```jsx
    const first = 'wes';
    let second = 'bos';
    var third = 100;

    console.log(window.first); // undefined
    console.log(window.second); // undefined
    console.log(window.third); // 100
    ```

    The above occurs because `var` variables are attached to the window object and are globally scoped, whereas `const` and `let` variables are globally scoped but not attached to the window object.

    Anything except `let` and `const` declared things which are globally declared are attached to window object.

    ```jsx
    function sayHi() {
    	console.log('HI');
    }

    sayHi(); // HI
    window.sayHi(); // HI
    ```

    Using global scoped variables etc. are not advised in general.

    More examples:

    ```jsx
    const age = 100;
    function go() {
    	const cool = true;
    }
    go();

    console.log(age); // 100
    console.log(cool); // Uncaught ReferenceError: cool is not defined
    ```

    Above, `cool` is function-scoped. Function scoping means anything declared inside of a function is only accessible inside the function and not outside (unless we return it from the function and store the returned value in a variable when the function is run)

    **Scope Lookup:** If variables are not found inside a function, it goes a level higher to look for the variable in that scope and if its not available in that scope as well, it goes another level higher.

    ```jsx
    const age = 100;
    function go() {
    	const cool = true;
    	console.log(age); 
    	console.log(cool); 
    }
    go();

    // console output:
    // 100 - this is printed as it doesn't find variable age in go function scope it goes a level higher to find it
    // true
    ```

    ```jsx
    const age = 100;
    function go() {
    	const cool = true;
    	const age = 200; // global variable age has been shadowed by this variable - shadow variable
    	console.log(age); 
    	console.log(cool); 
    	}
    go();

    // console output:
    // 200 - this is printed because it finds variable age in go function scope only
    // true
    ```

    **Block Scope:**

    ```jsx
    if(1 === 1){
    	const cool = true; // or let cool = true;
    }

    console.log(cool);

    //Output: Uncaught ReferenceError: cool is not defined
    ```

    ```jsx
    if(1 === 1){
    	var cool = true;
    }

    console.log(cool);

    //Output: true - var varibales leak outside the block
    ```

    A set of curly brackets are referred to as a block.

    To access a variable outside a block, we use:

    ```jsx
    let cool;
    if(1 === 1){
    	cool = true;
    }

    console.log(cool);

    //Output: true
    ```

    Above the `cool` variable is declared in the higher scope, here global scope.

    `var` variables are *function scoped*. Let's see here:

    ```jsx
    function isCool(name) {
      if (name === 'wes') {
        var cool = true;
      }
      console.log(cool);
      return cool;
    }

    isCool('wes');

    //Output: true
    ```

    Above, as the variable `cool` was declared using `var` keyword, it was not limited within the `if` block, rather it was available inside the entire `isCool` function.

    `let` and `const` variables are *block scoped.*

    Example:

    ```jsx
    const dog = "snickers";

    function logDog() {
      console.log(dog);
    }

    function go() {
      const dog = "sunny";
      logDog();
    }

    go();

    // Output: snickers
    ```

    Above happens as JavaScript uses *Lexical Scoping* or *Static Scoping.* It means, *variable lookup or scope lookup happens where the functions are defined not where they are run.*

    In the above example, `logDog` function is defined above where there is no `dog` variable inside its definition, so it goes and looks in upper/higher scope to find value as 'snickers'. It doesn't care where it is run, in this case inside `go` function.

    ```jsx
    const dog = "snickers";

    function logDog(dog) {
      console.log(dog);
    }

    function go() {
      const dog = "sunny";
      logDog("Rufus");
    }

    go();

    //Output : Rufus
    ```

    The above is the output because here the function `logDog` creates a local variable for parameter `dog` which has value 'Rufus' passed to it. So, 'Rufus' is printed.

     **Best practices for variables:**

    - Try not to create global variables.

    **Function Scoping:**

    Functions are scoped the exact same way as variables.

    ```jsx
    function sayHi(name) {
     function yell() {
      console.log(name.toUpperCase());
    	}
    }
    yell();

    // Output: Uncaught ReferenceError: yell is not defined
    ```

    Just like variables, functions are scoped to the parent function. So `yell` function above is only accessible inside `sayHi` function, and not outside it.


[1]: https://stackoverflow.com/questions/11901427/an-example-of-variable-shadowing-in-javascript
[2]: https://eloquentjavascript.net/03_functions.html
[3]: https://www.notion.so/Beginner-JavaScript-e2ef045754d14e96b93791f638bbcaf6