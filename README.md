Welcome to **Gecko's Temperature Sensor Build**! This project is all about using a **DS18B20 temperature sensor** and a 16x2 **LCD screen** to display temperature readings, for **Tails the Gecko** 🦎! 

This fun project is a great way to monitor the temperature of your little reptilian friend’s home and keep their habitat just the right temperature, especially during the colder climate outside! ❄️

## 🔧 What You'll Need

- **Arduino Uno** 🛠️
- **DS18B20 Temperature Sensor** 🌡️
- **16x2 LCD Screen** (No I2C needed!) 💻
- **5kΩ Potentiometer** for adjusting the contrast on the LCD 🔧
- **4.7kΩ Resistor** for the sensor 🏷️
- **Tails the Crested Gecko** 🦎 (optional)

## 📸 Some pics! 

Heres some pics of what I've been working on!

### 🖼️ Hand-Drawn Circuit Diagram
Take a look at the **circuit diagram** that shows how everything is connected together. Drawn by hand with love, of course!
![Circuit Diagram](images/circuit_diagrams.jpg)

### 🖼️ Soldered Pins on the Back of the LCD
A close-up of the **LCD's soldered pins** showing all the connections I made. Was my first real soldering project so it's not the prettiest, but it gets the job done!
![LCD Soldered Pins](images/lcd_soldered_pins.jpg)

### 🎥 Temperature Test Video
Check out this **video of the temperature sensor** in action! Watch as the temperature readings are displayed on the LCD screen in real time.
[Watch the Sensor Test Video](images/sensor_reading_test.mp4)

### 🦎 Meet Tails the Gecko!
And of course, here’s **Tails**, the crested gecko that inspired this whole project!
![Tails the Gecko](images/tails_the_gecko.jpg)


## 🧑‍💻 Code
Here’s a very simple Arduino sketch that powers the entire setup! It reads the temperature from the DS18B20 sensor and displays it on the LCD.

```cpp
#include <OneWire.h>
#include <DallasTemperature.h>
#include <LiquidCrystal.h>

#define ONE_WIRE_BUS 7  //  DS18B20 data line
LiquidCrystal geckoLCD(12, 11, 5, 4, 3, 2); //Using LCD pins RS, E, D4-D7

OneWire oneWire(ONE_WIRE_BUS); //Controls sensor data
DallasTemperature sensors(&oneWire);

void setup() {
  Serial.begin(9600);        // Serial Monitor
  sensors.begin();           // DS18B20 sensor
  geckoLCD.begin(16, 2);     // 16x2 LCD screen
  geckoLCD.clear();          // Clear the LCD screen
}

void loop() {
  sensors.requestTemperatures();      // Command to get temperature
  float temperatureC = sensors.getTempCByIndex(0);  // Get temperature in Celsius

  geckoLCD.clear();                   // Clear the LCD for new readings
  geckoLCD.setCursor(0, 0);           // Set cursor to first row, first column
  geckoLCD.print("Temp: ");
  geckoLCD.print(temperatureC);
  geckoLCD.print(" C");
  

 //Convert to F
  float temperatureF = sensors.toFahrenheit(temperatureC);
  geckoLCD.setCursor(0, 1);           // Set cursor to second row, first column
  geckoLCD.print("Temp: ");
  geckoLCD.print(temperatureF);
  geckoLCD.print(" F");

  delay(1000);                        // Wait 1 second before next reading
}


 
💡 How It Works

Temperature Sensor: The DS18B20 measures the temperature inside the tank, ensuring that Tails the Gecko stays warm this winter! 🐍

LCD Display: The LCD screen shows the temperature in Celsius and Fahrenheit, updating every second, so you will always know what’s going on in the gecko habitat. 🌡️

Code: The Arduino code is straightforward—read the sensor, print the value to the screen, and repeat! ⚡



📄 License

This project is open-source and licensed under the MIT License. Feel free to adapt it and create your own temperature-monitoring projects!



Thank you for checking out my fun little temperature sensor project! 🦎 If you have any questions, want to share your own version, or just want to talk about geckos, feel free to reach out.
