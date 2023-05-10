# Estacion de subte

![Arduino_Logo_Registered svg](https://user-images.githubusercontent.com/109388659/234407445-1de9faf7-fd9b-4d31-9f8d-089b83dd0892.png)
## Integrantes

-Ivan Gonzalez

-Lucas Ibarrola

-Thiago Vallejos

-Juan Bermudez

## Trabajo practico de SPD

## Descripcion

Sistema que permite al usuario saber a qué estación de subte está llegando, aparte  el sistema muestra las estaciones que faltan hasta llegar a destino.
Esta vez el buzzer emiter un sonido diferente cada vez que se llegue a una estación.


## funcion principal
-La funcion ferrocarril() recibe por parametro las listas listanumer[] y listaled[] y se encarga de iterar la funcion encender_led_display_y_piezo() de dos formas diferentes
para simular el tren yendo i viniendo
```c++
void ferrocarril(int listanumero[][7], int listaled[]){
  for(int i = 0; listaled[i] != -1; i++){
  	encender_led_display_y_piezo(listaled[i],listanumero[i]);
  }
  for(int i = 2; listaled[i] != 2; i--){
  	encender_led_display_y_piezo(listaled[i],listanumero[i]);
  }
}
```
-estadoBoton es para saber si el boton esta activado o desactivado
```c++
int estadoBoton = digitalRead(Boton);
```
-listanumeros[] es un conjunto de listas que contiene los led que hay que encender el el 7 segmentos para que se active el numero deseado.(todas las listas terminan en -1)
```c++
int listanumeros[][7] = {
    			 {A, B, C, D, G, -1},
                         {A, B, G, D, E, -1},
                         {B, C, -1},
                         {A, B, C, D, E, F, -1}};
```

-leds[] es una lista de los leds a utilizar ordenados de forma especifica para que coincida con listanumeros[]
```c++
int leds[] = {led1, led2, led3, led4, -1};
```

-La funcion encender_led_display_y_piezo() recibe un led y una lista de leds y se encarga de encenderlos y apagarlos de forma sucesiva junto con el piezo
```c++
void encender_led_display_y_piezo(int led,int *lista){
  digitalWrite(led, HIGH);
  Controlador_de_7_segmentos(lista, HIGH);
  sonido_por_led(led);
  delay(1000);
  Controlador_de_7_segmentos(lista, LOW);
  digitalWrite(led, LOW);
```
-La funcion sonido_por_led() recibe un un led y se encarga de asignarle un sonido diferente a cada led para el piezo llamando a la funcion bocina
```c++
void sonido_por_led(int led){
if(led == led1){
    bocina(400);
  }
  else if (led == led2){
  bocina(300);
  }
  else if(led == led3){
    bocina(200);
  }
  else{
  bocina(100);
  }
}
```
-La funcion bocina() recibe un int el cual se utiliza hacer sonar el piezo con una frecuencia en especifico 
```c++
void titilar_y_bocina(int led,int seg ,int tono, int pausa){
	digitalWrite(led, HIGH);
  	bocina(seg, tono, pausa);
	digitalWrite(led, LOW);
}
```
-la funcion Controlador_de_7_segmentos() recibe una lista de leds y un estado que puede ser "HIGH" o "LOW" y con estos enciende o apaga los leds
correspondientes a el display de 7 segmentos
```c++
void Controlador_de_7_segmentos(int lista[],int estado){
  for (int i = 0; lista[i] != -1; i++){
  	int letra = lista[i];
    Serial.println(letra);
    digitalWrite(letra, estado);
  }
}
```

## :eight_pointed_black_star:Link al proyecto

[Proyecto](https://www.tinkercad.com/things/9mvFr9pk2P8-powerful-gaaris-krunk/editel?sharecode=BOefq5cHaTxn0SszWn3oPzG7zET1XoFudZWGyhD-rGo)
