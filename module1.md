## Module 1
### Common Design Patterns
(This document is optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

---

### Agenda
1. High Order Component 
2. Logical / View component separation
3. Component Index
4. Composition vs Inheritance  
5. Lazy loading and Suspense
6. Controlled / Uncontrolled Components

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

### []()

---

### []()

---

### []()



---
overview on each
practice (on single page environment):
* High Order Component 
* Logical / View component separation
* Lazy loading and Suspense

### Further reading
* [A Quick Intro to React's Higher-Order Components](https://alligator.io/react/higher-order-components/)
* [An introduction to HOC](https://levelup.gitconnected.com/understanding-react-higher-order-components-by-example-95e8c47c8006)
* [Render Props](https://reactjs.org/docs/render-props.html)
* [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

---

### Home Work:
* Finish class practice

### Extra
* Investigate demo project
