/**
  @page MSC_Standalone USB Host Mass Storage (MSC) example
  
  @verbatim
  ******************** (C) COPYRIGHT 2016 STMicroelectronics *******************
  * @file    USB_Host/MSC_Standalone/readme.txt 
  * @author  MCD Application Team
  * @version V1.4.0
  * @date    29-April-2016
  * @brief   Description of the USB Host MSC example.
  ******************************************************************************
  * @attention
  *
  * <h2><center>&copy; Copyright � 2016 STMicroelectronics International N.V. 
  * All rights reserved.</center></h2>
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

@par Example Description

This application shows how to use the USB host application based on the Mass Storage Class (MSC). 

This is a typical example on how to use the STM32F105x/107x USB OTG Host peripheral to operate with an USB 
flash disk using the Bulk Only Transfer (BOT) and Small Computer System Interface (SCSI) transparent
commands combined with a file system FatFs (Middleware component).

At the beginning of the main program the HAL_Init() function is called to reset all the peripherals,
initialize the Flash interface and the systick. The user is provided with the SystemClock_Config()
function to configure the system clock (SYSCLK) to run at 72 MHz. The Full Speed (FS) USB module uses
internally a 48-MHz clock, which is generated from an integrated PLL.

When the application started, the connected USB flash disk device is detected in MSC mode and gets 
initialized. The STM32 MCU behaves as a MSC Host, it enumerates the device and extracts VID, PID, 
manufacturer name, Serial no and product name information and displays it on the LCD screen. 
This example is based on read/write file and explore the USB flash disk content trough a MSC routine.

A menu is displayed and the user can select any operation from the menu using the Joystick buttons:
 - "File Operations" operation writes a small text file (less to 1 KB) on the USB flash disk.
 - "Explorer Disk" operation explores the USB flash disk content and displays it on the LCD screen.
    User has to press the Key button to display the whole USB flash disk content (recursion level 2).
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


@par Directory contents

  - USB_Host/MSC_Standalone/Src/main.c                  Main program
  - USB_Host/MSC_Standalone/Src/system_stm32f1xx.c      STM32F1xx system clock configuration file
  - USB_Host/MSC_Standalone/Src/stm32f1xx_it.c          Interrupt handlers
  - USB_Host/MSC_Standalone/Src/menu.c                  MSC State Machine
  - USB_Host/MSC_Standalone/Src/usbh_conf.c             General low level driver configuration
  - USB_Host/MSC_Standalone/Src/explorer.c              Explore the USB flash disk content
  - USB_Host/MSC_Standalone/Src/file_operations.c       Write/read file on the disk
  - USB_Host/MSC_Standalone/Src/usbh_diskio.c           USB diskio interface for FatFs
  - USB_Host/MSC_Standalone/Inc/main.h                  Main program header file
  - USB_Host/MSC_Standalone/Inc/stm32f1xx_it.h          Interrupt handlers header file
  - USB_Host/MSC_Standalone/Inc/lcd_log_conf.h          LCD log configuration file
  - USB_Host/MSC_Standalone/Inc/stm32f1xx_hal_conf.h    HAL configuration file
  - USB_Host/MSC_Standalone/Inc/usbh_conf.h             USB Host driver Configuration file
  - USB_Host/MSC_Standalone/Inc/ffconf.h                FatFs Module Configuration file
 

@par Hardware and Software environment

  - This example runs on STM32F107xx/STM32F105xx devices.
    
  - This example has been tested with STMicroelectronics STM3210C-EVAL RevC 
    evaluation boards and can be easily tailored to any other supported device 
    and development board.

  - STM3210C-EVAL RevC Set-up
    - Plug the USB key into the STM3210C-EVAL board through 'USB micro A-Male 
      to A-Female' cable to the connector CN2

@par How to use it ?

In order to make the program work, you must do the following :
 - Open your preferred toolchain 
 - Rebuild all files and load your image into target memory
 - Run the example
 
 * <h3><center>&copy; COPYRIGHT STMicroelectronics</center></h3>
 */
