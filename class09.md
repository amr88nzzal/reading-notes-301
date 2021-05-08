# 301 class-09 reading notes

## [Concepts of Functional Programming in Javascript](https://medium.com/the-renaissance-developer/concepts-of-functional-programming-in-javascript-6bc84220d2aa)

### What is functional programming?

Typically functions are used for one of three things: procedures - a list of the instructions for the computer to call, mapping inputs to outputs, or IO - Network requests, user input, drawing to the screen etc. [[1]](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-pure-function-d1c076bec976)

### Pure functions

* Given the same parameters, it will always produce the same output.

* Avoids shared state.

* It does not cause any observable side effects - mutates an original object or array.

* What's not a pure function:

  * Anything that depends on time.

  * Random numbers generation within in the function, but can be passed to a function.

  * If it directly depends on [IO]( https://en.wikipedia.org/wiki/Input/output "Communication between an information processing system, such as a computer, and the outside world") e.g. user input, disk or network access.

### Immutability

* State cannot change after it’s created. Instead create a new object with the new value.

### Referential transparency

* When a function consistently yields the same result for the same input, it can be called referentially transparent.

* <b>pure functions + immutable data = referential transparency</b>

```JavaScript
const square = (n) => n * n;
square(2) // 4
```

### Functions as first-class entities

* The idea is to treat functions as values and pass functions like data. This way we can combine different functions to create new functions with new behavior.

* Functions as first-class entities can:

  1. Refer to it from constants and variables
  2. Pass it as a parameter to other functions
  3. Return it as result from other functions

```JavaScript
// These functions have similar logic, but the difference is the operators
const doubleSum = (a, b) => (a + b) * 2;
const doubleSubtraction = (a, b) => (a - b) * 2;
// A function that receives the operator function and use it inside our function.
const sum = (a, b) => a + b;
const subtraction = (a, b) => a - b;
const doubleOperator = (f, a, b) => f(a, b) * 2;
doubleOperator(sum, 3, 1); // 8
doubleOperator(subtraction, 3, 1); // 4
```

#### <b>Filter</b>

```JavaScript
// Imperative approach - Getting Even Numbers
let numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumber = numbers.filter(number => number % 2 === 0);
console.log(evenNumbers); // (6) [0, 2, 4, 6, 8, 10]
// Declarative approach - Getting Even Numbers
const even = n => n % 2 == 0; // Even comparison is assigned to a constant
const listOfNumbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
listOfNumbers.filter(even); // [0, 2, 4, 6, 8, 10]
```

#### <b>Map</b>

```JavaScript
// A List of People Objects
let people = [
  { name: "TK", age: 26 },
  { name: "Kaio", age: 10 },
  { name: "Kazumi", age: 30 }
];
// Imperative approach - Getting People Over 21
var peopleOver21 = people.filter(person => person.age > 21);
console.log(peopleOver21);
// Declarative approach - Getting People Over 21
const olderThan21 = person => person.age > 21;
const overAge = people => people.filter(olderThan21);
overAge(people); // [{ name: 'TK', age: 26 }, { name: 'Kazumi', age: 30 }]
```

#### <b>Reduce</b>

```JavaScript
// A List of Order Objects
var orders = [
  { productTitle: "Product 1", amount: 10 },
  { productTitle: "Product 2", amount: 30 },
  { productTitle: "Product 3", amount: 20 },
  { productTitle: "Product 4", amount: 60 }
];
// Imperative approach - Sum Amounts
var totalAmount = orders.reduce((a, b) => a + b.amount, 0);
console.log(totalAmount); // 120
// Declarative approach - Sum Amounts
const sumAmounts = (runningTotal, input) => runningTotal + input.amount;
const getTotalAmount = input => input.reduce(sumAmounts, 0);
getTotalAmount(orders);
```

## [Refactoring JavaScript for Performance and Readability](https://dev.to/healeycodes/refactoring-javascript-for-performance-and-readability-with-examples-1hec)

* It's important to get your code right the first time because in many businesses there isn't much value in refactoring.

### Using a Hash Function

* A hash function is used to map a given key to a location in the hash table.

```JavaScript
// Unrefactored code - On average we need to check half of those buckets before we find the correct short URL
const URLstore = [];
function makeShort(URL) {
  const rndName = Math.random().toString(36).substring(2);
  URLstore.push({[rndName]: URL});
  return rndName;
}
function getLong(shortURL) {
  for (let i = 0; i < URLstore.length; i++) {
    if (URLstore[i].hasOwnProperty(shortURL) !== false) {
      return URLstore[i][shortURL];
    }
  }
}
// Refactored Code -  On average we only need to check one bucket — no matter how many total buckets there are!
const URLstore = new Map(); // Change this to a Map
function makeShort(URL) {
  // Assuming that the random function have a collision
  const rndName = Math.random().toString(36).substring(2);
  // Place the short URL into the Map as the key with the long URL as the value
  URLstore.set(rndName, URL);
  return rndName;
}
function getLong(shortURL) {
  // Leave the function early to avoid an unnecessary else statement
  if (URLstore.has(shortURL) === false) {
    throw 'Not in URLstore!';
  }
  return URLstore.get(shortURL); // Get the long URL out of the Map
}
```

### Strategies

```JavaScript
// Return early from functions
function showProfile(user) {
  if (user.authenticated === true) {
    // ..
  }
}
// Refactor into ->
function showProfile(user) {
  // People often inline such checks
  if (user.authenticated === false) { return; }
  // Stay at the function indentation level, plus less brackets
}
```

```JavaScript
// Cache variables so functions can be read like sentences
function searchGroups(name) {
  for (let i = 0; i < continents.length; i++) {
    for (let j = 0; j < continents[i].length; j++) {
      for (let k = 0; k < continents[i][j].tags.length; k++) {
        if (continents[i][j].tags[k] === name) {
          return continents[i][j].id;
        }
      }
    }
  }
}
// Refactor into ->
function searchGroups(name) {
  for (let i = 0; i < continents.length; i++) {
    const group = continents[i]; // This code becomes self-documenting
    for (let j = 0; j < group.length; j++) {
      const tags = group[j].tags;
      for (let k = 0; k < tags.length; k++) {
        if (tags[k] === name) {
          return group[j].id; // The core of this nasty loop is clearer to read
        }
      }
    }
  }
}
```

```JavaScript
// Check for Web APIs before implementing your own functionality
function cacheBust(url) {
  return url.includes('?') === true ?
    `${url}&time=${Date.now()}` :
    `${url}?time=${Date.now()}`
}
// Refactor into ->
function cacheBust(url) {
  // This throws an error on invalid URL which stops undefined behaviour
  const urlObj = new URL(url);
  urlObj.searchParams.append('time', Date.now); // Easier to skim read
  return url.toString();
}
```