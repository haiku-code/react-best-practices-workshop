## Module 3
### Functional Components and Hooks
(Optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goals
* Understand the motivation behind hooks
* Practice using hooks and custom-hooks
* Hopefully - never writing a Class-component (almost) ever again

---

### Agenda
1. Functional vs Class Components
2. React Hooks introduction
3. Writing Custom Hooks
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
    <!-- .element: class="fragment" -->
    <tr><td>Stateful</td><td>Stateless</td></tr>
    <!-- .element: class="fragment" -->
    <tr><td>Lifecycle events</td><td>X</td></tr>
    <!-- .element: class="fragment" -->
    <tr><td>Complex</td><td>Simple</td></tr>
    <!-- .element: class="fragment" -->
    <tr><td>?... </td><td>Readable</td></tr>
    <!-- .element: class="fragment" -->
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
Let's Talk about Hooks

<div>
    <img src="./assets/captainhook.jpg">
</div>


---

### React Hooks introduction
* [Hooks Overview](https://reactjs.org/docs/hooks-overview.html)
* [State hook](https://reactjs.org/docs/hooks-state.html)
* [Effect hook](https://reactjs.org/docs/hooks-effect.html)
* Live Demo

---

### React Hooks introduction
Practice Time

Starting point: `practice1/react-hooks-intro-practice-step0.html`
1. Convert to App to Function using hooks
2. create re-usable logic for input and title changes (as if you want to use it on a different component)

---

### Writing [Custom Hooks](https://reactjs.org/docs/hooks-custom.html)
* Review useFormInput - what we've done so far
* [Hooks Intro - including useFormInput demo](https://youtu.be/dpw9EHDh2bM?t=707)
* [Rooks](https://github.com/imbhargav5/rooks)
* [usehooks](https://usehooks.com/)

You'll find many custom hooks online - not all hooks are good hooks! 
Check the code and make sure it fit your requirements.
<!-- .element: class="fragment" -->

---

### Writing Custom Hooks
Practice Time

Starting point: `practice1/react-hooks-intro-practice-step3.html`
1. ~~Convert to App to Function using hooks~~
2. ~~Create re-usable logic for input and title changes (as if you want to use it on a different component)~~
3. Add a clear button for each input (useFormInput should be improved for that...)

---

### Writing Custom Hooks
Practice Time On Okat-Cupid Repo
1. Convert components from Classes to Functions 
2. Adding a feature: text-filter with clear button

---

### [More Hooks](https://reactjs.org/docs/hooks-reference.html)

* [useContext](https://reactjs.org/docs/hooks-reference.html#usecontext)
* [useRef](https://reactjs.org/docs/hooks-reference.html#useref)
* [useReducer](https://reactjs.org/docs/hooks-reference.html#usereducer)

---

### [More Hooks](https://reactjs.org/docs/hooks-reference.html)

* [useMemo](https://reactjs.org/docs/hooks-reference.html#usememo)
* [useCallback](https://reactjs.org/docs/hooks-reference.html#usecallback)

React.useMemo will call the function and return its result, while React.useCallback will return the function without calling it.
<!-- .element: class="fragment" -->

Therefore:
<!-- .element: class="fragment" -->

> useCallback(fn, deps) is equivalent to useMemo(() => fn, deps).
<!-- .element: class="fragment" -->


---

### Pitfalls
<div style="text-align:left">

* Not following<!-- .element: class="fragment" --> [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html)


* <!-- .element: class="fragment" -->Functional component run (entirely) on each change

* <!-- .element: class="fragment" -->Tip: Think about the whole component as render function

</div>

---

### Pitfalls
Practice Time

Starting point: `pitfalls/react-hooks-intro-pitfall1.html`

See the changes and fix the 2 bugs

---

### Pitfalls
> Functional component run (entirely)  on each change
<div style="text-align:left">

* <!-- .element: class="fragment" -->Every variable and function will be recreated

* <!-- .element: class="fragment" -->You can prevent that using Hooks
    * useState / useEffect
    <!-- .element: class="fragment" -->
    * useMemo / useCallback
    <!-- .element: class="fragment" -->
    * useRef
    <!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->When using hooks remember - Function close 
upon creation (like in <code>useEffect</code>);

</div>

---

### Pitfalls
* <!-- .element: class="fragment" -->overusing hook 
    - Should it be stateful?
    <!-- .element: class="fragment" -->
    - Do i really need hook for that?
    <!-- .element: class="fragment" -->
    - Is it the right way to do it? (fetching data useEffect?)
    <!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Forgetting deps for function-parameters hooks
    - not providing empty array - re-create on each call
    <!-- .element: class="fragment" -->
    - deps does not include all dependencies
    <!-- .element: class="fragment" -->
    - not understanding useMemo / useCallback
    <!-- .element: class="fragment" -->

---

### Pitfalls
Few Tips: 
* <!-- .element: class="fragment" -->strive to using the full power of hooks - logic reuse
* Always check deps to avoid <!-- .element: class="fragment" --> [exhaustive-deps](https://github.com/facebook/react/issues/14920)
* Use<!-- .element: class="fragment" --> [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks)
* Keep asking yourself -<!-- .element: class="fragment" --> [what can I memoize?](https://medium.com/@sdolidze/react-hooks-memoization-99a9a91c8853)

---

### Wrap Up
We started with the problems with Class components:
<!-- .element: class="fragment" -->

Hard to reuse logic, hard to read, "this"
<!-- .element: class="fragment" -->

Hooks give much more power to Function Component, and solve all these issues
<!-- .element: class="fragment" -->


But... You must follow the Rules of Hooks! So remember...
<!-- .element: class="fragment" -->

---
<blockquote 
style="position: absolute; top: 0; left: 0; width: 94%; font-weight: bold; 
margin: 39px 24px; background-color: gray">

with great power comes great responsibility
</blockquote>
<img src="assets/spiderman.jpeg">

---

### Further reading
* [Making Sense of React Hooks](https://medium.com/@dan_abramov/making-sense-of-react-hooks-fdbde8803889)
* [A Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
* [Under the Hook](https://www.youtube.com/watch?v=2anI7jiGjbg)

### Extra
* [Code from Dan Abramov Hooks Intro](https://github.com/donycisneros/react-hooks-demo)
* [Introduction to React.memo, useMemo and useCallback](https://dev.to/dinhhuyams/introduction-to-react-memo-usememo-and-usecallback-5ei3)
* [React Hooks: Memoization](https://medium.com/@sdolidze/react-hooks-memoization-99a9a91c8853)
