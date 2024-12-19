# BehaviorTree.CPP: Node Types and Architecture

## Node Types

BehaviorTree.CPP defines several categories of nodes, each serving a distinct purpose within a behavior tree:

- **Action Nodes**  
  Represent executable tasks that can be performed by your application (e.g., moving a robot, sending a command, performing a calculation).  
- **Condition Nodes**  
  Evaluate a condition (e.g., checking sensor data, a variable’s state) and return `SUCCESS` or `FAILURE`.  
- **Control Nodes**  
  Orchestrate the flow of execution among multiple child nodes. Control nodes define the logic for sequences, fallbacks, parallels, and more.  
- **Decorator Nodes**  
  Modify the execution logic or status of a single child node (e.g., inverting results, repeating until success, introducing delays or timeouts).  
- **Subtree Nodes**  
  Reference and encapsulate entire subtrees, allowing you to compose larger trees from modular parts.

### NodeType and NodeStatus

The library defines enums to categorize node types and represent node execution states:

```cpp
enum class NodeType
{
  UNDEFINED = 0,
  ACTION,
  CONDITION,
  CONTROL,
  DECORATOR,
  SUBTREE
};

enum class NodeStatus
{
  IDLE = 0,
  RUNNING = 1,
  SUCCESS = 2,
  FAILURE = 3,
  SKIPPED = 4,
};

enum class PortDirection
{
  INPUT,
  OUTPUT,
  INOUT
};

inline bool isStatusActive(const NodeStatus& status)
{
  return status != NodeStatus::IDLE && status != NodeStatus::SKIPPED;
}

inline bool isStatusCompleted(const NodeStatus& status)
{
  return status == NodeStatus::SUCCESS || status == NodeStatus::FAILURE;
}

enum class PreCond
{
  // order of the enums also tell us the execution order
  FAILURE_IF = 0,
  SUCCESS_IF,
  SKIP_IF,
  WHILE_TRUE,
  COUNT_
};

enum class PostCond
{
  // order of the enums also tell us the execution order
  ON_HALTED = 0,
  ON_FAILURE,
  ON_SUCCESS,
  ALWAYS,
  COUNT_
};
```

## Core Classes and File Paths

| Node Type       | Class Name           | File Path                                         |
| --------------- | -------------------- | ------------------------------------------------- |
| Action Node     | `SyncActionNode`     | `include/behaviortree_cpp/action_node.h`          |
| Control Node    | `ControlNode`        | `include/behaviortree_cpp/control_node.h`         |
| Decorator Node  | `DecoratorNode`      | `include/behaviortree_cpp/decorator_node.h`       |
| Condition Node  | `ConditionNode`      | `include/behaviortree_cpp/condition_node.h`       |
| SubTree Node    | `SubTreeNode`        | `include/behaviortree_cpp/subtree_node.h`         |
| Stateful Action | `StatefulActionNode` | `include/behaviortree_cpp/stateful_action_node.h` |

**Note:** While these are the core classes, most real-world use cases require implementing your own `Action` and `Condition` nodes derived from these base classes.

## Control Flow Nodes

Control flow nodes manage multiple children and determine the overall execution pattern:

| Node Name            | Description                                                                  | Class/Type         |
| -------------------- | ---------------------------------------------------------------------------- | ------------------ |
| **Sequence**         | Executes children in order; stops on the first failure.                      | `SequenceNode`     |
| **SequenceStar**     | “Sequence with memory”; remembers which child is currently running.          | `SequenceStarNode` |
| **Fallback**         | Executes children in order; stops on the first success.                      | `FallbackNode`     |
| **FallbackStar**     | “Fallback with memory”; remembers which child is currently running.          | `FallbackStarNode` |
| **Parallel**         | Executes children in parallel; criteria for success/failure is configurable. | `ParallelNode`     |
| **ReactiveSequence** | Like `Sequence`, but continuously re-checks conditions each tick.            | `ReactiveSequence` |
| **ReactiveFallback** | Like `Fallback`, but continuously re-checks conditions each tick.            | `ReactiveFallback` |
| **PipelineSequence** | Executes children in a pipeline fashion to "pipe" data through.              | `PipelineSequence` |
| **RoundRobin**       | Cycles through children in a round-robin manner each tick.                   | `RoundRobinNode`   |

## Decorator Nodes

Decorator nodes modify the logic or status of their single child node:

