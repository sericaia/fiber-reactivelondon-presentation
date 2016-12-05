## Fiber Reconciler


## Fiber Reconciler

- Tries to solve problems in stack reconciler and long-standing issues

- Aims to make common use cases faster

- Complete **rewrite** of the Reconciler

- In dev/experimental


### Major improvement

**pause and resume**

but also...
- return multiple things in `render()`
- error support


<img src="./slides/images/fiber-reconciler.png" class="common" />
Note: Reconciler asks "What's changed?" ==== (fiber output) ===> render app (with changed info)


### **Incremental** rendering
- Prioritize!
  - animation
  - layout
  - gestures

Note: chunks; multiple frames; means rendering part of the virtualDOM in one cycle instead of the whole thing; e.g scroll large table - prioritize render of custom scrollbar instead of row's content and fill rows in spare time/when possible.


### Scheduling
- When?
- Which computations are more relevant?

Note: - delay computations if necessary;
- priorities;
- offscreen vs not offscreen (e.g user clicks a button)


```js
// src/renderers/shared/fiber/ReactPriorityLevel.js

export type PriorityLevel = 0 | 1 | 2 | 3 | 4 | 5 | 6;

module.exports = {
  NoWork: 0,
  SynchronousPriority: 1,
  TaskPriority: 2,
  AnimationPriority: 3,
  HighPriority: 4,
  LowPriority: 5,
  OffscreenPriority: 6,
};
```

Note: - ReactPriorityLevel - less value => higher priority;
- NoWork = default value when fiber is created, no work pending, or set when work finished


### GOAL: 60 fps

Note: avoid dropping frames; React must be capable of deciding what is important to occur first;


### How to achieve that goal?
- `requestAnimationFrame()`

- `requestIdleCallback()`

[/src/renderers/dom/fiber/ReactDOMFiber.js#L147-L149](https://github.com/facebook/react/blob/master/src/renderers/dom/fiber/ReactDOMFiber.js#L147-L149)

Note: - requestAnimationFrame() - schedules high priority functions to be called on the next automation frame;
- requestIdleCallback() - schedules low priority functions to be called in a idle period;


### What is a Fiber?
- Unit of work
- JS object

Note: Fiber has information about the component;


### Fiber Fields

<img src="./slides/images/fiber-fields.gif" />

([*from* /src/renderers/shared/fiber/ReactFiber.js#L46-L143](https://github.com/facebook/react/blob/master/src/renderers/shared/fiber/ReactFiber.js#L46-L143))


### Fiber Fields
- tag

```js
// src/renderers/shared/fiber/ReactTypeOfWork.js

export type TypeOfWork = 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10;

module.exports = {
  IndeterminateComponent: 0,
  FunctionalComponent: 1,
  ClassComponent: 2,
  HostRoot: 3,
  HostPortal: 4,
  HostComponent: 5,
  HostText: 6,
  CoroutineComponent: 7,
  CoroutineHandlerPhase: 8,
  YieldComponent: 9,
  Fragment: 10,
};
```

Note: - Tag identifying the type of fiber.
- used when scheduler has to beginWork, completeWork or commitWork (update lifecyle, set props, etc...)


### Fiber Fields
copied from the element:
- type
- key

Note: - type - to understand if it's a composite component (type = function/class) or host component (type = string);
- key - to understand if it should be reused;


### Fiber Fields
- child
- sibling

```
render() {
  return [<Navigation />, <SearchBar />];
}
```
Note: with fiber we can return multiple children (new feature)


### Fiber Fields
- pendingWorkPriority

```js
// src/renderers/shared/fiber/ReactPriorityLevel.js

export type PriorityLevel = 0 | 1 | 2 | 3 | 4 | 5 | 6;

module.exports = {
  NoWork: 0,
  SynchronousPriority: 1,
  TaskPriority: 2,
  AnimationPriority: 3,
  HighPriority: 4,
  LowPriority: 5,
  OffscreenPriority: 6,
};
```

Note: - Priorities we just saw in ReactPriorityLevel.js;
- helps to answer the question "What to pick next?"
- The priority of a fiber is **greater than or equal to the priority of all its descendent** fibers.
- If a tree has pending work priority, its root is scheduled.


### Fiber Fields
- effectTag

```js
// src/renderers/shared/fiber/ReactTypeOfSideEffect.js
export type TypeOfSideEffect = 0 | 1 | 2 | 3 | 4 | 8 | 16 | 32;

module.exports = {
  NoEffect: 0,
  Placement: 1,
  Update: 2,
  PlacementAndUpdate: 3,
  Deletion: 4,
  ContentReset: 8,
  Callback: 16,
  Err: 32,
};
```

Note: - side effects when work is being commited by the scheduler.
- commitDeletion: Recursively delete all host nodes from the parent.
- When work is commited: (1) First, we'll perform all the host insertions, updates, deletions and ref unmounts. (2) we'll perform all life-cycles and ref callbacks. Life-cycles happens as a separate pass so that all effects in the entire tree have already been invoked.


### Fiber Fields
- alternate

Note: current flushed fiber OR work in progress fiber (one is alternate of the other); implementation detail


## Fiber Conclusions

- Each fiber has information about a component

- A component may have more than one fiber

- Fibers have priorities, types of work and side effects

- Fiber work may be paused and resumed

- Scheduler controls everything
