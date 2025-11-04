// Ultrasonic Sensor - Detect Objects Rolling Past
// HC-SR04 with Arduino
// Lab #3

const int TRIG_PIN = 9;
const int ECHO_PIN = 10;

long duration;
float distanceCm;
bool objectPresent = false;

void setup() {
  Serial.begin(9600);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
}

void loop() {
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  duration = pulseIn(ECHO_PIN, HIGH);
  distanceCm = duration * 0.034 / 2;

  if (distanceCm < 10 && !objectPresent) {
    Serial.println("Object Detected & Present");
    objectPresent = true;
  } 
  else if (distanceCm >= 10 && objectPresent) {
    Serial.println("Detected Object Is Gone");
    objectPresent = false;
  } 
  else if (!objectPresent) {
    Serial.println("Waiting To Detect An Object");
  }

  delay(500);
}
