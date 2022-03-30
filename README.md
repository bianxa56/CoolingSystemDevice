# CoolingSystemDevice

//MAZARATE, BIANCA AMOR T.
//Creating an Automated Cooling System Device

#define buzzer 9
const int Motor_pin = 6;
int flag,Speed;
int tempPin = 0;


void setup()
{
 Serial.begin(9600);
 pinMode(Motor_pin, OUTPUT); 
 pinMode(buzzer, OUTPUT);
 pinMode(12, OUTPUT);
 pinMode(11, OUTPUT);
 pinMode(10, OUTPUT);
 Serial.println("Enter value from 50 to 225");
}

void loop() 
{
   int reading = analogRead(tempPin);  
   float voltage = reading * 5.0;
   voltage /= 1024.0; 
  //Serial.println(voltage);
  
   // now print out the temperature
   float temperatureC = (voltage - 0.5) * 100 ; 
   Serial.print("Temperature is ");
   Serial.print(temperatureC);
   Serial.print(" Celsius");

   // now convert to Fahrenheit
   float temperatureF = (temperatureC * 9.0 / 5.0) + 32.0;
   Serial.print(" or ");
   Serial.print(temperatureF);
   Serial.println(" Fahrenheit");
  
  //Turn on LEDlight red
  if (temperatureC > 37)
  {
    digitalWrite(12, LOW);
    digitalWrite(11, LOW);
    digitalWrite(10, HIGH);
    digitalWrite(buzzer, HIGH);
    analogWrite(Motor_pin,255);  
    Serial.println("Temperature is HOT");
    
  }
  
  //Turn on LEDlight green
  else if (temperatureC > 27 && temperatureC < 37)
  {
    digitalWrite(12, LOW);
    digitalWrite(11, HIGH);
    digitalWrite(10, LOW);
    digitalWrite(buzzer, LOW);
    analogWrite(Motor_pin,100); 
    Serial.println("Temperature is MODERATE");
  }
  
  //Turn on LEDlight yellow
  else if (temperatureC < 27)
  {
  	digitalWrite(12, HIGH);
    digitalWrite(11, LOW);
    digitalWrite(10, LOW);
    digitalWrite(buzzer, HIGH);
    analogWrite(Motor_pin,0); 
    Serial.println("Temperature is COLD");
  }
  
   delay(1000);   
 
}
