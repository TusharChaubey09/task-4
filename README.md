# task-4
#include <TFT_HX8357_Due.h> // https://github.com/Bodmer/TFT_HX8357_Due
#include <Sodaq_DS3231.h>  //RTC Library https://github.com/SodaqMoja/Sodaq_DS3231
float minTemperature = 100;
float maxTemperature = -40;
String dateString;
String hours;
int minuteNow=0;
int minutePrevious=0;
TFT_HX8357_Due tft = TFT_HX8357_Due();       // Invoke custom library
void setup()
{  
  rtc.begin();
  tft.init();
  tft.setRotation(1);
  tft.fillScreen(0xC618);
  delay(100);
  printUI();
  
}
void loop()
{
   float temperature = rtc.getTemperature();
   getAndPrintTime();
   printTemperature(temperature);
   if(temperature>maxTemperature)
  {
    maxTemperature = temperature;
    updateMaxTemperature();
  }
  if(temperature<minTemperature)
  {
    minTemperature = temperature;
    updateMinTemperature();
  }
 delay(1000);
}
