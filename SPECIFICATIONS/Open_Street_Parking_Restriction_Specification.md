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
**curb_type**| JSON | {color: "", duration_allowed: n} | A description of the curb and its corresponding meaning | color(string), duration_allowed(integer number of minutes allowed to park)
**side**| integer | 0 - north,<br> 1 - south,<br> 2 - east,<br> 3 - west,<br> 4 - northeast,<br> 5 - northwest,<br> 6 - southeast,<br> 7 - southwest | cardinality |
**orientation**| integer | 0 = parallel, 1 = perpendicular (head in), 2 = perpendicular (no restriction), 3 = acute (45 degree) | The orientation at which a driver may park |
**permit**| string|  commercial, residential, disability, none| type of permit and permit number or value |prop: 'value', null
**days**|string| "0000000" | days rule is active | 0 = not active, 1 = active, First bit is Monday
**weeks**|string| "0000" | weeks rule is active | 0 = not active, 1 = active, First bit is first week
**months**| string | "000000000000" | months rule is active | 0=not active, 1 = active, First bit is January
**start**| integer | 0 -> 1440 | time of rule start(minutes)|
**end**| integer | 0 -> 1440 | time of rule end (minutes)|
**location**|array | coordinates only | array of points in [longitude,latitude] format  | [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]

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
  "curb_type": { color: string, duration_allowed: integer(minutes) },
  "sideofstreet":0 -> 7,
  "orientation": 0 -> 3
  "permit": {type: ["commercial", "residential", "disability", "none"], value: [integer, null]},

  "effective":{
    "length":{
      "days": "0000000",    /* Monday = Bit 0 */
      "weeks": "0000",   /* First thursday of month = days: 0001000 weeks: 1000 */
      "months": "000000000000"  /* All months (year round): 111111111111 */
    },
    "time":{
      "start": "1320", /* 10pm */
      "end": "1440" /* 12am */
    }
  },
  "location": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]],
  "metadata":{
    "standard": "OSPRS",
    "version": "0.0.0", 		//required
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
