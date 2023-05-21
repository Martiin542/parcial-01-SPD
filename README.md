# Parcial SPD (22/5/23)
## Alumno
- Martin Simone
## Ascensor
![image](https://github.com/Martiin542/parcial-01-SPD/assets/116306654/9e037fa6-06fc-4e63-8329-b4755b935d08)


## Proyecto: 
Se nos pide armar un modelo de montacarga funcional como maqueta para un hospital. El
objetivo es que implementes un sistema que pueda recibir ordenes de subir, bajar o pausar
desde diferentes pisos y muestre el estado actual del montacargas en el display 7
segmentos.

## Consigna:
1) Interfaz de usuario:
 Deberá haber 3 botones, uno para subir pisos, otro para bajar pisos y otro para detener el montacarga.
/ Deberá tener 2 LEDs, uno verde que indicará cuando el montacarga este en movimiento, otro rojo que indique cuando el montacarga esté pausado./• En el display 7 segmentos deberán informar en tiempo real en qué piso se encuentra el elevador.
/ Se sabe que el tiempo de trayecto entre pisos es de 3 segundos (3000 ms). 
/ Se deberá informar por monitor serial el piso en el que se encuentra el montacarga, este en funcionamiento o en pausa.

2) Funcionamiento del montacarga:
 Implementa un algoritmo que permita que el elevador suba y baje o frene presionando los botones correspondientes.
/ Deberán buscar una forma para pausar el montacargas cuando el usuario lo determine.

~~~ C++
#define BOTON_UP A0
#define BOTON_DOWN A1
#define BOTON_STOP A2
#define LED_GREEN A5
#define LED_RED A4

#define LED_A 11
#define LED_B 10
#define LED_C 9
#define LED_D 8
#define LED_E 7
#define LED_F 6
#define LED_G 5

int direction = 0;
int piso = 0;
int tiempo = 3000;
void setup()
{
  pinMode(BOTON_UP, INPUT);
  pinMode(BOTON_DOWN, INPUT);
  pinMode(BOTON_STOP, INPUT);
  pinMode(LED_GREEN, OUTPUT);
  pinMode(LED_RED, OUTPUT); 
  pinMode(LED_A, OUTPUT);
  pinMode(LED_B, OUTPUT);
  pinMode(LED_C, OUTPUT);
  pinMode(LED_D, OUTPUT);
  pinMode(LED_E, OUTPUT);
  pinMode(LED_F, OUTPUT);
  pinMode(LED_G, OUTPUT);
  Serial.begin(9600);
}

void loop()
{
  int estadUP = digitalRead(BOTON_UP);
  Serial.println(estadUP);
  int estadDOWN = digitalRead(BOTON_DOWN);
  int estadSTOP = digitalRead(BOTON_STOP);
  if(estadUP == HIGH)
  {
    direction = 1;
    estadDOWN = LOW;
    estadSTOP = LOW;
    prender(LED_RED);
    apagar(LED_GREEN);
  }
  else if (estadDOWN == HIGH)
  {
    direction = -1;
    estadUP = LOW;
    estadSTOP = LOW;
    prender(LED_RED);
    apagar(LED_GREEN);
  }
  else if (estadSTOP == HIGH)
  {
    direction = 0;
    estadUP = LOW;
    estadDOWN = LOW;
    prender(LED_GREEN);
    apagar(LED_RED);
  }
  display();
  delay(1000);
}

// Prender
void prender(int pin)
{
  digitalWrite(pin, HIGH);
}

// Apagar
void apagar(int pin)
{
  digitalWrite(pin, LOW);
}

// Display       
void display()
{
  piso += direction;
  switch(piso)
  {
    case 0:
    	digitalWrite(LED_A, HIGH);
  		digitalWrite(LED_B, HIGH);
  		digitalWrite(LED_C, HIGH);
  		digitalWrite(LED_D, HIGH);
  		digitalWrite(LED_E, HIGH);
  		digitalWrite(LED_F, HIGH);
  		digitalWrite(LED_G, LOW);
     	delay(tiempo);
    break;
    case 1:
     	digitalWrite(LED_A, LOW);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, LOW);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, LOW);
    	digitalWrite(LED_G, LOW);
    	delay(tiempo);
    break;
    case 2:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, LOW);
    	digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, HIGH);
    	digitalWrite(LED_F, LOW);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 3:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, LOW);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 4:
    	digitalWrite(LED_A, LOW);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, LOW);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, HIGH);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 5:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, LOW);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, HIGH);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 6:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, LOW);
    	digitalWrite(LED_C, HIGH);
   		digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, HIGH);
    	digitalWrite(LED_F, HIGH);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 7:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, LOW);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, LOW);
    	digitalWrite(LED_G, LOW);
    	delay(tiempo);
    break;
    case 8:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, HIGH);
    	digitalWrite(LED_F, HIGH);
   		digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
    case 9:
    	digitalWrite(LED_A, HIGH);
    	digitalWrite(LED_B, HIGH);
    	digitalWrite(LED_C, HIGH);
    	digitalWrite(LED_D, HIGH);
    	digitalWrite(LED_E, LOW);
    	digitalWrite(LED_F, HIGH);
    	digitalWrite(LED_G, HIGH);
    	delay(tiempo);
    break;
   
  }
}
~~~

## Diagrama esquematico:
![Parcial-SPD-Martin-Simone](https://github.com/Martiin542/parcial-01-SPD/assets/116306654/ca693b41-5c46-4bca-ad67-4d84dba60743)
* Botones: Accion de subir, bajar y parar.
* Leds: Indica si se esta moviendo el ascensor (led verde) o si esta parado (led roja).
* Display 7 segmentos: Mustra en que piso se encuentra el ascensor.
## Link al projecto:
* https://www.tinkercad.com/things/bOt68sz9TEo-epic-hango/editel?sharecode=HI7Y5420NCKOrAOS4x-CcE8tXO0nRWrJHi_yScABo2g


