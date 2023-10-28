# Synthetic Relationships

Communication lies at the core of all media. From speech to the written word, from radio to social networks - the core function of media has been to enable and facilitate communication. In this project we're going to take on this radical approach to communication, and try to get to the root of mediated exchange. We will examine how data is collected, how it is transformed into information, how it can be encoded, transmitted, and decoded. In the process we will encounter the need to build contextualized systems of meaning: systems of representation that maintain internal coherence, but might not make a lot of sense when seen from the outside.

My partner and I construct two electronic beings capable of perceiving some aspects of the environment around them. Then we connect them into a network that would enable them to communicate their findings, and respond to the communications of their counterpart.

## Sensors/Input
### Yuanlin: Flex Sensor
A turbulance-control glove, Bend the finger to generate turbulance in specific position  

<img width="600" alt="Screenshot 2023-10-27 at 8 36 47 PM" src="https://github.com/GuanLuoyi/CreativeTechFA23/assets/95225808/98f8645d-a2ff-45a3-8e8b-a68f3818ca30">

### Luoyi: Adafruit APDS9960 Proximity, Light, RGB and Gesture Sensor
A sensor to receive RGB value in order to change the material color of the monitor in digital world
  
<img width="600" alt="Screenshot 2023-10-27 at 8 38 51 PM" src="https://github.com/GuanLuoyi/CreativeTechFA23/assets/95225808/2999941f-6176-4754-b769-b608ad51ef7d">

## Input Code
### Set Up
```C
#include "config.h"
#define BLEN A3
//#define BLEN2 A4

AdafruitIO_Feed *bl1 = io.feed("10-19");
AdafruitIO_Feed *bl2 = io.feed("10-20");
AdafruitIO_Feed *r_feed = io.feed("r_feed", "LuoyiGuan");
AdafruitIO_Feed *g_feed = io.feed("g_feed", "LuoyiGuan");
AdafruitIO_Feed *b_feed = io.feed("b_feed", "LuoyiGuan");

int newMsg = 0;
// int color[3] = 0;
int count = 0;

void setup() {
  // put your setup code here, to run once:
  pinMode(BLEN, INPUT);
  //pinMode(BLEN2, INPUT);
  Serial.begin(9600);
  while (!Serial)
    ;
  // Serial.print("Connecting to Adafruit IO");
  io.connect();

  while (io.status() < AIO_CONNECTED) {
    Serial.print(".");
    delay(500);
  }

  Serial.println();
  Serial.println(io.statusText());
  r_feed->onMessage(handleMessage);
  //g_feed -> onMessage(handleMessage);
  //b_feed -> onMessage(handleMessage);
}
```

### Loop and Upload Data to Adafruit IO
```C
void loop() {
  io.run();
  // put your main code here, to run repeatedly:
  //Serial.println(analogRead(POTCEN));

  float value = analogRead(BLEN);
  //float value2 = analogRead(BLEN2);
  //Serial.print(',');
  // Serial.print("Sending this: ");
  // Serial.println(value);
  bl1->save(value);
  //bl2->save(value2);

  delay(3000);
}

void handleMessage(AdafruitIO_Data *data) {
  // char *name = data.feedName();
  // newMsg = data->toInt();
  // if (count < 3)
  // {
  //   count++;
  //   // color[count] = newMsg;
  //   Serial.print(newMsg);
  //   Serial.print(",");

  // }
  // else
  // {
  //   count = 0;
  //   Serial.println();
  // }
  //Serial.print("received <- ");
  Serial.println(data->value());
}
```

## Output Code
### Main
```C#
using System;
using System.Collections;
using System.Collections.Generic;
using System.Text.RegularExpressions;
using UnityEngine;
using System.IO.Ports;

public class lightchange : MonoBehaviour
{
    // Start is called before the first frame update
    SerialPort myConnection = new SerialPort("/dev/cu.SLAB_USBtoUART", 
    9600);
    public string incomingData;
    public float values;
    MeshRenderer rndrdr;
    void Start()
    {
        Debug.Log("Serial Started");
        
        //Debug.Log(myConnection.IsOpen);
        rndrdr = GetComponent<MeshRenderer>();
        myConnection.Open();
        Debug.Log(myConnection.IsOpen);
    }

    // Update is called once per frame
    void Update()
    {
        string incomingData = myConnection.ReadLine();
        values = float.Parse(incomingData);
        Debug.Log(values);
        if (values <  )
        {
            rndrdr.material.color = Color.blue;
        }
        else
        {
            rndrdr.material.color = Color.white;
        }
    }
}

```
## Outcome
<img width="1512" alt="Screenshot 2023-10-27 at 8 57 17 PM" src="https://github.com/GuanLuoyi/CreativeTechFA23/assets/95225808/3388742e-b5ff-48fe-8f45-23403966156b">

### [Click to watch the video](https://youtu.be/1LQpFV82OjQ)
