CODIGO PROCESSING / CROMATIC TRANCE

```import processing.serial.*; // importamos al librería Serial
import oscP5.*; // libreria osc
import netP5.*; // libreria osc

OscP5 oscP5; //osc
NetAddress myRemoteLocation; //osc
Serial myPort; // Creamos un objeto de la clase serial

int numero = 0;

int lectura = 0;
int lectura2 = 0;
int lectura3= 0;

String lect;






void setup() {
  size (displayWidth, displayHeight); 
  oscP5 = new OscP5(this,12000); //osc

  println(Serial.list()); // Serial.list() nos permitirá saber que puerto estamos utilizando en MAC y en WIN
  //cambiaremos el puerto 0,1,2,3… dependiendo del que estemos utilizando
  String portName= Serial.list()[3];
  myPort= new Serial(this, portName, 9600);
  myRemoteLocation = new NetAddress("127.0.0.1",12001); //osc
  //myPort.bufferUntil('\n'); // don't generate a serialEvent() unless you get a newline character:
}

void draw(){
 // println("lectura:"+lectura+"lectura2:"+lectura2+"lectura3:"+lectura3);

 OscMessage s = new OscMessage ("sensor");
 OscMessage t = new OscMessage ("sensor2");
 OscMessage u = new OscMessage ("sensor3");
 
  if ( myPort.available() > 0) { // si tenemos datos en el puerto entonces
      char orden = char(myPort.read()); // lee la letra
      lect = myPort.readStringUntil('\n'); // lee la cadena que viene por el puerto y guárdala en la variable val
      if ((lect != null) && (lect.length() > 0)) { // si el valor que entra NO es NULL > valor nulo
        String lectTrim = lect.trim();
        
        try { // prueba esto
                numero= Integer.parseInt(lectTrim); // convierte el valor de val que viene de arduino en un número entero.
        
                if (orden == 'a') {
                  lectura = numero;
                } else if (orden == 'b') {
                  lectura2 = numero;
                } else if ( orden == 'c'){
                  lectura3 = numero;
                } 
        }
        catch (Exception e) { // y sino funciona capturar excepcion y no hacer nada
      
        }
      }
    s.add(lectura); //osc
    t.add(lectura2); //osc
    u.add(lectura3); //osc
    oscP5.send(s, myRemoteLocation); //osc
    oscP5.send(t, myRemoteLocation); //osc
    oscP5.send(u, myRemoteLocation); //osc
 }


   
  background(#000000);
  
  ellipse(width/2, height/2, lectura, lectura);
  ellipse(width/2, height/2, lectura*1.5, lectura*1.5);
  ellipse(width/2, height/2, lectura*2, lectura*2);
  ellipse(width/2, height/2, lectura*2.5, lectura*2.5);
  ellipse(width/2, height/2, lectura*3, lectura*3);
  ellipse(width/2, height/2, lectura*3.5, lectura*3.5);
  ellipse(width/2, height/2, lectura*4, lectura*4);
  ellipse(width/2, height/2, lectura*4.5, lectura*4.5);
  ellipse(width/2, height/2, lectura*5, lectura*5);
  fill(250,8,129,25);
  noStroke();

  ellipse(width/2, height/2, lectura2, lectura2);
  ellipse(width/2, height/2, lectura2*1.5, lectura2*1.5);
  ellipse(width/2, height/2, lectura2*2, lectura2*2);
  ellipse(width/2, height/2, lectura2*2.5, lectura2*2.5);
  ellipse(width/2, height/2, lectura2*3, lectura2*3);
  ellipse(width/2, height/2, lectura2*3.5, lectura2*3.5);
  ellipse(width/2, height/2, lectura2*4, lectura2*4);
  ellipse(width/2, height/2, lectura2*4.5, lectura2*4.5);
  ellipse(width/2, height/2, lectura2*5, lectura2*5);
  fill(250,242,8,25);
  noStroke();
  
  ellipse(width/2, height/2, lectura3, lectura3);
  ellipse(width/2, height/2, lectura3*1.5, lectura3*1.5);
  ellipse(width/2, height/2, lectura3*2, lectura3*2);
  ellipse(width/2, height/2, lectura3*2.5, lectura3*2.5);
  ellipse(width/2, height/2, lectura3*3, lectura3*3);
  ellipse(width/2, height/2, lectura3*3.5, lectura3*3.5);
  ellipse(width/2, height/2, lectura3*4, lectura3*4);
  ellipse(width/2, height/2, lectura3*4.5, lectura3*4.5);
  ellipse(width/2, height/2, lectura3*5, lectura3*5);
  fill(8, 171, 250, 25);
  noStroke();
  

}

void mousePressed() {
  /* in the following different ways of creating osc messages are shown by example */
  OscMessage myMessage = new OscMessage("/test");
  
  myMessage.add(123); /* add an int to the osc message */

  /* send the message */
  oscP5.send(myMessage, myRemoteLocation); 
}


void oscEvent(OscMessage theOscMessage) {
  /* print the address pattern and the typetag of the received OscMessage */
  print("### received an osc message.");
  print(" addrpattern: "+theOscMessage.addrPattern());
  println(" typetag: "+theOscMessage.typetag());
   /* in the following different ways of creating osc messages are shown by example */
  
}
```