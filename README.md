# Team 2 3D Printer - Firmware Repository

This repository contains the customized Marlin 2.1.x firmware for our MDPS374 Mechatronics design project. 

## Hardware
* **Motherboard:** BIGTREETECH SKR 1.4 Turbo (LPC1769 processor)
* **Stepper Drivers:** 5x TMC2209 running in UART mode
* **Display:** BIGTREETECH TFT24 
* **Power Supply:** 12V 29A (350W)

---

## Software Prerequisites

To compile and upload this firmware, you will need the following tools installed on your computer.

### 1. Visual Studio Code (VS Code)
This is the primary code editor used for Marlin development.
* Download and install from [code.visualstudio.com](https://code.visualstudio.com/).

### 2. PlatformIO IDE
PlatformIO is the compiler that turns our C++ code into the `.bin` file that the motherboard understands.
* Open VS Code.
* Go to the **Extensions** tab on the left sidebar (the 4 square blocks icon).
* Search for **PlatformIO IDE** and click Install. (Restart VS Code if prompted).

### 3. Auto Build Marlin
This is an official extension that makes compiling Marlin foolproof by automatically detecting our motherboard and selecting the correct processor environments.
* In the VS Code Extensions tab, search for **Auto Build Marlin** and click Install.

### 4. Pronterface (Printrun)
This is the software used to send G-code commands to the printer via USB for testing and calibration of our axes, heating, etc.
* Download the latest release from [pronterface.com](https://www.pronterface.com/).
* Extract the folder and run `pronterface.exe` (No setup required).

---

## How to Build the Firmware

1. **Clone the Repository:** Clone this GitHub repository to your local machine using Git, or download it as a ZIP and extract it.
2. **Open in VS Code:**
   Open VS Code, go to `File > Open Folder`, and select the root folder of this project (the folder containing `platformio.ini`).

From here, you have two options to compile the firmware:

### Option A: Using Auto Build Marlin
3. **Open Auto Build Marlin:** Click the **Auto Build Marlin** icon on the left sidebar (it looks like a small 'M'). 
4. **Compile:** Click the **Show ABM Panel** button. It will automatically read our `Configuration.h` file and detect the SKR 1.4 Turbo. 
   * Locate the **LPC1769** environment.
   * Click the **Build** button.

### Option B: Using Standard PlatformIO
3. **Press the ✓ icon:** Click the **✓** icon in your bottom toolbar, hovering over it should say **Platform IO: Build**. This will immediately build your `firmware.bin`.

### Locating the Output (Both Options)
Once the terminal finishes running and shows a green `SUCCESS` message, the newly compiled file will be generated. You can find it inside your project folder at this exact path:
`\.pio\build\LPC1769\firmware.bin`

---

## How to Flash the SKR 1.4 Turbo

The SKR 1.4 Turbo does not flash via the USB cable. It must be flashed using an SD card.

1. **Prepare the SD Card:** Ensure you have a microSD card (32GB or smaller) formatted to **FAT32**.
2. **Transfer the File:** Copy the `firmware.bin` file generated in the previous step onto the root directory of the SD card.
3. **Flash:**
   * Ensure the printer's main 12V power supply is **OFF**.
   * Insert the SD card into the motherboard's slot.
   * Turn the power supply **ON** (or plug in the USB cable).
       *   In the case of powering it through the USB cable, make sure to use the VUSB jumper.
   * A green status LED on the board will light up confirming it is reading the SD card.
4. **Verify:** Once it is done, the computer will automatically reread the SD card. If you see `firmware.bin` changed to `FIRMWARE.CUR` then it was a successfull flash. 

---

## Initial Testing with Pronterface

Before mounting the motors to the chassis, you can run a desk test using Pronterface to ensure the TMC2209 drivers are communicating.

1. Ensure the 12V power supply is turned **ON** (motors will not move on 5V USB power).
2. Connect the SKR 1.4 Turbo to your laptop via a data-capable USB cable.
3. Open **Pronterface**.
4. Select the correct COM port from the top-left dropdown.
5. Set the Baud Rate to **250000** and click **Connect**.

If the motor spins smoothly, the firmware logic and UART communication are functioning correctly.
