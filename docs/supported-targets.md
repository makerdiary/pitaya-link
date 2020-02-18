# Supported Targets

## Using pyOCD

Through both built-in support and CMSIS-Packs, pyOCD supports nearly every Cortex-M MCU that is available on the market.

To see the available target types you can run the following command:

``` sh
pyocd list --targets
```

![](assets/images/supported-target-type.png)


## Drag-and-drop programming targets

A flash algorithm blob is needed to program the target MCU while programming an image across the Drag-and-drop channel. This blob contains position independent functions for erasing, reading and writing to the flash controller. 

The following table shows the targets that support Drag-and-drop programming. More targets are planned and will show up gradually over time.

|    **Target**       | **Firmware** |
| ------------------- | ------------ |
| nRF52 SoC (Default) | [pitaya_link_nrf52_if_crc_xxxx.bin](https://github.com/makerdiary/pitaya-link/releases)|


## Create an Issue

Interested in contributing to this project? Want to report a bug? Feel free to click here:

<a href="https://github.com/makerdiary/pitaya-link/issues/new?title=Supported%20Target%20List:%20%3Ctitle%3E"><button data-md-color-primary="red-bud"><i class="fa fa-github"></i> Create an Issue</button></a>
