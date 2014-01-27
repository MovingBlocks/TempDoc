TODO, copied from pathfinding module.

## Nodes

Nodes are the core elements of a behavior tree. A node is a piece of code, that is run while an Actor is interpreting the behavior tree. 

When run, every node must return one of this states: SUCCESS, FAILURE, RUNNING.

SUCCESS and FAILURE are returned, depending on the behavior node's task. If the task takes some time, a node may return RUNNING. 

## Decorators & Composites

Nodes may have child nodes assigned. 
If a node accepts exactly one child, this node is called a Decorator. Such nodes add some functionality to another node, or subtree.  
If a node accepts many children, this node is called a Composite. The order of the children is important, since a composite delegates execution to one of its children.
The three basic composite nodes are:
* `Sequence` - All children run after each other. Failing child will fail the sequence.
* `Selector` - All children run after each other. Succeeding child will succeed the selector.
* `Parallel` - All children run in parallel. When the parallel finishes, depends on its policies.
* `Monitor` - All children are executed in parallel. As soon as any child succeeds or fails, the monitor succeed or fail.

Some basic decorators are:
* `Invert`   - Inverts the child's state.
* `Timer`    - Stops time and finishes with given state after defined duration.
* `Repeat`   - Repeats its decorated behavior forever.
* `Delay`    - Delays the execution of its decorated node some time.

## Actor and interpreter

A behavior tree can be assigned to be interpreted by several different minions. So, for each actor the tree has a unique state (state of timers, sequences, etc). This state is realized using a Task class. Instead of handling the actual work itself, a Node delegates its work to a Task class. So a node just create a Task for every actor, where the custom state data can be stored safely. 
