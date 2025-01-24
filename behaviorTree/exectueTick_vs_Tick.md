# Behavior Tree Node Overview

This document provides an overview of the `TreeNode` class and its key methods used within the behavior tree framework.

---

## Methods Overview

### `executeTick()`

- **Access**: `public`
- **Purpose**: 
  - This is a **framework-level function** in the `TreeNode` base class.
  - It is **invoked by the behavior tree framework** or users.
  - **Users should not override** this function.
- **Key Role**: Serves as the public entry point for executing a node's behavior.

---

### `tick()`

- **Access**: `protected virtual`
- **Purpose**:
  - This is an **internal implementation method** intended to be **overridden by derived classes**.
  - Derived classes define their specific behavior by implementing this method.
- **Key Role**: Represents the core logic of a node.

---

## Class Definition

```cpp
class TreeNode 
{
public:
    // Public method, called by the framework or users.
    NodeStatus executeTick();
    
protected:
    // Protected virtual method, must be overridden by derived node classes.
    virtual NodeStatus tick() = 0;
};
```

---

## Key Points to Remember

- **`executeTick()`**:
  - Public and used by the framework or users.
  - Should **not be overridden** by users.
  
- **`tick()`**:
  - Protected and **designed to be overridden** in derived classes.
  - Implements the specific behavior of a node.
