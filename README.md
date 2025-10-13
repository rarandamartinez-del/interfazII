# interfazII

##### Ejercicio n°1 hola mundo
```js
void setup() {
  Serial.begin(9600); // Inicia la comunicación serie a 9600 bps
  Serial.println("Hola, Mundo!"); // Envía "Hola, Mundo!" al monitor serial
}

void loop() {
}
```
##### Ejercicio n°2 LED intermitente (Blink)
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
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/led%20parpadeante.png"/>

##### Ejercicio n°3 Control por Pulsador
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
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/led%20pulsador.png"/>

##### Ejercicio n°4 LED con potenciometro
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
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/led%20potenciometro.png"/>

##### Ejercicio n°5 Semáforo
```js
int LED_1 = 6;  // Luz roja autos
int LED_2 = 7;  // Luz amarilla autos
int LED_3 = 8;  // Luz verde autos
int LED_4 = 9;  // Luz verde peatones
int LED_5 = 10; // Luz roja peatones

void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
}

void loop() {
  // 🚦 Fase 1: Autos en verde, peatones en rojo
  digitalWrite(LED_1, LOW);   // Rojo autos apagado
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado
  digitalWrite(LED_3, HIGH);  // Verde autos encendido
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 2: Amarillo autos, peatones siguen en rojo
  digitalWrite(LED_3, LOW);   // Verde autos apagado
  digitalWrite(LED_2, HIGH);  // Amarillo autos encendido
  delay(2000); // 2 segundos
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado

   // 🚦 Fase 3: Rojo autos, verde peatones
  digitalWrite(LED_1, HIGH);  // Rojo autos encendido
  digitalWrite(LED_5, LOW);   // Rojo peatones apagado
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(5000);             // Esperar 1 segundo
  digitalWrite(LED_4, LOW);   // Apagar LED
  delay(500);             // Esperar 1 segundo
   digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(500);             // Esperar 1 segundo
  digitalWrite(LED_4, LOW);   // Apagar LED
  delay(500);             // Esperar 1 segundo
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(500);             // Esperar 1 segundo


  // 🚦 Fase 4: Rojo autos, rojo peatones (tiempo intermedio)
  //digitalWrite(LED_4, LOW);   // Verde peatones apagado
  //digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  //delay(2000); // 2 segundos
}
```
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/Semaforo.png"/>

##### Ejercicio n°6 Arduino botón 
```js
PROCESSING:

import processing.serial.*;

Serial myPort;
ArrayList<PVector> circles; 

void setup() {
  size(1920, 1080);
  background(0);
  
  // Ajusta el nombre del puerto según tu Arduino
  println(Serial.list());
  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort = new Serial(this, Serial.list()[0], 9600);
  
  circles = new ArrayList<PVector>();
}

void draw() {
  //background(0);
  
  // Dibujar círculos almacenados
  fill(0, 0, 0);
  //noStroke();
  stroke(255, 0, 0);
  for (PVector c : circles) {
    ellipse(c.x, c.y, 30, 30);
  }
  
  // Revisar si llega algo de Arduino
  if (myPort.available() > 0) {
    String val = myPort.readStringUntil('\n');
    if (val != null) {
      val = trim(val);
      if (val.equals("1")) {
        // Cada vez que se aprieta el botón, agregar un círculo en posición aleatoria
        circles.add(new PVector(random(width), random(height)));
      }
    }
  }
}
```
```js
ARDUINO:

int buttonPin = 2;       // Pin del botón
int potPin = A0;         // Pin del potenciómetro
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    int potValue = analogRead(potPin);   // 0 - 1023
    Serial.print("BTN,");     // etiqueta para Processing
    Serial.println(potValue); // mando el valor junto con el evento
    delay(200);               // debounce simple
  }
}
```

