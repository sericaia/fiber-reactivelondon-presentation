### Side notes
Use Profiling with Chrome

<img src="./slides/images/react-perf.png" />

[https://facebook.github.io/react/blog/2016/11/16/react-v15.4.0.html#profiling-components-with-chrome-timeline](https://facebook.github.io/react/blog/2016/11/16/react-v15.4.0.html#profiling-components-with-chrome-timeline)

Note: v15.4.0 one thing that may give problems is expectations of something that is going to be mounted, updated or unmounted in a period of time. With fiber, this may not happen when we're expecting and chrome profiling tools may help to find bugs.


### Side notes
- To optimize performance we can always **avoid reconciliation**
  - using `shouldComponentUpdate()`
  - using `React.PureComponent`

Note: shouldComponentUpdate() triggered before the re-rendering start; PureComponent verifies props and state, but does a Shallow comparison (solution: immutable data for the rescue)


## Thanks!

Daniela Matos de Carvalho ([@sericaia](https://twitter.com/sericaia))

Dec, 6th - [reactivate.london](https://reactivate.london/)
