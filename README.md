# DWIN DGUS HMI Arduino Library
Official Arduino Library for DWIN DGUS T5L HMI Display
Supporting Features till date.
- getHWVersion
- restartHMI()
- setPage()
- getPage()
- setBrightness()
- getBrightness()
- setVP()
- setText()
- beepHMI()
- listenEvents()

## Usage
Download the Library and extract the folder in the libraries of Arduino IDE
#### Include DWIN Library (eg. DWIN.h) 
```C++
#include <DWIN.h>
```

#### Initialize the hmi Object with Rx | Tx Pins and Baud rate
```C++
HardwareSerial dwinSerial(PA3, PA2);

#define DGUS_BAUD     115200

  DWIN hmi(dwinSerial, DGUS_BAUD);
```

#### Define callback Function
```C++
// Event Occurs when response comes from HMI
void onHMIEvent(String address, int lastByte, String message, String response){  
  Serial.println("OnEvent : [ A : " + address + " | D : "+ String(lastByte, HEX)+ " | M : "+message+" | R : "+response+ " ]"); 
  if (address == "1002"){
  // Take your custom action call
  }
}
```

#### In void setup()
```C++
  hmi.echoEnabled(false);      // To get Response command from HMI
  hmi.hmiCallBack(onHMIEvent); // set callback Function
```

#### In loop()
```C++
  // Listen HMI Events
  hmi.listen();
```

---
