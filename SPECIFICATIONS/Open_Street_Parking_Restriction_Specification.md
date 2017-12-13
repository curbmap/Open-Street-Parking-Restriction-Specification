# Open Street Parking Restriction Specification
## Definitions
***All timestamps will be in ISO 8601 standard.
All times represnted in UTC, and no time zones will be used to alleviate confusion***

All Rules are singular. Meaning one day, week, or month per rule

Field | Type | Values | Description | Properties
--|--|--|--|--|
**id**|string| open location code | A >= 12 character plus code, 8 character location + 4 or more further specification | http://openlocationcode.com/<br>https://github.com/google/open-location-code implementations(Apache-2.0 License)
**parking**| integer | 1, 0 | 1 = yes, can park <br> 0 = cannot park|
**type**| integer| 0->13 | A description of the restriction type | see type table below
**duration**| integer | 0->1440 | A description of the length of the restriction (i.e. 2hour parking would be 120) | integer number of minutes allowed to park
**permit** | string | permit type | The permit type i.e. "Taxi" or "113" or "BB" | see table below
**side**| integer | 0 - north,<br> 1 - south,<br> 2 - east,<br> 3 - west,<br> 4 - northeast,<br> 5 - northwest,<br> 6 - southeast,<br> 7 - southwest | cardinality |
**angle**| integer | 0 = parallel, 1 = perpendicular (head in), 2 = perpendicular (no restriction), 3 = acute (45 degree) | The orientation at which a driver may park |
**days**|array (integer)| [0,0,0,0,0,0,0] | days rule is active | 0 = not active, 1 = active, First integer is Monday (starting on left)
**weeks**|string (integer)| [0,0,0,0] | weeks rule is active | 0 = not active, 1 = active, First integer is first week (starting on left)
**months**| string (integer) | [0,0,0,0,0,0,0,0,0,0,0,0] | months rule is active | 0=not active, 1 = active, First integer is January (starting on left)
**start**| integer | 0 -> 1440 | local time of rule start(minutes)|
**end**| integer | 0 -> 1440 | local time of rule end (minutes)|
**location**|array | coordinates only | array of points in [longitude,latitude] format  | [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]
**holiday**|bit | 1/0 | enforced during holidays = 1, not enforced during city celebrated holidays | True or False 
**vehicle_type**|integer| 0 -> 3 | vehicle type allowed | From vehicle type table below

**Type table**

| Integer value | Associated Restriction                                |
|---------------|-------------------------------------------------------|
| 0             | Short time limit (AKA green, <1hr)                    |
| 1             | Short time limit metered (AKA green with meter, <1hr) |
| 2             | Time limit (>=1hr )                                   |
| 3             | Time limit metered (>=1hr)                            |
| 4             | Time limit with permit exemption                      |
| 5             | No parking                                            |
| 6             | No parking with permit exemption                      |
| 7             | No stopping                                           |
| 8             | Fire hydrant                                          |
| 9             | Street cleaning                                       |
| 10            | Disabled parking                                      |
| 11            | Passenger loading (AKA white)                         |
| 12            | Commercial loading (AKA yellow)                       |
| 13            | Other                                                 |

**Permit table**

| Permits                                  |
|------------------------------------------|
| Commercial                               |
| Taxi                                     |
| Disabled                                 |
| Other                                    |
| Permit name for restriction              |

**Vehicle table**

| Integer | Type                                                    |
|---------|---------------------------------------------------------|
| 0       | Car, Truck (2 axel), Non-inhabiting                     |
| 1       | Motorcycle                                              |
| 2       | Truck, Bus (3+ axel, including trailer), Non-inhabiting |
| 3       | Vehicle for inhabitation (Camper, Car, Truck, etc.)     |

Metadata| | |
--|--|:--:
**Field**| **Description**| **required**
**standard**| standard of data formatting | *
**version**| version number of standard| *
**licence**| copyright or terms of use, and this format is being released under the MIT license| *
**timestamp**| time created or last modified (ISO 8601 Extended Format, UTC)|
**extensions**| JSON array of objects  municipality [{},...] |
```
"Rule":{
  "id": "85633Q34+CRMM"
  "parking": [1,0],
  "type": integer,
  "duration": integer(minutes),
  "permit": "1", /* since some cities like SF use Letters */
  "sideofstreet":0 -> 7,
  "angle": 0 -> 3,
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
  "holiday" : False,
  "metadata":{
    "standard": "OSPRS",
    "version": "0.0.0", 		//required
    "license": "Copyright, ...",	//required
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
