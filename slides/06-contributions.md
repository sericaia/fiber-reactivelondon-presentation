## How to contribute


### (follow) Who is working on it
Sebastian Markbåge [@sebmarkbage](https://twitter.com/sebmarkbage)

Dan Abramov [@dan_abramov](https://twitter.com/dan_abramov)

Andrew Clark [@acdlite](https://twitter.com/acdlite)

Ben Alpert [@soprano](https://twitter.com/soprano)

community <img src="./slides/images/heart.png" style="border:none;box-shadow:none" />... it can be you!


[Fiber Principles: Contributing To Fiber](https://github.com/facebook/react/issues/7942) - Sebastian Markbåge

<img src="./slides/images/fiber-principles.png" />


[React Core Meeting Notes](https://github.com/reactjs/core-notes)

<img src="./slides/images/core-notes.png" />


[How to Help](https://github.com/facebook/react/issues/7925?utm_campaign=React%2BNewsletter&utm_medium=email&utm_source=React_Newsletter_51#issuecomment-259258900) - Dan Abramov

<img src="./slides/images/how-to-help.png" />


[Follow open `[Fiber]` PRs](https://github.com/facebook/react/pulls?utf8=%E2%9C%93&q=is%3Apr%20%5Bfiber%5D%20is%3Aopen%20)

<img src="./slides/images/fiber-open-prs.png" />


### Code location
- [Stack - src/renderers/shared/stack/reconciler](https://github.com/facebook/react/tree/master/src/renderers/shared/stack/reconciler)

- [Fiber - src/renderers/shared/fiber](https://github.com/facebook/react/tree/master/src/renderers/shared/fiber)

Note: but also: src/renderers/dom/stack, src/renderers/dom/fiber, src/renderers/dom/shared


 `useFiber: true`

  [/src/renderers/dom/shared/ReactDOMFeatureFlags.js#L16](https://github.com/facebook/react/blob/master/src/renderers/dom/shared/ReactDOMFeatureFlags.js#L16)
Note: Test it changing a flag in React repo


**477 tests failing** (Nov, 15)

<img src="./slides/images/tests-november-15.png" />

**81 tests failing** (Nov, 26)

**? tests failing** (Dec, 6)


[http://isfiberreadyyet.com/](http://isfiberreadyyet.com/)
<img src="./slides/images/isfiberreadyyet.png" />


[/scripts/fiber](https://github.com/facebook/react/tree/master/scripts/fiber)
- tests-failing.txt
- tests-passing.txt

<img src="./slides/images/scripts-preview.png" />

Note: scripts that keep track of tests that are passing and failing


### Limitations

- [requestIdleCallback()](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback) not implemented in every browser
<img src="./slides/images/requestIdleCallback-mozilla.png" />

(*from* [https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback](https://developer.mozilla.org/en-US/docs/Web/API/Window/requestIdleCallback))


### Limitations

- Fiber has almost no documentation

<img src="./slides/images/fiber-architecture.png" />
(*from* [https://github.com/acdlite/react-fiber-architecture](https://github.com/acdlite/react-fiber-architecture))

Note: No docs - you have to search a lot in code


### Limitations
- Lots of TODOs and questions inside the codebase
<img src="./slides/images/isthisright.png" />
(*from* [/src/renderers/shared/fiber/ReactFiberBeginWork.js#L474](https://github.com/facebook/react/blob/7d2be2c9a7b4a976e20d2d7c312b43b1bee01a07/src/renderers/shared/fiber/ReactFiberBeginWork.js#L474))
