## Soil Moisture Monitoring with NodeMCU
This project uses a NodeMCU microcontroller to read the soil moisture level through an analog soil moisture sensor and display the value in percentage on the serial monitor. This is useful for monitoring the moisture levels in soil to assist with plant watering systems.

## Table of Contents
Introduction
Hardware Requirements
Circuit Diagram
Code Explanation
Usage
Troubleshooting

## Introduction
This project reads the soil moisture using the analog pin of a NodeMCU. The output is displayed as a percentage, where 0% represents fully dry soil and 100% represents fully saturated soil.

## Hardware Requirements
NodeMCU (ESP8266)
Soil Moisture Sensor (Analog output)
Jumper wires
Breadboard

## Circuit Diagram
Here's how you should connect the soil moisture sensor to the NodeMCU:

VCC of the sensor → 3.3V on NodeMCU
GND of the sensor → GND on NodeMCU
Analog Output of the sensor → A0 on NodeMCU
Note: Ensure that the sensor's analog output doesn't exceed 1V, as NodeMCU’s A0 pin can only handle up to 1V.

## Code Explanation
The following code reads the analog value from the sensor, converts it into a percentage, and prints it to the serial monitor.

cpp
Copy code
const int sensor_pin = A0;  /* Connect Soil moisture analog sensor pin to A0 of NodeMCU */

void setup() {
  Serial.begin(9600);  /* Initialize serial communication at a baud rate of 9600 */
}

void loop() {
  float moisture_percentage = 0.00;

  // Read analog value from the soil moisture sensor
  moisture_percentage = (100.00 - ((analogRead(sensor_pin) / 1023.00) * 100.00));

  // Print the moisture percentage to the Serial Monitor
  Serial.print("Soil Moisture (in Percentage) = ");
  Serial.print(moisture_percentage);
  Serial.println("%");

  delay(1000);  // Delay for 1 second before reading again
}

Breakdown of the Code
Pin Definition: sensor_pin is set to A0, where the soil moisture sensor is connected.
Serial Communication: Serial.begin(9600) starts serial communication to display the results on the serial monitor.
Reading Sensor Data: analogRead(sensor_pin) reads the analog value from the sensor (0-1023).
Conversion to Percentage: The value is scaled to a percentage:
moisture_percentage
=
100
−
(
analogRead
1023
)
×
100
moisture_percentage=100−( 
1023
analogRead
​
 )×100
This assumes 0 corresponds to 100% moisture and 1023 corresponds to 0% moisture.
Output: The moisture percentage is printed to the serial monitor every second.

## Usage
Upload the Code: Upload the code to your NodeMCU using the Arduino IDE.
Open Serial Monitor: After uploading, open the Serial Monitor (Ctrl + Shift + M) and set the baud rate to 9600.
Check Output: The moisture level of the soil will be printed every second.

## Troubleshooting
Incorrect Readings: If the soil moisture is constantly reading 0% or giving incorrect values:
Ensure the sensor is properly connected.
Make sure the sensor's output voltage does not exceed 1V, which is the limit for NodeMCU's analog pin.
Serial Monitor Not Working: Ensure the correct COM port and baud rate (9600) are selected in the Arduino IDE.
