# Vending Machine Controller using FSM

A Verilog implementation of a synchronous Vending Machine controller using a Finite State Machine (FSM). This design tracks coin inputs and dispenses a bottle once the required amount (15 units) is reached.

## 🚀 Design Overview
The controller is designed as a **Moore Machine**, where the output (`bottle`) depends solely on the current state.

### State Definitions:
* **s0 (00):** Initial state / 0 units.
* **s5 (01):** 5 units accumulated.
* **s10 (10):** 10 units accumulated.
* **s15 (11):** 15 units accumulated (Target reached).

### Input Logic:
The `coin` input is a 2-bit signal:
* `2'b00`: No coin inserted.
* `2'b01`: 5-unit coin inserted.
* `2'b10`: 10-unit coin inserted.

## 🛠️ Hardware Logic
* **Sequential Logic:** Updates the current state on every positive edge of the `clk`, with an asynchronous `rst` to return to `s0`.
* **Combinational Logic:** Determines the `next_state` based on the current state and the `coin` input.
* **Output Logic:** The `bottle` signal is set to high (`1'b1`) only when the FSM reaches the `s15` state.

## 📂 Code Structure
* `vending_machine.v`: The core module containing the FSM logic.
* **Inputs:** `clk`, `rst`, `coin[1:0]`
* **Outputs:** `bottle`

## 📊 State Transitions
1. From **s0**: `5` units move to **s5**, `10` units move to **s10**.
2. From **s5**: `5` units move to **s10**, `10` units move to **s15**.
3. From **s10**: Any coin (`5` or `10`) moves to **s15**.
4. From **s15**: Automatically resets to **s0** on the next cycle after dispensing.

---
Developed as part of the [adithprojects](https://github.com/AdithSoragu/adithprojects) collection.

------

*Simulation Results

<img width="1364" height="732" alt="image" src="https://github.com/user-attachments/assets/0cd20d59-750b-4fac-b8b9-dc5c0b85c0ab" />

