## State Machine
#### Node Based
A node based state machine uses nodes as states themselves. This is achieved by having a State class and StateMachine class controlling.
- **State Class**: This class ensures that each state has the same set of methods for a common interface.
- **StateMachine Class**: This class tracks the current state, changing states and calling state updates.

You can use these classes to create multiple state machines and we should be careful about using `_physics_process()` or `_process()` in the State class. This is because if we put them in here multiple states will all run. We only want one to run at any given time.

Here is the methods we want to use and their purposes:
- `enter()`: It’s called when the state becomes active.
- `exit()`: It’s called when the state is about to change.
- `update()`: The state machine calls it on the engine’s delta frames.
- `physics_update()`: The state machine calls it on the engine’s physics update tick.