##### Ejercicio n°7 Arduino botón 
```js
PROCESSING:
import processing.serial.*;

Serial myPort;
ArrayList<CircleData> circles; 

void setup() {
  size(1200, 720);
  background(0);
  
  // Ajusta el puerto según tu Arduino
  println(Serial.list());
  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort = new Serial(this, Serial.list()[0], 9600);
  
  circles = new ArrayList<CircleData>();
}

void draw() {
  //background(0);
  
  // Dibujar todos los círculos guardados
  //fill(0, 150, 255);
  //noStroke();
  fill(0, 0, 0);
  stroke(255, 0, 0);
  for (CircleData c : circles) {
    ellipse(c.x, c.y, c.size, c.size);
  }
  
  // Leer datos de Arduino
  if (myPort.available() > 0) {
    String val = myPort.readStringUntil('\n');
    if (val != null) {
      val = trim(val);
      if (val.startsWith("BTN")) {
        // Extraer el valor del potenciómetro
        String[] parts = split(val, ',');
        if (parts.length == 2) {
          float potVal = float(parts[1]);
          float circleSize = map(potVal, 0, 1023, 10, 100); // tamaño 10-100 px
          circles.add(new CircleData(random(width), random(height), circleSize));
        }
      }
    }
  }
}
```
```js
ARDUINO:
int buttonPin = 2;       // Pin del botón
int potPin = A0;         // Pin del potenciómetro
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    int potValue = analogRead(potPin);   // 0 - 1023
    Serial.print("BTN,");     // etiqueta para Processing
    Serial.println(potValue); // mando el valor junto con el evento
    delay(200);               // debounce simple
  }
}
```
##### Ejercicio n°8 Led par/impar
```js
int leds[] = {2, 3, 4, 5}; // Creamos un arreglo con los pines donde van conectados los LEDs

void setup() {
  // Esta función corre solo una vez al iniciar Arduino
  for (int i = 0; i < 4; i++) {         // Recorre el arreglo desde i = 0 hasta i = 3
    pinMode(leds[i], OUTPUT);           // Configura cada pin del arreglo como salida (para controlar LEDs)
  }
}

void loop() {
  // Esta función corre en bucle infinito
  for (int i = 0; i < 4; i++) {         // Recorre los 4 LEDs, uno por uno
    if (i % 1 == 0) {                   // Si el índice es par (0, 2)...
      digitalWrite(leds[i], HIGH);      // Enciende el LED correspondiente
    } else {                            // Si el índice es impar (1, 3)...
      digitalWrite(leds[i], LOW);       // Apaga el LED correspondiente
    }
    delay(500);                         // Espera 0,5 segundos antes de pasar al siguiente
  }
}
```
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/led%20par%20impar.png"/>

##### Ejercicio n°9 
```js
void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial
}

void loop() {
  for (int i = 0; i < 5; i++) {
    Serial.println(i);  // imprime 0,1,2,3,4
    delay(500);         // medio segundo entre cada número
  }
}
```
```js

int valor;  // aquí guardaremos la lectura del sensor

void setup() {
  Serial.begin(9600);   // Inicia la comunicación serial
}

void loop() {
  valor = analogRead(A0);   // lee el pin analógico A0

  if (valor < 200) {
    Serial.println("Muy bajo");
  } else if (valor < 500) {
    Serial.println("Medio");
  } else {
    Serial.println("Alto");
  }

  delay(500); // medio segundo entre lecturas
}
```

##### Ejercicio n°10 botonera  
```js
// Importamos librería para comunicación serial
import processing.serial.*;
// Importamos librería Minim para manejar audio
import ddf.minim.*;

// Declaramos el objeto serial para comunicarnos con Arduino
Serial myPort;
// Objeto principal de Minim
Minim minim;
// Array de reproductores de audio (3 pistas)
AudioPlayer[] players;
// Variable para guardar el índice de la pista que está sonando
int currentTrack = -1;  // -1 significa que no hay pista activa al inicio

void setup() {
  size(400, 200); // Ventana de 400x200 píxeles
  
  // --- Configuración del puerto serial ---
  printArray(Serial.list()); // Muestra en consola la lista de puertos disponibles
  myPort = new Serial(this, Serial.list()[0], 9600); // Abrimos el primer puerto de la lista a 9600 baudios
  
  // --- Configuración de audio ---
  minim = new Minim(this); // Inicializamos Minim
  players = new AudioPlayer[3]; // Creamos un array de 3 reproductores
  
  // Cargamos los 3 archivos de audio desde la carpeta "data"
  players[0] = minim.loadFile("wa.mp3", 2048); 
  players[1] = minim.loadFile("we.mp3", 2048); 
  players[2] = minim.loadFile("wi.mp3", 2048); 
}

void draw() {
  background(0); // Fondo negro
  fill(255);     // Color blanco para el texto
  textSize(16);  // Tamaño del texto
  
  // Mostramos en pantalla qué botón está activo
  text("Botón actual: " + (currentTrack == -1 ? "ninguno" : currentTrack), 20, 40);
}

void serialEvent(Serial myPort) {
  // Leemos la cadena que llega desde Arduino hasta el salto de línea
  String inString = trim(myPort.readStringUntil('\n'));
  
  // Si no llega nada, salimos
  if (inString == null) return;

  // --- Si el mensaje recibido empieza con "B" significa que es un botón ---
  if (inString.startsWith("B")) {
    // Quitamos la letra "B" y separamos el mensaje en partes (ejemplo "0:0")
    String[] parts = split(inString.substring(1), ':');
    
    // Si realmente recibimos dos partes (índice y estado)
    if (parts.length == 2) {
      int buttonIndex = int(parts[0]); // Número del botón (0,1,2)
      int state = int(parts[1]);       // Estado del botón (0 = presionado, 1 = suelto)
      
      // Si el botón fue presionado (LOW = 0 en Arduino)
      if (state == 0) { 
        playTrack(buttonIndex); // Llamamos a la función para reproducir la pista correspondiente
      }
    }
  }
}

// --- Función que reproduce una pista según el botón ---
void playTrack(int index) {
  // Si ya había una pista sonando, la pausamos y la rebobinamos al inicio
  if (currentTrack != -1 && players[currentTrack].isPlaying()) {
    players[currentTrack].pause();
    players[currentTrack].rewind();
  }
  
  // Reproducimos en bucle la pista seleccionada
  players[index].loop();
  
  // Actualizamos la variable para saber cuál es la pista activa
  currentTrack = index;
}
```
<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/Botonera.png"/>

