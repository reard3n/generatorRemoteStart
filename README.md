# generatorRemoteStart
This is a set of scripts that will remote start a generator wired up to a raspberry pi

## Remotely Starting A Terex AL-4
This script is intended to allow remote starting of a Terex model AL-4 light tower/generator combo. More information on this model can be found here:
https://www.genielift.com/en/material-handling/light-towers/al4

## Hardware
These scripts control i2c relay boards which can be sourced on Amazon:
https://www.amazon.com/gp/product/B07Y54FKC6/

The i2c relay boards are tiered through automotive relays which can handle more amperage:
https://www.amazon.com/gp/product/B07XC6HT5C/

## Methodology
Wires were spliced into each key position, 12V, GND (chassis), and the primer switch. Additionally, a separate 7.2AH battery was added to allow the Raspberry Pi to isolate itself from the main battery when the starter is cranking.

The Raspberry Pi controls 5 relays which are used to complete the following steps in order for startup and shutdown.

Startup:
1. Isolate itself from the "main power" of the 12V bus for the generator. This is done because the voltage drops low enough to shut down the pi when the starter is cranking.
2. Put the generator switch into the run position
3. Prime the generator for 6 seconds
4. Crank the starter for 3 seconds
5. Turn off the starter and primer switches
6. Un-Isolate the battery from the main generator power bus so that it can charge.

Shutdown:
1. Trigger all relays to off simultaneously
