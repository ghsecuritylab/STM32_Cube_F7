/**
  @page MTP_Standalone USB Host Media Transfer Protocol (MTP) application
  
  @verbatim
  ******************** (C) COPYRIGHT 2016 STMicroelectronics *******************
  * @file    USB_Host/MTP_Standalone/readme.txt 
  * @author  MCD Application Team
  * @version V1.2.0
  * @date    30-December-2016
  * @brief   Description of the USB Host MTP application.
  ******************************************************************************
  *
  * Copyright (c) 2016 STMicroelectronics International N.V. All rights reserved.
  *
  * Redistribution and use in source and binary forms, with or without 
  * modification, are permitted, provided that the following conditions are met:
  *
  * 1. Redistribution of source code must retain the above copyright notice, 
  *    this list of conditions and the following disclaimer.
  * 2. Redistributions in binary form must reproduce the above copyright notice,
  *    this list of conditions and the following disclaimer in the documentation
  *    and/or other materials provided with the distribution.
  * 3. Neither the name of STMicroelectronics nor the names of other 
  *    contributors to this software may be used to endorse or promote products 
  *    derived from this software without specific written permission.
  * 4. This software, including modifications and/or derivative works of this 
  *    software, must execute solely and exclusively on microcontroller or
  *    microprocessor devices manufactured by or for STMicroelectronics.
  * 5. Redistribution and use of this software other than as permitted under 
  *    this license is void and will automatically terminate your rights under 
  *    this license. 
  *
  * THIS SOFTWARE IS PROVIDED BY STMICROELECTRONICS AND CONTRIBUTORS "AS IS" 
  * AND ANY EXPRESS, IMPLIED OR STATUTORY WARRANTIES, INCLUDING, BUT NOT 
  * LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A 
  * PARTICULAR PURPOSE AND NON-INFRINGEMENT OF THIRD PARTY INTELLECTUAL PROPERTY
  * RIGHTS ARE DISCLAIMED TO THE FULLEST EXTENT PERMITTED BY LAW. IN NO EVENT 
  * SHALL STMICROELECTRONICS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT,
  * INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
  * LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, 
  * OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF 
  * LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING 
  * NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE,
  * EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
  *
  ******************************************************************************
  @endverbatim

@par Application Description 
  
This application is a part of the USB Host Library package using STM32Cube firmware. It describes how to use
USB host application based on the Media Transfer Protocol (MTP) on the STM32F7x6 devices.

MTP is used to transfer data between computer/Host and devices connected to it. This protocol was 
developed for intelligent storage devices for downloading photographs from digital cameras music files
on digital audio players and media files on portable media players.

At the beginning of the main program the HAL_Init() function is called to reset all the peripherals,
initialize the Flash interface and the systick. The user is provided with the SystemClock_Config()
function to configure the system clock (SYSCLK) to run at 200 Mhz. The Full Speed (FS) USB module uses
internally a 48-MHz clock which is coming from a specific output of two PLLs: main PLL or PLL SAI.
In the High Speed (HS) mode the USB clock (60 MHz) is driven by the ULPI.
 
When the application is started, the connected device (Android devices: Smartphone, Tablet...) 
is detected in MTP mode and gets initialized.
The STM32 MCU behaves as a MTP Host, it enumerates the device and extracts VID, PID, manufacturer name,
Serial number and product name information and displays it on the LCD screen. 
Then the Host detects the number of storage devices and displays on the LCD screen. The user will have 
to copy the .wav files on the root of the default storage. Only the files present on this space are visible 
by the application.

A menu is displayed and the user can select any operation from the menu using the Joystick buttons:
 - "Explore audio file" operation searches for all MTP objects, here are .Wav files and displays them 
    on the LCD screen.
 - "Start audio Player" operation starts playing the song from selected storage device.
   This application uses the I2S interface to stream audio data from USB Host to the audio codec implemented 
   on the evaluation board. Then audio downstream is driven to headphone or speaker.
   The USBH_AUDIO_ChangeOutBuffer() API is called while playing songs and the bytes are stored in a 
   circular buffer. Sampling frequency, Channels number and File size (duration) are detected. 
   The audio.c file contains a set of APIs for Audio Out playback, for example when the WAV file is 
   playing, the USBH_AUDIO_SetVolume() API is called to change the volume settings. 
 - "Re-Enumerate" operation performs a new Enumeration of the device.

@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in SysTick ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the SysTick interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the SysTick interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note The application needs to ensure that the SysTick time base is always set to 1 millisecond
      to have correct HAL operation.

For more details about the STM32Cube USB Host library, please refer to UM1720  
"STM32Cube USB Host library".

@note The application is compliant with the MTP implementation for the Android 4.0.x/ 4.1.x/4.2.x and 4.3.x
      with USB debug mode disabled on the device.

@note The STM32F7xx devices can reach a maximum clock frequency of 216MHz but as this application uses SDRAM,
      the system clock is limited to 200MHz. Indeed proper functioning of the SDRAM is only guaranteed 
      at a maximum system clock frequency of 200MHz.

@par USB Library Configuration

To select the appropriate USB Core to work with, user must add the following macro defines within the
compiler preprocessor (already done in the preconfigured projects provided with this application):
      - "USE_USB_HS" when using USB High Speed (HS) Core
      - "USE_USB_FS" when using USB Full Speed (FS) Core 
      - "USE_USB_HS" and "USE_USB_HS_IN_FS" when using USB High Speed (HS) Core in FS mode

It is possible to fine tune needed USB Host features by modifying defines values in USBH configuration
file �usbh_conf.h� available under the project includes directory, in a way to fit the application
requirements, such as:
- Level of debug: USBH_DEBUG_LEVEL
                  0: No debug messages
                  1: Only User messages are shown
                  2: User and Error messages are shown
                  3: All messages and internal debug messages are shown
   By default debug messages are displayed on the debugger IO terminal; to redirect the Library
   messages on the LCD screen, lcd_log.c driver need to be added to the application sources.
   

@par Keywords

Connectivity, USB Host, MTP, Android, Full Speed, High Speed, LCD, Enumeration, Removable drive, Audio, Wav

@Note  If the user code size exceeds the DTCM-RAM size or starts from internal cacheable memories (SRAM1 and SRAM2),
       it is recommended to configure the latters as Write Through.
       This is ensured by configuring the memory attributes at MPU level in order to ensure cache coherence on SRAM1 and SRAM2.
       Please, refer to Template project for a typical MPU configuration.

@Note  If external memory is shared between several processors, it is recommended to configure it as Write Back (bufferable), shareable and cacheable.
       The memory base address and size must be properly updated.
       The user needs to manage the cache coherence at application level.

For more details about the MPU configuration and use, please refer to AN4838 �Managing memory protection unit (MPU) in STM32 MCUs�

@par Directory contents

  - USB_Host/MTP_Standalone/Src/main.c                  Main program
  - USB_Host/MTP_Standalone/Src/system_stm32f7xx.c      STM32F7xx system clock configuration file
  - USB_Host/MTP_Standalone/Src/stm32f7xx_it.c          Interrupt handlers
  - USB_Host/MTP_Standalone/Src/menu.c                  MTP State Machine
  - USB_Host/MTP_Standalone/Src/usbh_conf.c             General low level driver configuration
  - USB_Host/MTP_Standalone/Src/audio.c                 Audio Out (playback) interface API
  - USB_Host/MTP_Standalone/Src/mtp.c                   Explore the MTP storage objects
  - USB_Host/MTP_Standalone/Inc/main.h                  Main program header file
  - USB_Host/MTP_Standalone/Inc/stm32f7xx_it.h          Interrupt handlers header file
  - USB_Host/MTP_Standalone/Inc/lcd_log_conf.h          LCD log configuration file
  - USB_Host/MTP_Standalone/Inc/stm32f7xx_hal_conf.h    HAL configuration file
  - USB_Host/MTP_Standalone/Inc/usbh_conf.h             USB Host driver Configuration file


@par Hardware and Software environment

  - This application runs on STM32F756xx/STM32F746xx devices.
    
  - This application has been tested with STMicroelectronics STM327x6G-EVAL RevB
    evaluation boards and can be easily tailored to any other supported device 
    and development board.

  - STM327x6G-EVAL RevB Set-up
    - Plug the MTP device into the STM327x6G-EVAL board through 'USB micro A-Male 
      to A-Female' cable to the connector:
      - CN8 : to use USB High Speed (HS) 
      - CN13: to use USB Full Speed (FS)
      - CN14: to use USB HS-IN-FS.
              Note that some FS signals are shared with the HS ULPI bus, so some PCB rework is needed.
              For more details, refer to section "USB OTG2 HS & FS" in STM327x6G-EVAL Evaluation Board 
              User Manual.
        @note Make sure that :
         - jumper JP8 must be removed when using USB OTG FS
    - Use CN26 connector to connect the board to external headset
    - Please ensure that jumpers JP4 and JP5 are fitted in position 2-3 (I2S)
    - Load .wav audio file (audio_sample.wav) available under "/Utilities/Media/Audio" to the root of MTP device

@par How to use it ?

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - In the workspace toolbar select the project configuration:
   - STM327x6G-EVAL_USBH-HS: to configure the project for STM32F7x6 devices using USB OTG HS peripheral
   - STM327x6G-EVAL_USBH-FS: to configure the project for STM32F7x6 devices using USB OTG FS peripheral
   - STM327x6G-EVAL_USBH-HS-IN-FS: to configure the project for STM32F7x6 devices and use USB OTG HS 
                                   peripheral In FS (using embedded PHY).
 - Run the application
 
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */