/**
  @page SSL_Server SSL Server application
  
  @verbatim
  ******************** (C) COPYRIGHT 2016 STMicroelectronics *******************
  * @file    mbedTLS/SSL_Server/readme.txt 
  * @author  MCD Application Team
  * @version V1.2.0
  * @date    30-December-2016
  * @brief   Description of SSL Server application.
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

This application guides STM32Cube HAL API users to run an SSL Server application 
based on mbedTLS crypto library and LwIP TCP/IP stack.

This application starts SSL server on the board waiting for connections from clients.
The board joins the local network using either a DHCP server or a static IP address.
Once done a green led is toggling informing that the server is ready.

As soon as a request from a client is received, the application establishes the secured
connection then sends the response to the client. the response is a HTML page with the text similar to:

"
mbed TLS Test Server
Successful connection using: TLS-ECDHE-RSA-WITH-AES-256-CBC-SHA
"

it is possible to test this application via two scenarios:

Scenario 1:
===========
  - the client is a PC with a web browser.
  - the browser connects to the address https://BOARD_IP_ADDRESS:4433
  - the afementioned string is displayed on the browser.
  
Scenario 2:
  - the client is a second board (STM32F769I-Discovery), running the "SSL_Client" application.
  - the second board connects to this application.
  - the "webpage content" is displayed in text format on the LCD screen of the second board.
  

In both scenarios, the "SSL_Server" Application log is displayed on the LCD screen.
  

@note the Scenario 1 was tested using Google Chrome 52 and Internet Explorer 11, earlier versions of those
      browsers may not work.

@note the ssl_server is not using a valid certificate to authentify, thus the browsers show a warning about
it, ignore that warning to let the application continue.

@note In this application the Ethernet Link ISR need the System tick interrupt 
to configure the Ethernet MAC, so the Ethernet Link interrupt priority must be 
set lower (numerically greater) than the Systick interrupt priority to ensure 
that the System tick increments while executing the Ethernet Link ISR.

@note Care must be taken when using HAL_Delay(), this function provides accurate delay (in milliseconds)
      based on variable incremented in HAL time base ISR. This implies that if HAL_Delay() is called from
      a peripheral ISR process, then the HAL time base interrupt must have higher priority (numerically lower)
      than the peripheral interrupt. Otherwise the caller ISR process will be blocked.
      To change the HAL time base interrupt priority you have to use HAL_NVIC_SetPriority() function.
      
@note The application needs to ensure that the HAL time base is always set to 1 millisecond
      to have correct HAL operation.

@note The STM32F7xx devices can reach a maximum clock frequency of 216MHz but as this application uses SDRAM,
      the system clock is limited to 200MHz. Indeed proper functioning of the SDRAM is only guaranteed 
      at a maximum system clock frequency of 200MHz.

For more details about this application, refer to UM1723 "STM32Cube mbedTLS application".

@par Keywords

Security, Middleware, mbedTLS, SSL Server, Crypto, TCP/IP, LwIP, AES 128,
AES 192, AES 256, Triple DES, MD5, SHA-1, RNG

@Note  If the user code size exceeds the DTCM-RAM size or starts from internal cacheable memories (SRAM1 and SRAM2),
       it is recommended to configure the latters as Write Through.
       This is ensured by configuring the memory attributes at MPU level in order to ensure cache coherence on SRAM1 and SRAM2.
       Please, refer to Template project for a typical MPU configuration.

@Note  If external memory is shared between several processors, it is recommended to configure it as Write Back (bufferable), shareable and cacheable.
       The memory base address and size must be properly updated.
       The user needs to manage the cache coherence at application level.

For more details about the MPU configuration and use, please refer to AN4838 �Managing memory protection unit (MPU) in STM32 MCUs�

@par Directory contents

    - mbedTLS/SSL_Server/Inc/ethernetif.h                   header for ethernetif.c file
    - mbedTLS/SSL_Server/Inc/main.h                         Main program header file 
    - mbedTLS/SSL_Server/Inc/config.h                       mbedTLS library configuration options
    - mbedTLS/SSL_Server/Inc/FreeRTOSConfig.h               FreeRTOS configuration options
    - mbedTLS/SSL_Server/Inc/lwipopts.h                     LwIP stack configuration options
    - mbedTLS/SSL_Server/Inc/stm32f7xx_it.h                 Interrupt handlers header file 
    - mbedTLS/SSL_Server/Inc/stm32f7xx_hal_conf.h           Library Configuration file
    - mbedTLS/SSL_Server/Inc/ssl_server.h                   header for ssl_server.c
    - mbedTLS/SSL_Server/Src/main.c                         Main program
    - mbedTLS/SSL_Server/Src/ssl_server.c                   SSL Server main thread
    - mbedTLS/SSL_Server/Src/ethernetif.c                   Interfacing the LwIP stack to ETH driver
    - mbedTLS/SSL_Server/Src/stm32f7xx_hal_msp.c            HAL MSP module
    - mbedTLS/SSL_Server/Src/stm32f7xx_it.c                 Interrupt handlers
    - mbedTLS/SSL_Client/Src/stm32f7xx_hal_timebase_tim.c   HAL time base functions
    - mbedTLS/SSL_Server/Src/system_stm32f7xx.c             STM32 system clock configuration file
    - mbedTLS/SSL_Server/Src/net_sockets.c                  the TCP/IP socket API implemented over the LwIP stack.

@par Hardware and Software environment  

  - This application runs on STM32F769I-Discovery Devices.
  
  - This application has been tested with two scenarios.
     - Using a Host PC as a client.
     - using two STM32F769I-Discovery boards the first as server, the second as client.

 - Screnario 1:
      - Remote PC Set-up
	  - Make sure that the PC is in the same local network as the baord.
	  - Web browser available on the PC.
	  
  - Screnario 2:
      - a second STM32F769I-Discovery running the "mdedTLS/SSL_Server" application
  
  - STM32F769I-Discovery Set-up 
    - Connect STM32F769I-Discovery to your local network (through a straight ethernet cable).
   
@par How to use it ? 

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the application
 - Use Scenario 1 or Scenario 2 described above.
  
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */