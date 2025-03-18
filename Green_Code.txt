#include <DHT.h>

#define DHT_PIN 2        // Digital pin to which DHT11 sensor is connected
#define LDR_PIN 3        // Pin to which LDR sensor is connected
#define MOISTURE_PIN A0  // Pin to which moisture sensor is connected
#define DHT_TYPE DHT11   // DHT sensor type, change it to DHT22 if you are using DHT22
#define WATER_RELAY_PIN 4 // Relay control pin for water pump
#define SHADE_RELAY_PIN 5 // Relay control pin for shade motor
#define FAN_RELAY_PIN 6   // Relay control pin for fan
#define MOISTURE_THRESHOLD 800 // Moisture threshold for turning on the water pump
#define LDR_THRESHOLD 800      // LDR threshold for activating the shade motor
#define TEMPERATURE_THRESHOLD 33 // Temperature threshold for turning on the fan

DHT dht(DHT_PIN, DHT_TYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("Sensor Readings Test");
  dht.begin();
  pinMode(WATER_RELAY_PIN, OUTPUT);
  pinMode(SHADE_RELAY_PIN, OUTPUT);
  pinMode(FAN_RELAY_PIN, OUTPUT);
}

void loop() {
  delay(2000);  // Wait for 2 seconds between readings

  // Read temperature and humidity from the DHT sensor
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();

  // Read analog values from LDR and moisture sensors
  int ldrValue = analogRead(LDR_PIN);
  int moistureValue = analogRead(MOISTURE_PIN);

  // Print temperature matrix
  Serial.println("Temperature Matrix:");
  printTemperatureMatrix(temperature);

  // Print the average temperature
  float averageTemperature = calculateAverageTemperature(temperature);
  Serial.print("Average Temperature: ");
  Serial.println(averageTemperature);

  // Print LDR value
  Serial.print("LDR Value: ");
  Serial.println(ldrValue);

  // Print moisture value
  Serial.print("Moisture Value: ");
  Serial.println(moistureValue);

  // Check if moisture level is above the threshold (indicating very dry soil)
  if (moistureValue > MOISTURE_THRESHOLD) {
    // Turn on the water pump for 5 seconds
    Serial.println("Turning on the water pump");
    digitalWrite(WATER_RELAY_PIN, HIGH);
    delay(5000); // Run the pump for 5 seconds

    // Turn off the water pump
    Serial.println("Turning off the water pump");
    digitalWrite(WATER_RELAY_PIN, LOW);
  }

  // Check if LDR value is above the threshold for activating the shade motor
  if (ldrValue > LDR_THRESHOLD) {
    // Turn on the shade motor relay for 5 seconds
    Serial.println("Activating the shade motor");
    digitalWrite(SHADE_RELAY_PIN, HIGH);
    delay(5000); // Run the motor for 5 seconds

    // Turn off the shade motor relay
    Serial.println("Deactivating the shade motor");
    digitalWrite(SHADE_RELAY_PIN, LOW);
  }

  // Check if temperature is above the threshold for turning on the fan
  if (temperature > TEMPERATURE_THRESHOLD) {
    // Turn on the fan relay
    Serial.println("Turning on the fan");
    digitalWrite(FAN_RELAY_PIN, HIGH);
  } else {
    // Turn off the fan relay
    Serial.println("Turning off the fan");
    digitalWrite(FAN_RELAY_PIN, LOW);
  }

  // Additional code can be added here for further functionality

  // Delay before the next reading
  delay(2000); // Adjust as needed
}

void printTemperatureMatrix(float temperature) {
  // Display the temperature in a 3x3 matrix
  for (int i = 0; i < 3; ++i) {
    for (int j = 0; j < 3; ++j) {
      Serial.print(int(temperature));
      Serial.print(" ");
    }
    Serial.println();
  }
}

float calculateAverageTemperature(float temperature) {
  // For simplicity, the average temperature is considered as the integer part of the temperature
  return int(temperature);
}
