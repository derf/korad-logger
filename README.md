# korad-logger - Data Logger and Controller for KAxxxxP power supplies

**korad-logger** acquires and visualizes voltage and current data from
KAxxxxP power supplies. These are sold under brand names such as Korad or RND
Lab and equipped with a USB serial port, allowing them to be used as simple,
low-resolution measurement devices. See the [sigrok
wiki](https://sigrok.org/wiki/Korad_KAxxxxP_series) for details.

korad-logger is capable of performing simple control tasks, such as stepping
through voltage/current slopes for automated I-V curve measurements, and
displaying live data.

It has been successfully used with "RND 320-KA3005P" (single-channel) and "RND
320-KA3305P" (dual-channel) supplies, and should work with similar variants as
well. Observed attributes:

* Time resolution: 10 .. 24 Hz
* Voltage range: 0 .. 30 V
* Voltage resolution: 10 mV
* Current range: 0 .. 5 A
* Current resolution: 1 mA

Voltage and current range depend on the device, the resolutions are probably
identical.

**Warning:** The KAxxxxP serial interface supports both reading current/voltage
data and writing current/voltage limits. korad-logger uses these to change
PSU attributes at runtime, if requested. The serial protocol does not use
checksums or similar mechanisms, so communication errors or bugs may cause the
power supply to receive a write command with an arbitrary voltage or current
value. This may result in damaged equipment, fire, or other harm. By using
this software, you acknowledge that you are aware of these risks.

See `bin/korad-logger --help` for usage details.

## Examples

Log voltage and current of a manually configured PSU whose output is already
enabled. Press Ctrl+C to exit. You may also specify a timeout in seconds
("0" means no timeout).

```
bin/korad-logger --save logfile 0
```

Generate an I-V curve for a power LED supporting up to 200mA and a voltage
limit of 5V. The output is turned on at the start of the measurement and
turned off at the end.

```
bin/kaxxxxp-viewer --voltage-limit 5 --current-range '0 0.2 0.001' --save led.log 210
```

## Dependencies

* Python 3 with the following modules: numpy, serial
* Data Visualization (--plot): python3-matplotlib

## Related work

This is by far not the first project for korad PSU logging and control. See also:

* [libsigrok](https://sigrok.org/wiki/Korad_KAxxxxP_series)
* [koradctl](https://github.com/attie/koradctl)
* [KoradControl](https://github.com/maximaximal/KoradControl)
* [Korad-KA6003P-Software](https://github.com/Tamagotono/Korad-KA6003P-Software)
