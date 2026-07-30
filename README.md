# APB-Based Countdown Timer

A Verilog RTL implementation of a countdown timer peripheral built around the
**AMBA APB (Advanced Peripheral Bus)** protocol, complete with a self-checking
testbench.

## Overview

This project implements a memory-mapped countdown timer that is configured,
started, and monitored entirely through APB read/write transactions — the
same interaction pattern used by real SoC peripherals such as watchdog
timers, GPIO controllers, and UARTs.

## Register Map

| Register         | Offset | Description                                            |
|-------------------|--------|--------------------------------------------------------|
| Load Register      | 0x00   | Write-only. Programs the countdown starting value.     |
| Control Register   | 0x04   | Bit[0]: start/stop control (auto-clears on completion). |
| Status Register    | 0x08   | Bit[0]: `timer_done` — read-only completion flag.      |

## Files

- `apb_timer.v` — RTL source for the APB timer peripheral
- `apb_timer_tb.v` — Testbench with reusable APB write/read tasks

## Tools Used

- Linux (Ubuntu)
- GVim
- Xilinx Vivado
- Verilog HDL
- GTKWave

## How It Works

1. Host writes the countdown value to the Load Register (0x00)
2. Host writes `1` to the Control Register (0x04) to start the timer
3. Counter decrements every clock cycle while running
4. On reaching zero, `timer_done` is asserted and the counter reloads
5. Host reads the Status Register (0x08) to check completion

## Author

**S N Ravindra**
