int ea = 12;
int eb = 13;
int in1 = 26;
int in2 = 25;
int in3 = 33;
int in4 = 32;
int s1 = 2;
int s2 = 4;
int s4 = 5;
int s5 = 18;

void setup() {
  // กำหนดพินสำหรับมอเตอร์และเซนเซอร์เป็น output/input
  pinMode(ea, OUTPUT);
  pinMode(eb, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  
  pinMode(s1, INPUT);
  pinMode(s2, INPUT);
  pinMode(s4, INPUT);
  pinMode(s5, INPUT);

  // กำหนดความเร็วเริ่มต้น
  analogWrite(ea, 255);
  analogWrite(eb, 255);
}

void loop() {
  int sensor1 = digitalRead(s1);
  int sensor2 = digitalRead(s2);
  int sensor4 = digitalRead(s4);
  int sensor5 = digitalRead(s5);

  // ถ้าเซนเซอร์ทั้ง s2 และ s4 จับเส้นได้แสดงว่ารถอยู่ตรงกลาง
  if (sensor2 == LOW && sensor4 == LOW) {
    forward();
  }
  // ถ้าเซนเซอร์ขวา (s4 หรือ s5) จับเส้นได้ รถจะเลี้ยวขวา
  else if (sensor4 == LOW || sensor5 == LOW) {
    turnRight();
  }
  // ถ้าเซนเซอร์ซ้าย (s1 หรือ s2) จับเส้นได้ รถจะเลี้ยวซ้าย
  else if (sensor2 == LOW || sensor1 == LOW) {
    turnLeft();
  }
  // กรณีที่ไม่พบเส้น (เซนเซอร์ทั้งหมดเป็น HIGH)
  else {
    stopMotors();
  }
}

void forward() {
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
}

void turnRight() {
  digitalWrite(in1, LOW);
  digitalWrite(in2, HIGH);
  digitalWrite(in3, HIGH);
  digitalWrite(in4, LOW);
}

void turnLeft() {
  digitalWrite(in1, HIGH);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, HIGH);
}

void stopMotors() {
  digitalWrite(in1, LOW);
  digitalWrite(in2, LOW);
  digitalWrite(in3, LOW);
  digitalWrite(in4, LOW);
}
