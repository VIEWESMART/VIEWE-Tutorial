# 在 Arduino IDE 中使用
还在不断完善中，有不清晰明了的地方请立即联系我们，我们将进行优化。

## 目录

- [在 Arduino IDE 中使用](#在-arduino-ide-中使用)
  - [目录](#目录)
  - [快速入门](#快速入门)
    - [环境准备](#环境准备)
    - [运行第一个示例](#运行第一个示例)
    - [示例进阶](#示例进阶)
  - [配置说明](#配置说明)
    - [调整驱动配置](#调整驱动配置)
    - [加载支持的开发板](#加载支持的开发板)
    - [加载自定义开发板](#加载自定义开发板)
  - [示例说明](#示例说明)
    - [Drivers](#drivers)
    - [Board](#board)
    - [GUI](#gui)
  - [其他说明](#其他说明)
    - [配置 esp-lib-utils](#配置-esp-lib-utils)
    - [配置 LVGL](#配置-lvgl)
    - [移植 SquareLine 工程](#移植-squareline-工程)
  - [常见问题及解答](#常见问题及解答)
    - [Arduino 库的目录在哪儿？](#arduino-库的目录在哪儿)
    - [arduino-eps32 的安装目录以及 SDK 的目录在哪儿？](#arduino-eps32-的安装目录以及-sdk-的目录在哪儿)
    - [如何在 Arduino IDE 中安装 ESP32\_Display\_Panel？](#如何在-arduino-ide-中安装-esp32_display_panel)
    - [如何在 Arduino IDE 中选择和配置支持的开发板？](#如何在-arduino-ide-中选择和配置支持的开发板)
    - [如何在 Arduino IDE 中使用 SquareLine 导出的 UI 源文件？](#如何在-arduino-ide-中使用-squareline-导出的-ui-源文件)
    - [在 Arduino IDE 中使用库点不亮屏幕，如何调试？](#在-arduino-ide-中使用库点不亮屏幕如何调试)
    - [在 Arduino IDE 中打开串口调试器看不到日志信息或日志信息显示不全，如何解决？](#在-arduino-ide-中打开串口调试器看不到日志信息或日志信息显示不全如何解决)
    - [在 Arduino IDE 中使用 ESP32-S3 驱动 RGB LCD 时出现画面漂移问题的解决方案](#在-arduino-ide-中使用-esp32-s3-驱动-rgb-lcd-时出现画面漂移问题的解决方案)
    - [在 Arduino IDE 中使用 ESP32\_Display\_Panel 时，如何降低其 Flash 占用及加快编译速度？](#在-arduino-ide-中使用-esp32_display_panel-时如何降低其-flash-占用及加快编译速度)
    - [在 Arduino IDE 中使用 ESP32\_Display\_Panel 时，如何避免 I2C 重复初始化（如使用 Wire 库）？](#在-arduino-ide-中使用-esp32_display_panel-时如何避免-i2c-重复初始化如使用-wire-库)
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
   
ESP32_Display_Panel 及依赖库已经上传到了 Arduino 库管理器，您可以按照如下步骤直接在线安装：

1. 在 Arduino IDE 中导航到 `Sketch` > `Include Library` > `Manage Libraries...`。
2. 搜索 `ESP32_Display_Panel` 库并选择 `1.0.3`及其以上版本，点击 `Install` 按钮进行安装这时会提示你是否安装其依赖库请点击 `INSTALL ALL`安装全部。
3. 搜索安装 `LVGL`库（可选），推荐安装版本 `8.4.0`（目前暂时为适配`lvgl v9`版本，保持在 `lvgl v8` 请不要跨越大版本）

如果想要手动安装，可以通过 [Github](https://github.com/esp-arduino-libs/ESP32_Display_Panel) 或者 [Arduino Library](https://www.arduinolibraries.info/libraries/esp32_display_panel) 下载所需版本的 `.zip` 文件，然后在 Arduino IDE 中导航到 `Sketch` > `Include Library` > `Add .ZIP Library...`，选择下载的 `.zip` 文件并点击 `Open` 按钮进行安装。

> [!NOTE]
> * lvgl并不是并不是必须库，只有在使用 `gui` 示例时使用，详细说明请参考[示例说明](#示例说明)

### 运行第一个示例 
**第一个示例显示彩条和打印触摸坐标来验证配置若使用ui界面示例请参考[示例进阶](#示例进阶)**

1. **选择和配置开发板**

- 导航到 `Tools` > `Board` > `esp32` > `ESP32S3 Dev Module`

2. **打开示例**

- 导航到 `File` > `Examples` > `ESP32_Display_Panel`
- 选择 `Arduino` > `board` > [`board_static_config`](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/board/board_static_config)

3. **修改代码**
   
- 请修改 *esp_panel_board_supported_conf.h* 配置文件中的宏定义来启用目标开发板。参阅 [加载支持的开发板](#加载支持的开发板) 获取更多信息。

> [!WARNING]
> * 同一目录下可以同时包含 *esp_panel_board_supported_conf.h* 和 *esp_panel_board_custom_conf.h* 两个配置文件，但不能同时启用它们。即 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 和 `ESP_PANEL_BOARD_DEFAULT_USE_CUSTOM` 不能同时设为 `1`，否则会导致编译错误。
> * 由于配置文件的内容可能会随版本更新而变化（如新增、删除或重命名配置项），为确保兼容性，本库对配置文件进行了独立的版本管理，并在编译时检查您当前使用的配置文件版本是否与库兼容。详细的版本信息及检查规则可在各配置文件末尾查看。

4. **编译上传**

- 连接开发板UART(Type-C类型)到电脑
- 导航到 `Tool` > `port` 选择正确的串口
- 点击上传按钮

## 示例进阶
- 尝试其他 [示例程序](#示例说明)
- 了解详细的 [配置说明](#配置说明)
- 学习如何 [移植 UI](#移植-squareline-工程)
- 查看 [常见问题及解答](#常见问题及解答)

**此处以 `simple_port` 为例，演示如何移植 `LVGL v8`。并且对于 `RGB/MIPI-DSI` 接口，它还可以启用避免撕裂和旋转功能,也尝试其他示例，使用方法基本差不多**

1. **选择和配置开发板**

- 导航到 `Tools` > `Board` > `esp32` > `ESP32S3 Dev Module`
- `Tools` 其他配置如下参考[支持的viewe开发板](#支持的viewe开发板)

2. **打开示例**

- 导航到 `File` > `Examples` > `ESP32_Display_Panel`
- 选择 `Arduino` > `gui` > `lvgl_v8` > [`simple_port`](https://github.com/esp-arduino-libs/ESP32_Display_Panel/tree/master/examples/arduino/gui/lvgl_v8/simple_port/)

3. **修改代码**

- 请修改 *esp_panel_board_supported_conf.h* 配置文件中的宏定义来启用目标开发板。参阅 [加载支持的开发板](#加载支持的开发板) 获取更多信息。

4. **编译上传**

- 连接开发板UART(Type-C类型)到电脑
- 导航到 `Tool` > `port` 选择正确的串口
- 点击上传按钮

  
关于使用lvgl颜色转换问题：`SPI`和 `QSPI`屏幕需将 `lv_conf.h` > `LV_COLOR_16_SWAP`的宏设置为 `1`而 `RGB` 屏则保持为 `0`,如下 :
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

### 加载支持的开发板

ESP32_Display_Panel 会根据 [esp_panel_board_supported_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/esp_panel_drivers_conf.h) 配置文件来设置 `esp_panel::board::Board` 中默认开发板的配置，请参考以下步骤进行设置：

1. 参阅 [配置说明](#配置说明) 来了解配置文件的搜索路径。
2. 确认 `当前工程目录` 或 `Arduino 库目录` 中存在 *esp_panel_board_supported_conf.h* 配置文件，若不存在，请从 ESP32_Display_Panel 的根目录或者示例工程中复制配置文件到任一目录中。
3. 设置配置文件中的 `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` 宏定义为 `1`。
4. 根据目标开发板的型号，取消对应的宏定义的注释。
5. 此时，调用 `esp_panel::board::Board` 默认构造函数时会加载目标开发板的配置。
6. 以使用 `UEDX48480040E-WB-A` 开发板为例，开发板选择请参考[支持的viewe开发板](#支持的viewe开发板)，下面是修改后的 *esp_panel_board_supported_conf.h* 文件的部分内容：
  
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

## 其他说明

### 配置 esp-lib-utils

ESP32_Display_Panel 依赖于 `esp-lib-utils` 库，使用其提供的 `日志`、`内存分配` 和 `检查` 等功能，`esp-lib-utils` 库同样采用了通过修改特定配置文件 [esp_utils_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/template_files/esp_utils_conf.h) 来调整库的行为和参数，您可以参考 [调整驱动配置](#调整驱动配置) 进行修改。

以设置 `日志` 等级为 `DEBUG` 并开启 `函数功能追踪` 功能为例，下面是修改后的 *esp_utils_conf.h* 文件的部分内容：

```c
...
/**
 * Global log level, logs with a level lower than this will not be compiled. Choose one of the following:
 *  - ESP_UTILS_LOG_LEVEL_DEBUG:   Extra information which is not necessary for normal use (values, pointers, sizes, etc)
 *                                 (lowest level)
 *  - ESP_UTILS_LOG_LEVEL_INFO:    Information messages which describe the normal flow of events
 *  - ESP_UTILS_LOG_LEVEL_WARNING: Error conditions from which recovery measures have been taken
 *  - ESP_UTILS_LOG_LEVEL_ERROR:   Critical errors, software module cannot recover on its own
 *  - ESP_UTILS_LOG_LEVEL_NONE:    No log output (highest level) (Minimum code size)
 */
#define ESP_UTILS_CONF_LOG_LEVEL                            (ESP_UTILS_LOG_LEVEL_DEBUG)
...
    /**
     * @brief Set to 1 if print trace log messages when enter/exit functions, useful for debugging
     */
    #define ESP_UTILS_CONF_ENABLE_LOG_TRACE                 (1)
...
```

### 配置 Arduino IDE

如果正在使用自定义开发板，请选择相同系列芯片的通用开发板，如 `ESP32S3 Dev Module`。然后根据开发板设置其他配置。

如果正在使用 [支持的开发板](../../README_CN.md#支持的开发板)，以下是开发板制造商提供的推荐配置指南：

- [Espressif](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/docs/board/board_espressif.md#arduino-ide)
- [VIEWE](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/docs/board/board_viewe.md#arduino-ide)

### 配置 LVGL

LVGL 的功能和参数可以通过修改 [lv_conf.h](https://github.com/esp-arduino-libs/ESP32_Display_Panel/blob/master/template_files/lv_conf.h) 配置文件来调整。以下是配置 LVGL 的说明：

1. **配置文件查找规则**

- 使用 arduino-esp32 v3 版本时，LVGL 按优先级查找配置文件：`当前工程目录` > `Arduino 库目录`
- 如果未找到配置文件，编译时会提示警告
- 请确保至少在一个目录中包含 *lv_conf.h* 文件

2. **配置文件使用方式**

- 单个工程配置：将配置文件放在工程目录下
- 多个工程共享配置：将配置文件放在 [Arduino 库目录](#arduino-库的目录在哪儿)

3. **配置步骤**

    a. 获取配置文件模板

    - 导航到 [Arduino 库目录](#arduino-库的目录在哪儿)
    - 进入 *lvgl* 文件夹
    - 复制 *lv_conf_template.h* 到目标目录并重命名为 *lv_conf.h*

    b. 启用配置文件

    - 打开 *lv_conf.h*
    - 将第一个 `#if 0` 修改为 `#if 1`

    c. 常用配置项

    ```c
    // 颜色配置
    #define LV_COLOR_DEPTH          16    // 通常使用 16 位色深(RGB565)
                                            // 设置为 32 可支持带透明度的 24 位色深(ARGB8888)
    #define LV_COLOR_16_SWAP        0     // SPI/QSPI LCD(如 ESP32-C3-LCDkit)需设置为 1
    #define LV_COLOR_SCREEN_TRANSP  1     // 带透明度的 LCD 需设置为 1
    // 内存配置
    #define LV_MEM_CUSTOM           1     // 使用 malloc/free 以提高性能
    #define LV_MEMCPY_MEMSET_STD    1     // 使用标准库函数
    // 资源配置
    #define LV_FONT_MONTSERRAT_N    1     // 启用所需的内置字体(N 替换为字体大小)
    // 调试配置
    #define LV_USE_PERF_MONITOR     1     // 显示 CPU 使用率和 FPS
    #define LV_USE_LOG              1     // 启用日志功能
    #define LV_LOG_PRINTF           1     // 使用 printf 输出日志
    // 其他配置
    #define LV_ATTRIBUTE_FAST_MEM   IRAM_ATTR  // 提高性能但会占用更多 SRAM
    ```

4. 更多说明请参阅 [LVGL 官方文档](https://docs.lvgl.io/8.4/get-started/platforms/arduino.html)

### 移植 SquareLine 工程

`SquareLine Studio (v1.4.x)` 提供了图形化界面编辑工具,可以快速设计精美的 UI。要在 Arduino IDE 中使用 SquareLine 导出的 UI 源文件,请参考以下步骤操作：

1. 创建新工程

- 打开 SquareLine Studio
- 进入 `Create` > `Arduino`
- 选择 `Arduino with TFT-eSPI` 模板
- 在 `PROJECT SETTINGS` 中根据开发板 LCD 配置参数(如分辨率、色深等)
- 点击 `Create` 创建工程

2. 配置已有工程

- 点击 `File` > `Project Settings`
- 在 `BOARD PROPERTIES` 中设置：

  - `Board Group`： `Arduino`
  - `Board`： `Arduino with TFT-eSPI`

- 在 `DISPLAY PROPERTIES` 中配置 LCD 参数
- 点击 `Save` 保存设置

3. 导出工程

- 完成 UI 设计并配置导出路径
- 依次点击 `Export` > `Create Template Project` 和 `Export UI Files`
- 导出的工程目录结构如下：

    ```
    Project
    ├── libraries
    │   ├── lv_conf.h
    │   ├── lvgl
    │   ├── readme.txt
    │   ├── TFT_eSPI
    │   └── ui
    ├── README.md
    └── ui
    ```

4. 配置 Arduino 库

- 将 *libraries* 文件夹中的 *lv_conf.h*、*lvgl* 和 *ui* 复制到 Arduino 库目录
- 如果使用本地安装的 LVGL，跳过复制 *lvgl* 和 *lv_conf.h* 并参考 [配置 LVGL](#配置-lvgl) 进行设置
- Arduino 库目录结构示例：

    ```
    Arduino
    └── libraries
        ├── ESP32_Display_Panel
        ├── esp_panel_drivers_conf.h (可选)
        ├── esp_panel_board_supported_conf.h (可选)
        ├── esp_panel_board_custom_conf.h (可选)
        ├── lv_conf.h (可选)
        ├── lvgl
        ├── ui
        ├── other_lib_1
        └── other_lib_2
    ```

  ## 常见问题及解答

### Arduino 库的目录在哪儿？

您可以在 Arduino IDE 的菜单栏中选择 `File` > `Preferences` > `Settings` > `Sketchbook location` 来查找和修改 Arduino 库的目录路径。

### arduino-eps32 的安装目录以及 SDK 的目录在哪儿？

arduino-esp32 的默认安装路径取决于您的操作系统：

- Windows： `C:\Users\<user name>\AppData\Local\Arduino15\packages\esp32`
- Linux： `~/.arduino15/packages/esp32`
- macOS： `~/Library/Arduino15/packages/esp32`

arduino-esp32 v3.x 版本的 SDK 位于默认安装路径下的 `tools > esp32-arduino-libs > idf-release_x` 目录中。

### 如何在 Arduino IDE 中安装 ESP32_Display_Panel？

请参阅 [安装库](#安装库) 。

### 如何在 Arduino IDE 中选择和配置支持的开发板？

请参阅 [配置 Arduino IDE](#配置-arduino-ide)。

### 如何在 Arduino IDE 中使用 SquareLine 导出的 UI 源文件？

请参阅 [移植 SquareLine 工程](#移植-SquareLine-工程)。

### 在 Arduino IDE 中使用库点不亮屏幕，如何调试？

请参考以下步骤进行排查：

1. 参考 [配置说明](#配置-esp-lib-utils) 将 `esp-lib-utils` 库的日志等级设置为 `DEBUG` 并开启函数追踪功能。
2. 在 Arduino IDE 中设置：`Tools` > `Core Debug Level` 为 `Debug` 或更低级别，然后重新编译上传代码。
3. 通过串口监视器查看详细的日志信息，分析问题所在。
4. 如果通过以上步骤仍无法解决问题，请在 [GitHub Issues](https://github.com/esp-arduino-libs/ESP32_Display_Panel/issues) 提交问题报告，并附上完整的日志信息。

### 在 Arduino IDE 中打开串口调试器看不到日志信息或日志信息显示不全，如何解决？

请参考以下步骤解决：

1. 检查 Arduino IDE 中 `Tools` > `Port` 是否设置正确
2. 检查 Arduino IDE 中 `Tools` > `Core Debug Level` 是否设置为期望等级，如 `Info` 或更低级别
3. 检查 Arduino IDE 中 `Tools` > `USB CDC On Boot` 是否设置正确，如 ESP32 使用 `UART` 端口连接则设置为 `Disabled`，使用 `USB` 端口连接则设置为 `Enabled`。修改设置后需要使能 `Erase All Flash Before Sketch Upload` 选项后重新烧录。
4. 检查 Arduino IDE 中串口调试器波特率是否设置正确，如 `115200`

### 在 Arduino IDE 中使用 ESP32-S3 驱动 RGB LCD 时出现画面漂移问题的解决方案

请参考以下步骤解决：

1. **了解问题**

- 请参阅 [ESP32-S3 RGB LCD 画面漂移问题说明](https://docs.espressif.com/projects/esp-faq/zh_CN/latest/software-framework/peripherals/lcd.html#esp32-s3-rgb-lcd)

2. **启用 `RGB LCD Bounce Buffer + XIP on PSRAM` 特性**

    a. **更新 SDK 以使能 `XIP on PSRAM` 功能**

    - 从 [arduino-esp32-sdk](https://github.com/esp-arduino-libs/arduino-esp32-sdk) 下载 `high_perf` 版本
    - 按照 [说明文档](https://github.com/esp-arduino-libs/arduino-esp32-sdk#how-to-use) 替换到 [arduino-esp32 安装目录](#arduino-eps32-的安装目录以及-sdk-的目录在哪儿)

    b. **配置 `RGB LCD Bounce Buffer`**

    - 对于支持的开发板：

        - 通常已默认配置 `ESP_PANEL_BOARD_LCD_RGB_BOUNCE_BUF_SIZE` 为 `(ESP_PANEL_BOARD_WIDTH * 10)`
        - 如果问题仍存在,可参考示例代码增大缓冲区

    - 对于自定义开发板：

        - 在 *esp_panel_board_custom_conf.h* 中设置 `ESP_PANEL_BOARD_LCD_RGB_BOUNCE_BUF_SIZE`
        - 如果问题仍存在,可参考示例代码增大缓冲区

    c. **配置 LVGL 任务**

    - 如果使用 LVGL，设置执行 `lv_timer_handler()` 的任务与执行 `board->begin()` 的任务在同一个核心上运行可以缓解画面漂移问题

3. **示例代码**

    a. 使用开发板时修改 `Bounce Buffer` 大小。

    ```c
    ...
    esp_panel::board::Board *board = new esp_panel::board::Board();
    board->init();
    ...
    /**
     * 1. Should be called after `board->init()` and before `board->begin()`
    * 2. `ESP_PANEL_BOARD_WIDTH` should be replaced with the actual width of the LCD
    */
    auto bus = static_cast<esp_panel::drivers::BusRGB *>(board->getLCD()->getBus());
    bus->configRGB_BounceBufferSize(ESP_PANEL_BOARD_WIDTH * 20);
    ...
    board->begin();
    ...
    ```

    b. 使用独立驱动时修改 `Bounce Buffer` 大小。

    ```c
    ...
    esp_panel::drivers::BusRGB *bus = new esp_panel::drivers::BusRGB(...);
    ...
    /**
     * 1. Should be called before `bus->init()`
        * 2. `EXAMPLE_LCD_WIDTH` should be replaced with the actual width of the LCD
        */
    bus->configRGB_BounceBufferSize(EXAMPLE_LCD_WIDTH * 20);
    ...
    bus->init();
    ...
    ```

### 在 Arduino IDE 中使用 ESP32_Display_Panel 时，如何降低其 Flash 占用及加快编译速度？

请参考以下步骤实现：

1. **禁用不需要的驱动**：

- 在 `esp_panel_drivers_conf.h` 中仅使能需要用到的驱动
- 例如，不需要使用 `RGB LCD` 驱动时：

    ```c
    ...
    #define ESP_PANEL_DRIVERS_BUS_USE_ALL    (0)
    ...
    #define ESP_PANEL_DRIVERS_BUS_USE_RGB    (0)
    ```

- 详细配置方法请参阅 [调整驱动配置](#调整驱动配置)

2. **关闭调试日志**：

- 在 `esp_utils_conf.h` 中设置：

    ```c
    #define ESP_UTILS_CONF_LOG_LEVEL    ESP_UTILS_LOG_LEVEL_NONE
    ```

- 详细配置方法请参阅 [配置 esp-lib-utils](#配置-esp-lib-utils)

### 在 Arduino IDE 中使用 ESP32_Display_Panel 时，如何避免 I2C 重复初始化（如使用 Wire 库）？

如果您需要使用 ESP32_Display_Panel 的 I2C 总线功能，如使用 `I2C IO_Expander` 或 `I2C Touch` 等驱动，而您的项目中已经使用了 `Wire` 库，可能会因为 I2C 总线重复初始化导致错误。为了避免这种情况，请在创建 `Board` 对象之前初始化 `Wire`，然后参考以下步骤设置 ESP32_Display_Panel 跳过初始化 I2C：

1. 通过代码的方法（适用于 [支持的开发板](#加载支持的开发板) 以及 [自定义开发板](#加载自定义开发板)）：

    ```c
    ...
    esp_panel::board::Board *board = new esp_panel::board::Board();
    board->init();
    ...
    /**
     * Should be called after `board->init()` and before `board->begin()`
     */
    // For I2C Touch
    static_cast<esp_panel::drivers::BusI2C *>(board->getTouch()->getBus())->configI2C_HostSkipInit();
    // For I2C IO_Expander
    board->getIO_Expander()->skipInitHost();
    ...
    board->begin();
    ...
    ```

