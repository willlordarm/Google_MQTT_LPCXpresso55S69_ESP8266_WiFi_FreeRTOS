Google MQTT Demo
================

This demo application connects to 
[Google Cloud IoT](https://cloud.google.com/solutions/iot/) 
through MQTT and publishes messages.

It requires a registered [device](https://www2.keil.com/iot/google) in the Google Cloud IoT.

The following describes the various components and the configuration settings.

Once the application is configured you can:
 - Build the application
 - Connect the debugger
 - Run the application and view messages in a debug printf or terminal window


Google IoT Client
-----------------
The file `demo.c` configures the connection to Google IoT with these settings:
 - PROJECT_ID:   Project ID
 - CLOUD_REGION: Cloud region
 - REGISTRY_ID:  Registry ID
 - DEVICE_ID:    Device ID

Note: These settings need to be configured by the user!

The file `pkey.h` configures the device private key.

Note: The device private key needs to be provided by the user!


FreeRTOS Real-Time Operating System
-----------------------------------
The [FreeRTOS RTOS](https://github.com/ARM-software/CMSIS-FreeRTOS) 
implements the resource management. It is configured with the following settings:

- Global Dynamic Memory size: 24000 bytes
- Default Thread Stack size: 3072 bytes


WiFi IoT Socket
---------------
This implementation uses an IoT socket layer that connects to a 
[CMSIS-Driver WiFi](https://arm-software.github.io/CMSIS_5/Driver/html/index.html).

The file `socket_startup.c` configures the WiFi connection with these settings:
 - SSID:          network identifier
 - PASSWORD:      network password
 - SECURITY_TYPE: network security

Note: These settings need to be configured by the user!


ESP8266 WiFi Module
-------------------
The [ESP8266 WiFi Module](https://www2.keil.com/iot/shields/wrl13287) 
is connected via an Arduino connector using a USART interface.
It exposes a **CMSIS-Driver WiFi**.


NXP LPCXpresso55S69 Target Board
--------------------------------
The Board layer contains the following configured interface drivers:

**CMSIS-Driver USART2** routed to Arduino UNO R3 connector (P18):
 - RX:         D0  (PLU_OUT6/GPIO/FC2_USART_RXD_ARD)
 - TX:         D1  (FC2_USART_TXD_ARD)

**CMSIS-Driver SPI8** routed to Arduino UNO R3 connector (P17):
 - SCK:        D13 (LSPI_HS_SCK)
 - MISO:       D12 (LSPI_HS_MISO)
 - MOSI:       D11 (LSPI_HS_MOSI)

**GPIO** pins routed to Arduino UNO R3 connector (P17):
 - output:     D10 (LSPI_HS_SSEL1)
 - input:      D9  (PIO1_5_GPIO_ARD)

**CMSIS-Driver VIO** with the following board hardware mapping:
 - vioBUTTON0: Button USER (PIO1_9)
 - vioLED0:    LED RED     (PIO1_6)
 - vioLED1:    LED GREEN   (PIO1_7)
 - vioLED2:    LED BLUE    (PIO1_4)

**STDIO** routed to Virtual COM port (DAP-Link, baudrate = 115200)

The board configuration can be modified using 
[MCUxpresso](https://www.keil.com/nxp) 
and is stored in the file `LPCXpresso55S69.mex`.
