//Sensores
int TRIGI = 7;
int ECOI = 4;

int TRIGD = 11;
int ECOD = 8;

int DURACIONI;
int DISTANCIAI;

int DURACIOND;
int DISTANCIAD;
int DT;

//motores

const int pinIN1 = 5;
const int pinIN2 = 6;
const int pinIN3= 10;
const int pinIN4 = 9;

const float izq = 9;
const float der = 10;
float Vl;
float Vr;

void setup(){

  pinMode(TRIGI, OUTPUT);
  pinMode(ECOI, INPUT);

  pinMode(TRIGD, OUTPUT);
  pinMode(ECOD, INPUT);

   pinMode(pinIN1, OUTPUT);
   pinMode(pinIN2, OUTPUT);
   pinMode(pinIN3, OUTPUT);
   pinMode(pinIN4, OUTPUT);


  Serial.begin(9600);

}



void loop(){
//Sensor 1
   digitalWrite(TRIGI, LOW);
   delayMicroseconds(20);
   digitalWrite(TRIGI, HIGH);
   delayMicroseconds(10);
   digitalWrite(TRIGI, LOW);
   DURACIONI = pulseIn(ECOI, HIGH);
   DISTANCIAI = (DURACIONI * 0.034) / 2 ;
   Serial.println("IZQUIERDA:"); 
   Serial.print(DISTANCIAI);
   Serial.print("\n");
   //Sensor 2
   digitalWrite(TRIGD, LOW);
   delayMicroseconds(20);
   digitalWrite(TRIGD, HIGH);
   delayMicroseconds(10);
   digitalWrite(TRIGD, LOW);
   DURACIOND = pulseIn(ECOD, HIGH);
   DISTANCIAD = (DURACIOND * 0.034) / 2 ; 
   Serial.println("DERECHA:"); 
   Serial.print(DISTANCIAD);
   Serial.print("\n");
   // Filtro Kalman
   DT = (0.9*DISTANCIAI)+(0.1*DISTANCIAD);
 if(DT>15){

  Vl = map(izq,0,20.94,0,255);
  Vr = map(der,0,20.94,0,255);
  analogWrite(pinIN1, Vr);
  analogWrite(pinIN2, LOW);
  analogWrite(pinIN4, Vl);
  digitalWrite(pinIN3, LOW);
   
  
 }else{
   analogWrite(pinIN1, LOW);
  analogWrite(pinIN2, LOW);
  analogWrite(pinIN4, LOW);
  digitalWrite(pinIN3, LOW);
 }
 }
 
  

  
