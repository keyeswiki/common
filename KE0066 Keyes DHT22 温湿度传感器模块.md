# **KE0066 Keyes DHT22 温湿度传感器模块**

![image-20250312164726630](media/image-20250312164726630.png)

---

## **1. 介绍**

KE0066 Keyes DHT22 温湿度传感器模块是一款基于 DHT22 数字温湿度传感器的模块，专为 Arduino 等开发板设计。它能够检测环境的温度和湿度，并通过数字信号输出数据。模块采用红色环保 PCB 板，设计简单，易于使用，适用于环境监测、智能家居等场景。

---

## **2. 特点**

- **高精度检测**：能够检测环境温度和湿度，精度高。
- **数字信号输出**：通过单总线协议输出温湿度数据。
- **高兼容性**：兼容 Arduino、树莓派等开发板。
- **环保设计**：采用红色环保 PCB 板，耐用且稳定。
- **易于固定**：模块自带两个定位孔，方便安装。

---

## **3. 规格参数**

| 参数            | 值                     |
|-----------------|------------------------|
| **工作电压**    | 3.3V ～ 5.5V（DC）     |
| **工作电流**    | 2.5mA（最大）          |
| **温度检测范围**| -40℃ ～ +80℃          |
| **湿度检测范围**| 0% ～ 100% RH          |
| **温度精度**    | ±0.5℃                 |
| **湿度精度**    | ±2% RH                |
| **输出信号**    | 数字信号（单总线协议） |
| **工作周期**    | 2 秒                   |
| **重量**        | 5g                     |

---

## **4. 工作原理**

DHT22 是一款数字温湿度传感器，内部包含一个电容式湿度传感器和一个热敏电阻。传感器通过单总线协议输出温湿度数据，数据格式为 40 位，其中包含湿度和温度的整数和小数部分。模块通过数字信号引脚（DATA）与主控板通信。

---

## **5. 接口说明**

模块有3个引脚：
1. **VCC**：电源正极（3.3V ～ 5.5V）。
2. **GND**：电源负极（接地）。
3. **DATA**：数字信号输出（温湿度数据）。

---

## **6. 连接图**

以下是 KE0066 模块与 Arduino UNO 的连接示意图：

| KE0066模块引脚 | Arduino引脚 |
| -------------- | ----------- |
| VCC            | 5V          |
| GND            | GND         |
| DATA           | D3          |

连接图如下：

![image-20250312164739944](media/image-20250312164739944.png)

---

## **7. 示例代码**

以下是用于测试 KE0066 模块的 Arduino 示例代码，需安装 **DHT库**（Adafruit DHT Sensor Library）。

#### **安装库**
1. 打开 Arduino IDE。
2. 点击 **工具 > 管理库**。
3. 搜索 **DHT**，安装 **Adafruit DHT Sensor Library** 和 **Adafruit Unified Sensor**。

#### **代码**
```cpp
#include <Adafruit_Sensor.h>
#include <DHT.h>
#include <DHT_U.h>

// 定义 DHT 引脚和类型
#define DHTPIN 3     // 数据引脚连接到 D3
#define DHTTYPE DHT22 // 使用 DHT22 传感器

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600); // 设置串口波特率为9600
  Serial.println("DHT22 Temperature and Humidity Sensor Test");

  dht.begin(); // 初始化 DHT 传感器
}

void loop() {
  // 读取湿度
  float humidity = dht.readHumidity();
  // 读取温度（摄氏度）
  float temperature = dht.readTemperature();

  // 检查是否读取失败
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  // 打印温湿度数据
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print(" %\t");
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" *C");

  delay(2000); // 每2秒读取一次
}
```

---

## **8. 实验现象**

1. **测试步骤**：
   - 按照连接图接线，将模块连接到 Arduino。
   
   - 将代码烧录到 Arduino 开发板中。
   
   - 上电后，打开 Arduino IDE 的串口监视器，设置波特率为 9600。
   
   - 观察串口监视器中显示的温湿度数据。
   
   	![image-20250312164804023](media/image-20250312164804023.png)
   
2. **实验现象**：
   - 模块会每隔 2 秒输出一次当前环境的温度和湿度数据。
   - 当环境温度或湿度变化时，串口监视器中的数据会随之变化。

---

## **9. 注意事项**

1. **电压范围**：确保模块工作在 3.3V ～ 5.5V 电压范围内，避免损坏模块。
2. **工作周期**：DHT22 每次测量需要 2 秒，避免频繁读取数据。
3. **环境干扰**：避免在高湿度或强风环境中使用，以免影响检测效果。
4. **固定模块**：通过模块上的定位孔将其固定在稳定的位置，避免震动影响测量结果。
5. **数据校验**：DHT22 内置 CRC 校验机制，确保数据传输的可靠性。

---

## **10. 应用场景**

- **环境监测**：用于检测室内外温湿度。
- **智能家居**：用于制作温湿度监测设备。
- **农业监控**：用于监测温室或农田的温湿度。
- **工业控制**：用于监测工业环境的温湿度。
- **教育实验**：用于学习温湿度传感器的工作原理和应用。

---

## **11. 参考链接**

以下是一些有助于开发的参考链接：
- [Arduino官网](https://www.arduino.cc/)
- [Keyes官网](http://www.keyes-robot.com/)
- [DHT22传感器数据手册](https://cdn-shop.adafruit.com/datasheets/DHT22.pdf)

---

如果需要补充其他内容或有其他问题，请告诉我！
