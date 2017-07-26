/**
  @page Demo   STM327x6G-EVAL Demonstration Firmware
 
  @verbatim
  ******************************************************************************
  * @file    Demonstrations/readme.txt 
  * @author  MCD Application Team
  * @version V1.3.0
  * @date    23-September-2016
  * @brief   Description of STM327x6G-EVAL Demonstration
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

@par Demo Description

The STM32Cube Demonstration platform comes on top of the STM32CubeTM as a firmware
package that offers a full set of software components based on a modules architecture
allowing re-using them separately in standalone applications. All these modules are
managed by the STM32Cube Demonstration kernel allowing to dynamically adding new
modules and access to common resources (storage, graphical components and widgets,
memory management, Real-Time operating system)

The STM32Cube Demonstration platform is built around the powerful graphical library
STemWin and the FreeRTOS real time operating system and uses almost the whole STM32
capability to offer a large scope of usage based on the STM32Cube HAL BSP and several
middleware components.

@par Demonstration Overview

The STM32 F7 demonstration is running on STM32756G/STM32746 evaluation boards 
  
Below you find an overview of the different offered module in the demonstration:
 
  + Video
 -------
 The video player module provides a video solution based on the STM32F7xx. 
 It supports playing movie in AVI format.
 You can use the *.avi video files provided under "Utilities/Media/Video".
 
 + Audio
 -------
 The audio player module provides a complete audio solution based on the STM32F7xx and
 delivers a high-quality music experience. It supports playing music in WAV format but may
 be extended to support other compressed formats such as MP3 and WMA audio formats.
 You can use the *.wav audio provided under "Utilities/Media/Audio" or any other ones.
  
 + Home alarm
 ------------ 
 Control of Home alarm system, equipped with cameras.
 Static picture shown when a room is selected and then the camera icon pressed
 General room alarm activation/deactivation when pressed.
 
 + Gardening control
 -------------------
 The gardening control module provides a graphic garden watering system behaviour
 
 + Game
 ------
 The game coming in the STM32Cube demonstration is based on the Reversi game. It is a
 strategy board game for two players, played on an 8�8 board. The goal of the game is to
 have the majority of disks turned to display your colour when the last playable empty square
 is filled.
 
 + System Info
 --------------  
 The system info module provides information about the core, supported eval boards, 
 CPU speed and demonstration version.  

 For more details about the demonstration modules please refers to  STM32CubeF7 demonstration (UM1906)
    
@note The STM32F7xx devices can reach a maximum clock frequency of 216MHz but as this demonstration uses SDRAM,
      the system clock is limited to 200MHz. Indeed proper functioning of the SDRAM is only guaranteed 
      at a maximum system clock frequency of 200MHz.
      
@par Keywords

Demonstration, FreeRTOS, RTOS, Middleware, Audio record, wav, Video Player, avi, MP3, Audio player, Graphic,
Game, System, CPU, VNC, SAI, QSPI, USB, Microphone, 

@par Hardware and Software environment

  - This demonstration runs on STM32F756xx and STM32F746xx devices.    
  - This demonstration has been tested with STM327x6G-EVAL RevB evaluation board.
  - Jumpers configuration:
      - JP5:  <1-2> ==> PD6 is as FMC_NWAIT (For NOR write)
      - JP10: must be not fitted ==> NOR write protection is disabled
      - JP18: <1-2> ==> Data signal on digital microphone is connected to audio codec(used for audio player module)   
      - JP19: <1-2> ==> Clock signal on digital microphone is connected to audio codec(used for audio player module)	   	  
      - JP21: <1-2> ==> PA2 is connected to SAI2_SCKB(used for audio player module)   
      - JP22: <1-2> ==> PC1 is connected to SAI1_SDA(used for audio player module)   
  - Make sure to connect an external power supply to CN17 (PSU jumper must be fitted in JP13)

@par How to use it ? 

The NOR external flash loader is not integrated with supported toolchains, it�s only supported with STM32
ST-Link Utility V3.7.
To load the demonstration, use STM32 ST-Link Utility to program both internal Flash and external NOR memory.
To edit and debug the demonstration you need first to program the external NOR memory using STLink utility
and then use your preferred toolchain to update and debug the internal flash content.

In order to program the demonstration you must do the following:
1- Open STM32 ST-Link Utility V3.7, click on "External Loader" from the bar menu then check 
   "M29W128GL_STM32F756G-EVAL" box 
2- Connect the STM327x6G-EVAL board to PC with USB cable through CN21
3- Use "STM32CubeDemo_STM327x6G-EVAL_V1.3.0.hex" file provided under �Binary� with STM32 ST-Link Utility
   to program both internal Flash and external NOR memory
4- copy the audio and video files provided under "Utilities/Media/" in the USB key
5- Plug a USB micro A-Male to A-Female cable on CN8 connector
-> The internal Flash and the external NOR are now programmed and the demonstration is shown on the board.

In order to Edit and debug the program, you must do the following
- if not done, perform step 1, 2, 3, 4 and 5 described above,
- Open your preferred toolchain,
- Use the IDE to update and load the internal flash content, 
- Run the demonstration.

@Note  If the user code size exceeds the DTCM-RAM size or starts from internal cacheable memories (SRAM1 and SRAM2),
       it is recommended to configure the latters as Write Through.
       This is ensured by configuring the memory attributes at MPU level in order to ensure cache coherence on SRAM1 and SRAM2.
       Please, refer to Template project for a typical MPU configuration.

@Note  If external memory is shared between several processors, it is recommended to configure it as Write Back (bufferable), shareable and cacheable.
       The memory base address and size must be properly updated.
       The user needs to manage the cache coherence at application level.

For more details about the MPU configuration and use, please refer to AN4838 �Managing memory protection unit (MPU) in STM32 MCUs�

 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
 
