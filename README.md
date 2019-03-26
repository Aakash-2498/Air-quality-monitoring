# Air-quality-monitoring
Arduino code to interface MQ135 sensor with Arduino
include "MQ135.h"
#include <SoftwareSerial.h>
#define DEBUG true
SoftwareSerial esp8266(9,10);
const int sensorPin= 0;
int air_quality;
#include <LiquidCrystal.h> 
LiquidCrystal lcd(12,11, 5, 4, 3, 2);

void setup() {
pinMode(8, OUTPUT);
lcd.begin(16,2);
lcd.setCursor (0,0);
lcd.print ("circuitdigest ");
lcd.setCursor (0,1);
lcd.print ("Sensor Warming ");
delay(1000);
Serial.begin(115200);
lcd.clear();
}

void loop() {

MQ135 gasSensor = MQ135(A0);
float air_quality = gasSensor.getPPM();


    


lcd.setCursor (0, 0);
lcd.print ("Air Quality is ");
lcd.print (air_quality -1600);
lcd.print (" PPM ");
lcd.setCursor (0,1);
if (air_quality<=1000)
{
lcd.print("Fresh Air");
digitalWrite(8, LOW);
}
else if( air_quality>=1000 && air_quality<=2000 )
{
lcd.print("Poor Air, Open Windows");
digitalWrite(8, HIGH );
}
else if (air_quality>=2000 )
{
lcd.print("Danger! Move to Fresh Air");
digitalWrite(8, HIGH);   // turn the LED on
}
lcd.scrollDisplayLeft();
delay(1000);
}
  
  
