Touch Pad Sense Control System (STM32 + FreeRTOS)

Overview
This project implements a Touch Pad Sense Control System using an STM32 microcontroller and FreeRTOS. The system uses external interrupt-based touch inputs to switch between multiple operating modes. Each mode activates a specific task that toggles LEDs at different intervals. The system also supports UART commands to monitor system status and change operating modes dynamically.
The project demonstrates real-time multitasking, event handling, interrupt handling, and task synchronization using FreeRTOS.

🎯Features:                                                                                       
Touch pad input using GPIO interrupts

FreeRTOS multitasking

Mode switching using Event Groups
Software timers for periodic operations
UART command interface
Mutex protection for shared resources
Task monitoring using FreeRTOS task list
Emergency mode support

⚡Hardware Requirements
STM32 development board (STM32F4 series)
4 Push Buttons / Touch Inputs
LEDs connected to GPIO pins
UART interface (115200 baud)
USB to Serial converter

🏎️Operating Modes:

Emergency Mode
Triggered by PA0
Toggles Emergency LED
Higher priority task

Task1 Mode
Triggered by PA1
Toggles LED every 500 ms

Task2 Mode
Triggered by PA2
Toggles LED every 1000 ms

Task3 Mode
Triggered by PA3
Toggles LED every 1500 ms
Only one task runs at a time. Others remain suspended.

FreeRTOS Components Used
Tasks
Emergency_Task
Task1
Task2
Task3
Control_Task
UART_Task

Synchronization
Mutex
LED Mutex
UART Mutex
Event Groups
Used for mode switching.

Event Bits:
EMER  = 0x01
TASK1 = 0x02
TASK2 = 0x04
TASK3 = 0x08

UART Commands
Check System Status
STATUS?
Displays task status using FreeRTOS vTaskList().
Example Output

Task Name   State   Priority   Stack   Number
----------------------------------------------
Task1       Ready     1        ...
Task2       Suspended 1        ...
Task3       Suspended 1        ...
Emergency   Running   2        ...

💡Change Operating Mode
Emergency Mode
SET_MODE=EMERG
#Task1 Mode
SET_MODE=TASK1
#Task2 Mode
SET_MODE=TASK2
#Task3 Mode
SET_MODE=TASK3

System Health Monitoring
Every 15 seconds, the system prints:
No of times Events Changed: X
This indicates how many times the operating mode has changed.

Interrupt Handling
GPIO Interrupt
When a touch input is detected:
External interrupt is triggered
Debounce timer starts
Event bit is set
Control task switches the active task

🎨Software Architecture
Touch Input
     ↓
GPIO Interrupt
     ↓
Debounce Timer
     ↓
Event Group
     ↓
Control Task
     ↓
Resume Selected Task
     ↓
Suspend Other Tasks

🔖Learning Outcomes
This project demonstrates:
FreeRTOS task scheduling
Event group synchronization
Interrupt-driven design
UART communication
Real-time system control
Embedded multitasking
