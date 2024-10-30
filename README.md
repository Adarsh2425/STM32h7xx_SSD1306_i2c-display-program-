# STM32H723ZG I2C Display Program

This repository contains a program developed in **STM32CubeIDE v1.16.1** for interfacing an OLED display with an **STM32H723ZG** microcontroller using the I2C communication protocol. This example demonstrates initializing the I2C interface, configuring the display, and showing basic text or graphics.

## Features

- **I2C Communication**: Interface with the display using the I2C protocol.
- **Display Control**: Initialize, write, and update the OLED display.
- **STM32Cube HAL Usage**: Uses STM32Cube's Hardware Abstraction Layer (HAL) for I2C management.
- **SSD1306 Support**: Supports the popular SSD1306 OLED driver with easy-to-modify code for other I2C displays.

## Requirements


- **STM32H723ZG Nucleo Board** (or similar STM32H7 board)
- **STM32CubeIDE v1.16.1** (or compatible version)
- **OLED Display** with an SSD1306 or compatible driver using I2C interface

## Project Structure

- `main.c`: Core program that includes I2C initialization, OLED configuration, and display updates.
- `i2c.c`: Handles I2C setup and configurations using STM32Cube HAL functions.
- `ssd1306.c` and `ssd1306.h`: SSD1306 driver code, providing functions to send data to the display.

## Getting Started

### Hardware Setup

1. Connect the **OLED Display** to the STM32H723ZG board using the I2C pins:
   - **SCL** (Serial Clock): Connect to I2C1_SCL (typically `PB8`).
   - **SDA** (Serial Data): Connect to I2C1_SDA (typically `PB9`).
2. Make sure the display power is correctly connected to a 3.3V or 5V supply depending on your display specifications.

### Connection Diagram

Add a connection diagram to help with the setup. Place the image in the `images` folder and name it `connection_diagram.png` for it to display correctly.

![STM32H723ZG I2C Display Connection](img/WhatsApp%20Image%202024-10-27%20at%2017.11.49_dd6320ea.jpg)

ie D14 SDA PB9
D15 SCL PB8
and +5 v and gnd 


### Software Setup

1. Open the project in **STM32CubeIDE v1.16.1**.
2. Go to **Project > Build Project** to compile.
3. Flash the program onto your STM32 board.

### Usage

Upon powering up the STM32 board with the display connected, the program initializes the display, configures it via I2C, and shows a welcome message or basic graphics. You can modify `main.c` to display custom messages or graphics as needed.

## Code Overview

### I2C Initialization

The I2C interface is initialized in `i2c.c` using STM32Cube’s HAL libraries. The configuration settings (e.g., clock speed) are chosen to work with the SSD1306 display.

### Display Initialization

In `ssd1306.c`, the OLED display is initialized by sending the required setup commands (contrast, orientation, etc.). The SSD1306 library provides functions to write text, draw shapes, and control individual pixels.

### Display Update

To refresh the display, the program periodically sends data to the SSD1306 to update its content. This can be modified to show dynamic information such as sensor readings, system states, etc.

## Debug Process

To ensure correct I2C communication and display initialization, follow these steps:

1. **Monitor I2C Signals**: Use an oscilloscope or logic analyzer to check the I2C SCL and SDA signals on pins PB6 and PB7. This helps ensure that the STM32 board is correctly sending data to the display.
   
2. **STM32CubeIDE Debug Mode**:
   - Connect the STM32 board to your PC and open STM32CubeIDE.
   - Set breakpoints in `main.c` (e.g., after `HAL_I2C_Init()` and in display update functions) to monitor the program flow.
   - Start the debug session (**Run > Debug**) and step through the code. This allows you to inspect variables and verify successful I2C transactions.

3. **Error Handling**:
   - Check for `HAL_I2C_Error()` in case of communication issues. It returns specific codes for common errors, such as bus faults or address mismatches.
   - Ensure the display address in `ssd1306.h` matches your OLED display’s I2C address. Adjust if needed.

4. **Console Output**:
   - Use `printf()` for debugging if a UART connection is available. You can log I2C status and initialization steps, which can be helpful for tracking down issues.

## Customization

- **Text and Graphics**: Use the SSD1306 driver functions in `ssd1306.c` to add custom text or shapes.
- **Clock Speed Adjustment**: Modify the I2C clock speed in `i2c.c` if using a different display or experiencing communication issues.
- **Alternate Displays**: The code can be adapted for other I2C displays with minor modifications to the driver code.

## Troubleshooting

- **Display Not Responding**: Verify I2C connections and check the display’s address in `ssd1306.h`.
- **I2C Errors**: Ensure correct pin mapping in `i2c.c` and check that no other I2C devices are conflicting on the same bus.

## License

This project is licensed under the MIT License. See `LICENSE` file for more details.
