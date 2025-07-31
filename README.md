# 🔥 Smoke Detector using MQ2 Sensor & Arduino Uno

A low-cost, real-time smoke detection system using MQ2 Gas Sensor, Arduino Uno, and buzzer alerts. Ideal for basic fire hazard prevention and awareness. Designed as an educational project for embedded systems and IoT integration.

---

## 🔍 Introduction

This smoke detection system uses the MQ2 sensor to monitor air quality. If smoke concentration exceeds a predefined threshold, the system triggers visual (LEDs) and audible (buzzer) alerts. The goal is to enable early fire detection and real-time alerts to minimize fire-related risks.

---

## 🎯 Objectives

- Detect smoke using MQ2 Gas Sensor.
- Alert users via buzzer and LEDs when smoke levels are high.
- Support IoT-based extension for remote monitoring and alerting.

---

## 🧰 Components Required

| Component              | Quantity |
|------------------------|----------|
| Arduino Uno            | 1        |
| MQ2 Gas Sensor         | 1        |
| Piezoelectric Buzzer   | 1        |
| LED Indicators (R/G/Y) | 3        |
| Resistors (220Ω, 10KΩ) | Few      |
| Jumper Wires           | As Needed|
| 5V Power Supply        | 1        |

---

## 🔌 Circuit Connections

### MQ2 Sensor ↔ Arduino Uno

| MQ2 Sensor Pin | Arduino Pin |
|----------------|-------------|
| VCC            | 5V          |
| GND            | GND         |
| A0             | A0          |
| D0             | D2          |

### Buzzer ↔ Arduino Uno

| Buzzer Pin   | Arduino Pin |
|--------------|-------------|
| + (Positive) | D6          |
| – (Negative) | GND         |

### LED Indicators

| LED Color | Arduino Pin |
|-----------|-------------|
| Green     | D7          |
| Yellow    | D8          |
| Red       | D9          |

---

## ⚙️ Working Principle

1. MQ2 sensor constantly measures smoke/gas concentration via its analog output.
2. Arduino reads the analog value and compares it to a threshold.
3. Based on levels:
   - **Low:** Green LED ON → Safe
   - **Moderate:** Yellow LED ON → Warning
   - **High:** Red LED + Buzzer ON → Danger
4. System provides **real-time alerts** for smoke detection.

---

## 🧾 Arduino Code

```cpp
const int gasSensor = A0;
const int buzzer = 6;
const int greenLED = 7;
const int redLED = 8;

int threshold = 300; // Adjust for environment

void setup() {
  pinMode(gasSensor, INPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(greenLED, OUTPUT);
  pinMode(redLED, OUTPUT);

  digitalWrite(buzzer, LOW);
  digitalWrite(greenLED, HIGH);
  digitalWrite(redLED, LOW);

  Serial.begin(9600);
}

void loop() {
  int gasValue = analogRead(gasSensor);
  Serial.print("Gas Sensor Value: ");
  Serial.println(gasValue);

  if (gasValue > threshold) {
    digitalWrite(buzzer, HIGH);
    digitalWrite(redLED, HIGH);
    digitalWrite(greenLED, LOW);
    Serial.println("Smoke Detected! Alarm ON");
  } else {
    digitalWrite(buzzer, LOW);
    digitalWrite(redLED, LOW);
    digitalWrite(greenLED, HIGH);
    Serial.println("Safe Environment");
  }

  delay(1000);
}
