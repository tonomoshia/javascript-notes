## Hoisting

Allows us to access functions and variables *before they are created*.

2 things that are hoisted in JavaScript:

- Function declarations
- Variable declarations

**Function hoisting**

```jsx
sayHi();

function sayHi() {
  console.log('Hi');
}

// Output - Hi
```

The above happens because when we run the JavaScript file, JavaScript compiler will take all function declarations and move them to the top of the file available for use.

Suggestion: Always define functions *before* using them.

**Note**: Functions made using a variable are not hoisted.

```jsx
add(10,20);

const add = function(a,b) {
	return a + b;
}

//Output - Uncaught ReferenceError: Cannot access 'add' before initialization
```

**Variable hoisting**

```jsx
console.log(age);
var age = 10;

// Output - undefined
```

This happens because JavaScript hoists the variable declaration but not the actual setting of the values or assignment. This essentially means this happens:

```jsx
var age;
console.log(age);
age = 10;

// Output - undefined
```