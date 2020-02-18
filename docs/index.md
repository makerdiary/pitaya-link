# Pitaya-Link <br/><small>An Open-Source CMSIS-DAP Debug Probe based on DAPLink</small>

## Description

[**Pitaya-Link**](https://store.makerdiary.com/products/pitaya-link) is a low-cost debug probe based on the CMSIS-DAP (also known as [DAPLink](https://github.com/ARMmbed/DAPLink)) protocol standard. It can be used to program and debug the application software running on Arm Cortex Microcontrollers.

The design enables developers with Drag-And-Drop programming, Virtual COM Port, CMSIS-DAP compliant debug channel, and access to Arm Cortex Microcontrollers in the browser using [WebUSB](https://wicg.github.io/webusb/).

The probe comes with indicator LEDs, a button to reset the target or trigger the firmware update, reversible USB-C connector and easy-to-use 7-pin 2.54mm Header.

![](assets/images/pitaya-link-prod.jpg)

## Features

* NXP Semiconductors [LPC11U35FHI33](https://www.nxp.com/part/LPC11U35FHI33#/) microcontroller
	- 50 MHz Arm® Cortex-M0 processor
	- 64kB flash & 12kB SRAM
	- ROM-based USB drivers. Flash updates via USB supported.
* Shipped with [Arm Mbed DAPLink](https://github.com/ARMmbed/DAPLink) Firmware
	- MSC - drag-n-drop programming flash memory
	- CDC - virtual com port for log, trace and terminal emulation
	- HID - CMSIS-DAP compliant debug channel
	- WEBUSB HID - CMSIS-DAP compliant debug channel
* Supported by various IDEs and applications: [pyOCD](pyocd.md), [DAP.js](dapjs.md), [VS Code](vscode.md), [KEIL](keil-mdk.md), [IAR](iar-ewarm.md) etc.
* RGB LED indicator & Button
* 3.3V DC-DC regulator with 1A output current
* 3.3V Digital I/O Operating Voltage
* Reversible USB-C Connector
* Easy-to-use 7-pin 2.54mm Header with SWD & UART interface
* Very small form factor: 25 x 40 mm

## Hardware Diagram

[![](assets/images/pitaya-link_diagram_v1_0.png)](assets/images/pitaya-link_diagram_v1_0.png)

## Included in the Box

|    **Part**               | **Qty** |
| ------------------------- | ------- |
| Pitaya-Link Board         | 1       |
| 7-pin Female/Male Cable   | 1       |
| 7-pin Female/Female Cable | 1       |
| USB-C Cable               | 1       |

## Tutorials
In order to help you use Pitaya-Link in your development environment, we have provided a series of tutorials. Find the details below:

* [Getting Started with Pitaya-Link](getting-started.md)
* [Using Pitaya-Link with pyOCD](pyocd.md)
* [Using Pitaya-Link with DAP.js](dapjs.md)
* [Using Pitaya-Link with Visual Studio Code](vscode.md)
* [Using Pitaya-Link with GNU MCU Eclipse](eclipse.md)
* [Using Pitaya-Link with ARM KEIL MDK](keil-mdk.md)
* [Using Pitaya-Link with IAR Embedded Workbench](iar-ewarm.md)
* [Upgrading the DAPLink Firmware](upgrading.md)
* [Building your own DAPLink Firmware](building.md)


## Design Files

* [Pitaya-Link Hardware Diagram V1.0](hw/pitaya-link_diagram_v1_0.pdf)
* [Pitaya-Link Schematic V1.0](hw/pitaya-link_schematic_v1_0.pdf)
* [Pitaya-Link Board File V1.0](hw/pitaya-link_board_file_v1_0.pdf)
* [Pitaya-Link 3D STEP V1.0](hw/pitaya-link_3d_v1_0.step)

## Create an Issue

Interested in contributing to this project? Want to report a bug? Feel free to click here:

<a href="https://github.com/makerdiary/pitaya-link/issues/new"><button data-md-color-primary="red-bud"><i class="fa fa-github"></i> Create an Issue</button></a>
