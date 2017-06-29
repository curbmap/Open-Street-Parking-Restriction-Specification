# Open Street Parking Restriction Specification
## Definitions
***All Date / Time / Week formats will be in ISO 8601 standard
All times represnted in UTC no time zones will be used to alleviate confusion***

All Rules are singular. Meaning one day, week, or month per rule

Field | Type | Values | Description | Properties
--|--|--|--|--|
**geohash**|string| geohash | A 12+ character geohash |
**parking**| integer | 1, 0 | 1 = yes, can park <br> 0 = cannot park|
**type**| string| meter, curb |  |
**side**| integer | N,S,E,W,NE,NW,SE,SW | 0 - north,<br> 1 - south,<br> 2 - east,<br> 3 - west,<br> 4 - northeast,<br> 5 - northwest,<br> 6 - southeast,<br> 7 - southwest |
**permit**| string|  commercial, residential, disability, none| type of permit and permit number or value |prop: 'value', null
**days**|string| "0000000" | days rule is active | 0 = not active, 1 = active, First bit is Monday
**weeks**|string| "0000" | weeks rule is active | 0 = not active, 1 = active, First bit is first week
**months**| string | "000000000000" | months rule is active | 0=not active, 1 = active, First bit is January
**start**| string |00:00:00 -> 23:59:59| time of rule start|
**end**| string |00:00:00 -> 23:59:59| time of rule end|
**location**|array |geojson |geojson data structure | "type": "Feature", "geometry" "type": "LineString", "coordinates": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]}

Metadata| | |
--|--|:--:
**Field**| **Description**| **required**
**standard**| standard of data formatting | *
**version**| version number of standard| *
**licence**| copyright or terms of use| *
**timestamp**| time created or last modified (ISO 8601 Extended Format, UTC)|
**extensions**| JSON array of objects  municipality [{},...] |
```
"Rule":{
  "geohash": "9q5ctr4xf65v"
  "parking": [1,0],
  "type": ["Meter", "Curb"],
  "sideofstreet":[ 0, 1, 2, 3, 4, 5, 6, 7 ],
  "permit": {type: ["commercial", "residential", "disability", "none"], value: [integer, null]},

  "effective":{
    "length":{
      "days": "0000000",    /* Monday = Bit 0 */
      "weeks": "0000",   /* First thursday of month = days: 0001000 weeks: 1000 */
      "months": "000000000000"  /* All months (year round): 111111111111 */
    },
    "time":{
      "start": "23:59:59",
      "end": "23:59:59"
    }
  },
  "location": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]],
  "metadata":{
    "standard": "OSPRS",
    "version": "0.0.1", 		//required
    "license": "Copyright, ...",	    //required
    "timestamp": "",
    "extensions": {
      [{
        meterID: 0x0203
        cost: 0.25 /* US Dollars */
        rate: 15 /* Minutes */
        }]
      }
    }
}
  ```
