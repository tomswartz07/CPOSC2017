# CPOSC Talk 2017: Software Defined Radio
## Listening to the bleeps and bloops around you

## About This Repository
This repository contains several items that are useful to those who are
interested in SDR and would like some 'quick-start' resources.

### Quick Start
> Help! I don't have an SDR, and I'm too impatient to wait for Amazon Prime to deliver one to me!

Never fear, Web SDR is here!

Check out [WebSDR.org](http://websdr.org/) to get started using Software Defined Radio right away.

Keep in mind that these are somewhat limited in frequency ranges, a device you have/own locally
can (typically) tune from 24MHz to 1.7GHz.

> Okay, I ordered an SDR and now what do I do?

Well, read on, intrepid radio user!

## Commands and Programs Used/Mentioned in Talk

- [GQRX](http://gqrx.dk/): Used for general tuning and reception
- [Multimon-ng](https://github.com/EliasOenal/multimon-ng/): POCSAG/Pager decoding. Used in conjunction with NetCat and SOX audio manipulation.
- [Dump1090](https://github.com/antirez/dump1090): Used to display ADS/B Airplane Tracking.
- [RTL_433](https://github.com/merbanan/rtl_433): Used to decode ISM devices; thermometers, doorbells, Tire Pressure Sensors, etc.
- [Robot36](https://play.google.com/store/apps/details?id=xdsopl.robot36): Android App used to decode SSTV images from ISS and ham radio bands.
- [WXtoImg](http://www.wxtoimg.com/): Slightly out-of-date program used to decode NOAA Satellite Telemetry.

GQRX has a feature which allows for UDP streaming of any captured signal.
Using Unix-y philosophy, we could integrate netcat (`nc`) to allow various command-line programs to interpret the audio from the RTL-SDR.

For example, to decode POCSAG messages, start the UDP stream feature and run:
```bash
nc -l -u -p 7355 | sox -t raw -esigned-integer -b16 -r \
48000 - -esigned-integer -b16 -r 22050 -t raw - | \
multimon-ng -t raw -a SCOPE -a POCSAG512 -a POCSAG1200 -a POCSAG2400 -f alpha -
```

This will take the raw I/Q signals from GQRX, perform audio levelling and sample rate modifications,
then pass it to Multimon-NG for decoding.

It's also possible to change the arguments for Multimon-NG to allow for decoding of Morse Code and several other
signal types.

## Software Defined Radio Frontends
GQRX is an excellent Linux and Mac based SDR frontend.
It has a very easy to use interface in addition to support for many of the common SDR hardware devices.

More information, including download links, can be found at the [GQRX Homepage](http://gqrx.dk/).

If you're using Windows; follow the [SDR# Setup guide](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/).

Also of interest might be the [Big List of SDR Software](https://www.rtl-sdr.com/big-list-rtl-sdr-supported-software/)

Included in this repo is a Lancaster-County specific Bookmarks file.
This will allow for quick setup of bookmarks, which indicate the frequency, type, origin, and mode of common
broadcasts in Lancaster County and surrounding areas.

**Linux Setup:**
Copy the bookmarks file to `~/.config/gqrx/bookmarks.csv`

## Setting Up Your RTL-SDR
If your RTL-SDR device has a Temperature Controlled Crystal Oscillator (TCXO), you can forego this step.

The commonly available inexpensive RTL-SDR devices use commonly available crystal oscillators.
Because of the generic quality of these oscillators, the tuning accuracy of the RTL-SDR
can 'drift' over time.

It's ideal that the first time the RTL-SDR is used, you calibrate it against a known,
strong signal. Doing so will ensure that you're correctly tuning to the correct frequency.

I would recommend tuning to one of the NOAA weather radio frequencies accessible in your area.

You will find NOAA broadcasts on one of the following frequencies:

- 162.400 MHz
- 162.425 MHz
- 162.450 MHz
- 162.475 MHz
- 162.500 MHz
- 162.525 MHz
- 162.550 MHz

Set the tuner to exactly one of these frequencies (whichever is strongest), then
adjust your PPM/Frequency Correction value until the exact center of the signal
is directly underneath your tuner selection bar.

Be sure to check your calibration often, as changes in temperature (the RTL-SDR can get warm)
will subtly affect the frequency, which can lead to errors in tuning.

## Going Further

As you get more familiar with the SDR, you might find that you require certain specific items to
catch that one extra signal.

### Low or High Frequencies
An unmodified RTL-SDR can receive signals from around 24MHz to 1700MHz.
If you desire to listen to frequencies outside of this range, you will need to have
an up-converter, or down-converter. These devices will 'move' signals up or down, into the
listening range of the SDR.

I would recommend that an Up-Converter would be purchased first, as there are a large number
and variety of signals that can be observed on frequencies from 0Hz to 24Mhz.

The Ham-It-Up and SpyVerter are the two most popular up-converters offered at a reasonable price.

High frequencies can be 'down-converted' by using a modified SUP-2400 DirecTV device.
Check out [RTL-SDR.com](https://www.rtl-sdr.com/modded-sup-2400-downconverters-now-available-at-rxtxdx-com-for-25/) for more info.

## Transmitting

It's possible to combine your SDR with a Raspberry Pi device to 'replay' certain
transmissions.

I've successfully been able to control wireless light switches, doorbells, 
and temperature sensors.

**PLEASE BE AWARE THAT YOU MUST BE LICENSED IN ORDER TO TRANSMIT ON MOST FREQUENCIES**

Projects such as [RPiTx](https://github.com/F5OEO/rpitx) allow to replay captured SDR data.

**PLEASE BE AWARE THAT YOU MUST BE LICENSED IN ORDER TO TRANSMIT ON MOST FREQUENCIES**

If you're interested in transmitting on licensed frequencies, check out 
[ARRL](http://www.arrl.org/) for information on obtaining an amateur radio license.
