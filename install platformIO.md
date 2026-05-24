好，我们先解决 PlatformIO 安装问题，再继续第二阶段。

---

## 离线安装 PlatformIO（最稳方法）

### Step 1 · 下载 .vsix 文件

用浏览器打开这个链接，直接下载安装包：

👉 https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide

页面长这样，点右侧的 **Download Extension**：PlatformIO 装好之后，继续第二阶段正式内容👇

---

## 装好后：新建猫猫神谕项目

### Step 6 · 新建项目

1. 点左侧蚂蚁图标 → **PlatformIO Home**
2. 点 **New Project**
3. 填写：
   - Name: `neko-oracle`
   - Board: 搜索 `ESP32-S3` → 选 **Espressif ESP32-S3-DevKitC-1**
   - Framework: **Arduino**
4. 点 Finish，等待依赖下载完

### Step 7 · 替换 platformio.ini

项目生成后，打开根目录的 `platformio.ini`，**全部替换**成这个：

```ini
[env:m5stack-cores3]
platform = espressif32@6.7.0
board = esp32-s3-devkitc-1
framework = arduino
upload_speed = 1500000
monitor_speed = 115200
build_flags =
  -DESP32S3
  -DBOARD_HAS_PSRAM
  -mfix-esp32-psram-cache-issue
  -DARDUINO_USB_CDC_ON_BOOT=1
  -DARDUINO_USB_MODE=1
lib_deps =
  m5stack/M5Unified
  m5stack/M5GFX
```

### Step 8 · 写 Hello World 验证环境

打开 `src/main.cpp`，替换成：

```cpp
#include <M5Unified.h>

void setup() {
  auto cfg = M5.config();
  M5.begin(cfg);
  
  M5.Display.fillScreen(TFT_BLACK);
  M5.Display.setTextColor(TFT_YELLOW);
  M5.Display.setTextSize(2);
  M5.Display.setCursor(50, 90);
  M5.Display.println("Neko Oracle");
  M5.Display.setTextColor(TFT_WHITE);
  M5.Display.setTextSize(1);
  M5.Display.setCursor(70, 130);
  M5.Display.println("Env OK!");
}

void loop() {
  M5.update();
}
```

### Step 9 · 连接设备并烧录

1. CoreS3 用 USB-C 连电脑
2. 底部工具栏点 **→ Upload**（右箭头图标）
3. PlatformIO 会自动识别串口，开始编译+烧录
4. 屏幕显示黄色 "Neko Oracle" 字样 → **环境完全OK！**

---

**现在按步骤走，先把 PlatformIO 装好，装好了告诉我**，我们继续写猫脸表情系统的代码 🐱