##### led rgb con potenciometro

```js
// Definición de pines para los colores del LED RGB
const int pinRojo = 9;   // Pin PWM para el color Rojo
const int pinVerde = 10; // Pin PWM para el color Verde
const int pinAzul = 11;  // Pin PWM para el color Azul

// Definición de pines analógicos para los Potenciómetros
const int potRojo = A0;  // Potenciómetro para el Rojo
const int potVerde = A1; // Potenciómetro para el Verde
const int potAzul = A2;  // Potenciómetro para el Azul

void setup() {
  // Configura los pines del LED como salidas
  pinMode(pinRojo, OUTPUT);
  pinMode(pinVerde, OUTPUT);
  pinMode(pinAzul, OUTPUT);
  
  // Puedes inicializar la comunicación serial para depuración si lo deseas
  // Serial.begin(9600);
}

void loop() {
  // 1. Lectura de los valores analógicos de los potenciómetros (0 a 1023)
  int valorPotRojo = analogRead(potRojo);
  int valorPotVerde = analogRead(potVerde);
  int valorPotAzul = analogRead(potAzul);

  // 2. Mapeo de los valores leídos al rango de PWM (0 a 255)
  // La función 'map' convierte un rango de valores a otro
  int intensidadRojo = map(valorPotRojo, 0, 1023, 0, 255);
  int intensidadVerde = map(valorPotVerde, 0, 1023, 0, 255);
  int intensidadAzul = map(valorPotAzul, 0, 1023, 0, 255);

  // 3. Escribir los valores PWM a los pines del LED
  // Esto controla la intensidad de cada color, creando el color resultante
  analogWrite(pinRojo, intensidadRojo);
  analogWrite(pinVerde, intensidadVerde);
  analogWrite(pinAzul, intensidadAzul);

  /*
  // Descomentar para ver los valores en el Monitor Serial (opcional)
  Serial.print("R: "); Serial.print(intensidadRojo);
  Serial.print("\tG: "); Serial.print(intensidadVerde);
  Serial.print("\tB: "); Serial.println(intensidadAzul);
  */
  
  // Una pequeña pausa para estabilidad, aunque no es estrictamente necesaria aquí
  delay(5); 
}

```
<img src="http://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/rgb.png"/>

##### Sensor sharp
```js
PROCESSING
import processing.serial.*;

Serial myPort;  // Create object from Serial class
static String val;    // Data received from the serial port
int sensorVal = 0;

void setup()
{
  background(0); 
  //fullScreen(P3D);
   size(1080, 720);
   noStroke();
  noFill();
  String portName = "COM5";// Change the number (in this case ) to match the corresponding port number connected to your Arduino. 

  myPort = new Serial(this, Serial.list()[0], 9600);
}

void draw()
{
  if ( myPort.available() > 0) {  // If data is available,
  val = myPort.readStringUntil('\n'); 
  try {
   sensorVal = Integer.valueOf(val.trim());
  }
  catch(Exception e) {
  ;
  }
  println(sensorVal); // read it and store it in vals!
  }  
 //background(0);
  // Scale the mouseX value from 0 to 640 to a range between 0 and 175
  float c = map(sensorVal, 0, width, 0, 00);
  // Scale the mouseX value from 0 to 640 to a range between 40 and 300
  float d = map(sensorVal, 0, width, 40,800);
  fill(255, c, 0);
  ellipse(width/2, height/2, d, d);   

}
```

```js
ARDUINO
// Definir el pin del sensor Sharp
int sharpPin = A0;

void setup() {
  Serial.begin(9600); // Iniciar comunicación serial
}

void loop() {
  int sensorValue = analogRead(sharpPin); // Leer valor del sensor
  Serial.println(sensorValue); // Enviar valor a Processing
  delay(100); // Esperar un momento
}

```

<img src="https://raw.githubusercontent.com/rarandamartinez-del/interfazII/refs/heads/main/img/sharp.png"/>

##### Sensor sharp
```js
/*******************************
           Conexión:
             VCC-5V
             GND-GND
             S-Analog pin A0

Puedes ponder el sensor en la palma de tu mano
para sensar la humedad de  tu palma.
 ********************************/

void setup()
{
  Serial.begin(9600);// abre el puerto serial y Establece la velocidad en baudios a 9600 bps
}
void loop()
{
  int sensorValue;
  sensorValue = analogRead(0);   //conectar el sensor de humedad al pin analogo 0
  Serial.println(sensorValue); //imprime el valor a serial.
  delay(200);
}
```
