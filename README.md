# robot-seguidor-de-linea-
Robot seguidor de linea con ayuda de dos sensores infrarrojos, arduino uno, un controlador de sensores L298, 
codigo Arduino uno

// Pines de sensores
const int sensorIzquierdo = 3;
const int sensorDerecho  = 4;

// Pines del controlador de motores
const int IN1 = 9;
const int IN2 = 8;
const int IN3 = 7;
const int IN4 = 6;
const int ENA = 10;
const int ENB = 5;

void setup() {
  // Configurar sensores como entrada
  pinMode(sensorIzquierdo, INPUT);
  pinMode(sensorDerecho, INPUT);

  // Configurar pines de motor como salida
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);

  // Detener motores al iniciar
  detener();
}

void loop() {
  // Leer sensores
  int izquierdo = digitalRead(sensorIzquierdo);  // HIGH = negro, LOW = blanco
  int derecho = digitalRead(sensorDerecho);

  // Motor izquierdo (controlado por sensor izquierdo)
  if (izquierdo == LOW) {
    motorIzquierdoAdelante();  // blanco → avanza
  } else {
    detenerMotorIzquierdo();   // negro → se detiene
  }

  // Motor derecho (controlado por sensor derecho)
  if (derecho == LOW) {
    motorDerechoAdelante();    // blanco → avanza
  } else {
    detenerMotorDerecho();     // negro → se detiene
  }
}

// FUNCIONES DE CONTROL DE MOTORES

void motorDerechoAdelante() {
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  analogWrite(ENA, 150);  // Velocidad motor derecho
}

void motorIzquierdoAdelante() {
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
  analogWrite(ENB, 150);  // Velocidad motor izquierdo
}

void detenerMotorDerecho() {
  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  analogWrite(ENA, 0);
}

void detenerMotorIzquierdo() {
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);
  analogWrite(ENB, 0);
}

void detener() {
  detenerMotorDerecho();
  detenerMotorIzquierdo();
}
