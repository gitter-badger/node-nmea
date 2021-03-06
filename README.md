# node-nmea

[![npm version](https://badge.fury.io/js/node-nmea.svg)](http://badge.fury.io/js/node-nmea)
[![Build Status](https://travis-ci.org/leonciokof/node-nmea.svg)](https://travis-ci.org/leonciokof/node-nmea)
[![devDependency Status](https://david-dm.org/leonciokof/node-nmea/dev-status.svg)](https://david-dm.org/leonciokof/node-nmea#info=devDependencies)
[![Downloads](http://img.shields.io/npm/dm/node-nmea.svg)](https://npmjs.org/package/node-nmea)

Parser for NMEA sentences.

Available sentences:
* GPRMC - recommended minimum data for gps

Example: `$GPRMC,161006.425,A,7855.6020,S,13843.8900,E,154.89,84.62,110715,173.1,W,A*30`

Where:

Value         | Definition
--------------| ----------
RMC           | Recommended Minimum sentence C
161006.425    | Fix taken at 16:10:06.425 UTC
A             | Status A=active or V=Void.
7855.6020,S   | Latitude 78 deg 55.6020' N
13843.8900,E  | Longitude 138 deg 43.8900' E
154.89        | Speed over the ground in knots
84.62         | Track angle in degrees True
110715        | Date - 11 of July 2015
173.1,W       | Magnetic Variation in degrees
A             | FAA Mode A=autonomous, D=differential, E=estimated (dead-reckoning), M=manual input, S=simulated, N=data not valid, P=precise (4.00 and later)
\*30          | The checksum data, always begins with \*

## Parse data

```js
import * as nmea from "nmea"

const raw = "$GPRMC,161006.425,A,7855.6020,S,13843.8900,E,154.89,84.62,110715,173.1,W,A*30"
const data = nmea.parse(raw)
data.isValid() // true
data.raw // '$GPRMC,161006.425,A,7855.6020,S,13843.8900,E,154.89,84.62,110715,173.1,W,A*30'
data.type // RMC
data.datetime // Sat Jul 11 2015 13:10:06 GMT-0300 (CLT)
data.loc // { type: 'Point', coordinates: [ 138.73149999999998, -78.9267 ] }
data.speed // 286.85627999999997
data.track // '84.62'
data.magneticVariation // '173.1,W'
data.mode // 'Autonomous'
```

## Random data

```js
import * as nmea from "nmea"

const raw = nmea.randomData()
const data = nmea.parse(raw)
data.isValid() // true
data.raw // '$GPRMC,161006.425,A,7855.6020,S,13843.8900,E,154.89,84.62,110715,173.1,W,A*30'
data.time // '161006.425'
data.gpsStatus // 'A'
data.latitude // '7855.6020,S'
data.longitude // '13843.8900,E'
data.speed // '154.89'
data.track // '84.62'
data.date // '110715'
data.magneticVariation // '173.1,W'
data.faa // 'A'
data.checkSum // '30'
```
