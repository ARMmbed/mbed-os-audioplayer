# An Audio Player for mbed-os

This library can be used to play audio on mbed-os devices with AnalogOut support.

## Hardware setup

To play audio the AnalogOut pin of your board must be connect to the right circuitry. If you are connected to speakers using a headphone jack you can use a ~10:1 voltage divider (analog out to 9K ohm to 1K  to ground is sufficient) to reduce the voltage to the correct level. You'll also need an electrolytic or ceramic capacitor in series to act as a DC filter (0.1uf or larger recommended).

## Example usage

```
#include "mbed.h"

#include "SDBlockDevice.h"
#include "FATFileSystem.h"
#include "AudioPlayer.h"

SDBlockDevice sd(PTE3, PTE1, PTE2, PTE4);
FATFileSystem fs("sd", &sd);

AnalogOut aout(DAC0_OUT);
AudioPlayer player(&aout);

int main()
{
    // Set the maximum speed so it can keep up with audio
    sd.frequency(25000000);

    File file(&fs, "songs/my_song.wav");
    player.play(&file);
}

```