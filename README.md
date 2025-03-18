# 🌱 Arduino Smart Irrigation & Environment Control System

This project automates irrigation, shade control, and temperature regulation using DHT11, LDR, and Soil Moisture Sensors with an Arduino.

## 🛠 Features

✅ **Automatic Watering** – Activates the water pump when soil is dry  
✅ **Shade Control** – Adjusts shade based on light intensity (LDR)  
✅ **Temperature Regulation** – Turns on a fan when it gets too hot  
✅ **Real-time Monitoring** – Displays sensor data in a matrix format  

## 🔧 Hardware Requirements

| Component              | Description                               |
|------------------------|-------------------------------------------|
| Arduino Uno/Nano      | Microcontroller                           |
| DHT11 / DHT22         | Temperature & Humidity Sensor            |
| LDR Sensor           | Light Intensity Detection                 |
| Soil Moisture Sensor  | Detects soil dryness                     |
| Relays (x3)           | Controls water pump, shade motor, and fan |
| Water Pump           | Turns on based on moisture levels         |
| Fan                 | Turns on based on temperature             |
| Shade Motor         | Adjusts based on light intensity          |
| Jumper Wires        | Connect components                        |

## 📝 Pin Configuration

| Sensor/Device        | Arduino Pin |
|----------------------|-------------|
| DHT11 Sensor        | D2          |
| LDR Sensor          | A3          |
| Moisture Sensor     | A0          |
| Water Pump Relay    | D4          |
| Shade Motor Relay   | D5          |
| Fan Relay           | D6          |

## 🚀 Installation & Setup

### 1️⃣ Clone this repository
```sh
git clone https://github.com/your-username/Arduino-Smart-Irrigation.git
```

### 2️⃣ Upload the Code to Arduino

- Open Arduino IDE
- Install DHT library (`DHT.h`) from Library Manager
- Select Arduino Board & COM Port
- Click **Upload**

### 3️⃣ Monitor Sensor Readings

- Open **Serial Monitor**
- Set baud rate to **9600**

## 🛠 How It Works

### 📌 Sensor Readings
```cpp
float temperature = dht.readTemperature();
int moistureValue = analogRead(MOISTURE_PIN);
int ldrValue = analogRead(LDR_PIN);
```
Reads temperature, humidity, soil moisture, and light intensity.

### 📌 Water Pump Activation
```cpp
if (moistureValue > MOISTURE_THRESHOLD) {
  digitalWrite(WATER_RELAY_PIN, HIGH);
  delay(5000);
  digitalWrite(WATER_RELAY_PIN, LOW);
}
```
If soil is too dry, the pump runs for 5 seconds.

### 📌 Shade Motor Activation
```cpp
if (ldrValue > LDR_THRESHOLD) {
  digitalWrite(SHADE_RELAY_PIN, HIGH);
  delay(5000);
  digitalWrite(SHADE_RELAY_PIN, LOW);
}
```
If light is too intense, the shade motor is activated.

### 📌 Fan Control
```cpp
if (temperature > TEMPERATURE_THRESHOLD) {
  digitalWrite(FAN_RELAY_PIN, HIGH);
} else {
  digitalWrite(FAN_RELAY_PIN, LOW);
}
```
If temperature exceeds 33°C, the fan turns on.

## 📌 Future Enhancements

🔹 **Add WiFi & IoT support** using ESP8266/ESP32  
🔹 **Store sensor data in Firebase or ThingSpeak**  
🔹 **Build a mobile app for real-time monitoring**  

## 📜 License

This project is open-source under the **MIT License**.

## 📢 Contribute & Support

⭐ **Fork & Star** this repo if you found it useful!  
📌 Pull Requests are welcome for new features.  
💬 Join the Arduino & DIY Automation Community!  

**Happy Coding! 🚀🌿**
