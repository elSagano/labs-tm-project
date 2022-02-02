# Michał Sagan
 
# Projekt - TM----

# Arduino - Kostka do gry z diodami

Arduino złożone z siedmiu diód, rezystorów oraz przycisku ma za zadanie zastąpić sześciokątną klasyczną kostkę do gry.

# Elementy:

- Arduino UNO R3
- 7 x LED
- Rezystor 10kΩ
- Rezystor 7 x 240Ω
- Przycisk
- Płytka PCB
- Przewody

# Link do elementów

https://botland.com.pl/arduino-seria-podstawowa-oryginalne-plytki/1060-arduino-uno-rev3-a000066-8058333490090.html?cd=15425572033&ad=125523543810&kd=&gclid=Cj0KCQiA9OiPBhCOARIsAI0y71Ai6b8dqZoXvZEArn-SgiU0GLXjxS9MFbzNt8hIOuSYjm7Fs8YdEicaAg4AEALw_wcB


# Schemat w programie Fritzing:

![img](C:\Users\Sajgo\Desktop\zdj3.jpg)

# Wygląd złożonego schematu

![img](C:\Users\Sajgo\Desktop\zdj1.jpg)
![img](C:\Users\Sajgo\Desktop\zdj2.jpg)

# Kod programu:

```cpp
void setup() {
//diody
pinMode(1,OUTPUT);
pinMode(2,OUTPUT);
pinMode(3,OUTPUT);
pinMode(4,OUTPUT);
pinMode(5,OUTPUT);
pinMode(6,OUTPUT);
pinMode(7,OUTPUT);
//przycisk
pinMode(12,INPUT);
}
int oczka=0; //Zmienna, która będzie przechowywała liczbę wylosowanych oczek
int przeskok=0; //zmienna, która będzie określała liczbę przejść przed pokazaniem właściwego wyniku
void loop() {
randomSeed(millis()); //Zwraca liczbę milisekund, które upłynęły od momentu rozpoczęcia wykonywania programu
if(digitalRead(12)==HIGH){ //Losujemy liczbę przejść 
  delay(20);
przeskok=random(3,15);
  while(digitalRead(12)==HIGH);
delay(20);
}
int czas=50; // Czas przerwy między pierwszym, a drugim wynikiem w trakcie losowania
//Pętla, która wykonuje się tyle razy, ile jest przejść
for(int i=1; i<=przeskok; i++){
digitalWrite(1,LOW);
  digitalWrite(2,LOW);
digitalWrite(3,LOW);
  digitalWrite(4,LOW);
digitalWrite(5,LOW);
  digitalWrite(6,LOW);
digitalWrite(7,LOW);
  oczka=random(1,7); //losowanie liczby oczek
//W zależności od liczby oczek zapalane są określone diody
switch (oczka){
  case 1:
digitalWrite(4,HIGH);
  break;
case 2:
    digitalWrite(1,HIGH);
digitalWrite(7,HIGH);
  break;
case 3:
    digitalWrite(1,HIGH);
digitalWrite(4,HIGH);
    digitalWrite(7,HIGH);
break;
  case 4:
digitalWrite(1,HIGH);
    digitalWrite(3,HIGH);
digitalWrite(5,HIGH);
    digitalWrite(7,HIGH);
break;
  case 5:
digitalWrite(1,HIGH);
    digitalWrite(3,HIGH);
digitalWrite(4,HIGH);
    digitalWrite(5,HIGH);
digitalWrite(7,HIGH);
  break;
case 6:
    digitalWrite(1,HIGH);
digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
digitalWrite(5,HIGH);
    digitalWrite(6,HIGH);
digitalWrite(7,HIGH);
  break;
default:
  break;
}
  delay(czas);
czas+=60; //spowolnienie przejścia kostki
}
while(digitalRead(12)==LOW); //ponowne wciśnięcie przycisku
}
```
# Filmik z działania programu 
https://www.youtube.com/watch?v=qWsvkY9TDUc
