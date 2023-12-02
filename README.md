# Magnum
Magnum is a development/debug probe supporting SWD and serial communication.

This is not your regular debug probe as it has some neat features that other
debug probes don't provide. Magnum was designed to pack as many useful features
as possible into one small USB-dongle and minimizing the needed cables.

## Pass-through USB
Magnum connects to your PC via a USB-C cable. It has an onboard hub with a
USB-C plug, meaning that if your target also has a USB-C connector, you can
plug Magnum directly into your target. You now get all of the probe
functionality AND the target's USB connection with only a single cable. Due
to the onboard hub, it looks as though Magnum passes the USb connection
straight through.

## Target power managment
When using the target USB-C plug, Magnum can measure power on the VBUS supply
lines. This is useful to do simple power measurements. If the measurement
bandwidth is not high enough or if one simply want to "look" at the current as
a waveform (i.e. with a scope), there is an analog output that can be directly
connected to a scope or other analog measurement device. This analog output
reflects the real-time measured current as a voltage.

Additionally, Magnum allows to control the target's power using a load switch.
The USB hub has control over this too, so in normal operation if the host
detects an issue and attempts to reset the device, the hub's power control pin
will cycle target power. This can of course interfere with debugging and so
Magnum allows to override the hub's power control so the user can dictate when
power to the target is on or off. The default configuration is to let the USB
hub (and therefore the host) control the power state.

## Integrated serial port
A lot of debug probes don't provide an extra serial port. Not Magnum, it
integrates a debug serial port and makes it available on the same USB interface
with all other probe functionality. This serial port is part of the 10-pin
debug connector along with SWD and SWO.

One of the key differentiators, however, is that this debug serial port is also
mapped onto the target's USB-C connector's SBU lines. The SBU lines are not
defined in the USB-C specification and can be used/defined by the device
manufacturer. This means that if the target device connects its debug UART
signals to the SBU lines, then Magnum can act as a simple serial dongle with no
extra cables needed. It goes without saying that this also implies that the
debug UART lines can now be accessed without opening the target's enclosure.

Magnum uses the USB-C connector's CC lines to detect the connector orientation
and then automatically swaps the Rx/Tx signals.

