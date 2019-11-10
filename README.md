
# XTronical_XT_DAC_Audio_Mirror
Mirror of XTronical's excellent XT_DAC_Audio library for ease of integration into platformio projects

XTronical, if you're reading this, please consider uploading your projects/this library to your personal git. I have mirrored this for personal convenience.

## Links
https://www.xtronical.com/introduction-to-dac-audio/
https://www.xtronical.com/dacaudio-hardware/

## To integrate into a platformio project:

platformio.ini
```ini
lib_deps =
    https://github.com/WeekendWarrior1/XTronical_XT_DAC_Audio_Mirror/archive/master.zip
```

main.cpp or sketch.ino
```cpp
// Playing a digital WAV recording repeatadly using the XTronical DAC Audio library
// prints out to the serial monitor numbers counting up showing that the sound plays 
// independently of the main loop
// See www.xtronical.com for write ups on sound, the hardware required and how to make
// the wav files and include them in your code

#include "SoundData.h"
#include "XT_DAC_Audio.h"

XT_Wav_Class ForceWithYou(Force);     // create an object of type XT_Wav_Class that is used by 
                                      // the dac audio class (below), passing wav data as parameter.
                                      
XT_DAC_Audio_Class DacAudio(25,0);    // Create the main player class object. 
                                      // Use GPIO 25, one of the 2 DAC pins and timer 0

uint32_t DemoCounter=0;               // Just a counter to use in the serial monitor
                                      // not essential to playing the sound

void setup() {
  Serial.begin(115200);               // Not needed for sound, just to demo printing to the serial
                                      // Monitor whilst the sound plays, ensure your serial monitor
                                      // speed is set to this speed also.
}


void loop() {
  DacAudio.FillBuffer();                // Fill the sound buffer with data
  if(ForceWithYou.Playing==false)       // if not playing,
    DacAudio.Play(&ForceWithYou);       // play it, this will cause it to repeat and repeat...
  Serial.println(DemoCounter++);        // Showing that the sound will play as well as your code running here.
}
```
