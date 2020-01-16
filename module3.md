## Module 3
### Functional Components and Hooks
(This document is optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goals
* Understand the motivation behind hooks
* Practice using hooks and custom-hooks
* Hopefully - never writing a Class-component (almost) ever again

---

### Agenda
1. Functional vs Class Components
2. React Hooks introduction
3. Writing Custom Hooks
4. Refactoring with Hooks
5. More Hooks
6. Pitfalls

---

### Functional vs Class Components
Abilities and Tendencies
<table>
    <tr>
        <th>Class Component</th>
        <th>Function Component</th>
    </tr>
    <tr><td>Stateful</td><td>Stateless</td></tr>
    <tr><td>Lifecycle events</td><td>X</td></tr>
    <tr><td>Complex</td><td>Simple</td></tr>
    <tr><td>?... </td><td>Readable</td></tr>
</table>

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
<!-- .element: class="fragment" -->

>* Complex components become hard to understand
<!-- .element: class="fragment" -->

>* Classes confuse both people and machines (this) 
<!-- .element: class="fragment" -->

---

### React Hooks introduction
* [Hooks Overview](https://reactjs.org/docs/hooks-overview.html)
* [State hook](https://reactjs.org/docs/hooks-state.html)
* [Effect hook](https://reactjs.org/docs/hooks-effect.html)
* Live Demo

---

### Practice Time
Practice 1 - **step 0** is the starting point
1. Convert to App to Function using hooks
2. create re-usable logic for input and title changes (as if you want to use it on a different component)



---

### Writing Custom Hooks
Writing Costume hooks - useInput
Rooks and other hooks

---

### Practice Time
On Okat-Cupid Repo
1. Convert components from Classes to Functions 
2. Adding a feature: text-filter with clear button

---

### Refactoring with Hooks
1. ~~Convert components from Classes to Functions ~~
2. ~~Adding a feature: text-filter with clear button~~
3. Make hook reusable - use it in a different component

---

### More Hooks

More Hooks
useContext
useRef
useMemo
useCallback
> React.useMemo will call the function and return its result while React.useCallback will return the function without calling it.


useReducer
https://dev.to/dinhhuyams/introduction-to-react-memo-usememo-and-usecallback-5ei3
https://medium.com/@sdolidze/react-hooks-memoization-99a9a91c8853

---

### Pitfalls
* Not following [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html)
* Functional component run (entirely)  on each change
* Think about the whole component as render function

### Practice:
Pitfalls - see the changes and fix the 2 bugs

---

### Pitfalls
> Functional component run (entirely)  on each change
* Every variable and function will be recreated
* You can prevent that using Hooks
    * useState
    * useEffect
    * useMemo / useCallback
    * useRef
* When using hooks remember - Function close upon creation (like in `useEffect`);

---

### Pitfalls
* overusing hook 
    - should it be stateful?
    - do i really need hook for that?
    - is it the right way to do it? (like `useEffect` for fetching data)
* forgetting deps for function-parameters hooks (like `useEffect`)
    - not providing empty array - re-create on each call
    - deps does not include all dependencies - `useEffect` will not update)
    - not understanding useMemo / useCallback
* not using the full power of hooks - reusability

---

### Wrap Up

---

### Agenda


---

### Further reading
* [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)
* [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
* [Under the Hook](https://www.youtube.com/watch?v=2anI7jiGjbg)

# Extra
https://github.com/donycisneros/react-hooks-demo
