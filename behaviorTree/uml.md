```bash
void applyRecursiveVisitor(const TreeNode* root_node,
                           const std::function<void(const TreeNode*)>& visitor);


class LeafNode : public TreeNode
class ActionNodeBase : public LeafNode
class ConditionNode : public LeafNode

class ControlNode : public TreeNode
class DecoratorNode : public TreeNode
```

```bash
+-------------------+
|     TreeNode      |
+-------------------+
          ^
          |
  +----------------+
  |   ControlNode  |
  +----------------+
          ^
          |
+-----------------------+
|   ReactiveFallback    |
+-----------------------+
| + ReactiveFallback()  |
| + ~ReactiveFallback() |
| + tick(): NodeStatus  |
| + halt()              |
+-----------------------+

```

```bash
+-------------------------------------+
|             TreeNode                |
+-------------------------------------+
| - name_: std::string                |
| - status_: NodeStatus               |
| - uid_: uint16_t                    |
| - config_: NodeConfig               |
| - pre_conditions_: PreScripts       |
| - post_conditions_: PostScripts     |
| - wake_up_signal_: WakeUpSignal     |
+-------------------------------------+
| + TreeNode(name: std::string,       |
|            config: NodeConfig)      |
| + ~TreeNode()                       |
| + executeTick(): NodeStatus         |
| + haltNode()                        |
| + isHalted(): bool                  |
| + status(): NodeStatus              |
| + name(): const std::string&        |
| + waitValidStatus(): NodeStatus     |
| + type(): NodeType (pure virtual)   |
| + UID(): uint16_t                   |
| + fullPath(): const std::string&    |
| + registrationName(): const std::string& |
| + config(): const NodeConfig&       |
| + getInput<T>(key: std::string):    |
|     Expected<T>                     |
| + setOutput<T>(key: std::string,    |
|     value: T): Result               |
| + getLockedPortContent(key:         |
|     std::string): AnyPtrLocked      |
| + getRawPortValue(key: std::string):|
|     StringView                      |
| + emitWakeUpSignal()                |
| + requiresWakeUp(): bool            |
| + ... (other methods)               |
+-------------------------------------+

```


```mermaid
classDiagram
    %% Base Classes
    class TreeNode {
        <<abstract>>
        #NodeStatus status_
        #NodeConfig config_
        +NodeStatus tick()
        +virtual NodeType type()
        +virtual void halt()
        +string name()
        +uint16_t UID()
        +NodeStatus status()
        +getInput()
        +getOutput()
    }
    
    %% Main Node Types
    class ActionNodeBase {
        <<abstract>>
        #NodeStatus tick()
        +halt()
    }
    class ControlNode {
        <<abstract>>
        #std::vector~TreeNode*~ children_nodes_
        +addChild(TreeNode*)
        #halt()
    }
    class DecoratorNode {
        <<abstract>>
        #TreeNode* child_node_
        +setChild(TreeNode*)
        #halt()
    }
    
    %% Action Node Types
    class SyncActionNode {
        +NodeStatus tick()
        #virtual NodeStatus tick() abstract
    }
    class StatefulActionNode {
        +NodeStatus tick()
        #virtual NodeStatus onStart()
        #virtual NodeStatus onRunning()
        #virtual void onHalted()
    }
    class CoroActionNode {
        -std::shared_ptr~Coroutine~ coroutine_
        +NodeStatus tick()
        #virtual NodeStatus tick()
    }
    
    %% Control Node Types  
    class SequenceNode {
        -size_t current_child_idx_
        #NodeStatus tick()
    }
    class FallbackNode {
        -size_t current_child_idx_
        #NodeStatus tick() 
    }
    class ParallelNode {
        -size_t success_threshold_
        #NodeStatus tick()
    }
    
    %% Decorator Node Types
    class InverterNode {
        #NodeStatus tick()
    }
    class RetryNode {
        -int retry_count_
        #NodeStatus tick()
    }
    class SubtreeNode {
        -string subtree_id_
        +NodeStatus tick()
        +setSubtreeID(string)
    }

    %% Class Hierarchy
    TreeNode <|-- ActionNodeBase
    TreeNode <|-- ControlNode  
    TreeNode <|-- DecoratorNode
    
    ActionNodeBase <|-- SyncActionNode
    ActionNodeBase <|-- StatefulActionNode
    ActionNodeBase <|-- CoroActionNode
    
    ControlNode <|-- SequenceNode
    ControlNode <|-- FallbackNode
    ControlNode <|-- ParallelNode
    
    DecoratorNode <|-- InverterNode
    DecoratorNode <|-- RetryNode
    DecoratorNode <|-- SubtreeNode
```

