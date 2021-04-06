## Module 1
### Common Design Patterns
(Optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goals
* Get familiar with React's common design patterns 
* Understand the motivation and when should you apply them

---

### Agenda
1. Logical / View component separation
2. High Order Component 
3. Components Index
4. Composition vs Inheritance  
5. Lazy loading and Suspense
6. Controlled / Uncontrolled Components
7. Some more patterns

---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
A design pattern of separate complex logic from other aspects a component. 

Other names:
<!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Smart and Dumb components
* <!-- .element: class="fragment" -->Container and View components
* <!-- .element: class="fragment" -->Logic / Data and Presentational components

---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
[Example:](https://gist.github.com/chantastic/fc9e3853464dffdb1e3c)
```
const Commentlist = comments => (
  <ul>
    {comments.map(({ body, author }) =>
      <li>{body}-{author}</li>
    )}
  </ul>
)

class CommentListContainer extends React.Component {
  constructor() {
    super();
    this.state = { comments: [] }
  }

  componentDidMount() {
    // get images somehow and update state
  }

  render() {
    return <CommentList comments={this.state.comments} />;
  }
}

```
---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
Practice time

File `module1\logic-view-separation.html`

---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
Keep in mind:

There are other technique to achieve this goals, like [hooks](https://reactjs.org/docs/hooks-custom.html).
Make sure not to enforce this technique without necessity.

---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
<div style="text-align:left">

Usage:

* <!-- .element: class="fragment" -->When separation can make components reusable. 
* <!-- .element: class="fragment" -->When you want to simplify complex component. 
* <!-- .element: class="fragment" -->When writing test seams hard due to component complexity. 

Pitfalls:
<!-- .element: class="fragment" -->
* Over - usage <!-- .element: class="fragment" -->[when not required](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

</div>

---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
> A higher-order component (HOC) is an advanced technique in React for reusing component logic

Simply put, its is a function that takes a component and returns a new component.
<!-- .element: class="fragment" -->

Remember, component is (mostly a) function. 
<!-- .element: class="fragment" -->

---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
Simple example
```
const withUser = InnerComponent => {
  const user = sessionStorage.getItem('user');
  return props => <InnerComponent user={user} {...props} />;
};

const UserComponent = props => (
    <p>My name is {props.user}!</p>
);
// this is why export should be on seperate line...
export default withUser(UserPage);
```

---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
More examples:
* [react-docs](https://reactjs.org/docs/higher-order-components.html)
* react-redux [connect](https://react-redux.js.org/api/connect)
* react [withRouter](https://reacttraining.com/react-router/core/api/withRouter)
* [Wrapping Apollo GQL hooks](https://medium.com/@yuval.bar.levi/how-to-skyrocket-your-react-app-with-apollo-clientv3-ec384ba02bd6)

---
### [High Order Component](https://reactjs.org/docs/higher-order-components.html)

Practice time

File `module1\HOC.html`

---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
<div style="text-align:left">

Usage:

* Mostly when using 3rd Party libraries. 
<!-- .element: class="fragment" -->
* You can enhance you component (like - custom state-management access)  
<!-- .element: class="fragment" -->

Pitfalls:
<!-- .element: class="fragment" -->
* [Don’t Use HOCs Inside the render Method](https://reactjs.org/docs/higher-order-components.html)
<!-- .element: class="fragment" -->
* [Static Methods Must Be Copied Over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)
<!-- .element: class="fragment" -->
* [Refs Aren’t Passed Through](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)
<!-- .element: class="fragment" -->
* [Other solutions (like Hooks) might be simpler for some cases](https://reactrouter.com/web/api/Hooks)
<!-- .element: class="fragment" -->

</div>

---

### [Components Index](https://alligator.io/react/index-js-public-interfaces/)
It's a technique rather than Design Pattern (not React specific)
```
// atoms/index.js
export {default as Button} from './Button';
export {default as Slider} from './Slider';
export {default as TextBox} from './TextBox';

// HomePage.js - using index file
import {Button, Slider, TextBox} from './atoms'
```
<!-- .element: class="fragment" -->
Usage: Create explicit public interfaces (useful when working in large teams)
<!-- .element: class="fragment" -->

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)
Where should we use Components Inheritance?

> "At Facebook, we use React in thousands of components, and we haven’t found any use cases where we would recommend creating component inheritance hierarchies."
<!-- .element: class="fragment" -->

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)

Sometimes we think about components as being “special cases” of other components.

Using composition, we can create **Specific** Component by rendering more **Generic**
Component with **Specific `props` or `children`**
<!-- .element: class="fragment" -->

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)
```
const Dialog = ({title, message) => (
  <div className="dialog">
    <h1 className="dialog-title">
      {title}
    </h1>
    <p className="dialog-message"
      {message}
    </p>
  </div>
);

const WelcomeDialog = () => (
  <Dialog title="Welcome"
    message="Thank you for visiting our spacecraft!" />
);
```

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)
Some components don’t know their children ahead of time. 
This is especially common for components like Sidebar or Dialog that represent generic “boxes”.

```
const SplitPane({left, right) => (
  <div className="SplitPane">
    <div className="SplitPane-left">
      {left}
    </div>
    <div className="SplitPane-right">
      {right}
    </div>
  </div>
);

const App() => (
  <SplitPane 
    left={<Contacts />}
    right={<Chat />} 
  />
);
```
<!-- .element: class="fragment" -->

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)

Usage:

When it can make the app more consistent. When composition can make components reusable (usually the two comes together)

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)

Practice time

File `module1\composition.html`

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
Suspense lets your components "wait" for something before they can render.
* [Code Splitting](https://reactjs.org/docs/code-splitting.html#code-splitting)
* [React.lazy](https://reactjs.org/docs/code-splitting.html#reactlazy)
* [Error boundaries](https://reactjs.org/docs/code-splitting.html#error-boundaries)
* [Route-based code splitting](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting)
* [Example with data](https://codesandbox.io/s/frosty-hermann-bztrp)

---
### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
Usage of suspend (stable)
```
import Component1 from './Component1';
const Component2 = React.lazy(() => import('./Component2'));
const Component3 = React.lazy(() => import('./Component3'));

// Show a single spinner while components are loading
// Note you can include synchronious component in suspend
<Suspense fallback={<Spinner />}>
  <Component1 />
  <Component2 />
  <Component3 />
</Suspense>
```

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
Some words about Concurrent Mode (Experimental)

The problem - UI may freeze / stuck / etc - because:
<!-- .element: class="fragment" -->
* Single UI thread
<!-- .element: class="fragment" -->
* Render cannot be paused after started
<!-- .element: class="fragment" -->

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
The (React) solution: Concurrent Mode

> Concurrent Mode is a **set of new features** that help React apps stay responsive and gracefully adjust to the user’s device capabilities and network speed
<!-- .element: class="fragment" -->

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
Concurrent Mode is a set of new features. 

Some are stable (like fiber) while other still experimental (some aspects of Suspend)
<!-- .element: class="fragment" -->

Experimental Features:
<!-- .element: class="fragment" -->

* <!-- .element: class="fragment" -->Pause render 
    - Example: pause showing spinner if data become available before render required
    <!-- .element: class="fragment" -->

* <!-- .element: class="fragment" -->Scheduling - set priorities for different tasks
    - Example: user input vs render<!-- .element: class="fragment" -->


---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
<div style="text-align:left">

Usage: 

When waiting for code / data (preferably split code)

Pitfalls:
<!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Coupling (Fetching data from inside components)

* <!-- .element: class="fragment" -->Using when not required (as a state replacement)


</div>

---

### Controlled / Uncontrolled Components
Question: What's the problem with forms elements in React (input, textarea, and select) in React?
<!-- .element: class="fragment" -->

Answer: they already have some sort of "state"
<!-- .element: class="fragment" -->

Example: when we type inside an input we change it's value
<!-- .element: class="fragment" -->

---

### Controlled / Uncontrolled Components

There are two ways to treat this "internal state"

* Manage it - Force them to behave like any other component <!-- .element: class="fragment" -->([Controlled Components](https://reactjs.org/docs/forms.html#controlled-components))
* Leave it - Keep the default behaviour <!-- .element: class="fragment" -->([Uncontrolled Components](https://reactjs.org/docs/uncontrolled-components.html))

---

### Controlled / Uncontrolled Components
The common way to use form elements in React is using [Controlled Components](https://reactjs.org/docs/forms.html#controlled-components).
```jsx harmony
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};
  }

  handleChange = (event) => {
    this.setState({value: event.target.value});
  }

  handleSubmit = (event) => {
    event.preventDefault();
    props.doStuff(this.state.value);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" 
                 value={this.state.value}           
                 onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
<!-- .element: class="fragment" -->

---

### Controlled / Uncontrolled Components
The alternative is [Uncontrolled components](https://codepen.io/gaearon/pen/WooRWa?editors=0010), where form data is handled by the DOM itself.
```jsx harmony
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.input = React.createRef();
  }

  handleSubmit = (event) => {
    event.preventDefault();
    props.doStuff(this.input.current.value);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
<!-- .element: class="fragment" -->

---

### Controlled / Uncontrolled Components

Notice the [usage of Ref](https://reactjs.org/docs/refs-and-the-dom.html).
> Refs provide a way to access DOM nodes or React elements created in the render method

* <!-- .element: class="fragment" -->Access the DOM node using <code>current</code> property
* <!-- .element: class="fragment" --><code>current</code> property will be assigned by React (using `ref` prop) 



---

### Controlled / Uncontrolled Components
* Ref can hold any value - not just DOM nodes
<!-- .element: class="fragment" -->
* Ref will be create once and live until component unmount (like state)
<!-- .element: class="fragment" -->
* Ref can be <!-- .element: class="fragment" -->[forwarded](https://reactjs.org/docs/forwarding-refs.html)

```jsx harmony
// use forwardRef HOC
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```
<!-- .element: class="fragment" -->

---

### Some more patterns
* [Forwarding Refs](https://reactjs.org/docs/forwarding-refs.html)
* [Fragments](https://reactjs.org/docs/fragments.html)
* [React.PureComponent](https://reactjs.org/docs/react-api.html#reactpurecomponent)
* [React.memo](https://reactjs.org/docs/hooks-reference.html#usememo)
* [Portals](https://reactjs.org/docs/portals.html)
* [Error Boundaries](https://reactjs.org/docs/error-boundaries.html)
* [Context](https://reactjs.org/docs/context.html)
* [JSX Dot Notation](https://reactjs.org/docs/jsx-in-depth.html#using-dot-notation-for-jsx-type)

---

### Wrap Up
Design Patterns are general repeatable solution to common problems in software design

Let's go over the problems and solutions we have covered
<!-- .element: class="fragment" -->

<div style="text-align:left">


Reusing component logic
<!-- .element: class="fragment" -->
* HOC
<!-- .element: class="fragment" -->
* Logical / View component separation
<!-- .element: class="fragment" -->

</div>

---

### Wrap Up
<div style="text-align:left">


Reusing Component view
<!-- .element: class="fragment" -->
* Logical / View component separation
<!-- .element: class="fragment" -->
* Composition
<!-- .element: class="fragment" -->



Large app with lots of code
<!-- .element: class="fragment" -->
* Code splitting and lazy loading
<!-- .element: class="fragment" -->

</div>

---

### Wrap Up
<div style="text-align:left">


Default element behavior is preferable  
<!-- .element: class="fragment" -->
* Uncontrolled Components
<!-- .element: class="fragment" -->

DOM element access required 
<!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Using `ref`

</div>

---

### Further reading
* [A Quick Intro to React's Higher-Order Components](https://alligator.io/react/higher-order-components/)
* [An introduction to HOC](https://levelup.gitconnected.com/understanding-react-higher-order-components-by-example-95e8c47c8006)
* [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
* [Categorizing Components Into Smart & Dumb Components](https://alligator.io/react/smart-dumb-components/)

---

### Extra
* [Render Props](https://reactjs.org/docs/render-props.html)
* [Modern React - The Essentials](https://www.youtube.com/watch?v=sjjaGxs3e1c&t=879s)
* [Concurrent Mode](https://reactjs.org/docs/concurrent-mode-intro.html)
* [Real world examples of Higher Order Components](https://medium.com/@onoufriosm/real-world-examples-of-higher-order-components-hoc-for-react-871f0d8b39d8)
* [Use React Memo Wisely/](https://dmitripavlutin.com/use-react-memo-wisely/)
