## 快速入门

### 环境准备

1. **安装 Arduino IDE**
- 导航到[Arduino入门教程](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/Arduino%20Tutorial/Arduino%20IDE%E5%AE%89%E8%A3%85%E5%8F%8A%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md)

2. **安装 ESP32 SDK**

- 打开 Arduino IDE
- 导航到 `File` > `Preferences`
- 在 `Additional boards manager URLs` 中添加:

  ```
  https://espressif.github.io/arduino-esp32/package_esp32_index.json
  ```

- 导航到 `Boards Manager`
- 搜索 `esp32` by `Espressif Systems` 并安装, 版本需>=3.1.0

3. **安装必需的库**

- 导航到 `Manage Libraries`
- 搜索安装 `ESP32_Display_Panel`库及其所有依赖库，安装版本 `>=1.0.3`
- 搜索安装 `LVGL`库（可选），推荐安装版本 `8.4.0`（目前暂时为适配`lvgl v9`版本，保持在 `lvgl v8` 请不要跨越大版本）

注意：lvgl并不是并不是必须库，只要在使用 `gui` 示例时使用，详细说明请参考[示例说明](#示例说明)

### 运行第一个示例 
**第一个示例显示彩条和打印触摸坐标来验证配置若使用ui界面示例请参考[示例进阶](#示例进阶)**

1. **选择和配置开发板**

- 导航到 `Tools` > `Board` > `esp32` > `ESP32S3 Dev Module`

2. **打开示例**

- 导航到 `File` > `Examples` > `ESP32_Display_Panel`
- 选择 `Arduino` > `board` > [`board_static_config`](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/board/board_static_config)

3. **修改代码**

由于 Arduino IDE 无法像 ESP-IDF 通过 menuconfig 或 PlatformIO 通过编译选项来调整配置，本库提供了通过修改特定配置文件的方式进行配置。主要包括以下4个配置文件：

- `esp_panel_drivers_conf.h`:
- `esp_panel_board_supported_conf.h`:
- `esp_panel_board_custom_conf.h`:
- `esp_utils_conf.h` :
  
如果使用 `gui`的示例还会包括以下两个配置文件：
- `lvgl_v8_port.h` :
- `lv_conf.h` :

加载支持的开发板
  1. 设置配置文件中的 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 宏定义为 `1`。
  2. 根据目标开发板的型号，取消对应的宏定义的注释。
  3. 此时，调用 `esp_panel::board::Board` 默认构造函数时会加载目标开发板的配置。
  6. 以使用 `UEDX48480040E-WB-A` 开发板为例，下面是修改后的 *esp_panel_board_supported_conf.h* 文件的部分内容：
  
      ```c
      ...
      /**
      * @brief Flag to enable supported board configuration (0/1)
      *
      * Set to `1` to enable supported board configuration, `0` to disable
      */
      #define ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED       (1)
      ...
      // #define BOARD_VIEWE_SMARTRING
      // #define BOARD_VIEWE_UEDX24240013_MD50E
      // #define BOARD_VIEWE_UEDX24320024E_WB_A
      // #define BOARD_VIEWE_UEDX24320028E_WB_A
      // #define BOARD_VIEWE_UEDX24320035E_WB_A
      // #define BOARD_VIEWE_UEDX32480035E_WB_A
      // #define BOARD_VIEWE_UEDX46460015_MD50ET
      // #define BOARD_VIEWE_UEDX48270043E_WB_A
      // #define BOARD_VIEWE_UEDX48480021_MD80E_V2
      // #define BOARD_VIEWE_UEDX48480021_MD80E
      // #define BOARD_VIEWE_UEDX48480021_MD80ET
      // #define BOARD_VIEWE_UEDX48480028_MD80ET
      #define BOARD_VIEWE_UEDX48480040E_WB_A
      // #define BOARD_VIEWE_UEDX80480043E_WB_A
      // #define BOARD_VIEWE_UEDX80480050E_AC_A
      // #define BOARD_VIEWE_UEDX80480050E_WB_A
      // #define BOARD_VIEWE_UEDX80480050E_WB_A_2
      // #define BOARD_VIEWE_UEDX80480070E_WB_A
      ...
      ```

> [!WARNING]
> * 同一目录下可以同时包含 *esp_panel_board_supported_conf.h* 和 *esp_panel_board_custom_conf.h* 两个配置文件，但不能同时启用它们。即 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 和 `ESP_PANEL_BOARD_DEFAULT_USE_CUSTOM` 不能同时设为 `1`，否则会导致编译错误。
> * 由于配置文件的内容可能会随版本更新而变化（如新增、删除或重命名配置项），为确保兼容性，本库对配置文件进行了独立的版本管理，并在编译时检查您当前使用的配置文件版本是否与库兼容。详细的版本信息及检查规则可在各配置文件末尾查看。

4. **编译上传**

- 连接开发板UART(Type-C类型)到电脑
- 导航到 `Tool` > `port` 选择正确的串口
- 点击上传按钮

上传成功后设备屏幕上将显示彩条和打印触摸坐标来验证配置。

## 示例进阶
- 尝试其他 [示例程序](#示例说明)
- 了解详细的 [配置说明](#配置说明)
- 学习如何 [移植 UI](#移植-squareline-工程)
- 查看 [常见问题及解答](#常见问题及解答)

**这里以一个简单的lvgl示例为例**

1. **选择和配置开发板**

- 导航到 `Tools` > `Board` > `esp32` > `ESP32S3 Dev Module`
- `Tools` 其他配置如下：

2. **打开示例**

- 导航到 `File` > `Examples` > `ESP32_Display_Panel`
- 选择 `Arduino` > `gui` > `lvgl_v8` > [`simple_port`](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/simple_port/)

3. **修改代码**

- `esp_panel_board_supported_conf.h`
- `lvgl_v8_port.h` 
- `lv_conf.h`
  1. 打开 `esp_panel_board_supported_conf.h`
  2. 设置配置文件中的 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 宏定义为 `1`。
  3. 根据目标开发板的型号，取消对应的宏定义的注释。
  4. 此时，调用 `esp_panel::board::Board` 默认构造函数时会加载目标开发板的配置。
     
以使用 `UEDX48480040E-WB-A` 开发板为例，开发板选择请参考[支持的viewe开发板](#支持的viewe开发板)
下面是修改后的 *esp_panel_board_supported_conf.h* 文件的部分内容：
  
    ```c
    ...
    /**
    * @brief Flag to enable supported board configuration (0/1)
    *
    * Set to `1` to enable supported board configuration, `0` to disable
    */
    #define ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED       (1)
    ...
    // #define BOARD_VIEWE_SMARTRING
    // #define BOARD_VIEWE_UEDX24240013_MD50E
    // #define BOARD_VIEWE_UEDX24320024E_WB_A
    // #define BOARD_VIEWE_UEDX24320028E_WB_A
    // #define BOARD_VIEWE_UEDX24320035E_WB_A
    // #define BOARD_VIEWE_UEDX32480035E_WB_A
    // #define BOARD_VIEWE_UEDX46460015_MD50ET
    // #define BOARD_VIEWE_UEDX48270043E_WB_A
    // #define BOARD_VIEWE_UEDX48480021_MD80E_V2
    // #define BOARD_VIEWE_UEDX48480021_MD80E
    // #define BOARD_VIEWE_UEDX48480021_MD80ET
    // #define BOARD_VIEWE_UEDX48480028_MD80ET
    #define BOARD_VIEWE_UEDX48480040E_WB_A
    // #define BOARD_VIEWE_UEDX80480043E_WB_A
    // #define BOARD_VIEWE_UEDX80480050E_AC_A
    // #define BOARD_VIEWE_UEDX80480050E_WB_A
    // #define BOARD_VIEWE_UEDX80480050E_WB_A_2
    // #define BOARD_VIEWE_UEDX80480070E_WB_A
    ...
    ```
4. **编译上传**

- 连接开发板UART(Type-C类型)到电脑
- 导航到 `Tool` > `port` 选择正确的串口
- 点击上传按钮

  
若你使用是VIEWE的SPI屏幕请编辑 `lv_conf.h` > `LV_COLOR_16_SWAP`的宏设置为 `1`,如下 :
```c
/**
 * @file lv_conf.h
 * Configuration file for v8.4.0
 */

/* clang-format off */
#if 1 /*Set it to "1" to enable content*/

#ifndef LV_CONF_H
#define LV_CONF_H

#include <stdint.h>

/*====================
   COLOR SETTINGS
 *====================*/

/*Color depth: 1 (1 byte per pixel), 8 (RGB332), 16 (RGB565), 32 (ARGB8888)*/
#define LV_COLOR_DEPTH 16

/*Swap the 2 bytes of RGB565 color. Useful if the display has an 8-bit interface (e.g. SPI)*/
#define LV_COLOR_16_SWAP 1
...
```

## 示例说明

您可以在 Arduino IDE 中通过 `File` > `Examples` > `ESP32_Display_Panel` 访问所有示例。

> [!WARNING]
> 如果未看到 `ESP32_Display_Panel` 选项，请检查：
> * ESP32_Display_Panel 库是否已正确安装
> * SDK 是否已正确安装
> * 是否已选择 ESP 开发板

### Drivers

以下示例演示了如何使用 `esp_panel::drivers::LCD` 驱动不同接口和不同型号的 LCD 控制器，并通过显示彩条进行测试：

* [SPI LCD](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/lcd/lcd_spi)
* [QSPI LCD](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/lcd/lcd_qspi/)
* [Single RGB LCD](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/lcd/lcd_single_rgb/)
* [3-wire SPI + RGB LCD](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/lcd/lcd_3wire_spi_rgb/)
* [MIPI-DSI LCD](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/lcd/lcd_mipi_dsi/)

以下示例演示了如何使用 `esp_panel::drivers::Touch` 驱动不同接口和不同型号的触摸控制器，并通过打印触摸点坐标进行测试：

* [I2C Touch](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/touch/touch_i2c/)
* [SPI Touch](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/drivers/touch/touch_spi/)

### Board

以下示例演示了如何使用 `esp_panel::board::Board` 一站式驱动内置开发板或自定义开发板的屏幕：

* [Board Dynamic Config](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/board/board_dynamic_config/)：此示例演示了如何通过代码动态加载开发板的显示屏设置，并通过显示彩条和打印触摸坐标来验证配置。
* [Board Static Config](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/board/board_static_config/)：此示例演示了如何通过 `esp_panel_board_supported_conf.h` 和 `esp_panel_board_custom_conf.h` 配置文件静态加载开发板的显示屏设置，并通过显示彩条和打印触摸坐标来验证配置。

### GUI

以下示例演示了如何使用 `LVGL v8` 版本来开发 GUI 界面：

* [Simple Port](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/simple_port/)：此示例演示了如何移植 `LVGL v8`。并且对于 `RGB/MIPI-DSI` 接口，它还可以启用避免撕裂和旋转功能。
* [Simple Rotation](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/simple_rotation/)：此示例演示了如何使用 `LVGL v8` 旋转显示屏。
* [SquareLine Port](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/squareline_port/)：此示例演示了如何移植 `SquareLine (v1.4.x)` 项目。并且对于 `RGB/MIPI-DSI` 接口，它还可以启用避免撕裂和旋转功能。
* [SquareLine Wi-Fi Clock](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/squareline_wifi_clock/)：此示例演示了通过 `SquareLine (v1.4.x)` 实现一个简单的 Wi-Fi 时钟，并且可以显示天气信息。

> [!NOTE]
> * 使用上述示例时，请确保已经安装了符合版本要求的 `LVGL` 库。
> * 关于如何配置 `LVGL`（v8.4.x），请参阅 [配置 LVGL](#配置-lvgl) 以获取更多详细信息。
> * 关于如何移植 `Squarelina`（v1.4.x）项目，请参阅 [移植 SquareLine 工程](#移植-SquareLine-工程) 获取更多详细信息。

> [!WARNING]
> 目前，`LVGL` 的防撕裂功能仅支持 `RGB/MIPI-DSI` LCD，并且需要其版本满足 `>= v8.3.9`，如果使用的是其他类型的 LCD 或不符合要求的 `LVGL` 版本，请不要启用此功能。

## 配置说明

由于 Arduino IDE 无法像 ESP-IDF 通过 menuconfig 或 PlatformIO 通过编译选项来调整配置，本库提供了通过修改特定配置文件的方式进行配置。主要包括以下三个配置文件：

- [esp_panel_drivers_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/esp_panel_drivers_conf.h)
- [esp_panel_board_supported_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/esp_panel_board_supported_conf.h)
- [esp_panel_board_custom_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/esp_panel_board_custom_conf.h)

以下是配置文件的使用特点：

1. ESP32_Display_Panel 查找配置文件的优先级顺序为：`当前工程目录` > `Arduino 库目录`。如果在当前工程目录中找到配置文件，将优先使用该配置；否则继续查找 Arduino 库目录中的配置文件。若未找到任何配置文件，则使用库中的默认配置。
2. 所有示例工程都默认包含了各自所需的配置文件，您可以直接修改其中的宏定义来更新配置。
3. 对于没有配置文件的自定义工程，您可以从 ESP32_Display_Panel 的根目录或示例工程中复制所需的配置文件。
4. 如果多个工程需要使用相同的配置，可以将配置文件放在 [Arduino 库目录](#arduino-库的目录在哪儿) 中，这样所有未包含配置文件的工程都可以共享这些配置。

> [!WARNING]
> * 同一目录下可以同时包含 *esp_panel_board_supported_conf.h* 和 *esp_panel_board_custom_conf.h* 两个配置文件，但不能同时启用它们。即 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 和 `ESP_PANEL_BOARD_DEFAULT_USE_CUSTOM` 不能同时设为 `1`，否则会导致编译错误。
> * 由于配置文件的内容可能会随版本更新而变化（如新增、删除或重命名配置项），为确保兼容性，本库对配置文件进行了独立的版本管理，并在编译时检查您当前使用的配置文件版本是否与库兼容。详细的版本信息及检查规则可在各配置文件末尾查看。

下面是关于如何配置 ESP32_Display_Panel 的详细说明，主要面向三种使用场景： [调整驱动配置](#调整驱动配置)、[加载支持的开发板](#加载支持的开发板) 和 [加载自定义开发板](#加载自定义开发板)，这些场景都是通过修改各自指定的配置文件进行实现，

### 调整驱动配置

ESP32_Display_Panel 会根据 [esp_panel_drivers_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/esp_panel_drivers_conf.h) 配置文件来调整 `esp_panel::drivers` 中代码的功能和参数，请参考以下步骤进行设置：

1. 参阅 [配置说明](#配置说明) 来了解配置文件的搜索路径。
2. 确认 `当前工程目录` 或 `Arduino 库目录` 中存在 *esp_panel_drivers_conf.h* 配置文件，若不存在，请从 ESP32_Display_Panel 的根目录或者示例工程中复制配置文件到任一目录中。
3. 修改配置文件中的宏定义来更新驱动的行为或默认参数。以设置触摸最大点数为 `5` 为例，下面是修改后的 *esp_panel_drivers_conf.h* 文件的部分内容：

    ```c
    ...
    /**
     * @brief Touch panel configuration parameters
    */
    #define ESP_PANEL_DRIVERS_TOUCH_MAX_POINTS              (5)    // Maximum number of touch points supported
    ...
    ```

> [!NOTE]
> *esp_panel_drivers_conf.h* 中默认只启用了部分驱动，如果想要通过代码动态加载开发板配置（如示例 [board_dynamic_config](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/board/board_dynamic_config)），请先启动所有需要使用的驱动。

## 支持的viewe开发板
| **Picture** |  Supported Boards   |   Selected Board   | PSRAM | Flash Mode | Flash Size | USB CDC On Boot | Partition Scheme |
| :-----------------: | :-----------------: | :----------------: | :---: | :--------: | :--------: | :-------------: | :--------------: |
|     <img src="https://github.com/VIEWESMART/UEDX24240013-MD50ESP32_1.3inch-Knob/blob/main/image/1.3.png" width="160">     | UEDX24240013-MD50E  | ESP32C3 Dev Module |  OPI  | QIO 80MHz  |    4MB     |     Enabled     |        4M        |
|     <img src="https://github.com/VIEWESMART/UEDX46460015-MD50ESP32-1.5inch-Touch-Knob-Display/blob/main/image/1.5.jpg" width="110">  | UEDX46460015-MD50E  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2025/06/1.11.jpg" width="180"> |   VIEWE-SMARTRING   | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://github.com/VIEWESMART/UEDX48480021-MD80ESP32_2.1inch-Knob/blob/main/image/2.1.jpg" width="180"> | UEDX48480021-MD80E  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://github.com/VIEWESMART/UEDX48480021-MD80ESP32-2.1inch-Touch-Knob-Display/blob/main/image/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20241129110611.jpg" width="130"> | UEDX48480021-MD80ET | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/11/UEDX24320024E-WB-A.jpg" width="150">  | UEDX24320024E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/11/UEDX24320028E-WB-A.jpg" width="150">   | UEDX24320028E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/11/UEDX24320035E-WB-A-1.jpg" width="150">  | UEDX24320035E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/11/UEDX32480035E-WB-A.jpg" width="150"> | UEDX32480035E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/07/UEDX80480043E-13.jpg" width="150">  | UEDX48270043E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/07/DX48480040E-WB-A-%E6%AD%A3.jpg" width="150"> | UEDX48480040E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/07/UEDX80480043E-13.jpg" width="150">  | UEDX80480043E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/06/DX80480050E-aa.jpg" width="150">   | UEDX80480050E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
|     <img src="https://viewedisplay.com/wp-content/uploads/2024/08/DX80480070E-a2.jpg" width="150">   | UEDX80480070E-WB-A  | ESP32S3 Dev Module |  OPI  | QIO 80MHz  |    16MB    |     Enabled     | 16M Flash (3MB)  |
