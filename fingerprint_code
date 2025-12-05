#include <Arduino.h>
#include <Adafruit_Fingerprint.h>

// UART2 for Fingerprint Sensor (R307)
HardwareSerial serialPort(2);   // UART2

Adafruit_Fingerprint finger = Adafruit_Fingerprint(&serialPort);

// ------------------------------------------------------
// SETUP
// ------------------------------------------------------
void setup() {
  Serial.begin(115200);
  delay(1000);

  Serial.println("\nFingerprint Sensor - Multi-ID Enroll & Match");

  // UART2 GPIO (RX = 16, TX = 17)
  serialPort.begin(57600, SERIAL_8N1, 16, 17);

  finger.begin(57600);
  delay(5);

  if (finger.verifyPassword()) {
    Serial.println("Fingerprint sensor detected!");
  } else {
    Serial.println("Fingerprint sensor NOT found!");
    while (1) delay(1);
  }

  finger.getTemplateCount();
  Serial.print("Sensor contains ");
  Serial.print(finger.templateCount);
  Serial.println(" templates");

  Serial.println("Type e<ID> to enroll a fingerprint. (Example: e1, e2, e3)");
}

// ------------------------------------------------------
// LOOP
// ------------------------------------------------------
void loop() {

  // Check if user typed "e<ID>" in Serial Monitor
  if (Serial.available()) {
    char ch = Serial.read();
    if (ch == 'e') {
      while (!Serial.available());  // wait for the ID
      int id = Serial.parseInt();

      if (id >= 1 && id <= 127) {
        Serial.print("Starting enrollment for ID: ");
        Serial.println(id);
        enrollFinger(id);
      } else {
        Serial.println("Invalid ID! Use 1–127.");
      }
    }
  }

  // Continuously check matching
  getFingerprintID();
  delay(500);
}

// ------------------------------------------------------
// ENROLL FUNCTION
// ------------------------------------------------------
uint8_t enrollFinger(uint8_t id) {
  int p = -1;

  Serial.println("Place your finger on the sensor...");

  // 1st Scan
  while (p != FINGERPRINT_OK) {
    p = finger.getImage();
    if (p == FINGERPRINT_NOFINGER) continue;
    if (p != FINGERPRINT_OK) {
      Serial.println("Failed to capture first image.");
      return p;
    }
  }

  p = finger.image2Tz(1);
  if (p != FINGERPRINT_OK) {
    Serial.println("Failed to convert first image.");
    return p;
  }

  Serial.println("First scan complete. Remove finger...");
  delay(2000);

  // Wait for removal
  while (finger.getImage() != FINGERPRINT_NOFINGER);

  // 2nd Scan
  Serial.println("Place the SAME finger again...");
  p = -1;
  while (p != FINGERPRINT_OK) {
    p = finger.getImage();
    if (p == FINGERPRINT_NOFINGER) continue;
    if (p != FINGERPRINT_OK) {
      Serial.println("Failed to capture second image.");
      return p;
    }
  }

  p = finger.image2Tz(2);
  if (p != FINGERPRINT_OK) {
    Serial.println("Failed to convert second image.");
    return p;
  }

  // Create model
  p = finger.createModel();
  if (p != FINGERPRINT_OK) {
    Serial.println("Failed to create model.");
    return p;
  }

  // Store model
  p = finger.storeModel(id);
  if (p == FINGERPRINT_OK) {
    Serial.println("Fingerprint enrolled successfully!");
  } else {
    Serial.println("Failed to store fingerprint.");
  }

  return p;
}

// ------------------------------------------------------
// MATCH FUNCTION
// ------------------------------------------------------
int getFingerprintID() {
  int p = finger.getImage();
  if (p != FINGERPRINT_OK) return -1;

  p = finger.image2Tz();
  if (p != FINGERPRINT_OK) return -1;

  p = finger.fingerSearch();

  if (p == FINGERPRINT_OK) {
    Serial.println("Fingerprint MATCH Found!");
    Serial.print("ID: ");
    Serial.print(finger.fingerID);
    Serial.print("  Confidence: ");
    Serial.println(finger.confidence);
    return finger.fingerID;
  }
  else if (p == FINGERPRINT_NOTFOUND) {
    Serial.println("No match found.");
  }
  else {
    Serial.println("Communication error.");
  }

  return -1;
}
