## Module 4
### State Management
(Optimized for presentation using [reveal-md](https://github.com/webpro/reveal-md))

### Goals
* Understand the motivation for using Application State Management
* Understand the guidelines for State Management 
* Practice State Management with MobX

---

### Agenda
1. What is an Application State?
2. State Management motivation and limits
3. Libraries and Tools
4. Design Patterns
5. Guidelines

---

### What is a Application State?
Discussion: What is an Application State?

* <!-- .element: class="fragment" -->The outcome of all of the events occur in the app (whatever the source)
* <!-- .element: class="fragment" -->A snapshot of the application in a specific moment of time
* <!-- .element: class="fragment" -->All the required data which represent the application in a specific moment
* <!-- .element: class="fragment" -->An object which contain All the required data to recover application snapshot
* <!-- .element: class="fragment" -->Single source of truth for the application UI


---

### State Management motivation and limits
Why should we manage Application State?

<div style="height: 45vh">
    <img src="./assets/spaghetti_code_monster.svg">
    <p>
    Because of the Flying Spaghetti Code Monster
    </p>
</div>
<!-- .element: class="fragment" -->

---

### State Management motivation and limits
Discussion: 
1. Why should we manage Application State?
<br><br>

* <!-- .element: class="fragment" -->As application grows so their complexity, without a good pattern code will become hard to maintain

* <!-- .element: class="fragment" -->Multiple Components may use the same data

* <!-- .element: class="fragment" -->Multiple Components affect the same data (and each other)

* <!-- .element: class="fragment" -->Make it easy for saving application state for later load (think of local storage)

---

### State Management motivation and limits
Discussion: 
1. ~~Why should we manage Application State?~~
2. Why using state management solutions (mobx, redux) instead of doing it ourselves?

* <!-- .element: class="fragment" -->It's <a href="https://github.com/mobxjs/awesome-mobx#examples">battle tested</a>

* <!-- .element: class="fragment" -->Community <a href="https://mobx.js.org/README.html">Information, Documentation and Support</a>

* <!-- .element: class="fragment" --><a href="https://github.com/mobxjs/mobx-utils">Ecosystem</a>

---

### State Management motivation and limits
And - There is no need to reinvent the wheel

<div>
    <img src="./assets/wheel.jpeg" style="height: 50vh">
</div>
    

---

### Libraries and Tools
Redux

<img src="./assets/redux.png" height="220px">

* <!-- .element: class="fragment" -->Store - manage your stuff
* <!-- .element: class="fragment" -->State - object represent app in a specific time
* <!-- .element: class="fragment" -->Action - plain object represent an event
* <!-- .element: class="fragment" -->Reducer - old state + action => new state

---

### Libraries and Tools
Redux
<img src="./assets/redux-with-code.png">


---

### Libraries and Tools
MobX works Differently - [Concepts](https://mobx.js.org/intro/concepts.html#concepts):

* <!-- .element: class="fragment" -->State : State is the data that drives your application

* <!-- .element: class="fragment" -->Actions: Any piece of code that changes the state

* <!-- .element: class="fragment" -->Derivations : Computed values and Reactions


---

### Libraries and Tools
MobX
<img src="./assets/mobx_flow.png">

---

### Libraries and Tools
MobX works Differently

There are no reducers, State is mutable
<!-- .element: class="fragment" -->

Result in much less boilerplate code!
<!-- .element: class="fragment" -->
 
 
---
 
### Libraries and Tools
 
Uses Observers - Observables Pattern
<!-- .element: class="fragment" -->

There is no need to specify 
which part of the store each component should watch!
<!-- .element: class="fragment" -->

Data Push (Mobx) VS Pull (Redux)
<!-- .element: class="fragment" -->

 
Uses Computed Values - Think of them as functions in Excel sheet
<!-- .element: class="fragment" -->

---

### Libraries and Tools - MobX
```jsx harmony
class ObservableTodoStore {
	@observable todos = [];

    constructor() {
        // Reaction
        mobx.autorun(() => console.log('Updated!'));
    }

	@computed get completedTodosCount() {
    	return this.todos.filter(
			todo => todo.completed === true
		).length;
    }
    
    @action
	addTodo(task) {
		this.todos.push({
			task: task,
			completed: false,
			assignee: null
		});
	}
}

```
---

### Libraries and Tools - MobX
Decorators are simply [sugar coating for a wrapper function](https://www.sitepoint.com/javascript-decorators-what-they-are/) 

```jsx harmony

class ObservableTodoStore {
	todos = [];

    constructor() {
        // Reaction
        mobx.autorun(() => console.log(this.report));
    }

	get completedTodosCount() {
    	return this.todos.filter(
			todo => todo.completed === true
		).length;
    }
    
	addTodo(task) {
		this.todos.push({
			task: task,
			completed: false,
			assignee: null
		});
	}
}

decorate(TodoStore, {
    todos: observable,
    completedTodosCount: computed,
    addTodo: action
});
```

---

### Libraries and Tools - MobX

* <!-- .element: class="fragment" --><a href="https://mobx.js.org/getting-started">Introduction</a>
* keep in mind: decorators are simply<!-- .element: class="fragment" --> [sugar coating for a wrapper function](https://www.sitepoint.com/javascript-decorators-what-they-are/) 
* <!-- .element: class="fragment" -->keep in mind: decorators cannot be used for Function Components
* <!-- .element: class="fragment" -->Live Demo (Intro)
* <!-- .element: class="fragment" -->Dev tools
* <!-- .element: class="fragment" -->MobX is Framework agnostic. However, tools for easy integration with react are available

---

### Libraries and Tools - MobX

Some Rules:
* <!-- .element: class="fragment" -->Computed Values are Pure Functions - no side effects allowed (Network events / changing state)
* <!-- .element: class="fragment" -->Computed Values will be computed only when needed (Mobx will decide when)
* <!-- .element: class="fragment" -->Computed Values are preferable over reaction
* <!-- .element: class="fragment" -->Actions should be marked for better performance and debugging, although state will update even without it.
* <!-- .element: class="fragment" --><a href="https://mobx.js.org/refguide/api.html#enforceactions">enforceActions<a/> (AKA strict mode) 

---

### Libraries and Tools - MobX
What's the problem with passing store as prop?

```jsx harmony
    const Todos = observer(({store}) => (
        {store.todos.map(todo => (
            <p>{todo}</p>
        ))}
    ));   

    const App = ({store}) => (
        <Todos store={store}>
    );   

    ReactDOM.render(<App store={myStore}/>, rootElement);
```


---

### Libraries and Tools - MobX
Option 1 (Old): Using Mobx-React Provider
(might be removed in the furture)

```jsx harmony
const Todos = inject('store')(observer(({store}) => (
    {store.todos.map(todo => (
        <p>{todo}</p>
    ))}
)));   

<Provider store={MyStore}>
  <App/>
</Provider>;
```
---

### Libraries and Tools - MobX
Option 1 (Old): Using Mobx-React Provider 
(might be removed in the furture)

```jsx harmony
@inject['store']
@observer
class Todos {
    render () => {
        return (
            store.todos.map(todo => (
                <p>{todo}</p>
            ))
        )
    }
}

<Provider store={MyStore}>
  <App/>
</Provider>;
```

---

### Libraries and Tools - MobX
Option 2: using [React Context](https://reactjs.org/docs/context.html)

```jsx harmony
// Creating context
export const themes = {
  light: {
    foreground: '#000000',
    background: '#eeeeee',
  },
  dark: {
    foreground: '#ffffff',
    background: '#222222',
  },
};

export const ThemeContext = React.createContext(
  themes.dark // default value
);
```

---

### Libraries and Tools - MobX
Using context

```jsx harmony

const Toolbar = () => (
   <ThemeContext.Consumer>
    {({theme}) => (
      <div style={{backgroundColor: theme.background}}>
        ToolBar
      </div>
    )}
   </ThemeContext.Consumer>
);   

const App = () => (
   <ThemeContext.Provider>
      <Toolbar/>
   </ThemeContext.Provider>
);   

ReactDOM.render(<App/>, rootElement);
```

---

### Libraries and Tools - MobX
Using context with Hooks

```jsx harmony
const Toolbar = () =>  {
    const theme = useContext(ThemeContext)
    return (
        <div style={{backgroundColor: theme.background}}>
            ToolBar
        </div>
    );   
};   

const App = () => (
   <ThemeContext.Provider>
      <Toolbar/>
   </ThemeContext.Provider>
);   

ReactDOM.render(<App/>, rootElement);
```

---

### Libraries and Tools - MobX
Using context with [Hooks & Mobx](https://mobx-react.js.org/recipes-context)

```jsx harmony
export const store = new RootStore();
export const StoreContext = React.createContext(store);

export const useStore = () => {
  const store = React.useContext(StoreContext);
  // or use useLocalStore as the docs describe
  if (!store) {
    throw new Error('You have forgot to use StoreProvider')
  }
  return store
};

const Toolbar = () =>  {
    const store = useStore()
    // ...
};

const App = () => (
   <StoreContext.Provider value={store}>
      <Toolbar/>
   </StoreContext.Provider>
);

ReactDOM.render(<App/>, rootElement);
```

---

### Libraries and Tools - MobX
Using context with [Hooks & Mobx](https://mobx-react.js.org/recipes-context)

Why using `useLocalStore` on StoreProvider?

> `useLocalStore` turns a javascript literal into a store with observable properties. This is not needed if a store is created from a class object with observable attributes.
<!-- .element: class="fragment" -->

---

### Libraries and Tools - MobX

About [useLocalStore](https://mobx-react.js.org/state-local)
<!-- .element: class="fragment" -->

Keep in mind:  Mobx allows [multiple store](https://mobx-react.js.org/recipes-context#multiple-global-stores)
<!-- .element: class="fragment" -->

---

### Libraries and Tools - MobX
Practice Time

Starting point: `practice-todo/practice-todo-step0.html`
1. Set App State provider
2. Move local state into App State 
3. Assign reaction (rendering) using observers 


---

### Libraries and Tools - MobX
* <!-- .element: class="fragment" -->Abstractions - is it Dark Magic?
* What does<!-- .element: class="fragment" --> [MobX react to?](https://mobx.js.org/best/react.html#what-does-mobx-react-to)
* Using<!-- .element: class="fragment" --> [Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy)

```jsx harmony
var target = { message : 'It is alive!'};
var handler = {
    get: (target, key) => {
        console.log(`I am a handy handler - key is: ${key}`)
        return target[key]
    }
};
var myObj = new Proxy(target, handler);
console.log(myObj.message);
```
<!-- .element: class="fragment" -->

---

### Design Patterns
> People often use MobX as alternative for Redux. But please note that MobX is 
> just a library to solve a technical problem and 
> not an architecture or even state container in itself. 
<!-- .element: class="fragment" -->

* <!-- .element: class="fragment" -->It is Un-Opinionated (vs Redux)
* <!-- .element: class="fragment" -->It will allow you to do  things that might be problematic in the long run


---

### Design Patterns
Issues with inject and other decorators
<!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Harder to implement on functional component
* <!-- .element: class="fragment" -->Do not use the power of Hooks

Bye Bye Inject, Hello<!-- .element: class="fragment" --> [mobx-react-lite](https://mobx-react.js.org/libraries#fully-embraced-hooks) 

You can still use decorators on store classes
<!-- .element: class="fragment" -->
```jsx harmony
class TodoStore {
	@observable todos = [];
    
    @action completeTodo(index) {
        todos[i].completed = true;
    }
}
```
<!-- .element: class="fragment" -->

---

### Design Patterns
Embracing Hooks: Using [mobx-react-lite](https://mobx-react.js.org/libraries#fully-embraced-hooks) 

There are three ways to add reactivity to components:

1. <!-- .element: class="fragment" -->Observer HOC

```jsx harmony
const Title = () => {
    const store = useStore();
    return (<h1>{store.myTitle}</h1>);
};

export default observer(Title);
```
<!-- .element: class="fragment" -->


---

### Design Patterns
1. Observer HOC

> Along the observer capability, the React.memo is applied to the component. The general idea is, that observed components rarely need to re-render based on a complex props.
<!-- .element: class="fragment" -->

---

### Design Patterns
2. Observer component

```jsx harmony
const Title = () => {
    const store = useStore();
    return (
        <Observer>
            <h1>{store.myTitle}</h1>
        </Observer>
    );
};

export default Title;

```
<!-- .element: class="fragment" -->


[Nesting caveat](https://mobx-react.js.org/observer-component#nesting-caveat)
<!-- .element: class="fragment" -->

---

### Design Patterns
3. useObserver Hook

```jsx harmony
const Title = () => {
    const store = useStore();
    return useObserver(() => 
        <h1>{store.myTitle}</h1>
    );
};

export default Title;

```
<!-- .element: class="fragment" -->

Low level implementation used internally by observer HOC and Observer component. 
<!-- .element: class="fragment" -->
If any hook changes an observable for some reason then the component won't rerender twice unnecessarily
<!-- .element: class="fragment" -->

---

### Design Patterns
Practice - Okat Cupid Repo

Step See store provider and useStore Hook

1. Move App state to Mobx
2. Make App Reactive to state

---

### Design Patterns

3. Add favorite feature
    - User can mark favorite profiles
    - User can click favorite button on app bar to toggle favorite mode
    - On favorite mode, only favorite profiles will be displayed
    - Text filter should work correctly on both modes
    - Bonus: show favorite counter on app bar
4. Save state to local storage. On reload, state should be recovered from local storage.




---

### Design Patterns

[Mapping hooks](https://mobx-react.netlify.com/recipes-migration)

```jsx harmony
function useUserData() {
  const { user, order } = useStore()
  // note the usage of useObserver 
  return useObserver(() => ({
    username: user.name,
    orderId: order.id,
  }))
}

const UserOrderInfo = () => {
  const { username, orderId } = useUserData();
  //...
}
```

---

### Design Patterns

`window.store` in development / staging
```jsx harmony
// storeConfig.js
export const store = new RootStore();

if(process.env.NODE_ENV !== 'production') {
  window['store'] = store;
}

```

---

### Guidelines
* <!-- .element: class="fragment" -->Uni-directional data flow (Action => State => View)
* Use<!-- .element: class="fragment" --> [RootStore](https://mobx.js.org/best/store.html#combining-multiple-stores) to combine multiple stores.
* Prefer using<!-- .element: class="fragment" --> [trees over Graphs](https://github.com/mobxjs/mobx-state-tree).
* <!-- .element: class="fragment" -->State is pure logic structure (Think about dispatching actions from Console)
* <!-- .element: class="fragment" -->Single source of truth
    - <!-- .element: class="fragment" -->Preferably, use a single root store for all other stores
    - <!-- .element: class="fragment" -->Mobx is un-opinionated and allow you to use separate stores


---

### Guidelines

* <!-- .element: class="fragment" -->Treat state as read-only - To change the state use an Action.
* <!-- .element: class="fragment" --><a href="https://mobx.js.org/best/store.html#domain-stores">Data / UI separation</a>
* Computed <!-- .element: class="fragment" --> Values must be Pure Functions -[this is Why](https://medium.com/hackernoon/becoming-fully-reactive-an-in-depth-explanation-of-mobservable-55995262a254)
* <!-- .element: class="fragment" -->Computed values should always be preferred over reactions

---

### Guidelines

* <!-- .element: class="fragment" -->Think about serialization
    - <!-- .element: class="fragment" -->Option 1 : keep data in plain Objects (In Typescript use interfaces instead of classes)
    - Option 2 : Use<!-- .element: class="fragment" --> [serializr](https://github.com/mobxjs/serializr)
---

### Guidelines

* <!-- .element: class="fragment" -->Serialized state can be shared between clients using server (Like document live edit)

* Beware of<!-- .element: class="fragment" --> [data destruct](https://mobx-react.js.org/state-destruct)

* <!-- .element: class="fragment" -->reaction that trigger more reactions, or reactions that update state: They are both considered anti patterns in Mob

* <!-- .element: class="fragment" --><a href="https://mobx.js.org/best/pitfalls.html">Read Pitfall section</a>

---

### Wrap Up
State management can help us
<!-- .element: class="fragment" -->
 * <!-- .element: class="fragment" -->Managing our state in large applications
 * <!-- .element: class="fragment" -->Provide Separation of concerns (State / View)

State can be:
<!-- .element: class="fragment" -->
* <!-- .element: class="fragment" -->Local (Component - use Hooks)
* <!-- .element: class="fragment" -->Global (MobX)
* <!-- .element: class="fragment" -->Persistent (Local Storage)
* <!-- .element: class="fragment" -->Remote (Server)

---

### Wrap Up

* <!-- .element: class="fragment" -->MobX using Observer - Observable Pattern for simplicity and avoid boilerplate code
* <!-- .element: class="fragment" -->MobX prefer
    - <!-- .element: class="fragment" -->Derivation over explicit data
    - <!-- .element: class="fragment" -->Reacting to state changes over Acting on state changes
* <!-- .element: class="fragment" -->MobX is Un-Opinionated - design pattern and architecture design still required
---

### Further reading
* [What does MobX react to?](https://mobx.js.org/best/react.html)
* [Becoming fully reactive: an in-depth explanation of MobX](https://medium.com/hackernoon/becoming-fully-reactive-an-in-depth-explanation-of-mobservable-55995262a254)
* [The fundamental principles behind MobX](https://hackernoon.com/the-fundamental-principles-behind-mobx-7a725f71f3e8)
* [Reaction](https://mobx.js.org/refguide/reaction.html)

---

### Extra
* [awesome-mobx](https://github.com/mobxjs/awesome-mobx)
* [MobX State Tree philosophy](https://www.youtube.com/watch?v=ta8QKmNRXZM&feature=youtu.be&t=21m52s)
* [Introduction to MobX State Tree](https://www.youtube.com/watch?v=pPgOrecfcg4)
* [Mobx State Tree Tutorial](https://www.youtube.com/watch?v=uBymH1JbKHs&list=PLucG_ap4Oxzj5TKvdOKc7W10NLMMg319A)

### Free Courses
* [Manage Complex State in React Apps with MobX](https://egghead.io/courses/manage-complex-state-in-react-apps-with-mobx)  ([Code samples](https://github.com/eggheadio-projects/manage-complex-state-in-react-apps-with-mobx))
* [Manage Application State with Mobx-state-tree](https://egghead.io/courses/manage-application-state-with-mobx-state-tree) ([Code Samples](https://github.com/mweststrate/mst-course))





