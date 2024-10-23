
# Python Mutability, Immutability, Pass-by-Reference, and Pass-by-Value

This README explains the key concepts of mutability, immutability, pass-by-reference, and pass-by-value in Python. Examples are provided to clarify each concept.

## Key Concepts

### Mutability and Immutability

- **Immutable Types**: Once created, the values of these types cannot be changed. Examples:
  - `int` (Integers)
  - `float` (Floating-point numbers)
  - `str` (Strings)
  - `tuple` (Tuples)
  - `bool` (Booleans)
  - `frozenset` (Frozen sets)
  - `bytes` (Byte sequences)

- **Mutable Types**: These types allow their values to be changed after creation. Examples:
  - `list` (Lists)
  - `dict` (Dictionaries)
  - `set` (Sets)
  - `bytearray` (Byte arrays)
  - User-defined classes (if mutable attributes are defined)

### Pass-by-Reference vs Pass-by-Value

- **Pass-by-Reference**: When a **mutable** object is passed to a function, the function works with a reference to the original object. Modifications within the function will affect the original object.
  
- **Pass-by-Value**: When an **immutable** object is passed to a function, a copy of the object’s value is passed. Any changes made within the function will not affect the original object.

## Examples

### Immutable Type Example (Integer)

```python
def main():
    arg = 4
    square(arg)
    print(arg)  # Prints 4 because integers are immutable

def square(n):
    n *= n  # This modifies only the local variable n

main()
```

**Explanation**:  
- **Immutable Integer**: The variable `arg` is an integer, which is immutable.
- **Pass-by-Value**: The `square` function gets a copy of `arg`. Changing `n` inside `square` does not affect `arg`.
- **Output**: `print(arg)` prints the original value `4`, unchanged.

### Mutable Type Example (List)

```python
def main():
    arg = [4]
    square(arg)
    print(arg)  # Prints [16] because lists are mutable

def square(n):
    n[0] *= n[0]  # Modifies the original list

main()
```

**Explanation**:  
- **Mutable List**: The variable `arg` is a list, which is mutable.
- **Pass-by-Reference**: The `square` function receives a reference to the original list. Modifications inside `square` affect the list in `main`.
- **Output**: `print(arg)` prints `[16]`, the modified value of the list.

### Example with Class Object

```python
class MyClass:
    def __init__(self, value):
        self.value = value

def modify_object(obj):
    obj.value = 20

def main():
    my_obj = MyClass(10)
    print(my_obj.value)  # Prints 10
    modify_object(my_obj)
    print(my_obj.value)  # Prints 20

main()
```

**Explanation**:  
- **Class Definition**: `MyClass` defines an object with a mutable attribute `value`.
- **Pass-by-Reference**: The `modify_object` function receives a reference to `my_obj` and modifies its `value` attribute.
- **Output**: The `value` changes from `10` to `20` after `modify_object` is called.

### Threading Example

```python
import logging
import threading
import time

def worker(arg):
    while not arg['stop']:
        logging.debug('Worker thread running')
        time.sleep(0.5)

def main():
    logging.basicConfig(level=logging.DEBUG, format='%(relativeCreated)6d %(threadName)s %(message)s')
    info = {'stop': False}
    thread = threading.Thread(target=worker, args=(info,))
    thread.start()
    
    try:
        while True:
            logging.debug('Main thread running')
            time.sleep(0.75)
    except KeyboardInterrupt:
        info['stop'] = True

    thread.join()

if __name__ == '__main__':
    main()
```

**Explanation**:  
- **Mutable Dictionary**: The `info` dictionary is mutable and is passed by reference to both threads.
- **Thread Communication**: The `worker` and `main` functions share the `info` dictionary. When `info['stop']` is set to `True` in the main thread, the worker thread sees this change and stops.
- **Stopping the Thread**: A `KeyboardInterrupt` sets `info['stop']` to `True`, which stops the worker thread.

## Key Takeaways

- **Immutable types** (e.g., integers, strings) are passed by value, so changes within a function do not affect the original object.
- **Mutable types** (e.g., lists, dictionaries) are passed by reference, so changes within a function affect the original object.
- **Class objects** are passed by reference, allowing function modifications to their attributes.
- Understanding mutability, immutability, and how Python handles argument passing is essential for effective programming, especially when dealing with functions, classes, and threading.
