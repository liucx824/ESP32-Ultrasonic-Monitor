# Wokwi 仿真配置

## 一键导入

1. 打开 https://wokwi.com
2. 点击 **New Project** → 选择 **ESP32**
3. 左侧 **diagram.json** 标签 → 复制本目录下的 `diagram.json` 内容粘贴进去
4. 左侧 **sketch.ino** 标签 → 复制 `../src/main.cpp` 的内容粘贴进去
5. 点击绿色 ▶ **Start Simulation** 运行仿真

## 仿真电路说明

| 元件 | 连接 |
|------|------|
| HC-SR04 TRIG | ESP32 GPIO5 |
| HC-SR04 ECHO | ESP32 GPIO18 |
| HC-SR04 VCC/GND | ESP32 VIN(5V)/GND |
| LCD1602 SDA | ESP32 GPIO21 |
| LCD1602 SCL | ESP32 GPIO22 |
| LCD1602 VCC/GND | ESP32 VIN(5V)/GND |

## 仿真效果

- LCD 第一行：实时距离（cm）
- LCD 第二行：滞回状态（Near/Far）+ 运行时间
- 串口监视器：原始值、滤波值、状态、MQTT上报日志
- 内置LED：近=快闪 200ms，远=慢闪 800ms

## 注意

仿真环境中 MQTT 和 WiFi 无法真实连接，但代码逻辑完整。
实物连接时修改 `WIFI_SSID` / `WIFI_PASSWORD` 宏即可。
