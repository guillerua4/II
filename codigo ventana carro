// Definición de pines
#define rele_b 3
#define rele_s 9
#define pulsador 11

// Variables de control
bool activado;
int contador;
int tempo;
bool tope;

// Función de configuración (se ejecuta una vez al inicio)
void setup() {
  // Configuración de pines
  pinMode(rele_b, OUTPUT);
  pinMode(rele_s, OUTPUT);
  pinMode(pulsador, INPUT);

  // Inicialización de variables
  contador = -1;
  Serial.begin(9600);
  tempo = 0;
  tope = 0;
}

// Función principal (se ejecuta continuamente en un bucle)
void loop() {
  // Lectura del estado del pulsador
  activado = digitalRead(pulsador);

  // Si el pulsador está activado
  if (activado == 1) {
    // Cambiar el estado del contador al siguiente (0 o 1)
    contador = (contador + 1) % 2;

    // Pequeño retardo para evitar rebotes
    delay(100);

    // Restablecer la variable 'tope' y 'tempo'
    tope = 0;
    tempo = 0;

    // Esperar hasta que el pulsador sea liberado
    while (digitalRead(pulsador) == 1) {
      delay(10);
    }
  }

  // Si el contador es 1 y 'tope' es 0
  if (contador == 1 and tope == 0) {
    // Si 'tempo' alcanza 7000 o más, detener el movimiento
    if (tempo >= 7000) {
      parar();
    } else {
      // Si no, mover hacia arriba y actualizar 'tempo'
      subir();
      tempo += 10;
      delay(10);
    }
  }

  // Si el contador es 0 y 'tope' es 0
  if (contador == 0 and tope == 0) {
    // Si 'tempo' alcanza 7000 o más, detener el movimiento
    if (tempo >= 7000) {
      parar();
    } else {
      // Si no, mover hacia abajo y actualizar 'tempo'
      bajar();
      tempo += 10;
      delay(10);
    }
  }
}

// Funciones complementarias

// Mover hacia arriba
void subir() {
  digitalWrite(rele_b, LOW);
  digitalWrite(rele_s, HIGH);
}

// Mover hacia abajo
void bajar() {
  digitalWrite(rele_s, LOW);
  digitalWrite(rele_b, HIGH);
}

// Detener el movimiento
void parar() {
  tope = 1;
  digitalWrite(rele_s, LOW);
  digitalWrite(rele_b, LOW);
}
