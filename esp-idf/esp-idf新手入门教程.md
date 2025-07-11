# esp-idf新手入门教程

本章介绍 ESP-IDF 环境搭建和第一个程序的创建，包括 Visual Studio、Espressif IDF插件的安装。

## 下载和安装 Visual Studio

* 打开[VScode官网](https://code.visualstudio.com/download)的下载页面，选择对应系统和系统位数进行下载

![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/VScode-01.png)

* 运行安装包后，其余均可以默认安装，但这里为了后续的体验建议，建议在此处勾选框中的1、2、3项
![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/VScode-02.png)
  * 第一二项开启后，可以直接通过鼠标右键文件或者目录打开VSCode，可以提高后续的使用体验.
  * 第三项开启后，选择打开方式时，可以直接选择VSCode

> [!NOTE]
> * 环境设置是在 Windows 10 系统下进行，Linux和Mac用户可访问[ESP-IDF环境搭建](https://docs.espressif.com/projects/esp-idf/zh_CN/v5.1.4/esp32s3/get-started/windows-setup.html)参考

## 安装Espressif IDF插件

国内部分区域安装，一般推荐“在线安装”， 若因网络因素无法在线安装，则使用“离线安装”。

### 在线安装
* 打开VSCode，点击左侧的扩展，在扩展搜索并安装C/C++，ESP-IDF。可根据需求安装其他扩展
![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-01.png)

* 使用快捷键 F1 ，输入
  ```
  esp-idf: configure esp-idf extension
  ```
  ![plugin-02](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-02.png)

* 选择express（此教程针对第一次安装的用户，故只讲述初次的通用安装教程）
![plugin-03](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-03.png)

* 选择下载服务器，我们推荐国内用户使用Espressif作为你的下载服务器
![plugin-04](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-04.png)

* 选择想要的ESP-IDF版本，一般根据开发板要求选择支持的版本，若无要求推荐用最新的release version
![plugin-05](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-05.png)

* 下面两个分别为ESP-IDF容器安装地址和ESP-IDF所需的工具安装地址。
* 配置完成后，点击 install 进行下载
![plugin-06](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-06.png)

* 进入下载页面，其会自动安装对应工具与环境，稍等片刻即可
* 安装完成后，会进入以下界面，说明安装完成
![plugin-07](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-07.png)

> [!NOTE]
> * 如果之前有安装过ESP-IDF，或者失败过的，请务必彻底删除文件或者创建全新的无中文路径。

### 离线安装
离线安装请参见[离线安装教程]()

## 运行第一个 ESP-IDF 程序
如果你刚入门学习ESP32和ESP-IDF，还不知道如何创建、编译、烧录和运行ESP-IDF程序，希望可以帮助到你！

### 新建项目
![study-01](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-01.png)

![study-02](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-02.png)

### 创建例程
* 使用快捷键 F1 ，输入esp-idf:show examples projects
![study-03.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-03.png)

* 选择你当前的IDF版本
![study-04.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-04.png)

* 以Hello world例程为例
  
  ①选择对应例程
  
  ②其readme会说明该例程适用于什么芯片（下文有介绍例程怎么使用与文件结构，这里略）
  
  ③点击创建例程
![study-05.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-05.png)

* 选择放置例程的路径，要求无例程同名文件夹
![study-06.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-06.png)

### 修改COM口
* 此处显示使用对应的COM口，点击可以修改对应COM口
* 请根据设备对应COM口进行选择（可通过设备管理器查看）
* 若出现下载失败的情况请点击复位按键1秒以上或进入下载模式，等待 PC 端重新识别到设备后再次下载
![study-07.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-07.png)

### 修改驱动对象
* 选择我们需要驱动的对象，也就是我们的主芯片为ESP32S3
![study-08.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-08.png)

* 选择openocd的路径，这里对我们没有影响，所以我们随便选择一个即可
![study-09.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-09.png)

### 其余状态栏简介
  ①.ESP-IDF开发环境版本管理器，当我们的工程需要区分开发环境版本时，可以通过安装不同版本的ESP-IDF来分别管理，当工程使用特定版本时，可以通过使用它来切换
  
  ②.设备烧录COM口，选择以将编译好的程序烧录进芯片上
  
  ③.set-target 芯片型号选择，选择对应的芯片型号，如:ESP32-P4需要选择 esp32p4 为目标芯片
  
  ④.menuconfig，点击修改sdkconfig配置文件内容，[项目配置详细资料](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-reference/kconfig-reference.html)
  
  ⑤.fullclean 清理按钮，当工程编译报错或其他操作污染编译内容时，通过点击清理全部编译内容
  
  ⑥. Build 构建工程，当一个工程满足构建时，通过此按钮进行编译
  
  ⑦.当前下载方式，默认为UART
  
  ⑧.flash烧录按钮，当一个工程Build构建通过时，选择对应开发板COM口，点击此按钮可以将编译好的固件烧录至芯片
  
  ⑨.monitor开启烧录口监控，当一个工程Build-->flash后，可通过点击此按钮查看烧录、调试口输出的l0g，以便观察应用程序是否正常工作
  
  ⑩.Debug调试
  
  ⑪.Build Flash Monitor 一键按钮，用于连续执行Build-->Flash-->Monitor，常被称作小火苗

  ![study-10.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-10.png)

### 编译、烧录、串口监视
* 点击我们之前介绍的 设备烧录COM口，选择对应的设备COM口，也可自动识别COM口，直接下一步
* 点击我们之前介绍的 编译，烧录，打开串口监视器按键
![study-11.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-11.png)

* 编译可能需要较长时间才能完成，尤其是在第一次编译时
![study-12.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-12.png)

* 在此过程中，ESP-IDF可能会占用大量CPU资源，因此可能会导致系统卡顿
* 若是新工程首次烧录程序，将需要选择下载方式，选择 UART
![study-13.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-13.png)

* 后续也可在 下载方式 处进行修改（点击即可弹出选项）
![study-14.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-14.png)

* 点击下载
* 下载成功后，自动进入串口监视器，可以看到芯片输出对应的信息并提示10S后重启
![study-15.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-15.png)

### 使用IDF示例程序
**下文以使用随便使用一个示例为例介绍工程的三种打开方式及使用的一般步骤、ESP-IDF工程项目详解，若使用其他工程，操作步骤类似。**
#### 软件内部打开
* 打开 VScode 软件，导航到 `File` > `Open Folder...`
![study-16.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-16.png)

* 选择我们提供的 ESP-IDF 下的示例，点击选择文件（文件路径根据自己下载示例存放的的路径为准）
![study-17.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-17.png)



##### 软件外部打开
* 正确选择工程目录，打开工程，否则会影响后续程序编译烧录
![study-18.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-18.png)

* 连接设备后，选择好COM口和型号，点击下方编译并烧录即可实现程序控制
![study-19.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-19.png)

* 也可通过直接拖拽文件夹的方式，将文件夹拖拽到VSCode Studio即可打开

#### ESP-IDF工程项目详解
* 组件（Component）:ESP-IDF中的组件是构建应用的基本模块，每个组件通常是相对独立的代码库或库，能实现特定的功能或服务，可以被应用程序或是其他组件重复使用，类似于Python开发中的库的定义。
  * 组件的引用：Python开发环境中引入库只需要“import 库名或路径”即可，而ESP-IDF基于C语言基础，引入库是通过CMakeLists.txt进行配置和定义的。
  * CmakeLists.txt的作用：ESP-IDF编译时编译工具CMake会首先通过读取工程目录的顶层CMakeLists.txt的内容来读取构建规则，识别需要编译的内容。当在CMakeLists.txt中引入了需要的组件、程序后，编译工具CMake会根据索引导入每个所需要编译的内容。编译过程如：
  ![study-20](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-20.png)
* 大部分组件通过 idf component.yml 在编译时自动下载
  * [IDF组件管理器](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/tools/idf-component-manager.html)更多学习链接

**学习至此，你已经初步认识了idf的使用，已经可用开始在上面运行示例项目啦，后续我们还会添加更多的教程！！！**

## 技术支持
**联系人： 刘工**

**Email：smartrd1@viewedisplay.com**

**QQ群：1014311090**

**微信：扫下方二维码**
![微信](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/WeChat.jpg)
