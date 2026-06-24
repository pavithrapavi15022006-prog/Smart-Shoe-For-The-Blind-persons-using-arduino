Discription 

Smart-Shoe-For-The-Blind-persons-using-arduino
An Arduino-based smart shoe that detects obstacles using ultrasonic sensors and alerts visually impaired users through buzzer and vibration feedback for safe navigation.
Code
#define TRIG_PIN 9
#define ECHO_PIN 10
#define BUZZER 11
#define LED 13

long duration;
int distance;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER, OUTPUT);
  pinMode(LED, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  // Send ultrasonic pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);

  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);

  digitalWrite(TRIG_PIN, LOW);

  // Read echo pulse
  duration = pulseIn(ECHO_PIN, HIGH);

  // Calculate distance in cm
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  // Obstacle detection
  if (distance > 0 && distance <= 30) {
    digitalWrite(BUZZER, HIGH);
    digitalWrite(LED, HIGH);
  }
  else {
    digitalWrite(BUZZER, LOW);
    digitalWrite(LED, LOW);
  }

  delay(100);
}
