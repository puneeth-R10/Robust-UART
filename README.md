**Robust UART – Verilog Design and Verification**



📌 Project Overview

This project presents the design and simulation of a robust UART (Universal Asynchronous Receiver Transmitter) implemented in Verilog HDL. The design focuses on reliability, configurability, and real-world robustness, addressing common challenges in serial communication such as baud mismatch, data loss, and transmission errors.

The UART supports full-duplex communication, programmable baud rate, FIFO buffering, and parity-based error detection, along with a comprehensive self-checking testbench for verification.



🎯 Key Features

Full-Duplex Communication
Simultaneous transmission and reception of data using independent TX and RX paths.

Programmable Baud Rate
Baud rate can be changed dynamically using a baud divisor, allowing operation at different speeds without redesign.

TX and RX FIFO Buffers
FIFO buffering prevents data loss during burst transfers and decouples UART timing from system logic.

Oversampling-Based Receiver
The receiver uses oversampling to sample incoming bits at the center of each bit period, improving noise immunity and timing tolerance.

Parity-Based Error Detection
Supports even and odd parity for detecting single-bit transmission errors.

Error Handling and Retransmission (Testbench Driven)
On detecting a parity error, the testbench simulates a NAK request and forces retransmission, demonstrating robustness.



🧱 Architecture Description

Transmitter (TX) Path

Parallel data is written into the TX FIFO.

uart_tx reads data from FIFO when available.

Start bit, data bits, optional parity bit, and stop bit are serialized.

Output is driven on the tx_serial line at the selected baud rate.


Receiver (RX) Path

Incoming serial data is sampled using oversampling.

Start bit is detected, followed by data bit sampling.

Parity is checked (if enabled).

Valid data is pushed into the RX FIFO and made available to the system.


⏱ Baud Rate Generation

A baud generator produces:

Oversample tick → used by the RX for precise sampling

Baud tick → used by the TX to shift bits

Baud rate is controlled using a baud divisor, calculated as:

baud_divisor = Clock_Frequency / (Baud_Rate × Oversampling_Factor)



🧪 Verification Strategy

A stable, self-checking testbench is used to validate all core UART functions.

Verified Test Cases

Full-duplex TX ↔ RX communication

Multiple baud rates (fast, medium, slow)

FIFO buffering and tx_full behavior

Even and odd parity checking

Intentional data corruption and error detection

Retransmission after parity error

Waveform-based validation using VCD files

The testbench is designed to ensure all critical signals toggle at least once, making waveform analysis simple and clear.



📊 Waveform Observation

The waveform verifies:

Bit timing variation with baud rate changes

FIFO full condition during burst writes

Parity error assertion on corrupted frames

Correct data reception after retransmission

Only essential signals are dumped to keep waveforms clean and easy to analyze.



🛠 Tools & Technologies

Language: Verilog HDL

Simulation: Xilinx ISE 

Design Style: FSM-based control, synchronous FIFOs

Verification: Self-checking testbench with fault injection



🚀 Applications

Embedded systems communication

FPGA-based serial interfaces

ASIC/VLSI design practice

Reliable data links in noisy environments

📌 Conclusion

This project demonstrates a practical, industry-relevant UART design with strong emphasis on reliability, error handling, and verification. The combination of FIFO buffering, oversampling, and parity checking makes the UART robust and suitable for real-world deployment.
