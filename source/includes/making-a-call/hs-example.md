##Working with HotSchedules data  

The HotSchedules REST API provides a user-friendly way to obtain HS Data.  


### Examples  
Please ensure that API access has been enabled for your HotSchedules account. Contact customer service 1-866-753-3853 for access or questions.

The url path can look like any of the following, depending on which type is being queried:  
`../hotschedules/<concept_id>/<store_id>/<type_method>?`  

example:  
`../hotschedules/1/1/getDriversByInterval?..`

`../hotschedules/<concept_id>/<type_method>`

example:  
`../hotschedules/1/getStores?..`  

`../hotschedules/<type_method>`  

example:  
`../hotschedules/getConcept?..`

### Getting Data (Examples)
Note: Results are currently cached with a TTL of 60 minutes.

#### getConcept  
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/getConcept"```

#### getDriversByInterval  
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"```  

#### getEmpAvailability  
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getEmpAvailability?active_only=true"```  

#### getEmpInfo  
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getEmpInfo?active_only=true"```  

#### getEmpJobs
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getEmpJobs?active_only=true"```

#### getGroups
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/getGroups"```

#### getGuestCounts
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00"```

#### getLaborByBusDay
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getLaborByBusDay?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"```

#### getLaborByJobAndInterval
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getLaborByJobAndInterval?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"```

#### getProjectedSalesV3
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getProjectedSalesV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"```

#### getRCVs
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getRCVs"```

#### getSalesCats
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getSalesCats"```

#### getScheduleV3
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getScheduleV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"```

#### Example Results
```[{"outDate": {  
		"month": 5,
		"year": 2016,
		"day": 2
	},
	"jobHsId": 1111111,
	"payRate": 1,
	"inDate": {
		"month": 5,
		"year": 2016,
		"day": 2
	},
	"specialPay": 0,
	"empHSId": 222222,
	"ovtMinutes": 0,
	"inTime": {
		"hours": 9,
		"seconds": 0,
		"militaryTime": true,
		"minutes": 0
	}  ]
 ```

#### getShiftsV3
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getShiftsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"```

#### getStoreEmployees
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getStoreEmployees?active_only=true"```

#### getStoreJobs
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getStoreJobs"```

#### getStores
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/getStores?group_id=0"```

#### getTimeCards
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"```

#### getVolumeCounts
```curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE"```

### Writing Data (Examples)  
#### setTimeCardsV3
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{
  \"jobName\": \"Cook\",
  \"ovtTtl\": 0,
  \"ovtHrs\": 0,
  \"clockOut\": \"2016-07-31T22:05:00-05:00\",
  \"regWage\": 9,
  \"clockIn\": \"2016-07-30T15:56:00-05:00\",
  \"ovtWage\": 13.5,
  \"breakMinutes\": 0,
  \"jobId\": 16921407,
  \"businessDate\": {
    \"month\": 7,
    \"year\": 2016,
    \"day\": 31
  },
  \"regHrs\": 6.15,
  \"spcTtl\": 0,
  \"hsId\": 929931334634,
  \"spcHrs\": 0,
  \"ovtMins\": 0,
  \"storeNum\": 1,
  \"empPosId\": 1052,
  \"regTtl\": 55.35
}]"
```

#### setEmpJobs
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setEmpJobs?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setEmps
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setEmps?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setForecastDriversV2
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setForecastDriversV2?start_day=30&start_month=4&start_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setGuestCounts
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setGuestCounts?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setRVC
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setRVC?group=1&rvcId=1&rvcName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setSalesCat
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setSalesCat?group=1&salesCatId=1&salesCatName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```  

#### setSalesItemsV4
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setSalesItemsV4?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```

#### setTimeCardsDeclaredTips
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```  

#### setVolumeCountsV2
```curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setVolumeCountsV2" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"```