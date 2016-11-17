## Fiber Reconciler

- Tries to solve problems in stack reconciler and long-standing issues

- Aims to make common use cases faster

- Complete **rewrite** of the Reconciler
  - uses heap objects instead of a stack

- In dev/experimental

Note: uses heap objects instead of a stack - allows reusing in future updates and yielding to the event loop, without losing any in progress data


## Fiber Reconciler
Test it changing a flag in React repo `useFiber: true`
  - [src/renderers/dom/shared/ReactDOMFeatureFlags.js#L16](https://github.com/facebook/react/blob/master/src/renderers/dom/shared/ReactDOMFeatureFlags.js#L16)


### Major improvements
- pause and resume
- return multiple things in `render()`
- error support


## Fiber Reconciler

Reconciler asks "What's changed?" ==== (fiber output) ===> render app (with changed info)


- ReactDOM
- React Native

> different renderers, same reconciler


### **Incremental** rendering
- Prioritize!
  - animation
  - layout
  - gestures

Note: chunks; multiple frames; means rendering part of the virtualDOM in one cycle instead of the whole thing; e.g scroll large table - prioritize render of custom scrollbar instead of row's content and fill rows in spare time/when possible.


### Scheduling
- When?
- Which computations are more relevant?

Note: delay computations if necessary; priorities; offscreen vs not offscreen (e.g user clicks a button)


### GOAL: 60 fps

[src/renderers/shared/fiber/ReactPriorityLevel.js](https://github.com/facebook/react/blob/master/src/renderers/shared/fiber/ReactPriorityLevel.js)
Note: avoid dropping frames; React must be capable of deciding what is important to occur first; ReactPriorityLevel - less value => higher priority


### How to achieve that goal?
- `requestIdleCallback()`

- `requestAnimationFrame()`

Note: requestIdleCallback() - schedules low priority functions to be called in a idle period; requestAnimationFrame() - schedules high priority functions to be called on the next automation frame


### What is a Fiber?
- Unit of work
- JS object

Note: fiber has inputs, outputs and the component information; Fiber Reconciliation reimplements the stack by having in-memory stack frames


### Fiber Fields


### Fiber Fields
copied from the element:
- type
- key

Note: type - to understand if it's a composite component (type = function/class) or host component (type = string); key - to understand if it should be reused;


### Fiber Fields
- child
- sibling

Note: with fiber we can return multiple children (new feature)


### Fiber Fields
- return

Note: next fiber or parent fiber


### Fiber Fields
- pendingProps
- memoizedProps

Note: pendingProps - set at the beginning of execution; memoizedProps - set at the end; (if pending === momoized, output can be reused)


### Fiber Fields
- pendingWorkPriority

Note: Priorities we just saw in ReactPriorityLevel.js; helps to answer the question "What to pick next?"


### Fiber Fields
- alternate

Note: current flushed fiber OR work in progress fiber (one is alternate of the other); implementation detail


### Fiber Fields
- output

Note: it's the return value of a function, only at leaf nodes <p>, <span>, <div>, ... (only for platform-specific/host components); renderer defines how output is created and updated
