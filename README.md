ardino uno
#include <Servo.h>

Servo entryGate;  // Servo motor for entry gate
Servo exitGate;   // Servo motor for exit gate
int entrySensor = 2;  // IR sensor at entry
int exitSensor = 3;   // IR sensor at exit
int totalSlots = 10;  // Total parking slots
int availableSlots = totalSlots;

void setup() {
  entryGate.attach(9);  // Attach entry servo motor
  exitGate.attach(10);  // Attach exit servo motor
  pinMode(entrySensor, INPUT);
  pinMode(exitSensor, INPUT);

  Serial.begin(9600);  // Initialize serial communication
  updateAvailableSlots();
}

void loop() {
  // Check if a car is at the entry
  if (digitalRead(entrySensor) == HIGH && availableSlots > 0) {
    entryGate.write(90);  // Open entry gate
    delay(2000);          // Wait for car to pass
    entryGate.write(0);   // Close gate
    availableSlots--;     // Decrement available slots
    updateAvailableSlots();
  }

  // Check if a car is at the exit
  if (digitalRead(exitSensor) == HIGH && availableSlots < totalSlots) {
    exitGate.write(90);   // Open exit gate
    delay(2000);          // Wait for car to pass
    exitGate.write(0);    // Close gate
    availableSlots++;     // Increment available slots
    updateAvailableSlots();
  }
}

void updateAvailableSlots() {
  // Display available slots on serial monitor
  Serial.print("Available slots: ");
  Serial.println(availableSlots);
}
Working Concept:
IR Sensors: Detect cars at entry and exit.
Servo Motors: Open the gate when a car is detected.
Serial Monitor: Displays the available parking slots, which can be viewed in the Arduino IDE's serial monitor.
This approach is simpler and will output the number of available slots directly to the serial monitor, avoiding the need for an LCD.
You said:
Components:
Arduino Uno
2x IR Sensors (for detecting cars at entry and exit)
2x Servo Motors (for controlling entry and exit gates)
Jumper Wires
Breadboard (optional, for easy connections)
Power Supply
Diagram Description:
IR Sensors: Connect two IR sensors for entry and exit detection.
Sensor 1 (Entry): Connect VCC to 5V, GND to GND, and the output pin to digital pin 2 on the Arduino.
Sensor 2 (Exit): Connect VCC to 5V, GND to GND, and the output pin to digital pin 3 on the Arduino.
Servo Motors: Attach two servo motors for the gates.
Servo 1 (Entry Gate): Connect the signal pin to digital pin 9.
Servo 2 (Exit Gate): Connect the signal pin to digital pin 10.
Both servos' VCC to 5V and GND to GND.
The power for the Arduino and components can come from the Arduino’s 5V pin.

Let me visualize the connections for you. Generating the diagram...



Here is the diagram for your two-way car parking system using an Arduino, IR sensors, and servo motors. Let me know if you need any further adjustments!