| Node Name                   | Description                                                                 | Class/Type                      |
| --------------------------- | --------------------------------------------------------------------------- | ------------------------------- |
| **ForceFailure**            | Forces the child's status to always return failure.                         | `DecoratorAlwaysFailureNode`    |
| **ForceSuccess**            | Forces the child's status to always return success.                         | `DecoratorAlwaysSuccessNode`    |
| **Inverter**                | Inverts the child's result (success ↔ failure).                             | `DecoratorInvertNode`           |
| **RetryUntilSuccessful**    | Retries the child until success or until max retries are reached.           | `DecoratorRetryNode`            |
| **Repeat**                  | Repeats the child's execution a set number of times or indefinitely.        | `DecoratorRepeatNode`           |
| **Negation**                | Inverts a boolean value from the child's input ports.                       | `DecoratorNegationNode`         |
| **Timeout**                 | Limits the child's execution time; returns failure if it exceeds the limit. | `DecoratorTimeLimitNode`        |
| **Delay**                   | Delays the child's tick by a specified duration.                            | `DelayNode`                     |
| **IfThenElse**              | Executes one of three children based on a boolean condition.                | `IfThenElseNode`                |
| **Switch**                  | Selects which subtree to run based on an integer input.                     | `SwitchNode`                    |
| **KeepRunningUntilFailure** | Continues executing the child until it returns failure.                     | `KeepRunningUntilFailureNode`   |
| **Subtree / SubtreePlus**   | Wraps a subtree, allowing hierarchical composition of behavior trees.       | `SubtreeNode / SubtreePlusNode` |

## Leaf Nodes (Abstract and Template Classes)

Leaf nodes typically implement the "work" in a behavior tree, either directly or via user-defined logic:

| Node Name               | Description                                                                          |
| ----------------------- | ------------------------------------------------------------------------------------ |
| **ActionNodeBase**      | Abstract base for action nodes; users implement `tick()` and `halt()`.               |
| **CoroActionNode**      | Base class for coroutine-based actions, supporting asynchronous `tick()` operations. |
| **ConditionNode**       | Abstract base for conditions; returns `SUCCESS` or `FAILURE`.                        |
| **SimpleActionNode**    | Template allowing definition of actions with simple functions/lambdas.               |
| **SimpleConditionNode** | Template allowing definition of conditions with simple functions/lambdas.            |
| **SimpleDecoratorNode** | Template for succinctly defining custom decorators.                                  |

**Note:**  
- Example action and condition nodes such as `SaySomething`, `CheckBattery`, or `MoveBase` can be found in the repository’s `examples` or `sample_nodes` directories. These serve as learning references and are not part of the core library.
- The main strength of BehaviorTree.CPP is providing a flexible framework. Users typically extend it by creating new leaf nodes and registering them into a factory, composing them into complex behaviors.

## Inheritance Diagram

Below is a conceptual diagram of the inheritance relationships. Template-based classes (e.g., `SimpleActionNode`, `SimpleConditionNode`) appear as conceptual placeholders even though they are defined via templates rather than pure virtual base classes:

```
                  ┌─────────────────┐
                  │     TreeNode     │
                  └───────┬─────────┘
                          │
             ┌────────────┼───────────────┐
             │                               │
         ControlNode                      LeafNode (Abstract)
             │                               ├── ActionNodeBase (Abstract)
             │                               │      ├── SyncActionNode
             │                               │      ├── CoroActionNode
             │                               │      ├── StatefulActionNode
             │                               │      └── SimpleActionNode (Template)
             │                               │
             │                               ├── ConditionNode
             │                               ├── SimpleConditionNode (Template)
             │                               └── SimpleDecoratorNode (Template)
             │
             ├── DecoratorNode
             │      ├── DecoratorAlwaysFailureNode
             │      ├── DecoratorAlwaysSuccessNode
             │      ├── DecoratorInvertNode
             │      ├── DecoratorRetryNode
             │      ├── DecoratorRepeatNode
             │      ├── DecoratorNegationNode
             │      ├── DecoratorTimeLimitNode (Timeout)
             │      ├── DelayNode
             │      ├── IfThenElseNode
             │      ├── SwitchNode
             │      ├── KeepRunningUntilFailureNode
             │      └── SubtreeNode / SubtreePlusNode
             │
             ├── SequenceNode
             ├── SequenceStarNode
             ├── FallbackNode
             ├── FallbackStarNode
             ├── ParallelNode
             ├── ReactiveSequence
             ├── ReactiveFallback
             ├── PipelineSequence
             └── RoundRobinNode
```

## Composition

Beyond inheritance, behavior trees rely heavily on composition:

- **SubtreeNode** (and `SubtreePlusNode`) encapsulate entire subtrees, allowing hierarchical structuring of complex behaviors.
- **Decorator Nodes** hold a single child node, modifying its execution flow or result.
- **Control Nodes** maintain lists of child nodes and orchestrate their execution to define behavior patterns (sequence, fallback, etc.).

In essence, every node that isn’t a leaf node composes one or more child nodes, building up the tree structure from simple, reusable components.



Below is a conceptual UML-style class diagram representing some of the key classes in BehaviorTree.CPP, their inheritance, and common variables and methods. This diagram is an approximation based on the public API and general usage patterns described in the documentation. Actual class members and function signatures may vary depending on the library version.

