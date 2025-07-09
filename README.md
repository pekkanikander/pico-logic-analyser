# pico-logic-analyser

Adapted from https://github.com/develone/rp2040-logic-analyzer, also supports RP2350 aka Pico 2.

Develone's project modified the PIO logic analyser example, that is part of the
Raspberry Pi Pico examples. This project takes Develone's project, applies the
SDK 2.0.0 patches from the [pico-examples](https://github.com/raspberrypi/pico-examples/)
repo, and develops it a bit further.

The present project allows interactive configuration
of the capture and outputs the capture data in CSV formats suitable for
importing into sigrock or Pulseview, for further analysis.

# Plans / features

The main planned feature of this version is to package it into a library and
allow the analyser to analyse the Pico itself, running on CPU 1.
In this way, you can install the analyser on your own project and get a full
trace of what is going on in your I/O pins, without an external analyser.

However, at this writing, this is still work in progress.

# Usage

## Serial line interface

To use the analyser, install it on a Pico and connect to the USB COM port at 921600
baud. Once connected, press h to get help of the commands. The capture is
only limited by the abilities of the Pico.

The commands are:
  * p# - Set the first pin to receive capture data
  * n# - Set how many pins to receive capture data
  * f# - Set the freqency to capture data at in Hz
  * t(1)(0) - Set the trigger to high or low. Trigger happens off first pin
  * s# - Set how many samples to capture
  * g - Go!

Once "go" is selected, a trigger will arm and wait for the specified signal.
The output is a CSV file, each line contains every pin being sampled. The output
can be saved with any program that can read a serial port to a file. Just be
aware that a large number of samples can take quite a while to transfer. The
onboard LED will blink, as the transfer is happening, so you can know when to end
the save.

## USB MSC file interface

TBD.  Integrate with https://github.com/pekkanikander/pico-extras-usb-msc-bootrom-partitions
