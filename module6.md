## Module 6
### CSS in JS
(Optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goals
* Understand the motivation for CSS in JS
* Practice CSS in JS

---

### Agenda
1. What's wrong with CSS?
2. A Different Approach
3. Tools Overview
4. Material-UI styling system

---

### What's wrong with CSS?
Discussion:

What are the problems with css - based styling? (plain css, sass, less etc.)
<!-- .element: class="fragment" -->

* No out-of-the-box isolation - you should use a convention for it (like [BEM](http://getbem.com/))
* Convention-based isolation is prone to Errors
* Due to Cascading, style may be unpredictable
* Dead code elimination is difficult
* Maintaining Stylesheet and Component files separately
* Scale - maintaining a large number of stylesheets can be tedious

---

### A Different Approach
```
// Circle.css
.circle {
  border-radius: 50%;
  height: 100px;
  width: 100px;
}
    
// Circle.js
import 'Circle.css'

const Todo: React.FC = () => {
  return (
      <div className="circle"></div>
  )
};
```

---

### A Different Approach
Inline (CSS-in-JS) vs css/scss files
```
const Todo = () => {
  const styles = {
    circle: {
      border-radius: '50%',
      height: '100px',
      width: '100px'
    }
  }

  return (
      <div style={styles.circle}></div>
  )
};
```

---

### A Different Approach
Discussion: 
CSS-In-JS Pros vs Cons

---

### A Different Approach
Discussion: 
CSS-In-JS Pros vs Cons

* No styling collisions
* Encourage component thinking
* State-dependent changes are straightforward

Inline-Styling Cons:
* Can't use pseudo-selectors and media queries without external libraries
* Can't use css tools like pre-processing 
* No global styling
* Learning / adjustment time

---

### A Different Approach

> Can't use pseudo-selectors and media queries without external libraries

Use External tools - some of them are really great

> Can't use css tools like pre-processing 

No need to - Javascript-based styling is powerful. You can share style and constants just like objects. 

 
> No global styling

* You can still use global css for global stying  / normalize / reset.
* Suggestion: don't mix css files and CSS-in-JS more than that.


> Learning / adjustment time

True, but it worth your time

---

### A Different Approach

Practice
1. Convert all Atom Components css files to css-in-js
2. Remove Atom Components css files
---

### Tools Overview

[Trends](https://www.npmtrends.com/jss-vs-aphrodite-vs-radium-vs-styled-components-vs-glamorous-vs-emotion-vs-@material-ui/core)
* [CSS Modules](https://github.com/css-modules/css-modules)
* [Styled Component](https://styled-components.com/docs/basics#getting-started)
* [JSS](cssinjs.org/)
* [Material-UI](https://material-ui.com/styles/basics/#hook-api)

---

### Tools Overview
Why [Material-UI](https://material-ui.com/styles/basics/#hook-api)?

* Support everything you like on css (pseudo elements, media queries etc.)
<!-- .element: class="fragment" -->

* Javascript based - you can costume your styling with code (like based on component state)
<!-- .element: class="fragment" -->

* Compiled to encapsulated css classes - css-like performance
<!-- .element: class="fragment" -->

* Different APIs: Hooks, Styled components, HOC
<!-- .element: class="fragment" -->

* Theming support
<!-- .element: class="fragment" -->

* It's a UI library and CSS-in-JS tool (although you can use the latter separately)
<!-- .element: class="fragment" -->

* The most popular UI library for react, with react-in mind design and rapid updates.
<!-- .element: class="fragment" -->

---

### MaterialUI styling system
* [Components](https://material-ui.com/components/buttons/) - see Button, Card, Grid, AppBar
* [Styling API's](https://material-ui.com/styles/basics/)
* [Nesting selectors](https://material-ui.com/styles/basics/#nesting-selectors)
* [Adapting based on props](https://material-ui.com/styles/basics/#adapting-based-on-props)
* [The Styles Packages](https://material-ui.com/styles/basics/#material-ui-core-styles-vs-material-ui-styles)
* [withStyles and makeStyles](https://material-ui.com/styles/advanced/#withstyles)
* [createStyles](https://material-ui.com/styles/api/)

---

### MaterialUI styling system
Practice
Convert all Atoms to use MaterialUI JSS with HooK API

```jsx harmony
const useStyles = makeStyles({
  root: {
    background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)',
    border: 0,
    borderRadius: 3,
    boxShadow: '0 3px 5px 2px rgba(255, 105, 135, .3)',
    color: 'white',
    height: 48,
    padding: '0 30px',
  },
});

export default function MyButton() {
  const classes = useStyles();  // Hook API
  return <Button className={classes.root}>Click Me</Button>;
}
```

---

### Wrap Up

---

### Further reading
* []()
https://www.engineyard.com/blog/inline-styles-yes-or-no
https://medium.com/better-programming/all-you-need-to-know-about-css-in-js-984a72d48ebc

### Extra
* [What actually is CSS-in-JS?](https://medium.com/dailyjs/what-is-actually-css-in-js-f2f529a2757)

---

### Home Work:

