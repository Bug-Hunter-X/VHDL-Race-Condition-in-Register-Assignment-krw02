# VHDL Race Condition Bug
This repository demonstrates a common race condition bug in VHDL code.  The bug occurs in a simple register assignment within a clocked process. The `data_in` signal is read inside the rising edge of the clock.  If this signal changes simultaneously with the clock edge, the value stored in the register could be incorrect, leading to unexpected behavior in the system.

## Bug Description
The issue stems from the assumption that `data_in` will remain stable throughout the rising clock edge. If another process modifies `data_in` during this time, the register's value could be set to an intermediate, undefined value.  This problem is particularly difficult to detect through simulation as it may only occur under very specific timing conditions.

## Solution
The solution involves adding appropriate synchronization mechanisms to ensure that `data_in` is stable before being sampled. This could involve using a separate register to hold the `data_in` value, sampling it in a previous clock cycle, or using more sophisticated synchronization techniques depending on the design requirements.

## How to reproduce
1.  Synthesize the provided VHDL code.
2.  Simulate the design with a testbench where `data_in` changes very close to the clock edge.
3.  Observe the unpredictable output on `data_out`.
