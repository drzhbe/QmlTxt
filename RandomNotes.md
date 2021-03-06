* There are not allowed 2 singleton declarations in 1 qmldir file
* **Compile** and **Create**. If you define Component on the page, it will be *compiled*. If you initialize it on the page it will also be *created*. If you pass an url to Loader.source it will be *compiled* and *created* only after source will be set. Alse you can imperatively create component `var compo = Qt.createComponent(...)` and then `compo.createObject(...)` to achieve synchronous lazy object creation
* `flick` will be canceled (`cancelFlick()` called internally) after `ListModel.clear()`
* `QtObject` doesn't have `parent` property, even if you create it inside some element or create it via `component.createObject(parent)`. The only qml-like property it has is `objectName`
* You can not use `Connections{}` inside `QtObject` because last can not include `Element`s
* [`once`](https://gist.github.com/drzhbe/cacc4115f388d3753132) used in situations when `callback` should be called if `condition` or after `signal` emitted
* (2gis v4android specific) You can not affect an `opacity` of `TextEditItem` because of `TextEditAndroidNative`
* If some of `ListView`'s children will change `height` while `ListView`'s animation on `add` is running, `ListView`'s `contentHeight` will not update
* `Element` on destruction will `null` the `parent` property first, so when you have some bindings on it, they will run on this dying element with no `parent`
* Properties initialized in order you pass them on use, not in order you define them in the component:
  ```qml
  // YourElement.qml
  Item {
    property string firstName
    property string secondName
  }

  // Use.qml
  import 'YourElement'
  YourElement {
    secondName: 'Vasiliev'
    firstName: 'Vaska'
  }
  ```
  At first `onSecondNameChanged` will fire, and then `onFirstNameChanged` will fire
* Program could fail in `.js` file without any error notifications. I suspect that this js file executes in `binding` in c++ code and exception can be catched somewhere there
