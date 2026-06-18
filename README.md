# Real-Time x86 Assembly Falling Words Game

A high-performance, interactive text-based typing game engineered completely in Intel x86 Assembly using the Microsoft Macro Assembler (MASM) architecture and the `Irvine32` runtime library.

---

## Low-Level Technical Achievements

* **Dynamic Heap Memory Management:** Bypassed static data limits by manually managing runtime memory distribution. Engineered explicit allocations and deallocations within the OS heap space as text objects spawned, collided, or were neutralized by the user—demonstrating rigorous control over dynamic memory pointers without garbage collection abstractions.
* **C++ Inspired Event-Driven Architecture:** Adapted architectural concepts from high-level graphics frameworks (SFML) down to low-level assembly. Implemented a non-blocking asynchronous event-listener loop that continuously samples keyboard states, providing ultra-responsive input tracking.
* **Frame-Independent Physics & Delta Timings:** Divorced visual rendering from object logic. Built an independent tracking system where every dynamically spawned word maintains its own velocity vector and floating frame-counter delay, translating data coordinates relative to a target 60 FPS baseline (e.g., precise 1 unit/sec vector translation).
* **Direct Register-Level Mechanics:** Manually managed 32-bit Intel x86 registers (`EAX`, `EDX`, `EBX`, `ECX`) to execute string arithmetic, track runtime heap addresses, and process character comparisons.
* **Console Matrix Coordination:** Utilized the `Irvine32` API to surgically manipulate display coordinates (`Gotoxy`). By segmenting the console screen matrix into strict $X/Y$ bounds, the application handles continuous vertical translation of multiple string arrays seamlessly.

---

## Development Stack & Environment
* **Language:** Intel x86 Assembly (32-bit Protected Mode)
* **Assembler:** MASM (Microsoft Macro Assembler)
* **Linker Library:** `Irvine32.inc` (Win32 API Bridge)
* **Execution Environment:** Windows Console Subsystem

---

## How It Works (Architectural Flow)
1. **The Event-Driven Loop:** The core subsystem acts as an event-dispatcher. It samples hardware keystroke interrupts continuously without locking the application state, sending valid ASCII data down to comparison structures.
2. **Dynamic Heap Lifecycle:** When a word triggers, the application requests chunk sizing from the OS heap. Upon user clearing or baseline boundary collision, the structure executes an explicit memory free routine to ensure a zero-leak footprint.
3. **Delta Processing:** The state machine logs tick ticks. Words step along their individual trajectory arrays based on programmatic velocity variables, scaling their physics loop independently of basic processor cycles.
