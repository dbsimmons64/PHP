
1. **`__construct()`**: Called when a new object is instantiated.
2. **`__destruct()`**: Called when an object is destroyed.
3. **`__call($name, $arguments)`**: Called when invoking inaccessible or undefined methods on an object.
4. **`__callStatic($name, $arguments)`**: Called when invoking inaccessible or undefined static methods.
5. **`__get($name)`**: Called when accessing inaccessible or undefined properties.
6. **`__set($name, $value)`**: Called when setting inaccessible or undefined properties.
7. **`__isset($name)`**: Called when `isset()` or `empty()` is used on inaccessible or undefined properties.
8. **`__unset($name)`**: Called when `unset()` is used on inaccessible or undefined properties.
9. **`__sleep()`**: Called when serializing an object to specify the properties to serialize.
10. **`__wakeup()`**: Called when unserializing an object to reinitialize it.
11. **`__toString()`**: Called when an object is treated as a string.
12. **`__invoke()`**: Called when an object is used as a function.
13. **`__set_state($array)`**: Called when `var_export()` is used to return the array representation of an object.
14. **`__clone()`**: Called when an object is cloned.
15. **`__debugInfo()`**: Called when `var_dump()` is used to provide custom debug information.

Less Common Magic Functions
16. . **`__autoload($class)`**: Automatically loads classes when they are instantiated if they haven't been included yet (deprecated).
17. **`__serialize()`**: Customizes which properties of an object to serialize.
18. **`__unserialize($data)`**: Customizes how properties of an object are restored during unserialization.