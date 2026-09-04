# A Snake Game Engine

A high-performance, event-driven Python/Pygame implementation of classic spatial grid navigation. Built around an explicit SDL event loop, dynamic data structures for positional state tracking, and fixed-interval temporal frame throttling.

---

## Technical Features & Engineering Highlights

* **Event-Driven Input Handling**: Implements non-blocking keyboard event listening with explicit boolean grouping `((Key OR Alternative) AND Direction Guard)` to prevent instantaneous $180^\circ$ self-collision faults.
* **Spatial Memory Array Representation**: Manages snake body dynamic expansion and contraction using array insertion (`insert(0, list(head))`) and deletion (`pop()`) routines operating on discrete 2D spatial coordinates.
* **Deterministic Boundary & Wrap Physics**: Implements dynamic coordinate wrapping across discrete grid dimensions (`square_size = 30px`) to handle out-of-bounds continuous traversal.
* **Fixed Timestep Synchronization**: Leverages Pygame's high-resolution `Clock` engine to cap frame execution rates to fixed tick intervals, preventing unthrottled CPU usage and ensuring uniform gameplay speed across varied hardware setups.

---

## Architecture & Logic Flow

```text
[ User Input (WASD / Arrows) ]
              |
              v
[ Event Listener & Guard Logic ] ---> Validates 180° Inversion
              |
              v
[ Coordinate Vector Update ] -------> Increments/Decrements head_pos [X, Y]
              |
              v
[ Boundary Physics Check ] ---------> Wraps coordinates if out-of-bounds
              |
              v
[ Collision & State Processing ] ---> Food Check (Score++) / Self-Collision
              |
              v
[ Screen Render & Tick Sink ] -------> Draws surfaces and throttles via Clock
