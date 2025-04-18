# a07g-exploring-the-CLI

* Team Number: 17
* Team Name:Circuit Breaker
* Team Members:Shuowen Gu & Yuetian Zhao
* GitHub Repository URL:https://github.com/ese5160/final-project-a07g-a14g-t17-circuitbreaker
* Description of test hardware: (development boards, sensors, actuators, laptop + OS, etc)
# 01.1 Software Architecture(HRS & SRS)
## HRS
* IIC for MCU & ICM-42670-P communication
* UART for MCU & Fingerprint sensor communication
* button pressed for at least 5 seconds, no more than 10 seconds to get the IMU data
* LED 1 indicate fingerprint & button, LED 2 indicate IMU & CNN, LED 3 indicate WIFI, LED 4 indicate any failure
* Motor needs 1000Hz frequency to vibrate
## SRS
* IIC Speed for ICM-42670-P is 100 kHz
* UART Speed for fingerprint sensor is 9600 bps
* CNN for IMU to detect motion
* data buffered in FIFO for ICM-42670-P
* FREERTOS as RTOS
# 01.2 Software Architecture(Task)
![image](https://github.com/user-attachments/assets/4875c40e-b36e-4253-8593-0263f86790ae)

# 01.3 Software Architecture(State machine for Task)
fingerprint task:
![image](https://github.com/user-attachments/assets/0c4a5d6b-93f7-4f2d-8fe5-876ee9fe2582)

IMU task:
![image](https://github.com/user-attachments/assets/5f39b43e-141e-4592-be7a-0d457f74d0b6)

CNN task:
![image](https://github.com/user-attachments/assets/a76cadbf-c52d-444f-a723-d7e20a85b275)

Wifi task:
![image](https://github.com/user-attachments/assets/3381d91e-1dd1-4846-b5d5-5b31303c159a)

Haptic feedback task:
![image](https://github.com/user-attachments/assets/8d19b5e0-c525-46f6-95a5-339dc48092f7)

# 2 Understanding the Starter Code
* InitializeSerialConsole() Initializes the UART and registers callbacks, “cbufRx” and “cbufTx” are circular buffers for RX and TX, they are FIFO.
* “cbufRx” and “cbufTx” are initialized use circular_buf_init(), which will define buffer address and the size, they are defined in circular_buffer.c/h
* they are stored in char rxCharacterBuffer[RX_BUFFER_SIZE], char txCharacterBuffer[TX_BUFFER_SIZE], the size is 512 bytes.
* UART character received and UART character are defined in configure_usart_callbacks().
* Character Received (RX): usart_read_callback(), Character Sent (TX): usart_write_callback() 
* RX Callback (usart_read_callback), triggered when a character is received, then stores the received character in cbufRx, starts listening for the next character, and signals a waiting task that data is available. TX Callback (usart_write_callback) do the same and 
fetches the character from cbufTx.
* ![image](https://github.com/user-attachments/assets/54db3c57-57a8-4e78-a77f-cc902d00899d)
* ![image](https://github.com/user-attachments/assets/eecdcfad-f557-47cd-b2f7-d08456e5a547)
* It initializes and starts multiple FreeRTOS tasks, only one thread created vCommandConsoleTask.

# 3 Debug Logger Module
Done


# 4 Wiretap the convo!
![image](https://github.com/user-attachments/assets/235812a3-2ba1-4d0c-9064-d293da0789d2)
![image](https://github.com/user-attachments/assets/1eecf5f9-efb1-440f-91c4-ebb2e226339c)

* The net is PB10
* The setting is Async Serial and rate 115200 bps, 8 bits per frame & 1 stop bit, i didn't use any mode, but i guess trigger mode for rising and falling edge are ok

![image](https://github.com/user-attachments/assets/307641bf-39b7-4de8-a7aa-6c4059e747be)
  I use d0 & d1 for logic analyzer


![image](https://github.com/user-attachments/assets/c8236a53-7ac3-45ab-a3ed-b0fcb39c62d0)

see capture_uart.sal in Repository 

# 5 Complete the CLI
Done

# 6 Add CLI commands
Done 

https://youtu.be/TU_1CTaxab8?si=vMdGJFi94x1qaABw


