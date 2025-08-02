# 星智1.54 WiFi HA语音助手 (xingzhi-ha-voice) ESPHome 配置

本项目参考冬瓜大佬的 https://bbs.hassbian.com/thread-29342-1-1.html 帖子和esp32-s3-box-3的配置为 **星智1.54 WiFi (xingzhi-ha-voice)** 开发板提供了一套功能丰富的 ESPHome 配置，旨在将其打造为 Home Assistant 的本地智能语音中枢。

该配置利用了 ESPHome 强大的 `voice-assistant` 组件，并针对 星智1.54 WiFi 开发板的硬件特性进行了优化，支持本地唤醒、中文语音识别、屏幕状态反馈和物理按键等多种功能，为您提供开箱即用的智能家居语音控制体验。

![ESPHome Logo](https://esphome.io/_static/made-for-esphome-black-on-white.svg)

---

## ✨ 功能亮点
* **海绵宝宝表情图**:
    * ![hmbb](https://github.com/JochenZhou/xingzhi-ha-voice/blob/main/images/hmbb/240x240/replying.png)
* **完整语音助手功能**:
    * 支持 **离线唤醒词** (`micro_wake_word`)，默认包含 `okay_nabu`, `hey_mycroft`, `hey_jarvis` 等多个唤醒词模型。
    * 与 Home Assistant 深度集成，支持语音指令识别 (STT)、语音合成 (TTS) 和意图 (Intent) 处理。
* **丰富的屏幕交互**:
    * 通过屏幕上的动态插图，直观显示设备的 **空闲、聆听、思考、回复、错误** 等多种工作状态。
    * 在思考和回复页面，可直接显示您的语音请求和系统的文本回复。
* **完善的中文支持**:
    * 采用 `Noto Sans SC` 字体，确保在屏幕上完美显示中文语音指令和回复，解决了乱码问题。
    * 内置了数千个常用汉字和符号的字形库，覆盖绝大多数日常用语。
* **物理按键集成**:
    * **音量调节**: 使用 `GPIO39` (音量减) 和 `GPIO40` (音量加) 两个物理按键来控制媒体音量。
    * **一键静音**: 使用 `GPIO0` (Mute/Flash键) 作为麦克风静音开关。
* **屏幕实时音量显示**:
    * 在屏幕左上角实时显示当前音量百分比 (例如 "音量: 80%")，调节时即时反馈。
* **可视化定时器**:
    * 当 Home Assistant 的定时器运行时，屏幕底部会显示一个倒计时进度条，方便您随时查看。
* **双 Wi-Fi 配置**:
    * 支持配置两个备用 Wi-Fi 网络，增强了连接的稳定性。

---

## 🔧 安装与设置指南

### 先决条件

1.  一个正常运行的 **Home Assistant** 实例。
2.  在 Home Assistant 中安装了 **ESPHome Add-on**，并确保其已 **更新到最新版本**。此配置依赖于较新的 ESPHome 功能，旧版本可能无法编译。
3.  一块 **星智1.54 WiFi** 开发板。

### 安装步骤

1.  **下载代码**
    将此项目克隆或下载到您的本地计算机。
    ```bash
    git clone 本仓库
    ```

2.  **配置 Wi-Fi 凭据**
    ```yaml
    # secrets.yaml
    wifi_ssid: "你的主 Wi-Fi 名称"
    wifi_password: "你的主 Wi-Fi 密码"
    wifi_ssid2: "你的备用 Wi-Fi 名称"
    wifi_password2: "你的备用 Wi-Fi 密码"
    ```

3.  **上传并刷入固件**
    * 将整个项目文件夹上传到 ESPHome Add-on 的 `/config/esphome` 目录下。
    * 在 ESPHome 的仪表盘中，您会看到一个新的设备 `xingzhi-ha-voice`。
    * 使用 USB-C 数据线将您的 星智1.54 WiFi 开发板连接到运行 Home Assistant 的主机上。
    * 点击设备卡片上的 **"INSTALL"** 按钮。
    * 在弹出的窗口中选择 **"Plug into the computer running ESPHome Dashboard"**。
    * ESPHome 会自动编译固件并将其刷入您的设备。

    > **注意**: 首次编译可能需要较长时间，因为它需要从 Google Fonts 下载 `Noto Sans SC` 字体并处理数千个字符的字形。

4.  **添加到 Home Assistant**
    刷写完成后，设备会自动连接到您的 Wi-Fi。Home Assistant 会在“集成”页面自动发现新设备，点击“配置”即可将其添加到系统中。

---

## ⚠️ 重要说明

* **ESPHome 版本**: 再次强调，请务必使用**最新版本**的 ESPHome。此配置中的 `min_version` 已设置为 `2025.5.0`，以确保所有功能正常工作。
* **ADC2 引脚冲突**: ESP32-S3 的 ADC2 引脚与 Wi-Fi 模块共用，ADC2 pins are only usable when Wi-Fi is not configured on the device. GPIO17无法检测电池电量

---

## 🙏 致谢
* https://bbs.hassbian.com/thread-29342-1-1.html
* https://gemini.google.com/
* https://github.com/esphome/wake-word-voice-assistants
* https://github.com/RealDeco/xiaozhi-esphome
* 此项目基于 ESPHome 官方提供的语音助手示例进行修改和增强，并针对行者 星智1.54 WiFi 硬件进行了适配。感谢 ESPHome 和 Home Assistant 社区的卓越工作。

