* [English Version](./How_To_Configure_Arduino-esp32.md)

# 目录

- [Arduino入门教程](#Arduino入门教程)
- [环境搭建](#环境搭建)
  - [下载和安装Arduino IDE](#下载和安装Arduino-IDE)
  - [安装esp32](#安装esp32)
- [运行第一个Arduino程序](#运行第一个Arduino程序)
  - [新建工程](#新建工程)
  - [编译和烧录程序](#编译和烧录程序)
  
# Arduino入门教程

本章介绍 Arduino 环境搭建，包括 Arduino IDE、ESP32板管理、相关库的安装，程序编译下载及示例程序测试，帮助用户掌握开发板，便于二次开发。

![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/image.png)

# 环境搭建
  ## 下载和安装 Arduino IDE
  * [`点击`](https://www.arduino.cc/en/software) 这去进行下载
      *  找到 `Downloads` 并根据自己的系统选择对应的版本
      ![image](https://github.com/user-attachments/assets/7b2e1bde-566a-45b8-a1b6-027e4b473356)
      *  点击 `Just Download` 
      ![image](https://github.com/user-attachments/assets/84290f8a-55b1-4d0a-8373-4375d6fe45aa)
      ![image](https://github.com/user-attachments/assets/34f7f218-c5db-4d8f-a195-5a8c65501d78)
      * 下载完成之后运行安装程序，全部默认安装即可。
      * 环境设置是在 Windows 10 系统下进行，Linux和Mac用户可访问[Arduino-esp32环境搭建](https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html)参考

## 安装esp32
* ESP32相关主板在Arduino IDE使用，须先安装“esp32 by Espressif Systems”开发板的软件包
* 根据板安装要求进行安装，一般推荐“在线安装”， 若在线安装失败，则使用“离线安装”
* 在线安装如下：
  * 打开Arduino IDE
      ![image](https://github.com/user-attachments/assets/cb15d47b-ee2b-4fd7-b1c1-14518b545d35)
  * 如果出现如下画面点击安装即可
      ![image](https://github.com/user-attachments/assets/c6a3cb21-55d3-4aa1-8c5e-4ba4845acb96)
  * 设置语言
      * 点击 `文件- > 首选项`
      ![image](https://github.com/user-attachments/assets/628614e3-5151-4f2e-91f8-394ddb67a3ce)
      ![image](https://github.com/user-attachments/assets/45ba4791-4ef4-40a9-b7d4-5c1223ed9c11)
  * 设置 `其他开发板管理器地址`: https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json 并保持
      ![image](https://github.com/user-attachments/assets/14b6cdcd-3487-48f9-bb0d-5d0184e18ab1)

      * `注意`:
          * 您可以在不设置附加板管理器 URL 的情况下下载 esp32，但提供的版本不完整，需要精确控制版本时不太方便
          
  * 安装开发板
    
    ①. 在侧边栏选择“BOARDS MANAGER”（板管理）；
    
    ②. 在搜索框中输入要安装的板名称“ESP32”；
    
    ③. 在方框处选择 版本号；
    
    ④. 点击“INSTALL”（安装）。
    
    ![image](https://github.com/user-attachments/assets/a1d597df-0410-439c-aa5e-089a0c3bdef7)
 
  * 等待下载
    
    ![image](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/wait-06.png)
    
  * Arduino-esp32下载完成
    
     ![image](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/finish-07.png)
    
     * 如果下载失败，重置其他开发板管理器地址:
          *   https://espressif.github.io/arduino-esp32/package_esp32_index.json
          *   https://espressif.github.io/arduino-esp32/package_esp32_dev_index.json
      * 若还是失败请选择离线安装   
 
* 离线安装
  * 点击我们提供的百度网盘内的 ESP32 多个版本离线包，可根据板安装要求选择一个符合要求的版本进行下载，其余版本可按需自行下载。
  * 将提供的开发板压缩包解压缩
 
    ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/download-path.jpg)

    C:\Users\{用户名}\AppData\Local\Arduino15\packages\
    
  * 将解压文件放在对应用户的arduino器件包目录
    
    C:\Users\VIEWE\AppData\Local\Arduino15\packages\
    
  * 以用户名为VIEWE为例
  * 关闭全部arduino窗口，确保arduino关闭
  * 重新打开arduino，并打开板管理器,看到esp32-arduino已经安装即可
  若此路径下已有esp32的文件夹，建议将其另存并删除此路径下的原esp32文件夹，以便正常使用离线包新生成的esp32文件夹

# 运行第一个 Arduino 程序

  如果你刚入门学习ESP32和Arduino，还不知道如何创建、编译、烧录和运行Arduino ESP32程序，那么请从这里开始看看，希望可以帮助到你！

## 新建工程
* 运行Arduino IDE，选择 File -> New Sketch

  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/A-study-01.png)
  
* 输入代码：
```c
void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
}

void loop() {
  // put your main code here, to run repeatedly:
  Serial.println("Hello, World!");
  delay(2000);
}
```
* 保存代码工程，选择 `File -> Save As...`；在弹出的菜单选择保存工程路径，并输入工程名，如 **Hello_World**，点击`保存`
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-02.png)

## 编译和烧录程序
* 选择对应的开发板，以ESP32S3主板为例：
  
  ①. 点击选择下拉框选项“Select Other Board and Port”；
  
  ②. 搜索需要的开发板型号“esp32s3 dev module”并选择；
  
  ③. 选择COM口；
  
  ④. 保存选择。

  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-03.png)

* 若ESP32S3主板只有USB口，须打开（Enable）USB CDC，如下图所示
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-04.png)

* 编译并上传程序：
  ①. 编译程序；②. 编译并下载程序；③. 下载成功。
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-05.png)

* 打开串口监视窗口，程序每隔2秒会打印“Hello World!”，运行情况如下所示：
  ![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/Ar-study-06.png)

至此你的Arduino入门之旅已经完成，可以开始你的下一步旅程,根据你的产品进入示例使用学习，也可直接看通用教程[VIEWE开发板在Arduino IDE使用说明](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/Arduino%20Tutorial/VIEWE%E5%BC%80%E5%8F%91%E6%9D%BF%E5%9C%A8Arduino%20IDE%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E.md)
