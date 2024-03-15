/*Este script cambia co anterior xa que so se usa un motor mediante 
unha ponte H para poder cambiarlle o xiro ao motor.
Autor:Guillermo Salgueiro Chorén
Data:15/3/24
*/

// Definición de pines
#define izquierda 3
#define derecha 5
#define pulsador 11
#define final_ab 12
#define final_ar 13
#define ldr A0
#define salida 6
// Variables de control
bool activado;
int contador;
bool finalc_ab;
bool finalc_ar;
int vldr;
int enable;
// Función de configuración (se ejecuta una vez al inicio)
void setup() {
  // Configuración de pines
  pinMode(izquierda, OUTPUT);
  pinMode(derecha, OUTPUT);
  pinMode(pulsador, INPUT);
  pinMode(final_ab,INPUT);
  pinMode(final_ar,INPUT);
  pinMode(ldr,INPUT);
  pinMode(salida,OUTPUT);
  // Inicialización de variables
  contador = 0;
  activado=0;
}

// Función principal (se ejecuta continuamente en un bucle)
void loop() {
  //Mapeado da LDR e escritura da variable dependendo do nivel
  vldr=analogRead(ldr);
  enable=map(vldr,54,974,0,5);
  switch(enable){
   case 0:
    analogWrite(salida,12.75);
    break;
   case 1:
    analogWrite(salida,51);
    break;
   case 2:
    analogWrite(salida,102);
    break;
   case 3:
    analogWrite(salida,153);
    break;
   case 4:
    analogWrite(salida,204);
    break;
   case 5:
    analogWrite(salida,255);
    break;
  }
  // Lectura del estado del pulsador
  activado = digitalRead(pulsador);
  // Si el pulsador está activado
  if (activado == 1) {
    // Cambiar el estado del contador al siguiente (0, 1, 2, o 3)
    contador = (contador + 1) % 4;
    // Pequeño retardo para evitar rebotes
    delay(100);
    // Esperar hasta que el pulsador sea liberado
    while (digitalRead(pulsador) == 1) {
      delay(10);
    }
  }
  // Cambios de estado dos motores
  switch (contador) {
    //Parado
    case 0:
    case 2:
    parar();
    finalc_ab=0;
    finalc_ar=0;
    break;
    //Baixando
    case 1:
      if (digitalRead(final_ab) == 1 or finalc_ab==1) {
        parar();
        //Sale do if porque se activa o final de carrera 
        //e establecese o estado 2 para que o siguiente motor sexa 
        //o de subida
        finalc_ab++;
        contador=2;
      } else {
        bajar();
      }
    break;
    //Subindo
    case 3:
      if (digitalRead(final_ar) == 1 or finalc_ar==1) {
        parar();
       // Sale do if porque se activa o final de carrera 
       //e establecese o estado 0 para que o siguiente motor sexa 
       //o de baixada
        finalc_ar++;
        contador=0;
      } else {
        subir();
      }
    break;
  }
}

// Funciones complementarias

// Mover hacia arriba
void subir() {
  digitalWrite(izquierda, LOW);
  digitalWrite(derecha, HIGH);
}

// Mover hacia abajo
void bajar() {
  digitalWrite(derecha, LOW);
  digitalWrite(izquierda, HIGH);
}

// Detener el movimiento
void parar() {
  digitalWrite(izquierda, LOW);
  digitalWrite(derecha, LOW);
}
