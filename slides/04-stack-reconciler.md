## Stack Reconciler


### Stack Reconciler
- Used by ReactDOM and React Native

- Produces a tree of **internal instances**

<img src="./slides/images/internal-instances.png" class="common" />

Note: - current implementation of the algorithm;
- DOM tree is not exposed to the developer;


### Stack Reconciler
functions called on internal instances:
- mounts => `mountComponent(element)`
- updates => `receiveComponent(element)`
- unmounts => `unmountComponent(element)`

Note: When a component mounts, updates, or unmounts, the stack reconciler calls these method on that internal instance.


### Stack Reconciler recursion

<img src="./slides/images/tree.png" style="width:180px; border:0; box-shadow: none"/>

- `render()` decides when to update
- component tree is **sync**

Note: there's no pauses;


### Stack Reconciler works in a **suboptimal** way

<img src="./slides/images/scrolling-images.jpg" />

Note: because there's no pauses, it's difficult to process heavy/deep updates; limited CPU time
