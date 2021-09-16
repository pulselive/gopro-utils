# GoPro Metadata Format Parser

## Introduction

This is a fork of [JuanIrache gopro-utils](https://github.com/JuanIrache/gopro-utils) that retains only the package, to be used in other Golang code.

## Upstream info

**I have recently switched my efforts to a more comprehensive [JavaScript version of these tools](https://github.com/JuanIrache/gopro-telemetry), but feel free to send a PR if you think you can improve this one**

Examples of what can be achieved: https://goprotelemetryextractor.com/gallery

User friendly and cross-platform tool for extracting the telemetry: https://goprotelemetryextractor.com/free

## The Protocol

Data starts with a label that describes the data following it. Values are all big endian, and floats are IEEE 754. Everything is packed to 4 bytes where applicable, padded with zeroes so it's 32-bit aligned.

- **Labels** - human readable types of proceeding data
- **Type** - single ascii character describing data
- **Size** - how big is the data type
- **Count** - how many values are we going to get
- **Length** = size \* count

Labels include:

- `ACCL` - accelerometer reading x/y/z
- `DEVC` - device
- `DVID` - device ID, possibly hard-coded to 0x1
- `DVNM` - devicde name, string "Camera"
- `EMPT` - empty packet
- `GPS5` - GPS data (lat, lon, alt, speed, 3d speed)
- `GPSF` - GPS fix (none, 2d, 3d)
- `GPSP` - GPS positional accuracy in cm
- `GPSU` - GPS acquired timestamp; potentially different than "camera time"
- `GYRO` - gryroscope reading x/y/z
- `SCAL` - scale factor, a multiplier for subsequent data
- `SIUN` - SI units; strings (m/s², rad/s)
- `STRM` - ¯\\\_(ツ)\_/¯
- `TMPC` - temperature
- `TSMP` - total number of samples
- `UNIT` - alternative units; strings (deg, m, m/s)

Types include:

- `c` - single char
- `L` - unsigned long
- `s` - signed short
- `S` - unsigned short
- `f` - 32 float

For implementation details, see `reader.go` and other corresponding files in `telemetry/`.
