# Closures

(thank you [Soumaya Ranjan Mohanty](https://www.notion.so/Beginner-JavaScript-e2ef045754d14e96b93791f638bbcaf6))

Ability to access a parent level scope from a child scope even after the parent function has been closed/terminated.

```jsx
function outer() {
  const outerVar = 'Hey I am the outer var!';
  
   function inner() {
    const innerVar = 'Hey I am an inner var!'
    console.log(innerVar)
        console.log(outerVar)

    
  }
  return inner;

}

const innerFn = outer()
innerFn()

// Output - 
// "Hey I am an inner var!"
// "Hey I am the outer var!"
```

This happens because even though `outer` function is done running in the line `const innerFn = outer()` , the variable `outerVar` is still maintained in memory/accessible at a later time even if it is not returned. It is not cleaned up or garbage collected.

**More examples:**

```jsx
function createGreeting(greeting = '') {
  const myGreet = greeting.toUpperCase()
  return function (name) {
    return myGreet + ' ' + name
  }
}

const sayHello = createGreeting('hello')
const sayHey= createGreeting('hey')

console.log(sayHello('wes'))
console.log(sayHello('kait'))
console.log(sayHey('kait'))

// Output - 
// **"HELLO wes"
// "HELLO kait"
// "HEY kait"**
```

The `myGreet` variable is still accessible even after `createGreeting` is done running.

```jsx
function createGame(gameName) {
  let score = 0;
  return function win(){
    score += 1;
    return `Your game ${gameName} score is ${score}`
  }
}

const hockeyGame = createGame('hockey')
const soccerGame = createGame('soccer')

// In console run,
// hockeyGame()
// "Your game hockey score is 1"
// hockeyGame()
// "Your game hockey score is 2"
// hockeyGame()
// "Your game hockey score is 3"
// soccerGame()
// "Your game soccer score is 1"
// soccerGame()
// "Your game soccer score is 2"
```

`score` is a *private variable* here. We can access multiple games at once like that.