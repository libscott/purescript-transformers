## Module Control.Monad.Cont.Class

This module defines the `MonadCont` type class and its instances.

#### `MonadCont`

``` purescript
class (Monad m) <= MonadCont m where
  callCC :: forall a b. ((a -> m b) -> m a) -> m a
```

The `MonadCont` type class represents those monads which support the
`callCC`, or _call-with-current-continuation_ operation.

This action makes the current continuation available to the caller.

For example:

```purescript
delay :: forall eff. Number -> ContT Unit (Eff (timeout :: Timeout | eff)) Unit
delay n = callCC \cont ->
  lift $ setTimeout n (runContT (cont unit) (\_ -> return unit))
```
An implementation is provided for `ContT`, and for other monad transformers
defined in this library.


