# Notes from JavaScript Enlightenment

## Values

Values in JavaScript are either primitive or objects.


All primitive values have corresponding native constructors that creates wrapper objects when necessary. In fact, when performing operations on primitive values such as `"abd".toUpperCase()`, the string is converted from its primitive form into an object, then execute the method inherited from the native `String` constructor.

When calling the native primitive constructor without `new` operator, it will return a primitive represetation of the value. e.g.
```
"abc" === String("abc")
true === Boolean(true)
5 === Number(5)
```

## Instances and inheritance

You can create objects using one of the following methods:
- Object literals, e.g. `{}`
- `new` keyword, followed by a constructor, e.g. `new Object(template)`
- `Object.create` function, providing a template object, e.g. `Object.create(template)`

### Object literal

Considered an instance of global `Object` constructor, will inherit methods and properties in `Object.prototype`. If this is not the desired behavior, you can use `Object.create(null)` to get an empty object instead.

### `Object.create(template)`

Uses the template object as prototype for the instance it will return, which means if `template` is a nested object, then any changes made on `template` object will be reflected on the instances inherited from it.

The instance will inherit constructor of the template object.

### `new` operator

`new` operator will create a JavaScript object using the constructor function as a template, and inherit the prototype chain of the constructor function with a non-enumerable `prototype` property whose `constructor` property points to the function itself.

* setting `prototype` property to a primitive value will be ignored.
* instances reference the `prototype` object it is linked to at the time of instantiation. If the constructor function points to a difference `prototype` property later on, new instances will point to the new `prototype` while the previous instances will point to the previous `prototype` object.

When `new` is used, the value `this` literally means the new object/instance that will be created based on the statements inside the constructor function.

On the other hand, if you create a constructor function and call it without the use of the `new` keyword, `this` will refer to the "parent" object that contains the function, which usually refers to the global object unless `this` value is binded to other values (such as using arrow functions of ES6 or `.bind` or `.apply`)

### `typeof` and `instanceof`

`typeof` keyword, when used with RegExp or Function instances, return `"function"`

One thing to watch out for when dealing with the instanceof operator is that it will return true any time you ask if an object is an instance of Object since all objects inherit from the Object() Constructor.

The instanceof operator will return false when dealing with primitive values that leverage object wrappers (e.g. 'foo' instanceof String // returns false).

## JavaScript environment

Accidental global variable are created as delete-able global **property**, whereas declared global **variable** can not be deleted.

If you are in strict mode, you will get an error when trying to create accidental global variable.


The window object contains a cyclic reference to itself, i.e. window === window.window, hence, lookup is slower if you dictate that it should find window object first, then lookup the alert method.

Ref: https://www.quora.com/Why-is-window-alert-foo-slower-than-alert-foo
