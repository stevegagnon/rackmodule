Hardware interface similar to the Expert Sleepers Disting https://live.staticflickr.com/3665/33488084245_5f7cfd1eac_k.jpg

3 inputs channels, bipolar -10v - +10v, 48khz+ sample rate, connection detection (input-1,input-2,input-3)
2 output channels, bipolar -10v - +10v, 48khz+ sample rate, connection detection (output-1,output-2)
2 rotary encoders (encoder-1,encoder-2)
2 buttons (button-1,button-2)
5 rgb lights (light-r1,light-g1,light-b1,light-r2,...)

Microcontroller should access to a good amount of RAM for audio buffers. Floating point math is a huge plus. I'm kinda hoping to use a pi pico 2 unless there is a better choice for a reasonable price.

On the software side we will need headers, source files, build scripts that make it easy to take an existing vcv rack module and convert it to a hardware module.

A simple module to get started with is the VCA-1:
https://library.vcvrack.com/Fundamental/VCA-1

Source file:
https://github.com/VCVRack/Fundamental/blob/v2/src/VCA-1.cpp

The two methods needed will be the constructor VCA_1() that sets up components of the module and process() for reading and setting the hardware interface.

Will need to be able to configure how components are mapped from the vcv rack module to the hardware interface:

LEVEL_PARAM => encoder-1,
EXP_PARAM => (button-1, toggle),
CV_INPUT => input-1,
IN_INPUT => input-2,
OUT_OUTPUT => output-1

Unused outputs go nowhere. Unused inputs remain disconnected or return initial values. Bypass can be ignored. getChannels() on inputs and outputs will aways return 1.

Code for UI, drawing, etc can be removed.
