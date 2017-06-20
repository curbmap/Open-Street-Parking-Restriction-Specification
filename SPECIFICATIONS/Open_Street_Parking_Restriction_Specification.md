# Open Street Parking Restriction Specification
## Definitions
##All Date / Time / Week formats will be in ISO 8601 standard
##all times represnted in UTC no time zones will be used to alleviate confusion


## All Rules are singular.

Rule:{
	parking: Yes, No 
	type: Meter, Curb,
	Sideofstreet: N - north, S - south, E - east, W - west
	permit: commercial, residential, disability, none{
		prop: 'value', null
	}

	Effective:{
		Length:{
				Day: 0 - 6, null
	           	week: 1 - 4 , null ## eg: First thursday of month Day: 3 week: 1
	           	Month: 0 - 11 , null ## Only One Month Per Rule
	       	},
	 	Time:{
	 			Start: 23:59:59,
	 			End: 23:59:59
	 		}
	},
	## All Geospatial data will be represented in GEOJSON as Point or LineString
	{
	  "type": Feature,
	  "geometry": {
	    "type": "LineString",
	          "coordinates": [
	            	[102.0, 0.0], [103.0, 1.0], [104.0, 0.0], [105.0, 1.0]
	            ]
	},
	metadata:{
		standard: V0.0.1 			##required
		licence: Copyright, ...	    ##required 
		timestamp:
		geohash:
	}
}



