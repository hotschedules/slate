##Working with Macromatix Data
###MX RDS API

The mxrds api provides a RESTful way to access data stored in Macromatix RDS database

####Access Control
A Bearer Token is required to make calls to the service, ask the team to generate one for you

####Store endpoints
Returns store information as well as store roster

#####Get all stores

`
GET https://api.mxrds.io/<namespace>/stores
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/stores
`

#####Get store by store id

`
GET https://api.mxrds.io/<namespace>/stores/<store-id>
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/stores/<store-id>
`

#####Get store roster

`
GET https://api.mxrds.io/<namespace>/stores/<store-id>/roster
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/stores/<store-id>/roster
`

####Employee endpoints
Returns employee information

#####Get all employees

`
GET https://api.mxrds.io/<namespace>/employees
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/employees
`

#####Get employee by employee id

`
GET https://api.mxrds.io/<namespace>/employees/<employee-id>
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/employees
`

####Calendar endpoints
Returns the fiscal calendar

#####Get fiscal calendar by year

`
GET https://api.mxrds.io/<namespace>/calendar/<year>
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/calendar/<year>
`

####Resources endpoints
Returns resources filtered by store id and date of business

#####Get resource by store id and date of business
Store is required, DOB will use the current day if not specified

`
GET https://api.mxrds.io/<namespace>/resources/<resource>?store=<store-id>&dob=<yyyy-mm-dd>
`

#####List of resources  
/inventorywaste  
/inventorytransfer  
/inventorycount  
/forecast  
/salesitemforecast  
/inventoryforecast  
/roster  
/salestransaction  
/salesitem  
/depletion  
/schedule  
/timecards  
/paidinpaidout  
/settlement  
/storesettlementdetails  


####Admin endpoints
These endpoints can only be accessed by the mxrds api admin, they are meant to add or update customer configurations

#####New user config

`
POST https://api.mxrds.io/<namespace>/settings
`
ie.
`
curl -X POST -H 'Content-Type:application/json' -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/settings -d '{"token":"<bearer-token>","host":"<rds-host>","port":<rds-port>,"database":"<database>"}'
`

#######response

`
Code 201
`

#####Update existing config

`
PUT https://api.mxrds.io/<namespace>/settings
`
ie.
`
curl -X PUT -H 'Content-Type:application/json' -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/settings -d '{"token":"<bearer-token>","host":"<rds-host>","port":<rds-port>,"database":"<database>"}'
`
#######response
`
Code 204 
`

#####Get existing config

`
GET https://api.mxrds.io/<namespace>/settings
`
ie.
`
curl -H 'Authorization:Bearer <admin-token>' https://api.mxrds.io/<namespace>/settings
`
#######response

`
Code 200 {
  token: <token>,
  host: <host>,
  port: <port>,
  database: <database>
}
`

####Public endpoints

The following endpoints are the only ones that do not require bearer token authorization

#####Healthcheck

`
GET https://api.mxrds.io/
`
ie.
`
curl https://api.mxrds.io/
`
#######response

`
Code 200
Response {
  ping: true
}
`

#####App Info

Returns the name and version of the app
`
GET https://api.mxrds.io/info
`
ie.
`
curl https://api.mxrds.io/info
`
#######response

`
Code 200
Response {
  "name":"<app-name>",
  "version":"<version>"
}
`

#####Facts

Returns the system and environment information
`
GET https://api.mxrds.io/facts
`
ie.
`
curl https://api.mxrds.io/facts
`
#######response

`
Code 200
Response ie. {
    "os": "Linux",
    "isWindows": false,
    "isMac": false,
    "isLinux": true,
    "isBSD": false,
    "isSolaris": false,
    "platform": "linux/4.4.8-20.46.amzn1.x86_64",
    "title": "rds-api",
    "pid": 16849,
    "hostname": "ip-172-31-10-180",
    "arch": "x64",
    "cpu": "Intel(R) Xeon(R) CPU E5-2650 0 @ 2.00GHz",
    "speed": 1795,
    "cores": 1,
    "ram": 605.948,
    "cwd": "/var/app/current",
    "main": "/var/app/current/index.js",
    "paths": ["/var/app/current/node_modules", "/var/app/node_modules", "/var/node_modules", "/node_modules"],
    "process": "node/v4.4.3",
    "node_env": "not-set",
    "startedAt": "2016-06-14T23:02:19.021Z"
}
`

####getSalesItem

#####Request  
`curl -H '<bearer_toke>' https://api.mxrds.io/walmart/resources/salesitem?store=1&dob=2016-06-24`

#####Response  
`[{  "storeid": "1",
	"businessday": "2016-06-24T00:00:00.000Z",  
	"itemcode": "Undefined",
	"description": "All undefined sales items",
	"postransactionid": "1221",
	"registernumber": 4,
	"clerkkey": "3141414",
	"clerkname": "Brandon",
	"clerkid": null,
	"amount": "0.0000",
	"quantity": 1,
	"tax": "0.0000",
	"salescost": "0.0000"
}, {
	"storeid": "1",
	"businessday": "2016-06-24T00:00:00.000Z",
	"itemcode": "52791",
	"description": "Green Bns Sm",
	"postransactionid": "01011991",
	"registernumber": 4,
	"clerkkey": "28928",
	"clerkname": "Brandon",
	"clerkid": null,
	"amount": "0.0000",
	"quantity": 1,
	"tax": "0.0000",
	"salescost": "0.1129"
}]`

####getSalesItemForecast   

#####Request  
`curl -H 'Authorization:Bearer eyJhbGciOiJIUzI1NiJ9.cmRzLWFwaS1rZmNsdmw.AMtNZJqloEmC8hqfe6QbpxyBHytmU7RQqhZQD4nVO_Y' "https://api.mxrds.io/kfclvl/resources/salesitemforecast?store=179&dob=2016-06-24"`

#####Response  
`[{
	"description": "All undefined sales items",
	"itemcode": "Undefined",
	"intervalstart": "2016-06-24T10:30:00.000Z",
	"storeid": "23232",
	"businessday": "2016-06-24T00:00:00.000Z",
	"raw_forecast": 2,
	"system_forecast": 2,
	"user_forecast": 2
}, {
	"description": "Or foo",
	"itemcode": "232323",
	"intervalstart": "2016-06-24T10:30:00.000Z",
	"storeid": "23233",
	"businessday": "2016-06-24T00:00:00.000Z",
	"raw_forecast": 0.6,
	"system_forecast": 1,
	"user_forecast": 1
}, {
	"description": "Or stuff",
	"itemcode": "12121",
	"intervalstart": "2016-06-24T10:30:00.000Z",
	"storeid": "179",
	"businessday": "2016-06-24T00:00:00.000Z",
	"raw_forecast": 0.6,
	"system_forecast": 1,
	"user_forecast": 1
}]`
