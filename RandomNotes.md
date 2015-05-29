* `flick` will be canceled (`cancelFlick()` called internally) after `ListModel.clear()`
* You can not use `Connections{}` inside `QtObject` because last can not include `Element`s
* [`once`](https://gist.github.com/drzhbe/cacc4115f388d3753132) used in situations when `callback` should be called if `condition` or after `signal` emitted
* (2gis v4android specific) You can not affect an `opacity` of `TextEditItem` because of `TextEditAndroidNative`
* If some of `ListView`'s children will change `height` while `ListView`'s animation on `add` is running, `ListView`'s `contentHeight` will not update
