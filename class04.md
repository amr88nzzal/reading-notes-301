# Forms
#### HTML form elements work a little bit differently from other DOM elements in React, because form elements naturally keep some internal state. For example, this form in plain HTML accepts a single name:
### Controlled Components:
##### In HTML, form elements such as (input), (textarea), and (select) typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState().
##### We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. An input form element whose value is controlled by React in this way is called a “controlled component”.
### The textarea Tag:
##### In React, a (textarea) uses a value attribute instead.
##### Notice that this.state.value is initialized in the constructor, so that the text area starts off with some text in it.
### The select Tag:
##### Note that the Coconut option is initially selected, because of the selected attribute. React, instead of using this selected attribute, uses a value attribute on the root select tag. This is more convenient in a controlled component because you only need to update it in one place.
##### Overall, this makes it so that (input type="text"), (textarea), and (select) all work very similarly - they all accept a value attribute that you can use to implement a controlled component.
### The file input Tag:
##### In HTML, an (input type="file") lets the user choose one or more files from their device storage to be uploaded to a server or manipulated by JavaScript via the File API.
##### Because its value is read-only, it is an uncontrolled component in React. It is discussed together with other uncontrolled components later in the documentation.