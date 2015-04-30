* `flick` will be canceled (`cancelFlick()` called internally) after `ListModel.clear()`
* You can not use `Connections{}` inside `QtObject` because last can not include `Element`s
* [`once`](https://gist.github.com/drzhbe/cacc4115f388d3753132) used in situations when `callback` should be called if `condition` or after `signal` emitted
* (specific) You can not affect an `opacity` of `TextEdit` because of `TextEditAndroidNative`
