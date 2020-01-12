## Module 3
### Functional Components and Hooks
(This document is optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

---

### Agenda
1. Functional vs Class Components
2. React Hooks introduction
3. Writing Custom Hooks
4. Refactoring with Hooks
5. Pitfalls

---

### Functional vs Class Components
So far

| Class                 | Function      |
| -------------         |:-------------:|
| Stateful              | Stateless     |
| Lifecycle events      | X             |
| Complex               | Simple        |

---

### Functional vs Class Components
And there is...

    <div>
        <img src="./assets/this.gif">
    </div>
    <!-- .element: class="fragment" -->


---

### React Hooks introduction
[Motivation:](https://reactjs.org/docs/hooks-intro.html)
>* It’s hard to reuse stateful logic between components
>* Complex components become hard to understand
>* Classes confuse both people and machines (this) 

---

### React Hooks introduction
* [Hooks Overview](https://reactjs.org/docs/hooks-overview.html)
* [State hook](https://reactjs.org/docs/hooks-state.html)
* [Effect hook](https://reactjs.org/docs/hooks-effect.html)
* Live Demo

---

### Practice Time - warmup
convert class to hooks


---

### Writing Custom Hooks
Exist Hooks
Writing Costume hooks - useInput
Rooks and other hooks

---

### Practice Time
repo
1. Convert components from classes to functions 
2. Adding a feature search with clear - write useDynamicInput

---

### Refactoring with Hooks
1. ~~Convert components from classes to functions~~
2. ~~Adding a feature search with clear - write useDynamicInput~~
3. Make hook reusable - use it in a different component

---

### Pitfalls
* overusing hook - should it be stateful?
* useCallback

---

### Further reading
* [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)
* [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
* [Under the Hook](https://www.youtube.com/watch?v=2anI7jiGjbg)

