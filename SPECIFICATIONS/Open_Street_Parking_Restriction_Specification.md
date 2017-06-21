# Open Street Parking Restriction Specification
## Definitions
***All Date / Time / Week formats will be in ISO 8601 standard
All times represnted in UTC no time zones will be used to alleviate confusion***

All Rules are singular. Meaning one day, week, or month per rule

|Field | Type | Values | Description | Properties|
|--|--|--|--|--|
|**parking**| string| yes, no | can or can't park |
|**type**| string| meter, curb | | 
|**sideofstreet**| string| N,S,E,W,NW,NE,SE,SW | N - north, S - south, E - east, W - west cordinal direction of placement| |
|**permit**| string|  commercial, residential, disability, none| type of permit and permit number or value |prop: 'value', null|
| **length**| string| day, week, month | total lenght of time rule is active| Day: 0 - 6, null; week: 1 - 4 , null ; month: 0 - 11 , null|
| **start**| string |00:00:00 -> 23:59:59| time of rule start| |
| **end**| string |00:00:00 -> 23:59:59| time of rule end| |	
| **location**|array |geojson |geojson data structure | "type": "Feature", "geometry" "type": "LineString", "coordinates": [[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]]}|

|Metadata| | |
--|--|:--:
|**Feild**| **Description**| **required**|
|**standard**| standard of data formating | *
|**version**| version number of standard| *
|**licence**| copyright or terms of use| *
| **timestamp**| time created or last modified|
|**geohash** | encoded lat long |

    "Rule":{
        "parking": ["Yes", "No"], 
        "type": ["Meter", "Curb"],
        "sideofstreet":[ "N","S","E","W"],
        "permit":["commercial", "residential", "disability", "none"],

    	"effective":{
        	"length":{
        		"day": "0 -> 6",    /* IOS Monday Start of week*/
        	    "week": "1 -> 4",   /* First thursday of month Day: 3 week: 1*/
                "month": "0 -> 11"  /* Only One Month Per Rule */
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
        	"standard": "OSPDS",
        	"version": "0.0.1", 		//required
        	"license": "Copyright, ...",	    //required 
        	"timestamp": "",
        	"geohash": ""
        }
    }