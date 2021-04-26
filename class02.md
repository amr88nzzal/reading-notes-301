# State and Props
## State and Lifecycle
### Converting a Function to a Class

- You can convert a function component to a class in five steps:
    1. Create an `ES6 class`, with the same name, that extends React.Component.
    2. Add a single empty method to it called render().
    3. Move the body of the function into the render() method.
    4. Replace props with this.props in the render() body.
    5. Delete the remaining empty function declaration.

- The render method will be called each time an update happens, but as long as we render a **specified component**  into the same DOM node, only a single instance of that **component** class will be used. This lets us use additional features such as local state and lifecycle methods.

### Adding Local State to a Class

- You convert this:

```
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);

```

- to this :

```
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```  



### Adding Lifecycle Methods to a Class

- Whenever a component is changed, after it's rendered to the DOM for the first time. It is called “mounting” in React.

- We call clearing changes, whenever the DOM produced by the component is removed. “unmounting” in React.

- A pair of “**mounting**” and “**unmounting**” is called the **lifecycle methods**

### Using State Correctly

- There are three things you should know about `setState()`.

    1. Do Not Modify State Directly  
        this is wrong: `this.state.comment = 'Hello';`  
        instead : `this.setState({comment: 'Hello'});`  
        - The only place where you can assign this.state is the constructor.

    2. State Updates May Be Asynchronous  
        React may batch multiple `setState()` calls into a single update for performance.   
        Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.  
        - this fails: `this.setState({counter: this.state.counter + this.props.increment,});`  
        - this works: `this.setState((state, props) => ({  counter: state.counter + props.increment`
    3. State Updates are Merged  
        - When you call `setState()`, React merges the object you provide into the current state.

### The Data Flows Down

- Neither parent nor child components can know if a certain component is stateful or stateless, and they shouldn’t care whether it is defined as a function or a class.

- In React apps, whether a component is stateful or stateless is considered an implementation detail of the component that may change over time. You can use stateless components inside stateful components, and vice versa.

## Handling Events

- There are some syntax differences between **React** events and the **DOM** events:
    1. React events are named using camelCase, rather than lowercase.
    1. With JSX you pass a function as the event handler, rather than a string.

- In the **DOM** way:   


```
<button onclick="activateLasers()">
  Activate Lasers
</button>

```

- In the **React** way:  

```
<button onClick={activateLasers}>
  Activate Lasers
</button>

```

- Another difference is that you cannot return false to prevent default behavior in React. You must call `preventDefault` explicitly.

- When using React, you generally don’t need to call `addEventListener` to add listeners to a DOM element after it is created. Instead, just provide a listener when the element is initially rendered.

### Passing Arguments to Event Handlers

- You can pass an extra parameter to an event handler:
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

- the `e` argument representing the React event will be passed as a second argument after the ID. With an arrow function, we have to pass it explicitly, but with bind any further arguments are automatically forwarded.

### Conditional Rendering

- In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of your application.

- Conditional rendering in React works the same way conditions work in JavaScript. Use JavaScript operators like `if` or the `conditional operator` to create elements representing the current state, and let React update the UI to match them.

### Element Variables

- ou can use variables to store elements. This can help you conditionally render a part of the component while the rest of the output doesn’t change

### Inline If with Logical && Operator

- In JavaScript, **true** `&&` **expression** always evaluates to **expression**, and **false** `&&` **expression** always evaluates to `false`.

- Therefore, if the condition is `true`, the element right after &``& will appear in the output. If it is `false`, React will ignore and skip it.

- example :  

```
render() {
  const count = 0;
  return (
    <div>
      { count && <h1>Messages: {count}</h1>}
    </div>
  );
}

```


### Inline If-Else with Conditional Operator

- Another method for conditionally rendering elements inline is to use the JavaScript conditional operator `condition ? true : false`. 

- example:  

```
render() {
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoggedIn
        ? <LogoutButton onClick={this.handleLogoutClick} />
        : <LoginButton onClick={this.handleLoginClick} />
      }
    </div>
  );
}  

```


![Image](https://www.ionos.com/digitalguide/fileadmin/DigitalGuide/Teaser/pair-programming-t.jpg)