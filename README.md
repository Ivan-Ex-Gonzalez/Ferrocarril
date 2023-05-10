# Estacion de subte

![Arduino_Logo_Registered svg](https://user-images.githubusercontent.com/109388659/234407445-1de9faf7-fd9b-4d31-9f8d-089b83dd0892.png)
## Integrantes

-Ivan Gonzalez

-Lucas Ibarrola

-Thiago Vallejos

## Trabajo practico de SPD

## Descripcion

sistema que permite al usuario saber a qué estación de subte está llegando, aparte  el sistema muestra las estaciones que faltan hasta llegar a destino.
Esta vez el buzzer emiter un sonido diferente cada vez que se llegue a una estación.

1- El semáforo tiene que tener 2 leds de cada color como minimo, en caso de que uno se rompa, lo ideal serian 3.

2- Tiene que implementar los tiempos correctos como se detallan a continuación.

3- El verde dura 45 segundos.

4- El amarillo dura 5 segundos.

5- Rojo dura 30 segundos.

6- Tiene que tener señalización para personas no videntes como se detalla a continuación.

7- Durante el verde: No sonar

8- Durante el amarillo: Tiene que sonar 1 vez cada 2 segundos en un tono suave.

9- Durante el rojo: Tiene que sonar 1 vez por segundo en un tono fuerte.

## funcion principal
-La funcion semaforo() se encarga de llamar a las funciones titilar() y titilar_y_bocina() en el orden y con parametros correctos para haci hacer
que funcuione el semaforo de la forma solicitada. Esta funcion no recibe nada ni devuelve nada.
```c++
void semaforo(){
	titilar(Led_verde, 45000);
  
  	titilar_y_bocina(Led_amarillo,3 ,100, 1466);
  	
  	titilar_y_bocina(Led_rojo,30 ,300, 800);

  	titilar_y_bocina(Led_amarillo,3 ,100, 1466);
}
```
-Led_verde,Led_amarillo1, Led_rojo son #define que utilizamos para agregar los leds, asociandolo a pines de la placa arduino.
```c++
#define Led_verde 2
#define Led_amarillo 3
#define Led_rojo 4
```
-Bocina es un #define que utilizamos para agregar el piezo, asociandolo a un pin de la placa arduino.
```c++
#define Bocina 5
```
-La funcion titilar() se encarga de encender un led durante un tiempo determinado sin que se active el piezo. Esta funcion recibe por parametro 
el pin asociado al led que se quiera encender y la duracion con la que se desea mantener encendido dicho led.
```c++
void titilar(int led, long pausa){
	digitalWrite(led, HIGH);
	delay(pausa);
  	digitalWrite(led, LOW);
}
```
-La funcion bocina() se encarga de encender la bocina durante 200 milisegundo y luego apagarla durante un tiempo determinado por su parametro
ademas de iterarla las veces que se especifique por parametro. Esta funcion recibe las veces que se desea iterar la bocina, la cantidad de Hz(Hercios)
que se desee por parte del piezo y tambien recibe durante cuanto tiempo se desea que la bocina este apagada.
```c++
void bocina(int seg,int tono,int pausa){
  for (int i = 0; i < seg; i++){
  	 tone(Bocina, tono);
     delay(200);
     noTone(Bocina);
     delay(pausa);
  }
}
```
-La funcion titilar_y_bocina() se encarga de endender un led y luego llamar a la funcion bocina() para que el piezo se active durante 
un tiempo determinado para luego apagar el led. Esta funcion recibe por parametro el pin asociado al led que se quiera encender
las veces que se desea iterar la bocina, la cantidad de Hz(Hercios) que se desee por parte del piezo y tambien durante cuanto tiempo
se desea que la bocina este apagada.
```c++
void titilar_y_bocina(int led,int seg ,int tono, int pausa){
	digitalWrite(led, HIGH);
  	bocina(seg, tono, pausa);
	digitalWrite(led, LOW);
}
```
## :eight_pointed_black_star:Link al proyecto

[Proyecto](https://www.tinkercad.com/things/1gNFAecIVWj-trabajo-semaforo/editel?sharecode=M5SdX0AJQG7TelWFGErJqWsMhgbzaXoqOu697lifn-U)
