### Side notes
- To optimize performance we can always **avoid reconciliation**
  - using `shouldComponentUpdate()`
  - using `React.PureComponent`

Note: shouldComponentUpdate() triggered before the re-rendering start; PureComponent verifies props and state, but does a Shallow comparison (solution: immutable data for the rescue)


## Thanks!

Daniela Matos de Carvalho (@sericaia)

Dec, 6th - [reactivate.london](https://reactivate.london/)
