# Open Street Parking Restriction Specification
## Definitions
***All Date / Time / Week formats will be in ISO 8601 standard
All times represnted in UTC no time zones will be used to alleviate confusion***

All Rules are singular. Meaning one day, week, or month per rule

|Field | Type | Values | Description | Properties|
|--|--|--|--|--|
|**id**|string| municipality dependent | this could be a region_zone_street_number | |
|**parking**| string| yes, no | yes = can or no = can't park |
|**type**| string| meter, curb | | 
|**sideofstreet**| string| N,S,E,W,NW,NE,SE,SW | N - north, S - south, E - east, W - west cordinal direction of placement| |
|**permit**| string|  commercial, residential, disability, none| type of permit and permit number or value |prop: 'value', null|
|**effective**||||
|**length**||||
|**days**|string| "0000000" | days rule is active | 0 = not active, 1 = active, First bit is Monday |
|**weeks**|string| "0000" | weeks rule is active | 0 = not active, 1 = active, First bit is first week |
|**months**| string | "000000000000" | months rule is active | 0=not active, 1 = active, First bit is January |
|**start**| string |00:00:00 -> 23:59:59| time of rule start| |
|**end**| string |00:00:00 -> 23:59:59| time of rule end| |	
|**location**|array |geojson |geojson data structure | "type": "Feature", "geometry" "type": "LineString", "coordinates": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]}|

|Metadata| | |
--|--|:--:
|**Field**| **Description**| **required**|
|**standard**| standard of data formating | *
|**version**| version number of standard| *
|**licence**| copyright or terms of use| *
|**timestamp**| time created or last modified (ISO 8601 Extended Format, UTC)|
|**extensions**| JSON extension per municipality |

    "Rule":{
        "id": District11_West_LA_Olympic_11377W
        "parking": ["Yes", "No"], 
        "type": ["Meter", "Curb"],
        "sideofstreet":[ "N","S","E","W"],
        "permit":["commercial", "residential", "disability", "none"],

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

        "location":{
	        "type": "Feature",
	        "geometry": {
	        	"type": "LineString",
	        	"coordinates": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]
	        }
		},
        "metadata":{
        	"standard": "OSPRS",
        	"version": "0.0.1", 		//required
        	"license": "Copyright, ...",	    //required 
        	"timestamp": "",
        	"extensions": {
                meter: {
                    cost: 0.25 /* US Dollars */
                    rate: 15 /* Minutes */
                }
            }
        }
    }