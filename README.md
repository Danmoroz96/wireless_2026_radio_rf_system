# wireless_2026_radio_rf_system
The objective of this task is to understand the internal structure of a real radio frequency communication device by identifying and explaining its main RF system blocks based on publicly available datasheets.

Student name: Danila Morozov

Student ID: 2312827

Selected device name: Nordic nRF52840

Datasheet link: https://docs.nordicsemi.com/category/nrf52840-category



The signal flow generally moves from the MCU/Memory through the Radio Core (Modulation), out through the Frontend (PA/Matching), and finally to the Antenna. On the flip side, incoming signals enter the Antenna, go through the Matching/LNA, and are Demodulated back into data for the MCU.

Short explanation of each RF block: 

1. Information Source / MCU (ARM® Cortex®-M4)
Role: The "brain" of the operation. It handles the application code and the higher layers of the Bluetooth/Thread protocol stack.

Signal Flow: It prepares the digital data packets (0s and 1s) and sends them to the Radio Core via the internal bus for transmission.

2. RF Transceiver (Radio Core)
Role: A unified block that handles both transmission (Tx) and reception (Rx) logic.

Signal Flow: It acts as the gatekeeper, switching the device between "talk" and "listen" modes based on the timing requirements of the wireless protocol.

3. Modulation / Demodulation
Role: Translates digital data into radio waves (and vice-versa) using GFSK (Gaussian Frequency Shift Keying) for Bluetooth.

Signal Flow: During transmission, it shifts the carrier frequency to represent data bits; during reception, it "decodes" these frequency shifts back into digital bits.

4. Power Amplifier (PA)
Role: Boosts the signal strength before it leaves the chip.

Signal Flow: It takes the low-power modulated signal and amplifies it (up to +8 dBm on the nRF52840) to ensure the radio wave can travel the required distance to the receiver.

5. Low Noise Amplifier (LNA)
Role: Sensitizes the receiver to pick up very weak incoming signals from the air.

Signal Flow: It amplifies the tiny voltages captured by the antenna while adding as little "noise" as possible, making the signal clear enough for the demodulator to read.

6. RF Filtering & Matching Network
Role: Ensures maximum power transfer and filters out "noise" or harmonics that could cause interference.

Signal Flow: This passive network (usually external inductors and capacitors) matches the 50Ω impedance of the antenna to the chip's internal impedance, ensuring the signal doesn't "bounce back" into the chip.

7. Antenna Interface
Role: The physical point where the electrical signal is converted into an electromagnetic wave.

Signal Flow: It provides a single-ended connection (the ANT pin) where the filtered RF signal is finally radiated into the environment or captured from it.

8. Power Supply for RF Section (DC/DC & LDO)
Role: Provides clean, stable voltage specifically for the sensitive analog RF components.

Signal Flow: It converts battery voltage down to the specific levels needed by the PA and LNA, using filtering to ensure that "noise" from the digital MCU doesn't bleed into the radio signal.
