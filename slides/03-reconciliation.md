## Reconciliation


### Reconciliation

Sees what changed in every update

Note: done by React internally; it's an implementation detail



Aims to efficiently update UI to match tree updates

Note: props, state, for example


#### ReactDOM and React Native
- renderers share code & logic
- cross-platform consistency

Note: reconcilers are not packaged separately, they are in renderers such as ReactDOM and ReactNative


setState() => reconciler calls render() - mounts, updates, unmounts


### Reconcilers
- Stack reconciler
- Fiber reconciler


## Why is React fast?
Two major **assumptions** in React:
1. Elements of different types =>  Different trees

2. *key* property *hint*

Note: Two elements of diff types produce diff trees; The developers can *hint* at which child elements may be stable across different renders using *key* props; React achieves O(n)


### Reconciliation Algorithm
- Often mentioned "Virtual DOM"

- Starts with *root* elements


### Reconciliation Algorithm
*compares*
1. Elements w/ different type

2. DOM elements w/ same type

3. Component Elements w/ same type

4. Component Elements w/ different type


#### Reconciliation Algorithm
`1.` Elements w/ different type
```
<SearchBar>
<div>
```

Note: full rebuild; old components destroyed (componentWillUnmount()); new components created (componentWillMount(), componentDidMount()); old state is LOST


#### Reconciliation Algorithm
`2.` DOM elements w/ same type
```
<div>
```

Note: looks into attrs; only attrs are updated; DOM node stays; after root elements, looks into children;


#### Reconciliation Algorithm
`3.` Component Elements w/ same type
```
<SearchBar>
```

Note: state is maintained across renders; props are updated (componentWillReceiveProps(), componentWillUpdate())


#### Reconciliation Algorithm
`4.` Component Elements w/ different type
```
<SearchBar>
<Navigation>
```

Note: do not match; if components are similar, we may want them to be the same


#### Reconciliation Algorithm
Performance concerns
- adding to the end of a list has typically better performance

Note: adding to the top makes React mutate every child if we dont use KEYS (unique Ids)
