# Smart-Blind-Stick-IoT
An Arduino-based smart stick for visually impaired people using ultrasonic sensor and servo motor for obstacle detection and feedback.

# 🦯 Smart Blind Stick – IoT Based Assistive Device

> *"A small step in code, a giant leap in someone's independence."*

This project is a **beginner-friendly IoT solution** designed and built as part of my journey as a Computer Science engineering student learning **IoT development**. The Smart Blind Stick uses **ultrasonic sensing and microcontroller logic** to help visually impaired individuals detect nearby obstacles with vibration or sound feedback.

---

## 📚 Why This Project?

As a student exploring the real-world power of IoT, I wanted to:
- Work hands-on with **Arduino and sensors**
- Solve a **real-life social problem**
- Go beyond theory and build something that **can truly help people**

This stick helps detect obstacles ahead and gives feedback to the user using a buzzer and servo movement.

---

## 🔧 Components Used

| Component | Quantity | Purpose |
|----------|----------|---------|
| Arduino Uno | 1 | Main controller |
| Ultrasonic Sensor (HC-SR04) | 1 | Distance measurement |
| Servo Motor / Vibration Motor | 1 | Physical feedback |
| Buzzer | 1 | Sound alert |
| Jumper Wires + Breadboard | -- | Wiring |
| PVC/Metal Frame | 1 | Stick body |
| Power Bank or Battery Pack | 1 | Power supply |

---

## 💡 How It Works

1. **Ultrasonic sensor** sends a pulse forward.
2. It calculates **distance** to the nearest object.
3. If an object is:
   - **< 50 cm** → Servo rotates (or vibrates)
   - **< 20 cm** → Buzzer activates
4. **Real-time feedback** helps the blind user safely detect nearby obstacles.

---

## 💻 Code Logic (Arduino)

> Full code is available in the `Smart-Blind-Stick.ino` file

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

## 🌍 Real-World Application

- **Visually Impaired Assistance:** Helps navigate obstacles with sensory feedback
- **Smart Mobility Devices:** Can be added to wheelchairs, walkers, or smart shoes
- **Elderly Care:** Assisting seniors with limited visibility
- **Obstacle Detection in Robotics**

---

## 🚀 Future Enhancements

✅ These are features I plan to add as I learn more:

- 🎤 Voice Feedback using DFPlayer Mini  
- 📍 GPS Tracker for location sharing  
- 📱 Bluetooth or Wi-Fi Module for app integration  
- 🔋 Battery optimization & sleep mode  
- 💡 AI-based Object Recognition (future goal!)

---

## 🎓 My Learning Journey

This project was part of my **hands-on learning** during my Computer Science Engineering course. I wanted to explore how **coding, electronics, and real-world problems** come together in IoT.

Through this project, I learned:
- Arduino programming
- Sensor data handling
- Real-time decision making
- Basic embedded systems wiring
- Thinking beyond the screen and into the real world 🌐

---

## 🧠 Built With

- Arduino UNO & IDE  
- HC-SR04 Ultrasonic Sensor  
- Servo Motor / Buzzer  
- Passion + Curiosity to Learn IoT 💙

---

## 📷 Project Photos

![smartblindstick_iot](https://github.com/user-attachments/assets/2e2245a2-37e3-458a-8be4-983477ead97c)


![Smart Blind Stick](https://github.com/RakshithaMeleyyanavar/Smart-Blind-Stick-IoT/raw/main/circuit.jpg)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE)

---

## 🙋‍♀️ About Me

**Rakshitha Meleyyanavar**  
2nd Year Computer Science Engineering Student  
🔍 Learning Java, AI, and IoT to build a better tech-driven world.  

---

> 🌱 _"I may be just starting, but I'm growing into an engineer who builds for people."_

