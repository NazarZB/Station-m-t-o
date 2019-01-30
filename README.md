# **Station météo**

## **Vidéo :** 
[![video](https://img.youtube.com/vi/wMibktFO9a8/0.jpg)](https://www.youtube.com/watch?v=wMibktFO9a8)


# Matériels utilisés

>* [Arduino Uno](https://store.arduino.cc/arduino-uno-rev3) :
![Arduino](https://store-cdn.arduino.cc/uni/catalog/product/cache/1/image/520x330/604a3538c15e081937dbfbd20aa60aad/a/0/a000066_featured_1_.jpg)

>* [Ecran LCD 16x22](https://www.cdiscount.com/bricolage/electricite/1x-ecran-lcd-pour-arduino-retroeclairage-jaune-com/f-1661416-auc3327901526918.html?cid=search_pla&cm_mmc=PLA!COR!AUT!MP!287498165!bing&msclkid=0748671133ca14e48a803b40f8a5ed15) :
![LCD](https://i2.cdscdn.com/pdt2/9/1/8/1/550x550/auc3327901526918/rw/1x-ecran-lcd-pour-arduino-retroeclairage-jaune-com.jpg)

>* [Horloge RTC DS3231](https://www.amazon.fr/WINGONEER-minuscule-AT24C32-pr%C3%A9cision-Horloge/dp/B01H5NAFUY/ref=sr_1_4?s=electronics&ie=UTF8&qid=1548864518&sr=1-4&keywords=Horloge+RTC+%28DS3231) : 
![RTC](https://images-na.ssl-images-amazon.com/images/I/61DjGrZ%2ByLL._SL1100_.jpg)

>* [Capteur de témpérature DHT11](https://www.amazon.fr/DHT11-num%C3%A9rique-capteur-temp%C3%A9rature-humidit%C3%A9-Raspberry/dp/B01N1EYTUN/ref=sr_1_2?s=electronics&ie=UTF8&qid=1548864606&sr=1-2&keywords=Capteur+de+t%C3%A9mp%C3%A9rature+%28DHT11%29) :
![RTC](https://images-na.ssl-images-amazon.com/images/I/61GHnECJpzL._SL1174_.jpg)


>* [Potentiomètre](https://www.amazon.fr/Aerzetix-Potentiom%C3%A8tre-Lin%C3%A9aire-%C3%986mmx4-5mm-9-8x11x6-8mm/dp/B01N4X4YRX/ref=sr_1_19?s=electronics&ie=UTF8&qid=1548864727&sr=1-19&keywords=potentiom%C3%A8tre+arduino) :
![Potentimetre](https://images-na.ssl-images-amazon.com/images/I/51CEtKOoBML._SL1016_.jpg)


>* **Résistances 2k**



# Bibliothèques utilisées

* LiquidCrystal
* DHT-sensor-library
* Adafruit Unified Sensor
* Rtc by Makuna
# Code 

On ajoute toutes les bibliothèques dont on aura besoins (voir dans *"bibliothèques utilisées"*)
``` c++
#include "DHT.h"
#include <Adafruit_Sensor.h>
#include <Wire.h>
#include <RtcDS3231.h>
#include <LiquidCrystal.h>
```

On crée les objets suivants : 

>* Objet type **Rtc**
``` c++
DHT dht(7, DHT11);
```
>* Objet type **DHT**
``` c++
RtcDS3231<TwoWire> clock(Wire);
```


>* Objet type **Liquid crystal**
``` c++
 LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
```

On initialise tous nos modules : 

``` c++
   cd.begin(16, 2);
   clock.Begin();
   dht.begin();
```
On récupère les données (date,heure...) sur le module RTC :

``` c++ 
RtcDateTime now = clock.GetDateTime();
``` 
On affiche les données sur l'écran LCD : 

``` c++
 lcd.setCursor(0, 0);

    lcd.print(now.Hour());
    lcd.print(":");
    lcd.print(now.Minute());

//Cette commande permet d'espacer les minutes de la date...
    lcd.print(" ");
    lcd.print(now.Day());
    lcd.print("/");
    lcd.print(now.Month());
    lcd.print("/");
    lcd.print(now.Year());
 ```
On déclare nos deux variable (celle de la température et celle de l'humidité) : 

``` c++
   int temperature = dht.readTemperature();
   int humidity = dht.readHumidity();
```  

Enfin, on affiche nos information sur l'écran LCD : 

``` c++

 lcd.setCursor(0, 1);

   lcd.print("T");
   lcd.print(":");
   lcd.print(temperature);

//Cette commande permet d'afficher "°" ...
   lcd.print((char)223); 
   lcd.print("C");
   lcd.print(" ");
   lcd.print(" ");
   lcd.print("Hum");
   lcd.print(":");
   lcd.print(humidity);
   lcd.print("%");
```
