# Read: Class 03 - Readings: Passing Functions as Props

<p>&nbsp;</p>

## Lifting State Up
--- 
> When several components need to reflect the same changing data. It is recommended lifting the shared state up to their closest common ancestor.

<p>&nbsp;</p>

## Lists and Keys
---
### Rendering Multiple Components

example: 
1. Here we are creating multiple `<li>` elements  and we use the curly brackets for creating a collection of elements.

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```
<p>&nbsp;</p>

2. include the entire listItems array inside a <ul> element, and render it to the DOM:

```js
ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```
<p>&nbsp;</p>
<p>&nbsp;</p>

## The spread Operator
---
```js
Math.max(1,3,5) // 5
Math.max([1,3,5]) // NaN
```
<p>&nbsp;</p>

 > adding spread operator (...) removed the undefined.
` Math.max(...[1,3,5]) // 5 ` 
<p>&nbsp;</p>


##  Stuff the spread operator can do:
---
1. The spread syntax “spreads” the array into separate arguments.
2. Copying an array
3. Concatenating or combining arrays
4. Using Math functions
5. Using an array as arguments
6. Adding an item to a list
7. Adding to state in React
8. Combining objects
9. Converting NodeList to an array



<p>&nbsp;</p>
<p>&nbsp;</p>

## References:
---
1. [React Docs - Lifting State Up](https://reactjs.org/docs/lifting-state-up.html)
2. [React Docs - lists and keys](https://reactjs.org/docs/lists-and-keys.html)
3. [React Tutorial through ‘Declaring a Winner’](https://reactjs.org/tutorial/tutorial.html)
4. [The Spread Operator](https://medium.com/coding-at-dawn/how-to-use-the-spread-operator-in-javascript-b9e4a8b06fab)