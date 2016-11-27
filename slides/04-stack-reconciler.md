## Stack Reconciler


### Stack Reconciler
- Used by ReactDOM and React Native

- Produces a tree of **internal instances** of React Components
  <!-- - composite components (or *user defined*)
  - platform specific (or *host*) -->

<img src="./slides/images/internal-instances.png" class="common" />

Note: tree is not exposed to the user


### Stack Reconciler
- mounts => `mountComponent(element)`
- updates => `receiveComponent(element)`
- unmounts => `unmountComponent(element)`

Note: When a component mounts, updates, or unmounts, the stack reconciler calls these method on that internal instance.


### Platform specific
```
<View></View>
<div></div>
```


### Platform specific
- e.g ReactDOM
  - [/src/renderers/dom/stack/client/ReactDOMComponent.js](https://github.com/facebook/react/tree/master/src/renderers/dom/stack/client/ReactDOMComponent.js)

- ReactMultiChild helper

Note: e.g React DOM instructs the stack reconciler to use ReactDOMComponent to handle mounting, updates, and unmounting of DOM components; ReactMultiChild handles children in a similar way (used by ReactDOM and ReactNative)


### Composite components

```
<UsersHeader></UsersHeader>
<SearchBar></SearchBar>
```

- Same behaviour in all renderers
  - [.../stack/reconciler/ReactCompositeComponent.js](https://github.com/facebook/react/blob/master/src/renderers/shared/stack/reconciler/ReactCompositeComponent.js)
- User code


### Composite components
<img src="./slides/images/simple-reconciliation-stack.png" class="common" />


### Stack Reconciler recursion
- `render()` decides when to update
- component tree is **sync**

Note: there's no pauses;


### Stack Reconciler works in a **suboptimal** way

Note: because there's no pauses, it's difficult to process heavy/deep updates; limited CPU time