```text
            ┌─────────────────────┐
            │       TreeNode       │
            ├─────────────────────┤
            │ - name_: std::string │
            │ - status_: NodeStatus│
            │ - type_: NodeType    │
            │ - blackboard_:       │
            │     Blackboard::Ptr  │
            │ - input_ports_:      │
            │     std::map<std::string,PortInfo>│
            │ - output_ports_:     │
            │     std::map<std::string,PortInfo>│
            ├─────────────────────┤
            │ + tick(): NodeStatus │
            │ + halt(): void       │
            │ + status(): NodeStatus│
            │ + setStatus(NodeStatus): void│
            │ + name(): std::string│
            │ + initialize(): void │
            │ + ports(): PortsList │
            └───────┬─────────────┘
                    │
        ┌───────────┼───────────┐
        │                           │
  ┌─────────────┐          ┌───────────────┐
  │  ControlNode │          │  LeafNode      │(Abstract concept)
  ├─────────────┤          ├───────────────┤
  │ - children_: std::vector<TreeNode*>     │
  ├─────────────┤          │ (No direct     │
  │ + addChild(TreeNode*): void             │
  │ + haltChildren(): void                  │
  │ + numberOfChildren(): size_t            │
  │ + child(size_t): TreeNode*              │
  └─────┬───────┘          └───────┬──────┘
        │                            │
        │                            │
        │                       ┌────┼───────────────────┐
        │                       │                        │
        │                  ┌───────────────┐       ┌───────────────┐
        │                  │ DecoratorNode  │       │ ActionNodeBase │
        │                  ├───────────────┤       ├───────────────┤
        │                  │ - child_: TreeNode*   │                │
        │                  ├───────────────┤       │ + tick(): NodeStatus│
        │                  │ + setChild(TreeNode*): │ + halt(): void │
        │                  │     void              │                 │
        │                  │ + child(): TreeNode*  │                 │
        │                  └──────────┬─────────┘ └─────────────────┘
        │                              │
        │                       ┌──────┼──────────────────┐
        │                       │                          │
        │             ┌─────────────────┐        ┌─────────────────┐
        │             │  ConditionNode  │        │  StatefulActionNode│
        │             ├─────────────────┤        ├─────────────────┤
        │             │ (no extra fields│        │ - internal_state_ │
        │             │   typically)    │        │ - coroutine data? │
        │             ├─────────────────┤        ├─────────────────┤
        │             │ + tick(): NodeStatus     │ + tick(): NodeStatus
        │             │   (usually checks cond)  │ (state machine logic)
        │             │                           │ + halt(): void
        │             └─────────────────┘        └─────────────────┘

        ┌────────────────┐
        │SimpleActionNode│ (Template)
        ├────────────────┤
        │ - functor_: Callable   │
        ├────────────────┤
        │ + tick(): NodeStatus   │
        │   (executes functor)   │
        └────────────────┘

        ┌───────────────────┐
        │SimpleConditionNode│ (Template)
        ├───────────────────┤
        │ - predicate_: Callable │
        ├───────────────────┤
        │ + tick(): NodeStatus   │
        │   (checks predicate)   │
        └───────────────────┘

        ┌──────────────────┐
        │SimpleDecoratorNode│ (Template)
        ├──────────────────┤
        │ - modifier_: Callable  │
        ├──────────────────┤
        │ + tick(): NodeStatus   │
        │   (modifies child's     │
        │    status)              │
        └──────────────────┘
```

### Key Points About the Diagram:

- **TreeNode**:  
  - The base class for all nodes.  
  - Maintains a `status_`, a `name_`, and references to input/output ports and a blackboard.  
  - Implements `tick()`, `halt()`, and status management functions.

- **ControlNode**:  
  - Inherits from `TreeNode`.  
  - Contains multiple children and defines logic to execute them in a particular order or pattern (e.g., Sequence, Fallback).

- **DecoratorNode**:  
  - Inherits from `TreeNode`.  
  - Wraps a single child node and modifies its behavior or result (e.g., Inverter, Retry, Timeout).

- **LeafNode (Conceptual)**:  
  - Represents nodes without children (Actions or Conditions).  
  - `ActionNodeBase` and `ConditionNode` derive from the `TreeNode` interface but don’t manage children.

- **ActionNodeBase**:  
  - A base class for defining actions.  
  - Typically, actions implement `tick()` and `halt()` to perform work.  
  - `SyncActionNode`, `CoroActionNode`, `StatefulActionNode`, and template-based nodes like `SimpleActionNode` extend `ActionNodeBase`.

- **ConditionNode**:  
  - Checks a condition and returns `SUCCESS` or `FAILURE` immediately.  
  - Usually does not alter state or run over multiple ticks.

- **Template Nodes (SimpleActionNode, SimpleConditionNode, SimpleDecoratorNode)**:  
  - Allow defining nodes by providing simple lambdas or callable objects rather than creating new subclasses.

**Note:** This is a general overview. The actual code may have additional methods, friend classes, internal utilities, or slightly different naming conventions. If you need more detail, it’s best to refer directly to the BehaviorTree.CPP source code and its official documentation.
