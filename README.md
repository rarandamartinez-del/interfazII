# interfazII

##### hola mundo

##### LED intermitente (Blink)
```js
void setup() {  // Configuración inicial (ej: pines como entrada/salida)
  pinMode(13, OUTPUT);  // Pin 13 como salida
}

void loop() {   // Se repite infinitamente
  digitalWrite(13, HIGH);  // Encender LED
  delay(100);             // Esperar 1 segundo
  digitalWrite(13, LOW);   // Apagar LED
  delay(100);             // Esperar 1 segundo
  
    digitalWrite(12, HIGH);  // Encender LED
  delay(500);             // Esperar 1 segundo
  digitalWrite(12, LOW);   // Apagar LED
  delay(500);             // Esperar 1 segundo

     digitalWrite(11, HIGH);  // Encender LED
  delay(1000);             // Esperar 1 segundo
  digitalWrite(11, LOW);   // Apagar LED
  delay(1000);             // Esperar 1 segundo

}
```

##### Control por Pulsador
```js
void setup() {
  pinMode(2, INPUT);  // Botón como entrada
  pinMode(13, OUTPUT);
}
void loop() {
  if (digitalRead(2) == HIGH) {  // Si se presiona el botón
    digitalWrite(13, LOW);
  } else {
    digitalWrite(13, HIGH);
  }
}
```

##### LED con potenciometro
```js
void setup() {
  pinMode(2, INPUT);  // Botón como entrada
  pinMode(13, OUTPUT);
}
void loop() {
  if (digitalRead(2) == HIGH) {  // Si se presiona el botón
    digitalWrite(13, LOW);
  } else {
    digitalWrite(13, HIGH);
  }
}
```
