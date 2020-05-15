
## Functions - Custom

-   Functions are **created / defined** then they are **called / run**.
    
-   Defining a function:
    
    ```javascript
      // Function definition
      
      function calculateBill() {
      	// this is the function body
      	console.log('running calculateBill');
      }
    
    ```
    
-   Calling a function:
    
    ```javascript
      // Function call or run
      
      calculateBill(); // running calculateBill (returns undefined)
    
    ```
    
-   Variables created inside a function are not available outside the function. e.g. `total` above.
    
    It is a **temporary variable.** It is `function scoped`. After running of the function is complete, the variable is cleaned up or garbage-collected.
    
-   **Returning value from function:**
    
    ```javascript
      function calculateBill() {
      	const total = 100 * 1.13;
      	return total; // total is returned
      }
      
      calculateBill(); // returns 112.999999999
    
    ```
    
-   Capturing returned value from a function into a variable:
    
    `const myTotal = calculateBill();` (myTotal will have value 112.999999999)
    
-   You can also include the function in your interpolated string:
    ```console.log(`Your bill is $${calculateBill()}.`)```
