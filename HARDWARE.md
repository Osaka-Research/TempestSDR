# Hardware Requirements

TempestSDR does not capture signals itself — it decodes raw samples handed to
it by an actual SDR (Software Defined Radio) receiver. A phone, laptop WiFi
card, or any fixed-purpose radio **cannot** be used instead: those chips have
no way to retune to arbitrary frequencies and stream raw IQ samples, which is
what every plugin below requires.

## Supported receivers (by plugin, from this repo's source tree)

| Plugin | Hardware | Platform notes |
| --- | --- | --- |
| `TSDRPlugin_ExtIO` | Any ExtIO-compatible receiver (RTL-SDR, HackRF, Airspy, FUNcube, etc. via their ExtIO DLL) | Windows-only (ExtIO is a Windows DLL interface) |
| `TSDRPlugin_Mirics` | Dongles built on Mirics MSi001/MSi2500 chipsets | Cross-platform |
| `TSDRPlugin_SdrPlay` | SDRplay RSP1 / RSP2 / RSPduo | Needs the SDRplay API driver (`mir_sdr_api`, `sdrplay_api`) installed separately |
| `TSDRPlugin_UHD` | Ettus Research USRP boards | Needs UHD + Boost installed; built automatically on Linux/macOS |
| `TSDRPlugin_RawFile` | None — replays a previously recorded IQ file | For offline analysis/testing without any radio attached |

RTL-SDR dongles (the cheapest, most common entry point, ~$25-35) work through
the `ExtIO_RTL2832U` plugin on Windows; there is no native Linux RTL-SDR
plugin in this tree.

## Antenna

Any receiver above outputs electrical samples, not a picture — the antenna is
what actually picks up the compromising emanation. A simple wideband antenna
(e.g. a cheap log-periodic or Yagi) pointed at the target's video cable or
monitor housing, tuned near the leakage frequency the software estimates,
is standard practice. Higher pixel-clock signals (HDMI/DVI) leak at higher
frequencies than VGA and may need a receiver with wider frequency coverage
(HackRF/USRP) than a basic RTL-SDR can reach.

## Legal note

This toolkit works by intercepting unintentional electromagnetic emissions
from someone else's equipment. Only use it on hardware you own or are
explicitly authorized to test.
