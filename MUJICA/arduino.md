
CODIGO ARDUINO - CROMATIC TRANCE

```

                                                                                     #include <CapacitiveSensor.h>
CapacitiveSensor sensor = CapacitiveSensor(13,12); //sender y recive pines en puente. ver esquema       
CapacitiveSensor sensor2 = CapacitiveSensor(9,8);
CapacitiveSensor sensor3 = CapacitiveSensor(5,4);
//int lectura=0;

void setup()                    
{
     
   Serial.begin(9600); // serial
   pinMode(11,OUTPUT);
   pinMode(7,OUTPUT);
   pinMode(3,OUTPUT);
}

void loop()                    
{   
    long lectura =  sensor.capacitiveSensor(30);
    long lectura2 = sensor2.capacitiveSensor(30);
    long lectura3 = sensor3.capacitiveSensor(30);
 
    
if(lectura > 300){  //PARA PRENDER Y APAGAR EL LED
   digitalWrite(11,HIGH);
}   else{
   digitalWrite(11,LOW);
}

if(lectura2 > 300){  //PARA PRENDER Y APAGAR EL LED
   digitalWrite(7,HIGH);
}   else{
   digitalWrite(7,LOW);
}

if(lectura3 > 300){  //PARA PRENDER Y APAGAR EL LED
   digitalWrite(3,HIGH);
}   else{
   digitalWrite(3,LOW);
}

  Serial.print('a');  //serial
    Serial.println(lectura);// imprimo valor
    
    
  Serial.print('b'); // serial
    Serial.println(lectura2);
    
  Serial.print('c'); //serial
    Serial.println(lectura3);
    
    lectura = digitalRead(12); //serial
    lectura2= digitalRead(8);
    lectura3= digitalRead(4);
    
    

   delay(100);
   
}








```