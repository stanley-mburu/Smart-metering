# Smart-metering
# Using Gsm communication module, this system binds the meter's unique identification number with the consumer's mobile phone number, allowing timely notifications of low wattage, power cut offs and recharge balance. In addition, it also allow remote recharge from any place as far as the mobile network is available. 

#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0×27, 16, 2);

#include <Wire.h>
#include<EEPROM.h>

int led = 2;
#define pulsein8
#define relay 7

unsigned int pulse_count = 0;
float units = 0.0;
float watt_factor = 0.3125;
unsigned int temp = 0, i = 0, x = 0, k = 0;
String bal = "";

int m,p,a =0; 
float n;

void setup()
{
lcd.begin();
Serial.begin(9600);
pinMode(led, OUTPUT);
pinMode(pulsein, INPUT);
pinMode(relay, OUTPUT);
digitalWrite(pulsein, HIGH);
digitalWrite(relay, HIGH);
lcd.backlight();
lcd.setCursor(0,0);
lcd.print("Automatic Energy");
lcd.setCursor(0,1);
lcd.print("  Meter  ");
delay(2000);

lcd.clear();
lcd.print("GSM Initializing...");
gsm.init();
lcd.clear();
lcd.print("System ready");
Serial.println("AT+CNMI=2,2,0,0,0");
inti_sms();
send_data("System Ready");
send_sms();
delay(1000);
digitalWrite(led, LOW);
lcd.clear();

EEPROM.write(1,0);
shilling=EEPROM.read(1);
}
void loop()
...
