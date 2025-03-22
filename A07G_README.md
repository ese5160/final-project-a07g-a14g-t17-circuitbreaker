# a07g-exploring-the-CLI

* Team Number:
* Team Name:
* Team Members:
* GitHub Repository URL:
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
![image](https://github.com/user-attachments/assets/a3c7b6cc-9c70-4740-b462-a9390f0c0fd3)
# 01.3 Software Architecture(State machine for Task)

