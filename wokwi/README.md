# Wokwi 仿真配置

## 操作步骤（按截图顺序）

1. 打开 https://wokwi.com/projects/new/esp32
2. 页面会自动载入一个 ESP32 模板，你会看到两个标签页：
   - **diagram.json** —— 电路图
   - **sketch.ino** —— 代码
3. 点击 **diagram.json** 标签，全选删除，复制本目录下 `diagram.json` 的全部内容粘贴进去
4. 点击 **sketch.ino** 标签，全选删除，复制 `../src/main.cpp` 的全部内容粘贴进去
5. 修改两行代码（因为 Wokwi 有内置模拟 WiFi）：
   ```
   #define WIFI_SSID       "Wokwi-GUEST"
   #define WIFI_PASSWORD   ""
   ```
6. 点击顶部绿色的 ▶ 播放按钮，开始仿真

## 仿真电路

```
ESP32 GPIO5  ──▶ HC-SR04 TRIG
ESP32 GPIO18 ◀── HC-SR04 ECHO
ESP32 GPIO21 ◀──▶ LCD1602 SDA (I2C)
ESP32 GPIO22 ──▶ LCD1602 SCL (I2C)
ESP32 5V     ──▶ HC-SR04 VCC, LCD1602 VCC
ESP32 GND    ──▶ HC-SR04 GND, LCD1602 GND
```

## 仿真效果

| 位置 | 内容 |
|------|------|
| LCD 第一行 | 实时距离：`Dis: xx.x cm` |
| LCD 第二行 | 滞回状态：`Near`/`Far` + 运行时间 |
| 串口监视器 | 原始值 → 滤波值 → 状态 → MQTT 上报日志 |
| 内置 LED | 近=快闪(200ms)，远=慢闪(800ms) |

## 注意事项

- Wokwi 内置了模拟 WiFi 环境，SSID 改为 `Wokwi-GUEST` 即可联网
- MQTT 使用公共代理 `broker.emqx.io`，仿真中可以直接连接
- 仿真环境声速固定为 0.0343 cm/us（20°C），实物测试如有偏差可微调
