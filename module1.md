## Module 1
### Common Design Patterns
(This document is optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goal
Get familiar with common design patterns in React and when should you apply them. 

---

### Agenda
1. High Order Component 
2. Logical / View component separation
3. Component Index
4. Composition vs Inheritance  
5. Lazy loading and Suspense
6. Controlled / Uncontrolled Components
7. Some more patterns


---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
> A higher-order component (HOC) is an advanced technique in React for reusing component logic

Simply put, its is a function that takes a component and returns a new component.
<!-- .element: class="fragment" -->

And remember, component is (mostly a) function. 
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

---

### Practice 1

---

### [High Order Component](https://reactjs.org/docs/higher-order-components.html)
Usage:

Mostly when using 2rd Party libraries. You can enhance you component (like - custom state-management access)  

Pitfalls:
* [Don’t Use HOCs Inside the render Method](https://reactjs.org/docs/higher-order-components.html)
* [Static Methods Must Be Copied Over](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)
* [Refs Aren’t Passed Through](https://reactjs.org/docs/higher-order-components.html#static-methods-must-be-copied-over)

---

### [Logical / View component separation](https://medium.com/@thejasonfile/dumb-components-and-smart-components-e7b33a698d43)
A design pattern of separate complex logic from other aspects a component. Other names:
* smart and dumb components
* Container and View components

Note: there are other technic to achieve this goals, like [hooks](https://reactjs.org/docs/hooks-custom.html).
Make sure not to enforce this technic without necessity.
<!-- .element: class="fragment" -->

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
Usage:

When separation can make components reusable. When you want to simplify complex component. 

Pitfalls:
* [Over - usage when not required](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

---

### [Component Index](https://alligator.io/react/index-js-public-interfaces/)

```
// atoms/index.js
export {default as Button} from './Button';
export {default as Slider} from './Slider';
export {default as TextBox} from './TextBox';

// HomePage.js - using index file
import {Button, Slider, TextBox} from './atoms'
```

Usage: Create explicit public interfaces (useful when working in large teams)

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)
> "At Facebook, we use React in thousands of components, and we haven’t found any use cases where we would recommend creating component inheritance hierarchies."

Sometimes we think about components as being “special cases” of other components.
Using composition, we can create **Specific** Component by rendering more **Generic**
Component with **Specific `props` or `children`**

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)
```
const Dialog({title, message) => (
  <FancyBorder color="blue">
    <h1 className="Dialog-title">
      {title}
    </h1>
    <p className="Dialog-message"
      {message}
    </p>
  </FancyBorder>
);

const WelcomeDialog() => (
  <Dialog
    title="Welcome"
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

---

### [Composition vs Inheritance](https://reactjs.org/docs/composition-vs-inheritance.html)

Usage:

When it can make the app more consistent. When composition can make components reusable (usually the two comes together)

---

### Practice 2



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
* Single UI thread
* Render cannot be paused after started

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
The (React) solution:  Concurrent Mode

> Concurrent Mode is a **set of new features** that help React apps stay responsive and gracefully adjust to the user’s device capabilities and network speed

Some are stable (like fiber) while other still experimental (some aspects of Suspend), Like:
* Pause render (example: pause showing spinner if data become available before render required)
* Scheduling - set priorities for different tasks (user input vs render)

---

### [Lazy loading and Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)

Usage : When waiting for code / data (preferably split code)

Pitfalls:
* Coupling (Fetching data from inside components)
* Using when not required (as a state replacement)

---

### Controlled / Uncontrolled Components

---

### Practice 3

---

### Some more patterns

https://reactjs.org/docs/react-api.html#reactpurecomponent
https://reactjs.org/docs/refs-and-the-dom.html
https://reactjs.org/docs/forwarding-refs.html
https://reactjs.org/docs/hooks-reference.html#usememo
https://dev.to/dinhhuyams/introduction-to-react-memo-usememo-and-usecallback-5ei3
https://reactjs.org/docs/fragments.html
https://reactjs.org/docs/portals.html
https://reactjs.org/docs/error-boundaries.html
https://reactjs.org/docs/context.html
React.memo

---

### Further reading
* [A Quick Intro to React's Higher-Order Components](https://alligator.io/react/higher-order-components/)
* [An introduction to HOC](https://levelup.gitconnected.com/understanding-react-higher-order-components-by-example-95e8c47c8006)
* [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

---

### Extra
* [Render Props](https://reactjs.org/docs/render-props.html)
* [Modern React - The Essentials](https://www.youtube.com/watch?v=sjjaGxs3e1c&t=879s)
* [Concurrent Mode](https://reactjs.org/docs/concurrent-mode-intro.html)
