## Reconciliation


### Reconciliation

Sees what changed in every update

Note: done by React internally; it's an implementation detail


Aims to **efficiently** update UI to match tree updates

Note: props, state, for example


### Renderers

<img src="./slides/images/dom-vs-native.png" style="border-color: white; " />


### Renderers
#### (ReactDOM and React Native)
- share code & logic
- cross-platform consistency

> different renderers, same reconciler

Note: reconcilers are not packaged separately, they are in renderers such as ReactDOM and ReactNative


<img src="./slides/images/reconciler-job.png" class="common"/>

Note: setState() => reconciler calls render()


## Why is React fast?
Two major **assumptions** in React:
1. Elements of different types =>  Different trees

2. *key* property *hint*

Note: - Two elements of diff types produce diff trees;
- The developers can *hint* at which child elements may be stable across different renders using *key* props;
- React achieves O(n) - "order of N"


### Reconciliation Algorithm
- Often mentioned "Virtual DOM"

- Starts with *root* elements


### Reconciliation Algorithm
<img src="./slides/images/dirty-rerendered.png" class="common"/>
Note: dirty due to setState(); rerendered


### Reconciliation Algorithm
*compares*
1. (Elements || Component Elements) w/ different type

2. DOM elements w/ same type

3. Component Elements w/ same type


#### Reconciliation Algorithm
`1.` (Elements || Component Elements) w/ **different** type
```
<p></p>
<div></div>
```
OR
```
<SearchBar></SearchBar>
<div></div>
```
OR
```
<SearchBar></SearchBar>
<Navigation></Navigation>
```

Note: - full rebuild;
- old components destroyed (componentWillUnmount());
- new components created (componentWillMount(), componentDidMount());
- old state is LOST
- if(do not match && components are similar) we may want them to be the same


#### Reconciliation Algorithm
`2.` DOM elements w/ **same** type
```
<div></div>
<div></div>
```

Note: - looks into attrs; only attrs are updated;
- DOM node stays;
- after root elements, looks into children;


#### Reconciliation Algorithm
`3.` Component Elements w/ **same** type
```
<SearchBar></SearchBar>
<SearchBar></SearchBar>
```

Note: - state is maintained across renders;
- props are updated (componentWillReceiveProps(), componentWillUpdate())


### Reconcilers
- Stack reconciler
- Fiber reconciler
