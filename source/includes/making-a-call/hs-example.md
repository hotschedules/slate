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


#### getConcept
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/getConcept?hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getDriversByInterval
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getEmpAvailability
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getEmpAvailability?active_only=true&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getEmpInfo
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getEmpInfo?active_only=true&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getEmpJobs
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getEmpJobs?active_only=true&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getGroups
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/getGroups?hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getGuestCounts
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

### getLaborByBusDay
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getLaborByBusDay?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getLaborByJobAndInterval
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getLaborByJobAndInterval?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getProjectedSales
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getProjectedSales?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getRCV
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getRCV?hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getSalesCats
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getSalesCats?hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getSchedule
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getSchedule?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getStoreEmployees
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getStoreEmployees?active_only=true&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getStoreJobs
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getStoreJobs?active_only=true&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getStores
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/getStores?group_id=0&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getTimeCards
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`

#### getVolumeCounts
`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<organization_name>/controllers/vertx/hotschedules/1/1/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE&hsusr=<hs_api_username>&hspwd=<hs_api_password>"`
