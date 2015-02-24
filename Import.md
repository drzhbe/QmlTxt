- [Simple QML Module usage in QML file](#simple-qml-module-usage-in-qml-file)
- [Singleton QML Module usage in QML file](#singleton-qml-module-usage-in-qml-file)
- [JS file usage in QML file](#js-file-usage-in-qml-file)
- [JS file usage in JS file](#js-file-usage-in-js-file)

# Simple QML Module usage in QML file

Structure
```
-- Use.qml
-- FOLDER
---- Module
------ qmldir
------ Module.qml
```

Module.qml
```qml
QtObject {
    property string foo: 'bar'
}
```

qmldir
```qml
MyModule 1.0 Module.qml
```

Use.qml
```qml
import FOLDER.Module 1.0

QtObject {
    MyModule {
        id: myInitializedModule
    }
    Component.onCompleted: console.log(myInitializedModule.foo)
}
```

### Note
> There is need to initialize module
> ```qml
> ...
> MyModule {
>     id: myInitializedModule
> }
> ...
> ```

# Singleton QML Module usage in QML file

Structure
```
-- Use.qml
-- FOLDER
---- Module
------ qmldir
------ Module.qml
```

Module.qml
```qml
pragma Singleton
QtObject {
    property string foo: 'bar'
}
```

qmldir
```qml
singleton MyModule 1.0 Module.qml
```

Use.qml
```qml
import FOLDER.Module 1.0

QtObject {
    Component.onCompleted: console.log(MyModule.foo)
}
```

### Note
> - To make module a singleton use `pragma singleton` at start of file and the word `singleton` in `qmldir` before identifier
> - There is no need to initialize module, simply use the identifier used in `qmldir` file (`MyModule`)

# JS file usage in QML file

Structure
```
-- Use.qml
-- animal.js
-- FOLDER
---- Module
------ qmldir
------ human.js
------ robot.js
```

animal.js
```js
function AnimalConstructor(name) {
    this.name = name;
}
```

human.js
```js
.pragma library
function HumanConstructor(name) {
    this.name = name;
}
```

robot.js
```js
function RobotConstructor(name) {
    this.name = name;
}
```

qmldir
```qml
Human 1.0 human.js
Robot 1.0 robot.js
```

Use.qml
```qml
import FOLDER.Module 1.0
import "animal.js" as Animal

QtObject {
    property var human: new Human.HumanConstructor('vaska')
    proverty var robot: new Robot.RobotConstructor('r2d2')
    property var animal: new Animal.AnimalConstructor('petka')
    Component.onCompleted: console.log(human.name, animal.name)
}
```

### Note
> - To make js file a library — put `.pragma library` at start of it
> - It is no difference between importing `library` and simple js file. The difference is that `library` file will share its context between any file, that will import it
> - Js file names should start with lower case (`human.js`, not `Human.js`)
> - File content will be able by `Human` identifier used in `qmldir`, so to use functions from file you should use `Human.HumanConstructor`
> - When importing js file by `import "path/to/file.js"` you *have to* use qualifier (`as`)

# JS file usage in JS file

Structure
```
-- FOLDER
---- Module
------ human.js
------ hand.js
------ foot.js
```

human.js
```js
.import "hand.js" as Hand
Qt.include('foot.js');
function HumanConstructor(name) {
    this.name = name;
    this.hand = new Hand.HandConstructor();
    this.foot = new FootConstructor();
}
```

hand.js
```js
function HandConstructor() {}
HandConstructor.prototype.take = function() {...}
```

foot.js
```js
function FootConstructor() {}
FootConstructor.prototype.kick = function() {...}
```

### Note
> - When use `.import` you *have to* use a qualifier (`as`)
> - `.import` imports all the variables defined in the file
> - `Qt.include` imports only functions, but qualifier is not needed
