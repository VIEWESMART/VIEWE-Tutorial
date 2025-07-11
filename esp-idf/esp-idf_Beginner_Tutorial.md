[**中文**](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/esp-idf/esp-idf%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md)

# ESP-IDF Beginner Tutorial

This chapter introduces the setup of the ESP-IDF environment and the creation of the first program, including the installation of Visual Studio Code and the Espressif IDF plugin.

## Download and Install Visual Studio Code

* Open the download page at [VSCode official website](https://code.visualstudio.com/download), select your system and architecture to download.

![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/VScode-01.png)

* After running the installer, most options can be left as default. However, for a better experience, it is recommended to check items 1, 2, and 3 as shown:
![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/VScode-02.png)
  * Enabling the first two items allows you to open files/directories in VSCode directly via right-click, improving usability.
  * The third item adds VSCode to the "Open With" context menu.

> [!NOTE]
> * Environment setup is demonstrated on Windows 10. Linux/Mac users should refer to [ESP-IDF Environment Setup](https://docs.espressif.com/projects/esp-idf/en/v5.1.4/esp32s3/get-started/index.html).

## Install Espressif IDF Plugin

For users in some regions of China, "Online Installation" is recommended. Use "Offline Installation" if network issues prevent online installation.

### Online Installation
* Open VSCode, click the Extensions icon on the left, then search for and install the **C/C++** and **ESP-IDF** extensions. Install other extensions as needed.
![](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-01.png)

* Press **F1**, then type:
  ```
  esp-idf: configure esp-idf extension
  ```
  ![plugin-02](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-02.png)

* Select **Express** (This tutorial focuses on first-time installation).
![plugin-03](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-03.png)

* Choose a download server. We recommend **Espressif** for users in China.
![plugin-04](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-04.png)

* Select your desired ESP-IDF version. Choose a version compatible with your board, or use the latest release if unspecified.
![plugin-05](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-05.png)

* Specify the ESP-IDF container installation path and tools directory.
* Click **Install** after configuration.
![plugin-06](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-06.png)

* The download page will appear. Tools and environment will install automatically.
* Upon completion, you'll see this screen:
![plugin-07](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/plugin-07.png)

> [!NOTE]
> * If you have a previous failed installation, completely delete old files or create a new path without Chinese characters.

### Offline Installation
Refer to [Offline Installation Tutorial]()

## Run Your First ESP-IDF Program
This section guides beginners through creating, compiling, flashing, and running an ESP-IDF program.

### Create New Project
![study-01](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-01.png)

![study-02](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-02.png)

### Create Example Project
* Press **F1**, type:esp-idf:show examples projects
![study-03.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/study-03.png)

* Select your installed IDF version.
![study-04.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-04.png)

* Using the **Hello World** example:

① Select the example

② Read the README for chip compatibility 

③ Click "Create Example Project"
![study-05.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-05.png)

* Choose a directory path without existing project files.
![study-06.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-06.png)

### Configure COM Port
* Click to select the correct COM port (check via Device Manager).
* If flashing fails, hold the reset button for >1 second or enter download mode.
![study-07.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-07.png)

### Set Target Chip
* Select your main chip (e.g., ESP32S3).
![study-08.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-08.png)

* For OpenOCD path, any selection is acceptable.
![study-09.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-09.png)

### Status Bar Overview
①. **ESP-IDF Version Manager**: Switch between IDF versions for projects requiring specific environments.

②. **COM Port**: Select port for flashing.

③. **Set Target**: Choose chip model (e.g., ESP32-P4 → `esp32p4`).

④. **Menuconfig**: Modify `sdkconfig` ([Configuration Reference](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-reference/kconfig.html)).

⑤. **Full Clean**: Clean build artifacts when encountering errors.

⑥. **Build**: Compile the project.

⑦. **Flash Method**: Default is UART.

⑧. **Flash**: Burn compiled firmware to chip.

⑨. **Monitor**: View serial output after flashing.

⑩. **Debug**: Start debugging.

⑪. **Build Flash Monitor**: One-click button (often called "Fire" icon).

![study-10.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-10.png)

### Compile, Flash, and Monitor
* Select the correct COM port (auto-detection available).
* Click the **Build, Flash, and Monitor** button.
![study-11.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-11.png)

* Compilation may take significant time (especially on first build).
![study-12.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-12.png)

* ESP-IDF may cause system slowdowns during compilation.
* For first-time flashing, select **UART** as the download method.
![study-13.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-13.png)

* Change method later via the **Flash Method** selector.
![study-14.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-14.png)

* Click **Download**.
* After successful flashing, the monitor displays chip output (including restart countdown).
![study-15.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-15.png)

### Using IDF Example Projects
**The following demonstrates three ways to open projects using an example.**

#### Open Within VSCode
* In VSCode, navigate to `File` > `Open Folder...`
![study-16.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-16.png)

* Select your example project directory.
![study-17.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-17.png)

#### Open Externally
* Right-click the project folder → `Open with VSCode`.
* Ensure correct directory selection to avoid compilation issues.
![study-18.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-18.png)

* After connecting device: Select COM Port → Set Target → Click **Build and Flash**.
![study-19.png](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-19.png)

* Alternatively, drag the folder into VSCode.

#### ESP-IDF Project Structure Explained
* **Component**: Fundamental building blocks in ESP-IDF. Independent code libraries providing specific functionality (similar to Python libraries).
* **Usage**: While Python uses `import`, ESP-IDF uses `CMakeLists.txt` for configuration.
* **CMakeLists.txt**: The build tool (CMake) reads this file to determine compilation rules and dependencies. Process:
![study-20](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/idf-study-20.png)
* Most components auto-download via `idf_component.yml`.
* [IDF Component Manager Guide](https://docs.espressif.com/projects/esp-idf/en/latest/esp32s3/api-guides/tools/idf-component-manager.html)

**You've now taken your first steps with ESP-IDF! You can run example projects. More tutorials coming soon!**

## Technical Support
**Contact: Engineer Liu**

**Email: smartrd1@viewedisplay.com**

**QQ Group: 1014311090**

**WeChat: Scan QR Code Below**
![WeChat](https://github.com/VIEWESMART/VIEWE-Tutorial/blob/main/img/WeChat.jpg)
