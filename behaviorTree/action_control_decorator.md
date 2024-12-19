# BehaviorTree.CPP Overview

BehaviorTree.CPP is a framework for creating behavior trees, which are used to model the decision-making process of an agent. Below is an explanation of the different types of nodes and how they are used in the framework.

## Node Types

### Action Nodes (`ActionNodeBase`)
Action nodes are the leaf nodes of a behavior tree and execute actual behaviors. They return a status of `SUCCESS`, `FAILURE`, or `RUNNING`.

#### Types of Action Nodes:
1. **`SyncActionNode`**:
   - For immediate actions that complete in one tick.

2. **`StatefulActionNode`**:
   - For actions with states: `IDLE`, `RUNNING`, `SUCCESS`, or `FAILURE`.

3. **`CoroActionNode`**:
   - For asynchronous actions using coroutines.

#### Example:
```cpp
class MyAction : public BT::SyncActionNode {
    NodeStatus tick() override {
        // Perform the action and return SUCCESS or FAILURE
    }
};
```

---

### Control Nodes (`ControlNode`)
Control nodes manage the execution flow by controlling the behavior of multiple child nodes.

#### Common Types:
1. **`SequenceNode`**:
   - Executes children in sequence until one fails.

2. **`FallbackNode`**:
   - Executes children in sequence until one succeeds.

3. **`ParallelNode`**:
   - Executes multiple children simultaneously.

4. **`SwitchNode`**:
   - Selects which child to execute based on a condition.

#### Example:
```cpp
BT::SequenceNode sequence("sequence");
sequence.addChild(&action1);
sequence.addChild(&action2);
```

---

### Decorator Nodes (`DecoratorNode`)
Decorator nodes modify the behavior of a single child node.

#### Common Types:
1. **`InverterNode`**:
   - Inverts the result of its child.

2. **`RetryNode`**:
   - Retries the child on failure.

3. **`TimeoutNode`**:
   - Adds a time limit to the child’s execution.

#### Example:
```cpp
BT::RetryNode retry("retry", 3);  // Retry up to 3 times
retry.setChild(&action);
```

---

## Key Differences Between Node Types
1. **Action Nodes**:
   - Execute actual behaviors (e.g., open a valve, check pressure).

2. **Control Nodes**:
   - Manage the execution flow of multiple children.

3. **Decorator Nodes**:
   - Modify the behavior of a single child.

---

## Example: Valve Operation
For a system controlling a valve:

1. **Action Nodes**:
   - `OpenValveAction`: Opens the valve.
   - `CheckPressureAction`: Checks the pressure.

2. **Control Nodes**:
   - `SequenceNode`: Ensures actions are executed in order.

3. **Decorator Nodes**:
   - `TimeoutNode`: Enforces a time limit for operations.

#### Pseudo-Code:
```cpp
BT::SequenceNode sequence("sequence");
sequence.addChild(new OpenValveAction("open_valve"));
sequence.addChild(new CheckPressureAction("check_pressure"));

BT::TimeoutNode timeout("timeout", 5000);  // 5-second limit
timeout.setChild(&sequence);
```

With this structure, the valve will open and pressure will be checked in sequence, but the entire operation will timeout if it exceeds 5 seconds.

---

This overview provides a foundation for using BehaviorTree.CPP to build efficient and maintainable decision-making systems.

