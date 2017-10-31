# CPOSC Talk 2017: Software Defined Radio
## Listening to the bleeps and bloops around you

### About This Repository
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

#### Commands and Programs Used/Mentioned in Talk

- [GQRX](http://gqrx.dk/): Used for general tuning and reception
- [Multimon-ng](https://github.com/EliasOenal/multimon-ng/): POCSAG/Pager decoding. Used in conjunction with NetCat and SOX audio manipulation.
- [Dump1090](https://github.com/antirez/dump1090): Used to display ADS/B Airplane Tracking.
- [RTL_433](https://github.com/merbanan/rtl_433): Used to decode ISM devices; thermometers, doorbells, Tire Pressure Sensors, etc.
- [Robot36](https://play.google.com/store/apps/details?id=xdsopl.robot36): Android App used to decode SSTV images from ISS.
- [WXtoImg](http://www.wxtoimg.com/): Slightly out-of-date program used to decode NOAA Satellite Telemetry.

#### Software Defined Radio Frontends
GQRX is an excellent Linux and Mac based SDR frontend.
It has a very easy to use interface in addition to support for many of the common SDR hardware devices.

More information, including download links can be found at the [GQRX Homepage](http://gqrx.dk/).

Included in this repo is a Lancaster-County specific Bookmarks file.
This will allow for quick setup of bookmarks, which will indicate the type, origin, and mode of common
broadcasts in Lancaster County and surrounding areas.

**Linux Setup:**
Copy this file to `~/.config/gqrx/bookmarks.csv`

If you're using Windows; follow the [SDR# Setup guide](https://www.rtl-sdr.com/rtl-sdr-quick-start-guide/).

Also of interest might be the [Big List of SDR Software](https://www.rtl-sdr.com/big-list-rtl-sdr-supported-software/)

#### Setting Up Your RTL-SDR
If your RTL-SDR device has a Temperature Controlled Crystal Oscillator (TCXO), you can forego this step.

The commonly available inexpensive RTL-SDR devices use commonly available crystal oscillators.
Because of the generic quality of these oscillators, the tuning accuracy of the RTL-SDR
can 'drift' over time.

It's ideal that the first time the RTL-SDR is used, you calibrate it against a known,
strong signal. Doing so will ensure that you're correctly tuning to the correct frequency.

I would recommend tuning to one of the NOAA weather radio frequencies accessible in your area.

You will find NOAA broacasts on one of the following frequencies:

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

