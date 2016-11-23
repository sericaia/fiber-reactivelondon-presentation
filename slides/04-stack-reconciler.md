## Stack Reconciler


### Stack Reconciler
- Used by ReactDOM and React Native

- Produces a tree of **internal instances** of React Components
  - composite components (or *user defined*)
  - platform specific (or *host*)

Note: tree is not exposed to the user


### Stack Reconciler
- mounts => `mountComponent(element)`
- updates => `receiveComponent(element)`
- unmounts => `unmountComponent(element)`


### Platform specific (or *host*)
```
<View>
<div>
```

<img src="./slides/images/view-div.png" class="logo" />

- e.g ReactDOM
  - [/src/renderers/dom/stack/client/ReactDOMComponent.js](https://github.com/facebook/react/tree/master/src/renderers/dom/stack/client/ReactDOMComponent.js)

- ReactMultiChild helper

Note: e.g React DOM instructs the stack reconciler to use ReactDOMComponent to handle mounting, updates, and unmounting of DOM components; ReactMultiChild handles children in a similar way (used by ReactDOM and ReactNative)


### Composite components (or *user defined*)

<img src="./slides/images/usersheader-searchbar.png" class="logo" />

- Same behaviour in all renderers
  - [.../stack/reconciler/ReactCompositeComponent.js](https://github.com/facebook/react/blob/master/src/renderers/shared/stack/reconciler/ReactCompositeComponent.js)
- User code

<img src="./slides/images/simple-reconciliation-stack.png" class="logo" />


### Stack Reconciler recursion
- `render()` decides when to update
- component tree is **sync**

Note: there's no pauses;


### Stack Reconciler works in a **suboptimal** way

Note: because there's no pauses, it's difficult to process heavy/deep updates; limited CPU time
