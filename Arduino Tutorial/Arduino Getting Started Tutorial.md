* [中文版本](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/Arduino%20Tutorial/Arduino%20IDE%E5%AE%89%E8%A3%85%E5%8F%8A%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md)

# Table of Contents

- [Arduino Getting Started Tutorial](#arduino-getting-started-tutorial)
- [Setting Up the Environment](#setting-up-the-environment)
  - [Downloading and Installing Arduino IDE](#downloading-and-installing-arduino-ide)
  - [Installing ESP32](#installing-esp32)
- [Running Your First Arduino Program](#running-your-first-arduino-program)
  - [Creating a New Project](#creating-a-new-project)
  - [Compiling and Uploading the Program](#compiling-and-uploading-the-program)

# Arduino Getting Started Tutorial

This chapter introduces Arduino environment setup, including Arduino IDE installation, ESP32 board management, library installation, program compilation/download, and sample program testing to help users master the development board for secondary development.

![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/FlowChart_cn.png)

# Setting Up the Environment
## Downloading and Installing Arduino IDE
* [`Click here`](https://www.arduino.cc/en/software) to download
    * Find `Downloads` and select the version corresponding to your system
    ![image](https://github.com/user-attachments/assets/7b2e1bde-566a-45b8-a1b6-027e4b473356)
    * Click `Just Download`
    ![image](https://github.com/user-attachments/assets/84290f8a-55b1-4d0a-8373-4375d6fe45aa)
    ![image](https://github.com/user-attachments/assets/34f7f218-c5db-4d8f-a195-5a8c65501d78)
    * After downloading, run the installer and proceed with default settings
    * Environment setup is based on Windows 10. Linux and Mac users can refer to [Arduino-esp32 Environment Setup](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)

## Installing ESP32
* To use ESP32 boards in Arduino IDE, you must install the "esp32 by Espressif Systems" board package
* Recommended method: Online installation. Use offline installation if online fails
* Online Installation:
  * Open Arduino IDE
      ![image](https://github.com/user-attachments/assets/cb15d47b-ee2b-4fd7-b1c1-14518b545d35)
  * If this screen appears, click Install
      ![image](https://github.com/user-attachments/assets/c6a3cb21-55d3-4aa1-8c5e-4ba4845acb96)
  * Set language
      * Click `File -> Preferences`
      ![image](https://github.com/user-attachments/assets/628614e3-5151-4f2e-91f8-394ddb67a3ce)
      ![image](https://github.com/user-attachments/assets/45ba4791-4ef4-40a9-b7d4-5c1223ed9c11)
  * Set `Additional Boards Manager URLs`: 
    ```
    https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json
    ```
    ![image](https://github.com/user-attachments/assets/14b6cdcd-3487-48f9-bb0d-5d0184e18ab1)

    * `Note`: 
        * You can install without this URL, but version control will be limited
        
  * Install the board:
    
    ①. Select "BOARDS MANAGER" in sidebar
    
    ②. Search for "ESP32"
    
    ③. Select version
    
    ④. Click "INSTALL"
    
    ![image](https://github.com/user-attachments/assets/a1d597df-0410-439c-aa5e-089a0c3bdef7)
 
  * Wait for download
    
    ![image](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/wait-06.png)
    
  * Installation complete
    
     ![image](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/finish-07.png)
    
    * If download fails, try alternative URLs:
        * `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
        * `https://espressif.github.io/arduino-esp32/package_esp32_dev_index.json`
    * Proceed with offline installation if issues persist
 
* Offline Installation:
  * Download ESP32 offline package (provided via Baidu Netdisk)
  * Extract the compressed file to:
    
  ```
    C:\Users\{Username}\AppData\Local\Arduino15\packages\
  ```
  
    ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/download-path.jpg)


  * Example path (for user "VIEWE"):
    
  ```
    C:\Users\VIEWE\AppData\Local\Arduino15\packages\
  ```
  * Close all Arduino IDE windows
  * Reopen Arduino IDE and verify installation in Board Manager
  * If existing esp32 folder exists, back up and replace with new files

# Running Your First Arduino Program

## Creating a New Project
* Open Arduino IDE → `File → New Sketch`
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/A-study-01.png)
  
* Enter code:
  
```c
void setup() {
  // Initialize serial communication
  Serial.begin(115200);
}

void loop() {
  // Print message every 2 seconds
  Serial.println("Hello, World!");
  delay(2000);
}

```

* Save project: File → Save As... → Enter project name (e.g., Hello_World) → Click Save
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-02.png)

## Compiling and Uploading the Program

* Select development board (ESP32S3 example):

  ①. Click "Select Other Board and Port"
  
  ②. Search and select "esp32s3 dev module"
  
  ③. Select COM port
  
  ④. Confirm selection

  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-03.png)

* For USB-only ESP32S3 boards: Enable USB CDC
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-04.png)

* Upload program:
  ①. Verify (compile); ②. Upload; ③. Upload successful
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-05.png)

* Open Serial Monitor to see "Hello, World!" printed every 2 seconds:
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-06.png)

Your Arduino journey has begun! Proceed to product-specific examples or explore the general tutorial:
[VIEWE Development Board for Arduino IDE](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/Arduino%20Tutorial/VIEWE%20development%20board%20for%20Arduino%20IDE.md)
