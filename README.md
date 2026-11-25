# 16-Bit Digital Lock CPU

A 4-digit BCD electronic lock built on a custom 16-bit Harvard-architecture processor in **Logisim-evolution 5.0.0**.

## Architecture
* **ALU_16bit:** 16-bit `ADD`, `SUB`, `AND`, `OR`.
* **Data_Path:** Two 16-bit registers (`Reg_A`, `Reg_B`) + ALU.
* **Control_Memory:** 8-bit Program Counter (`CTR8`) with jump/reset + `256×8` Instruction ROM.
* **Control_Unit:** `16×8` ROM-based decoder generating control signals (`En_A`, `En_B`, `ALU_Op`, `Jump_En`, `RAM_WE`, `MUX_Sel`).
* **Memory_IO:** `16×16` non-volatile RAM storing the passcode at `RAM[0]`.
* **Main:** 4 BCD buttons/counters/7-seg displays, Reset button, 16-bit comparator, and `Unlock`/`Lock` LEDs.

## Instruction Set & ROM
* **Instruction ROM (`256×8`):** `10 60 50 10 20 30 43`
* **Decoder ROM (`16×8`):** `00 05 46 04 14 28 02`

| Opcode | Instruction | Action |
| :--- | :--- | :--- |
| `0` | `NOP` | No operation |
| `1` | `LOAD A` | Load input to `Reg_A` |
| `2` | `LOAD B (RAM)` | Load `RAM[addr]` to `Reg_B` |
| `3` | `SUB` | Compute `A - B` |
| `4` | `JMP` | Jump to `addr` |
| `5` | `STORE` | Write `A AND B` to `RAM[addr]` |
| `6` | `LOAD B (IN)` | Load input to `Reg_B` |

## Usage
1. Open `circuits/lock.circ` in **Logisim-evolution 5.0.0** (requires Java 9+).
2. Enable clock (`Simulate -> Auto-Tick Enabled`, `Ctrl+K`, 4–8 Hz).
3. Use the Poke Tool to set a 4-digit code with the bottom buttons.
4. Press **Reset** (top-left) to save the code to `RAM[0]`.
5. Change digits to test: matching code lights **Unlock**; mismatch lights **Lock**.

## Authors
* Phan Van Duc, Hoang Van An, Nguyen Truong An — Class K26-DT3, Hanoi Open University.
* **Supervisor:** MSc. Pham Tien Huy.
