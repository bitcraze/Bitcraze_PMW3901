# Arduino driver for PMW3901 optical flow sensor

Arduino driver for the Pixart PMW3901 optical flow sensor. The driver
is developed to support the [Bitcraze Flow Breakout board](https://wiki.bitcraze.io/breakout:flow). It communicates with
the sensor using SPI.

## Electrical connection

The library is using the standard SPI library, the sensor MOSI, MISO and SCK should be connected to the arduino according to the [SPI library documentation](https://www.arduino.cc/en/Reference/SPI). The CS (chip select) pin can be any digital pin (which allows to connect more than one SPI sensor to your Arduino).

## Usage

Look at the [flow](examples/flow/flow.ino) example for basic usage.

You can initialize a sensor by passing the chip select pin number:

``` C++
// Using digital pin 10 for chip select
Bitcraze_PMW3901 flow(10);
```

Initializing the sensor is done by calling *begin*, it returns *true* if the sensor is detected and initialized, *false* otherwise:

``` C++
  if (!flow.begin()) {
    Serial.println("Initialization of the flow sensor failed");
    while(1) { }
  }
```

As soon as it is initialized, the sensor will start accumulating motion count. Calling the *readMotionCount* function allows to get the value of the motion counters and resets the counters. So each time the function is called you get the motion count since the last call:

``` C++
  // Get motion count since last call
  flow.readMotionCount(&deltaX, &deltaY);
```
