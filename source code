#include <Wire.h>
#include <hd44780.h>
#include <hd44780ioClass/hd44780_I2Cexp.h>
#include <DHT.h>
#include "BluetoothSerial.h"

BluetoothSerial SerialBT;

#define GAS_PIN 34
#define LED_PIN 18
#define BUZZER_PIN 19

#define DHTPIN 4
#define DHTTYPE DHT11

hd44780_I2Cexp lcd;
DHT dht(DHTPIN, DHTTYPE);

// ===== Adjustable Gas Threshold =====
int gasThreshold = 350;

unsigned long previousMillis = 0;
const long interval = 1000;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("GasSafetyESP32");

  pinMode(LED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  lcd.begin(16, 2);
  dht.begin();

  lcd.setCursor(0,0);
  lcd.print("Gas Monitor");
  delay(2000);
  lcd.clear();
}

void loop() {

  unsigned long currentMillis = millis();

  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;

    int gasValue = analogRead(GAS_PIN);
    float temp = dht.readTemperature();
    float hum = dht.readHumidity();

    String status;

    // ===== Gas Level Classification =====
    if (gasValue < gasThreshold) {
      status = "SAFE";
      digitalWrite(LED_PIN, LOW);
      digitalWrite(BUZZER_PIN, LOW);
    }
    else if (gasValue >= gasThreshold && gasValue <= gasThreshold + 300) {
      status = "MODERATE";
      digitalWrite(LED_PIN, HIGH);
      digitalWrite(BUZZER_PIN, LOW);
    }
    else {
      status = "DANGER";
      digitalWrite(LED_PIN, HIGH);
      digitalWrite(BUZZER_PIN, HIGH);
    }

    // ===== LCD Display =====
    lcd.setCursor(0,0);
    lcd.print("G:");
    lcd.print(status);
    lcd.print(" V:");
    lcd.print(gasValue);
    lcd.print("   ");

    lcd.setCursor(0,1);
    lcd.print("T:");
    lcd.print(temp);
    lcd.print(" H:");
    lcd.print(hum);
    lcd.print("   ");

    // ===== Bluetooth Message =====
    SerialBT.print("Gas Status: ");
    SerialBT.print(status);
    SerialBT.print(" | Value: ");
    SerialBT.print(gasValue);
    SerialBT.print(" | Threshold: ");
    SerialBT.print(gasThreshold);
    SerialBT.print(" | Temp: ");
    SerialBT.print(temp);
    SerialBT.print("C | Hum: ");
    SerialBT.println(hum);

    Serial.println(gasValue);
  }
}
