# obstacle-detection
An autonomous obstacle detection project using Arduino uno and HC SR04



Parts required
Arduino board (uno)
Bread board
Jumper wires (male to male)
Piezo buzzer
Red LED
Green LED
Four-pin HC-SR04 ultrasonic sensor

CONNECTION OF HC SR04 TO ARDUINO UNO
VCC - 5V
Trig - 12
Echo - 13
GND - GND

CONNECCTION OF PIEZO BUZZER TO ARDUINO UNO
POSITIVE - PIN 9 
NEGATIVE - GND

CONNECTION OF LEDs
NEGATIVE (BOTH) - GND
POSITIVE (RED) - 3
POSITIVE (GREEN) - 2



CODE OF THE PROJECT.
int ECHO = 13;
int TRIG = 12;
int greenLed = 2;
int redLed = 3;
const int buzzer = 9;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  pinMode(ECHO,INPUT);
  pinMode(TRIG,OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(redLed, OUTPUT);
  pinMode(buzzer, OUTPUT); }


void loop() {
  // put your main code here, to run repeatedly:
int pulse, inches, duration, distance;
digitalWrite(TRIG, LOW);
delay(1000);
digitalWrite(TRIG, HIGH);
delay(2000);
digitalWrite(TRIG, LOW);
pulse = pulseIn(ECHO, HIGH);
//147 pulse per inch
inches = pulse /147;
//changing inch to cm and naming it distance
distance = inches*2.54;
if(distance <15)
{
 digitalWrite(greenLed, LOW); // Turn off green LED
 digitalWrite(redLed, HIGH); // Turn on red LED
 tone(buzzer, 1000); // Send 1KHz sound signal...
  delay(1000);        // ...for 1 sec
  noTone(buzzer);     // Stop sound...
  delay(1000);
 }
 // Otherwise
 else { 
 digitalWrite(redLed, LOW); // Turn off red LED
 digitalWrite(greenLed, HIGH); // Turn on green LED
}
delay(450);
}
