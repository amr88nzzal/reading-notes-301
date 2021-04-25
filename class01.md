# What is React ? 

Simply we can define react as a javaScript library for building interactive user interfaces ,It lets you compose complex UIs from small and isolated pieces of code called “components”. and React will efficiently update and render just the right components when your data changes.Each React component is encapsulated and can operate independently; this allows you to build complex UIs from simple components.


# Simple example on react :

	ReactDOM.render(<p>This a simple example on how to use react to render this paragraph inside the div container </p> , document.getElementById('container') );



# What is JSX ?
It's a syntax extension to write html elements directly in the javaScript .

`const htmlElement = <p>a paragraph element </p> ;`

We can also assign attributes for those elements and we can use expressions inside the elements .

`const stringVar = 'how to use expression using JSX ';
const htmlElement = <p id="paragraph" >this Example on {stringVar}</p>`


# Render using React :
we can render a react element inside a specific html element using ReactDOM.render() .

`const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));`


