# JavaScript

A general cheat sheet and notes regarding javascript.

## Overwriting a function in the prototype chain

```js
MyClass.prototype.onAfterRendering = function() {
  SuperClass.prototype.onAfterRendering.apply(this);
  // do your additional stuff AFTER calling super class
}
```