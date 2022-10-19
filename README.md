# SR-FRS Radio Module Programming not for SA818

My friend (W6IPA) and I developed a versatile Raspberry-Pi hat that
can be used for Allstar, Echolink, APRS, or any digital modes.

We use the program in this GitHub repository to program the radio
module SR-FRS used for the Pi-Hat.

**Before programming the SR-FRS module, make sure you consult the band
plan for your country and transmit on a frequency you are allowed to
use.**

## Intallation

```
$ git clone https://github.com/jumbo5566/SRFRS

```

## Example

```
[root@allstar ~]# python srfrs.py version
SRFRS: INFO: Firmware version: 110U-V223

[root@alarmpi SRFRS]# python srfrs.py radio --frequency 438.500
SRFRS: INFO: +DMOSETGROUP:0, RX frequency: 438.5000, TX frequency: 438.5000, squelch: 4, OK

[root@alarmpi SRFRS]# python srfrs.py radio --frequency 438.500 --offset -5
SRFRS: INFO: +DMOSETGROUP:0, RX frequency: 438.5000, TX frequency: 433.5000, squelch: 4, OK

[root@allstar ~]# python srfrs.py radio --frequency 145.230 --offset -.6 --ctcss 100
SRFRS: INFO: +DMOSETGROUP:0, RX frequency: 145.2300, TX frequency: 144.6300, ctcss: 100.0, squelch: 4, OK

[root@allstar ~]# python srfrs.py volume --level 5
SRFRS: INFO: +DMOSETVOLUME:0 Volume level: 5
```

If you use an FTDI dongle to program the SRFRS module the USB port can
be specified with the `--port` argument

```
[root@allstar ~]# python srfrs.py --port /dev/ttyAMA0 volume --level 5
SRFRS: INFO: +DMOSETVOLUME:0 Volume level: 5
```

## Usage

This program has for sections:

 - radio: Program the radio's frequency, tone and squelch level
 - volume: Set the volume level
 - filters: Turn on or off the [pre/de]-emphasis and as well as the high and low pass filter
 - version: display the firmware version of the SA818 module

```
usage: sa818 [-h] [--port PORT] [--debug]
                {radio,volume,filters,version} ...

generate configuration for switch port

positional arguments:
  {radio,volume,filters,version}
    radio               Program the radio (frequency/tome/squelch)
    volume              Set the volume level
    filters             Set filters
    version             Show the firmware version of the SA818

optional arguments:
  -h, --help            show this help message and exit
  --port PORT           Serial port [default: linux console port]
  --debug
```

### Radio

```
usage: srfrs radio [-h] --frequency FREQUENCY [--offset OFFSET]
                      [--squelch SQUELCH] [--ctcss CTCSS | --dcs DCS]

optional arguments:
  -h, --help            show this help message and exit
  --frequency FREQUENCY
                        Transmit frequency
  --offset OFFSET       0.0 for no offset [default: 0.0]
  --squelch SQUELCH     Squelch value (1 to 9) [default: 4]
  --ctcss CTCSS         CTCSS (PL Tone) 0 for no CTCSS [default: None]
  --dcs DCS             DCS code must me the number followed by [N normal] or
                        [I inverse] [default: None]
```

### Volume

```
usage: sa818 volume [-h] [--level LEVEL]

optional arguments:
  -h, --help     show this help message and exit
  --level LEVEL  Volume value (1 to 8) [default: 4]
```


## CTCSS codes (PL Tones 38 Sets)

```
67.0, 71.9, 74.4, 77.0, 79.7, 82.5, 85.4, 88.5, 91.5, 94.8, 97.4,
100.0, 103.5, 107.2, 110.9, 114.8, 118.8, 123.0, 127.3, 131.8, 136.5,
141.3, 146.2, 151.4, 156.7, 162.2, 167.9, 173.8, 179.9, 186.2, 192.8,
203.5, 210.7, 218.1, 225.7, 233.6, 241.8, 250.3
```

## DCS Codes not support YET




[1]: http://www.sunrisedigit.com/upload/file/1558943384.rar
