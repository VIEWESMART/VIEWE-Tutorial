# [English](README.md)
# 说明
目前提供 Arduino IDE 、ESP-IDF 和 PlatformIO 三种开发工具和框架以及ui设计工具 SquareLine Studio，提供了灵活的开发选择，你可以根据项目需求和个人习惯选择适合的开发工具。

# 开发工具介绍
	
* **Arduino IDE**

  * Arduino IDE是一款便捷灵活、方便上手的开源电子原型平台。不需要太多基础，简单学习后，你也可以快速地进行开发。同时，Arduino 拥有庞大的全球用户社区，提供了海量的开源代码、项目示例和教程，还有丰富的库资源，封装了复杂功能，让开发者能快速实现各种功能。

* **ESP-IDF**

  * ESP-IDF，全称Espressif IDE，是乐鑫科技为 ESP系列芯片推出的专业开发框架。它使用C语言开发，包括编译器、调试器、烧录工具等，可在命令行下或使用集成开发环境（如 Visual Studio Code 配合 Espressif IDF 插件）进行开发，插件提供代码导航、项目管理、调试等功能。

* **PlatformIO**

  * Platform是基于Visual Studio Code（vscode），利用了vscode强大的扩展extension功能，使得开发者可以在vscode中直接调用gcc、jlink、gdb等进行开发、调试。PlatformIO只是一个集成开发环境，其本身几乎不包括任何实质性功能，但是其集成了很多了例如编译器、调试器等，它使用Arduino框架。相比于Arduino编译更快时间更短、结构更加清晰明了，也更便于管理。但它的缺点也很明显，上手困难并不适合初学者。

* **UI设计工具：SquareLine**
  * SquareLine Studio 由 Game-Ever 设计的 lvgl 可视化拖拽式UI编辑器，可快速轻松地为嵌入式和桌面应用程序创建漂亮的图形用户界面。当编辑好界面后，需要确定下工程导出方式，默认为C/C++工程，它可以直接导出作为项目所需的库或者组件与项目完美兼容。SquareLine Studio 针对业余爱好者和专业人士提供便宜且灵活的订阅计划。

这三种开发方式各有其优势，开发者可以根据自身需求和技能水平进行选择。Arduino 适合初学者和非专业人士，因其简单易学、上手快。Platformio相对需要一定的基础。而对于有专业背景或对性能要求较高的开发者，ESP-IDF 是更好的选择，它提供了更高级的开发工具和更强的控制能力，适用于复杂项目的开发。

# 教程快速窗口

| Arduino开发教程|ESP-IDF开发教程|Platformio开发教程|SquareLine开发教程|
| :------------ |:---------------:|:--------:|:-------------:|
|![](img/Arduino.webp) |![](img/ESP-IDF-Logo.webp) |![](img/PlatformIO-Logo.png) |![](img/SquareLineStudio-Logo.webp) |
| [![](img/GetStarted.webp)](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/Arduino%20Tutorial/Arduino%20IDE%E5%AE%89%E8%A3%85%E5%8F%8A%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md) | [![](img/GetStarted.webp)](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/esp-idf/esp-idf%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md) | [![](img/GetStarted.webp)]() | [![](img/GetStarted.webp)]() |

在这个仓库中我们将对三个开发环境以及UI设计工具进行一一介绍，从安装到运行。力求为各位刚入行的或者DIY爱好者提供更加详细的使用教程，也希望能帮助大家。我们将持续更新完善！！！

