# KE0023 Keyes 热敏电阻传感器

![image-20250312153824886](media/image-20250312153824886.png)

---

## **1. 介绍**

KE0023 Keyes 热敏电阻传感器模块是一款基于热敏电阻的温度检测模块，适用于 Arduino 和其他微控制器开发板。热敏电阻是一种对温度敏感的电阻器，其阻值会随着温度的变化而变化。该模块通过检测热敏电阻的阻值变化，输出模拟信号，从而实现温度的测量。

该模块具有高灵敏度、响应速度快、稳定性好等特点，广泛应用于温度监控、环境检测、智能家居等领域。

---

## **2. 特点**

1. **高灵敏度**：对温度变化反应灵敏，适合实时温度监测。  
2. **稳定性好**：模块设计稳定，适合长期使用。  
3. **兼容性强**：支持 Arduino、Raspberry Pi 等多种开发板。  
4. **简单易用**：模块输出模拟信号，直接连接到开发板的模拟引脚即可读取温度变化。  
5. **小巧轻便**：便于集成到各种项目中。

---

## **3. 规格参数**

- **工作电压**：3.3V-5V  
- **输出信号**：模拟信号  
- **接口类型**：3PIN 接口（VCC、GND、AOUT）  
- **检测范围**：-55°C 至 +125°C（具体范围取决于热敏电阻参数）  
- **灵敏度**：温度变化时，输出电压随之变化  

---

## **4. 工作原理**

热敏电阻是一种温度敏感元件，其阻值会随着温度的变化而变化。KE0023 模块通过一个分压电路将热敏电阻的阻值变化转换为电压信号输出。  
- 当温度升高时，热敏电阻的阻值减小，输出电压增大。  
- 当温度降低时，热敏电阻的阻值增大，输出电压减小。  

开发板通过读取模块的模拟信号（AOUT 引脚），结合热敏电阻的特性曲线（或通过校准公式），即可计算出当前的温度值。

---

## **5. 接口**

KE0023 热敏电阻传感器模块提供 3 个引脚：  
- **VCC**：电源正极（3.3V 或 5V）  
- **GND**：电源负极  
- **AOUT**：模拟信号输出  

---

## **6. 连接图**

将 KE0023 热敏电阻传感器模块与 Arduino UNO 开发板连接，具体接线如下：  

| 模块引脚 | Arduino 引脚 |
|----------|--------------|
| VCC      | 5V           |
| GND      | GND          |
| AOUT     | A0           |

连接示意图：  

![image-20250312153836199](media/image-20250312153836199.png)

---

## **7. 示例代码**

以下是一个简单的示例代码，用于读取热敏电阻模块的模拟信号，并将其转换为温度值（假设热敏电阻为 10k NTC，需根据实际热敏电阻参数调整公式）：

```cpp
const int sensorPin = A0;  // 热敏电阻模块连接到 A0 引脚
float voltage;             // 模拟信号转换后的电压值
float resistance;          // 热敏电阻的阻值
float temperature;         // 计算出的温度值

void setup() {
  Serial.begin(9600);      // 初始化串口通信
}

void loop() {
  int sensorValue = analogRead(sensorPin);  // 读取模拟信号
  voltage = sensorValue * (5.0 / 1023.0);   // 将模拟信号转换为电压值
  resistance = (5.0 - voltage) * 10000 / voltage;  // 计算热敏电阻阻值（假设分压电阻为 10k）
  
  // 使用简单的公式计算温度（需根据热敏电阻特性调整）
  temperature = 1 / (log(resistance / 10000) / 3950 + 1 / 298.15) - 273.15;

  // 输出结果到串口监视器
  Serial.print("Voltage: ");
  Serial.print(voltage);
  Serial.print(" V, Resistance: ");
  Serial.print(resistance);
  Serial.print(" ohms, Temperature: ");
  Serial.print(temperature);
  Serial.println(" °C");

  delay(1000);  // 延迟 1 秒
}
```

---

## **8. 实验现象**

1. 将 KE0023 热敏电阻传感器模块与 Arduino UNO 按照连接图连接好。  
2. 将示例代码上传到 Arduino 开发板。  
3. 打开 Arduino IDE 的串口监视器，选择波特率为 9600。  
4. 在串口监视器中，可以看到实时的电压值、热敏电阻阻值和计算出的温度值。  
5. 用手触摸热敏电阻或改变周围环境温度，观察温度值的变化。

![image-20250312154002919](media/image-20250312154002919.png)

---

## **9. 注意事项**

1. **供电电压**：确保模块的供电电压在 3.3V-5V 范围内，避免损坏模块。  
2. **热敏电阻参数**：示例代码中的公式基于 10k NTC 热敏电阻，实际使用时需根据热敏电阻的参数调整计算公式。  
3. **环境温度**：模块适用于常规环境温度检测，极端温度下可能需要特殊处理。  
4. **校准**：为了提高测量精度，建议对模块进行校准，获取更准确的温度特性曲线。  
5. **避免短路**：在连接模块时，确保接线正确，避免短路或反接。  

---

## **10. 参考链接**

- **Arduino 官网**：[https://www.arduino.cc/](https://www.arduino.cc/)  
  提供 Arduino IDE 下载、官方教程和示例代码。  
- **Keyes 官网**：[http://www.keyes-robot.com/](http://www.keyes-robot.com/)  
  提供 Keyes 产品的详细信息和技术支持。  
- **Arduino 教程资源**：[https://www.arduino.cc/en/Tutorial/HomePage](https://www.arduino.cc/en/Tutorial/HomePage)  
  提供丰富的 Arduino 教程，适合初学者和进阶用户。  

---

KE0023 Keyes 热敏电阻传感器模块是一款简单易用的温度检测模块，适合初学者学习 Arduino 编程和传感器应用，也适用于各种物联网和环境监测项目。通过本教程，用户可以快速上手并实现温度检测功能。

