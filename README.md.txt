# 🦯 Smart Blind Stick – IoT Project

An Arduino-based assistive device designed to help visually impaired individuals detect obstacles using an ultrasonic sensor and provide real-time feedback through a servo motor and buzzer.

---

## 🔧 Components Used
- Arduino Uno
- Ultrasonic Sensor (HC-SR04)
- Servo Motor (or Vibration Motor)
- Buzzer
- Breadboard and Jumper Wires
- PVC or Metal Stick Frame
- Power Source (Battery/Power Bank)
- Resistors/Transistors (if needed)

---

## ⚙️ How It Works
- Ultrasonic sensor detects obstacles.
- If object is < 50 cm, servo moves based on distance.
- If object is very close (< 20 cm), buzzer activates.
- Provides directional and proximity feedback to the user.

---

## 💻 Arduino Code Logic

```cpp
#include <Servo.h>

const int trigPin = 2;
const int echoPin = 3;
const int servoPin = 9;
const int buzzerPin = 8;

Servo myServo;
long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  myServo.attach(servoPin);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance > 5 && distance < 50) {
    int angle = map(distance, 5, 50, 180, 0);
    myServo.write(angle);
  } else {
    myServo.write(0);
  }

  if (distance > 0 && distance < 20) {
    digitalWrite(buzzerPin, HIGH);
  } else {
    digitalWrite(buzzerPin, LOW);
  }

  delay(200);
}
```

---

## 📷 Images / Diagrams
> Add your circuit diagram and photos here

---

## ✅ Future Improvements
- Add voice feedback (DFPlayer mini + speaker)
- Integrate GPS for navigation
- Mobile app connectivity (Bluetooth)

---

## 🧠 Made With
- Arduino IDE
- Basic Electronics
- Creativity + Passion!

---

## ⚠️ Note
Due to privacy, personal images or recorded voice files are not uploaded. You can create your own dataset or features as needed.
