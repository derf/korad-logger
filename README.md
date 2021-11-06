# kaxxxxp-viewer - Data Logger and Viewer for KAxxxxP power supplies

**kaxxxxp-viewer** acquires and visualizes voltage and current data from
KAxxxxP power supplies. These are sold under brand names such as Korad or RND
Lab and equipped with a USB serial port, allowing them to be used as simple,
low-resolution measurement devices. See the [sigrok
wiki](https://sigrok.org/wiki/Korad_KAxxxxP_series) for details.

It has been successfully used with "RND 320-KA3005P" (single-channel) and "RND
320-KA3305P" (dual-channel) supplies. Observed attributes:

* Time resolution: **a few Hz**
* Voltage range: 0 .. 30 V
* Voltage resolution: 10 mV
* Current range: 0 .. 5 A
* Current resolution: 1 mA

Voltage and current range depend on the device, the resolutions are probably
identical.

**Warning:** In addition to reading voltage and current values, the serial
interface also supports *setting* them. This is not supported by
kaxxxxp-viewer. However, be warned that communication errors or bugs may cause
the power supply to receive a write command with an arbitrary voltage or
current value, which may result in damaged equipment, fire, or other harm. By
using this software, you acknowledge that you are aware of these risks.

See `bin/kaxxxxp-viewer --help` for usage details.

## Dependencies

* Python 3 with the following modules: numpy, serial
* Data Visualization (--plot): python3-matplotlib
