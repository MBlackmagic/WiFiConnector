[![latest](https://img.shields.io/github/v/release/GyverLibs/WiFiConnector.svg?color=brightgreen)](https://github.com/GyverLibs/WiFiConnector/releases/latest/download/WiFiConnector.zip)  
[![PIO](https://badges.registry.platformio.org/packages/gyverlibs/library/WiFiConnector.svg)](https://registry.platformio.org/libraries/gyverlibs/WiFiConnector)  
[![Website](https://img.shields.io/badge/Website-AlexGyver.ru-blue.svg?style=flat-square)](https://alexgyver.ru/)  
[![Support Author](https://img.shields.io/badge/%E2%82%BD%24%E2%82%AC%20%D0%9F%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B0%D1%82%D1%8C-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B0-orange.svg?style=flat-square)](https://alexgyver.ru/support_alex/)  
[![README ENGLISH](https://img.shields.io/badge/README-ENGLISH-blueviolet.svg?style=flat-square)](https://github-com.translate.goog/GyverLibs/WiFiConnector?_x_tr_sl=ru&_x_tr_tl=en)  
[![Subscribe](https://img.shields.io/badge/ПОДПИСАТЬСЯ-НА%20ОБНОВЛЕНИЯ-brightgreen.svg?style=social&logo=telegram&color=blue)](https://t.me/GyverLibs)

# WiFiConnector
Asynchronous WiFi connection with automatic fallback to Access Point (AP) mode if a connection times out.

## Compatibility
Supports **ESP8266** and **ESP32**

---

## Table of Contents
- [Usage](#usage)
- [Versions](#versions)
- [Installation](#installation)
- [Bugs and Feedback](#bugs-and-feedback)

---

## Usage

Use this library when your WiFi credentials are stored externally or are not known in advance.  
If the SSID is passed as an empty string, the device will launch in AP mode.  
If a connection fails, AP mode will be launched automatically for web-based configuration or user interaction.

### Class Overview

```cpp
// AP name, AP password, timeout in seconds, disable AP after STA connection
WiFiConnectorClass(const String& APname = "ESP AP",
                    const String& APpass = "",
                    uint16_t timeout = 60 * 3,
                    bool closeAP = true);

void setName(const String& name);              // Set AP name
void setPass(const String& pass);              // Set AP password
void setTimeout(uint16_t timeout);             // Set connection timeout
void setAPIdleTimeout(60000);                  // 60 second AP-Idle-Timeout
void closeAP(bool close);                      // Enable/disable AP shutdown after STA connect
void onConnect(ConnectorCallback cb);          // Set successful connect callback
void onError(ConnectorCallback cb);            // Set error callback after AP starts
bool connect(const String& ssid, const String& pass = ""); // Start connection
bool tick();                                   // Call in loop()
bool connected();                              // Returns true if STA connected
bool connecting();                             // Returns true if still connecting
