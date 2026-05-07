# 3.32 Super GPIO

> [!IMPORTANT]
> This page is intended for the Seeed `reComputer Super` carrier-board family, such as [`reComputer Super J4011`](https://www.seeedstudio.com/reComputer-Super-J401-Carrier-Board-p-6642.html). The 40-pin header layout and pin behavior are board-specific and should not be assumed to match other Jetson carrier boards.

## Introduction

GPIO stands for General Purpose Input/Output. These pins let software read external digital signals or drive simple peripherals such as LEDs, buttons, buzzers, and control lines. The reComputer Super features a 40-pin extension header that provides access to GPIO pins, allowing for easy integration with external devices.

## Hardware Connection

The reComputer Super features a 40-pin extension header that provides access to GPIO pins. To use the GPIO pins, you need to connect external devices to the appropriate pins on this header.

## GPIO Library Installation

The `Jetson.GPIO` library is required to work with GPIO pins on the reComputer Super. If you haven't installed it yet, you can do so by following the instructions in [3.27 Installing the GPIO Library](../3.27-Installing-the-GPIO-Library/README.md).

## Numbering Modes

The `Jetson.GPIO` library supports two common numbering schemes:

| Mode | Description | Typical Use |
| --- | --- | --- |
| `BOARD` | Numbers pins by their physical location on the 40-pin header | Best when you are wiring directly from the header silkscreen or a pinout diagram |
| `BCM` | Numbers pins by the GPIO mapping used by the library | Best when you are following Python GPIO examples that refer to logical GPIO IDs |

## GPIO Usage Examples

### Basic GPIO Output

```python
import Jetson.GPIO as GPIO
import time

# Set GPIO mode
GPIO.setmode(GPIO.BOARD)

# Define pin
output_pin = 12

# Set up the pin
GPIO.setup(output_pin, GPIO.OUT)

try:
    while True:
        # Turn on the pin
        GPIO.output(output_pin, GPIO.HIGH)
        time.sleep(1)
        # Turn off the pin
        GPIO.output(output_pin, GPIO.LOW)
        time.sleep(1)
except KeyboardInterrupt:
    # Clean up
    GPIO.cleanup()
```

### Basic GPIO Input

```python
import Jetson.GPIO as GPIO
import time

# Set GPIO mode
GPIO.setmode(GPIO.BOARD)

# Define pin
input_pin = 11

# Set up the pin
GPIO.setup(input_pin, GPIO.IN)

try:
    while True:
        # Read the pin value
        value = GPIO.input(input_pin)
        print(f"Pin value: {value}")
        time.sleep(0.5)
except KeyboardInterrupt:
    # Clean up
    GPIO.cleanup()
```

## Super-Specific GPIO Features

The reComputer Super's 40-pin header provides access to a range of GPIO pins, allowing for flexible integration with external devices. This makes it ideal for a variety of applications, including:

- Controlling LEDs and other indicators
- Reading button presses and sensor inputs
- Controlling motors and actuators
- Interfacing with other microcontrollers and devices

## Safety Precautions

- Always double-check pin connections before applying power
- Use appropriate resistors when connecting LEDs and other components
- Avoid short-circuiting GPIO pins
- Be mindful of the maximum current rating for GPIO pins

## Further Reading

- [Jetson.GPIO Library Documentation](https://github.com/NVIDIA/jetson-gpio)
- [reComputer Super Hardware and Interfaces Usage](https://wiki.seeedstudio.com/recomputer_jetson_super_hardware_interfaces_usage/)