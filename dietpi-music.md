Some notes to install and configure music services on a RaspberryPi running DietPi OS.

## ALSA devices

```
% aplay -l
```

In our case we can spot our USB DAC
```
card 1: m9XX [m9XX], device 0: USB Audio [USB Audio]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```

## Raspotify

Configuration file on dietpi is `/etc/default/raspotify`
Look for the line with `OPTIONS=...` and stick the device `plughw:<card number>:<subdevice>`.

```
OPTIONS="--device plughw:1,0"
```

More info https://www.volkerschatz.com/noise/alsa.html

## Shairport-sync

Configuration file is `/usr/local/etc/shairport-sync.conf`

Slighly different device string syntax, to see the device attached to your RaspberryPi, use
```
shairport-sync -h
```

And look at the bottom of the output after "hardware output devices:"

To restart shairport-sync, in case you made changes in the configuration file:

```
sudo dietpi-services restart shairport-sync
```

## Testing the device

```
speaker-test -t sine -f 500 -D plughw:1,0
```

## More info

https://www.jackenhack.com/shairport-crashing-when-using-usb-dac-with-raspberry-pi/




