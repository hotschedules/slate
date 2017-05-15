##Working with HotSchedules data  

The HotSchedules REST API provides a user-friendly way to obtain HS Data.  


Please ensure that API access has been enabled for your HotSchedules account. Contact customer service 1-866-753-3853 for access or questions.

The url path can look like any of the following, depending on which type is being queried:
<br>
`../hotschedules/<concept_id>/<store_id>/<type_method>?`
<br>
`../hotschedules/<concept_id>/<type_method>?`
<br>
`../hotschedules/<type_method>?`

<aside class="notice"> <strong>FETCHING DATA METHODS</strong> </aside>

Note: Results are currently cached with a TTL of 60 minutes.



#### getConcepts  
This method returns a list of concepts for a company.

`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/getConcepts"`

> **Sample JSON response:**

```
  [
    {
      "name": "HotSchedules",
      "extId": 13
    }
  ]
```

Key   | Type   | Description 
------|--------|-------------
name  | String | Concept Name
extId | Number | Concept external ID



#### getDriversByInterval  
This method will take a **concept ID**, **store number**, **start** and **end dates**, **volume type**, and **data type** and return a list of total driver amount for each interval in the date range requested for that concept, store and labor type.


Intervals are configured during initial setup for the customer and are typically 30 minutes or 15 minutes.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept
startDate       | hsSimpleDate | Start date for the range of data requested
endDate         | hsSimpleDate | End date for the range of data requested
volumeType      | driverClass  | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”
dataType        | driverType   | Type of driver requested.  Allowed types are “ACTUAL”, “ADJ_FORECASTED”, and “PRE_ADJ_FORECASTED”

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"`
  
> **Sample JSON response:**

```
  [
    {
      "driverAmount": 0,
      "driverClass": "TABLE",
      "intervalStartTime": {
        "hours": 0,
        "seconds": 0,
        "militaryTime": true,
        "minutes": 0
      },
      "intervalEndDate": {
        "month": 4,
        "year": 2016,
        "day": 30
      },
      "intervalEndTime": {
        "hours": 0,
        "seconds": 0,
        "militaryTime": true,
        "minutes": 15
      },
      "conceptExtRef": 1,
      "storeExtRef": 3,
      "companyExtRef": 234542,
      "driverType": "ACTUAL",
      "intervalStartDate": {
        "month": 4,
        "year": 2016,
        "day": 30
      }
    }
  ]
```
  
Key               | Type    | Description 
------------------|---------|-------------
driverAmount      | Number  | Quantity of driver for interval expressed in the record
driverClass       | String  | Description of driver type supplied for the interval expressed in the record
intervalStartTime | Object  | The hour, minutes, and seconds corresponding to the start of the interval expressed in the record.  Interval times are local to the store’s time zone
intervalEndTime   | Object  | The hour, minutes, and seconds corresponding to the end of the interval expressed in the record.  Interval times are local to the store’s time zone
intervalStartDate | Object  | The date corresponding to the start of the interval expressed in the record
intervalEndDate   | Object  | The date corresponding to the end of the interval expressed in the record
conceptExtRef     | Number  | The concept ID configured by HotSchedules for the concept of the store owning the data of the record., contact HotSchedules if Concept IDs need to be defined or configured
storeExtRef       | Number  | The store ID configured within HotSchedules for the store owning the data of the record., contact HotSchedules if Store IDs need to be defined or configured
companyExtRef     | Number  | The company ID defined by HotSchedules for the store owning the data of the record., contact HotSchedules if the Company ID needs to be defined.  This ID cannot be customized or configured
driverType        | String  | Type of driver requested. Allowed types are: “ACTUAL” - Corresponds to the actual values produced by the store. “ADJ_FORECASTED”- Corresponds to the final forecasted driver amount that the schedules were based off from for the driver. “PRE_ADJ_FORECASTED”- Corresponds to the original forecasted driver amount previous to any forecast adjustments



#### getEmpAvailability  

This method takes in a **concept ID** and a **store ID** and returns an **array of wsEmpAvailability objects**. It is meant to get a list of all employee availability for that store.

Query parameter | Type    | Description
----------------|---------|------------
concept         | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value
storeNum        | Number  | Numeric (integer) identifier for the store. Must be unique within the concept
active_only     | Boolean | Boolean that defines whether or not to include terminated employees in response

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpAvailability?active_only=true"`


> **Sample JSON response:**

```
[
  {
    "empNum": 2013,
    "availabilities": [
      {
        "parHoursMax": -1,
        "parShiftsMax": -1,
        "shiftId": 781691610,
        "shiftName": "PM",
        "parHoursMin": -1,
        "parShiftsMin": -1,
        "dayName": "Friday",
        "partialBeforeAfter": "",
        "statusName": "Not Available",
        "dayNum": 6,
        "partialTime": "",
        "statusNum": 3
      }
    ],
    "empHrId": -1
  }
]
```

Key            | Type    | Description 
---------------|---------|-------------
empNum         | Number  | Employee POS ID
availabilities | Array   | Returns an array of availability for an employee
empHrId        | Number  | Employee HR ID 



#### getEmpInfo  

This method takes in a **concept ID** and a **store ID** and returns an **array of wsEmpInfo** objects. It is meant to get a list of all employees for that store.

Query parameter | Type    | Description
----------------|---------|------------
concept         | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number  | Numeric (integer) identifier for the store. Must be unique within the concept.
active_only     | Boolean | Boolean that defines whether or not to include terminated employees in response.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpInfo?active_only=true"`
  
  
> **Sample JSON response:**

```  
  [
    {
      "lastUpdated": "2015-07-10T17:32:55.753-05:00",
      "accountCreated": "2012-12-28T13:31:25.913-06:00",
      "permissionSetName": "Employee",
      "empNum": 2001,
      "assignedSchedules": [
        {
          "hsId": 781691496,
          "name": "Bartender",
          "extId": 0
        },
        {
          "hsId": 781691492,
          "name": "Server",
          "extId": 0
        }
      ],
      "empHrId": -1
    }
  ]
```

Key               | Type   | Description 
------------------|--------|-------------
lastUpdated       | String | Last time the employee record was updated
accountCreated    | String | Date/time the account was created
permissionSetName | String | Permission set name assigned to the employee
empNum            | Number | Employee POS ID
assignedSchedules | Array  | The schedule in which the employee is assigned. Array contains extId, hsId and name
empHrId           | Number | Employees HR ID



#### getEmpJobs

This method takes in a **concept ID** and a **store ID** and returns an **array of wsEmpJob** objects. It is meant to get a list of all jobs assigned to all employees for that store.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpJobs?active_only=true"`
  
> **Sample JSON response:**

``` 
[ 
  {
    "hsJobId": 11878523,
    "clientId": 14935376,
    "regWage": 1,
    "posEmpId": 2069,
    "hsEmpId": 4177214,
    "storeNum": 3,
    "ovtWage": 1.5,
    "posJobId": 18,
    "primary": true
  }
]
```  

Key      | Type    | Description 
---------|---------|-------------
hsJobId  | Number  | HotSchedules internal job code ID
clientId | Number  | Unique identifier for client provided via HotSchedules
regWage  | Number  | Regular hourly wage rate for employee
posEmpId | Number  | POS numeric ID for employee
hsEmpId  | Number  | HotSchedules internal employee account ID
storeNum | Number  | Unique numeric store ID within HotSchedules, generally set up to mirror the client internal store IDs
ovtWage  | Number  | Overtime hourly wage rate for employee
posJobId | Number  | POS numeric ID for the job code
primary  | Boolean | Boolean flag to designate if the job code is the primary job for the employee



#### getGroups
This method takes in a **concept ID** and returns group information for the concept.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/getGroups"`

> **Sample JSON response:**

```
  [
    {
      "name": "HotSchedules",
      "extId": 0,
      "conceptExtId": 1
    }
  ]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
name         | String | Group name
extId        | Number | Group external ID
conceptExtId | Number | Concept external ID



#### getGuestCounts
This method will take a **concept ID**, **store number**, **start** and **end dates** and return a list of guest counts for the date range requested.

Query parameter | Type     | Description
----------------|----------|------------
concept         | Number   | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number   | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | dateTime | Start date for the range of data requested.  This is a basic dateTime object.
end             | dateTime | End date for the range of data requested.  This is a basic dateTime object.


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00"`

> **Sample JSON response:**

```
  [
    {
      "dateTime": "2016-04-30T11:00:00-05:00",
      "businessDate": "2016-04-30T00:00:00-05:00",
      "rvcExtId": 1,
      "guestCount": 2
    }
  ]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
dateTime     | String | Date time of the transaction
businessDate | String | Business date of transaction
rvcExtId     | Number | Represents the numeric revenue center ID associated with the guest 
guestCount   | Number | Number of guests for the transaction



#### getLaborByBusDay
This method will take a **concept ID**, **store number**, **start** and **end dates** and a **labor type** and return a list of total labor by job code for each interval in the date range requested for that concept, store and labor type.

Intervals are configured during initial setup for the customer and are typically 30 minutes.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept
start           | hsSimpleDate | Start date for the range of data requested
end             | hsSimpleDate | End date for the range of data requested
laborType       | laborType    | Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled".

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getLaborByBusDay?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"`


> **Sample JSON response:** 

```
[
  {
    "interval": {
      "intervalDate": {
        "day": 1,
        "month": 2,
        "year": 2016
      },
      "intervalTime": {
        "hours": 0,
        "militaryTime": true,
        "minutes": 0,
        "seconds": 0
      },
      "laborType": "forecasted",
      "volume": 0
    }
  }
]  
```  
  
Key          | Type   | Description 
-------------|--------|-------------
intervalDate | Object | Date expressed in the record
intervalTime | Object | The hour, minutes, and seconds expressed in record
laborType    | String | Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled". 
volume       | String | Number of employees based on demand at that interval


#### getLaborByJobAndInterval
This method will take a **concept ID**, **store number**, **start** and **end dates** and a **labor type** and return a list of total labor by job code for each interval in the date range requested for that concept, store and labor type.

Intervals are configured during initial setup for the customer and are typically 30 minutes.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | hsSimpleDate | Start date for the range of data requested
end             | hsSimpleDate | End date for the range of data requested
laborType       | laborType    | Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled".

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getLaborByJobAndInterval?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"`

> **Sample JSON response:**

```
[
  {
    "interval": {
      "intervalDate": {
        "day": 1,
        "month": 2,
        "year": 2016
      },
      "intervalTime": {
        "hours": 12,
        "militaryTime": true,
        "minutes": 0,
        "seconds": 0
      },
      "laborType": "scheduled",
      "volume": 0
    }
  }
]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
intervalDate | Object | Date expressed in the record
intervalTime | Object | The hour, minutes, and seconds expressed in record
laborType    | String | Type of labor requested. Allowed types are "optimal", "forecasted" and "scheduled".
volume       | String | Number of employees based on demand at that interval



#### getSalesItemsV3

This method takes in a **concept ID**, **store ID**, **start** and **end dates**.It returns an array of sales for that store. 

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | hsSimpleDate | First day of projected sales requested. This is an hsSimpleDate object.
end             | hsSimpleDate | Last day of projected sales requested. This is an hsSimpleDate object.


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getSalesItemsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


> **Sample JSON response:**

```
[
  {
    "clientId": 1234567,
    "empId": 7,
    "extId": -3,
    "rvc": 1,
    "rvcName": "TAKE OUT",
    "salesCat": 1,
    "storeNum": 13,
    "ttl": 7.99,
    "businessDate": {
      "day": 30,
      "month": 4,
      "year": 2016
    },
    "transDate": {
      "day": 30,
      "month": 4,
      "year": 2016
    },
    "transTime": {
      "hours": 7,
      "militaryTime": true,
      "minutes": 33,
      "seconds": 0
    }
  }
]
```

Key          | Type   | Description
-------------|--------|-------------
clientId     | Object | Business Date information, Day, Months and Year
empId        | Array  | Array of the day part total. Start Time and End Time
extId        | Number | Total projected sales for the day part
rvc          | Number | Revenue center
rvcName      | String | Name for the revenue center associated with the location within the restaurant
salesCat     | Number | Sales category
storeNum     | Number | Store number
ttl          | Number | Total sales for the sales category
businessDate | Object | Business Date information, Day, Months and Year
transDate    | Object | Transaction data
transTime    | Object | Transaction time


#### getProjectedSalesV3

This method will take a **concept ID**, **store number**, **start** and **end dates**. This method uses hsSimpleDate objects for dates and hsSimpleTime objects for times.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | hsSimpleDate | First day of projected sales requested. This is an hsSimpleDate object.
end             | hsSimpleDate | Last day of projected sales requested. This is an hsSimpleDate object.


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getProjectedSalesV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


> **Sample JSON response:**

```
  [
    {
      "businessDate": {
        "month": 4,
        "year": 2016,
        "day": 30
      },
      "dayPartTotals": [
        {
          "summaryItemTotals": {
            "summaryItemTotal": 5246.26,
            "summaryItemName": "Take out Drive through"
          },
          "dayPartEndTime": {
            "hours": 4,
            "seconds": 0,
            "amPm": "pm",
            "militaryTime": true,
            "minutes": 0
          },
          "dayPartName": "Evening",
          "dayPartTotal": 5246.26,
          "dayPartStartTime": {
            "hours": 18,
            "seconds": 0,
            "amPm": "am",
            "militaryTime": true,
            "minutes": 0
          }
        }
      ],
      "dateTotal": 9934.779
    }
  ]
```
  
Key           | Type   | Description 
--------------|--------|-------------
businessDate  | Object | Business Date information, Day, Months and Year
dayPartTotals | Array  | Array of the day part total. Start Time and End Time
dateTotal     | Number | Total projected sales for the day part



#### getRCVs
Revenue center information defined for a group.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getRCVs"`

> **Sample JSON response:**

```
  [
    {
      "revenueCenterName": "Take Out",
      "extId": 0,
      "groupLevel": true
    },
    {
      "revenueCenterName": "Drive Thru",
      "extId": 1,
      "groupLevel": true
    },
    {
      "revenueCenterName": "Beverage",
      "extId": 2,
      "groupLevel": true
    }
  ]
```  
  
Key               | Type    | Description 
------------------|---------|-------------
revenueCenterName | String  | Revenue center name
extId             | Number  | Revenue center ID
groupLevel        | Boolean | Indicates if the revenue center was created at a group level



#### getSalesCats
This method takes in a **concept ID** and a **store ID** and returns an **array of sales categories** for that store. Sales categories will typically establish what kind of item was sold: Food, Beverage, Alcohol, Merchandise.Sales categories can be local to a particular store, or defined in HotSchedules as belonging to an entire group (called group-level sales categories).

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getSalesCats"`

> **Sample JSON response:**

```
  [
    {
      "salesCategoryName": "Beverages",
      "extId": 1,
      "groupLevel": true
    }
  ]
```

  
Key               | Type    | Description 
------------------|---------|-------------
salesCategoryName | String  | Name of the sales category
extId             | Number  | External ID associated with the category
groupLevel        | Boolean | Indicates if the revenue center was created at a group level



#### getScheduleV3
This method takes in a **concept ID**, **store ID**, **start** and **end dates**. It returns an **array of WSScheduleItem3 objects**, which represent one scheduled shift each, for import into the POS. This method returns the same data as getSchedule, plus extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS.This method uses hsSimpleDate objects for dates.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | hsSimpleDate | First day of scheduled shifts you are requesting. This method uses hsSimpleDate objects for dates.
end             | hsSimpleDate | Last day of scheduled shifts you are requesting. This method uses hsSimpleDate objects for dates.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getScheduleV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


> **Sample JSON response:**

```
  [
      {
     "inDate": {
       "month": 5,
       "year": 2016,
       "day": 2
     },
     "inTime": {
       "hours": 9,
       "seconds": 0,
       "militaryTime": true,
       "minutes": 0
      },
      "outDate": {
       "month": 5,
       "year": 2016,
       "day": 2
     },
     "outTime": {
       "hours": 18,
       "seconds": 0,
       "militaryTime": true,
       "minutes": 0
      },
     "jobHsId": 1111111,
     "payRate": 1,
     "specialPay": 0,
     "empHSId": 222222,
     "ovtMinutes": 0,
    }  
  ]
```  
  
Key        | Type   | Description 
-----------|--------|-------------
outDate    | Object | Schedules out date
jobHsId    | Number | HotSchedules internal job code ID
payRate    | Number | Regular hourly pay rate for employee
inDate     | Object | Scheduled in date
specialPay | Number | Special Pay amounts
empHsId    | Number | HotSchedules internal employee account ID
ovtMinutes | Number | Total Overtime Minutes for employee
inTime     | Object | Scheduled in time
outTime    | Object | Scheduled out time



#### getShiftsV3
This method takes in a **concept ID**, **store ID**, **start** and **end dates** and three flags (**isHouse**, **isScheduled** and **isPosted**). It returns an array of WSScheduleItem3 objects, which represent one scheduled shift each. What shifts are returned depends on the flags set:

isHouse - includes scheduled or posted shifts that are not assigned to an employee (called 'house shifts' in HotSchedules).
isScheduled - includes shifts that are in schedules that have been saved in HotSchedules, but might not have been posted
isPosted - includes shifts that are in schedules that have been set to the 'posted' status within HotSchedules.

This method returns extended scheduled shift data, including location ID, regular pay rate, OT pay rate, scheduled regular minutes, scheduled OT minutes (if any), scheduled special pay (if any) and the unique schedule ID, internal to HS.

Query parameter | Type     | Description
----------------|----------|------------
concept         | Number   | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number   | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number   | Day formatted dd
Month           | Number   | Month formatted mm
Year            | Number   | Year formated yyyy
isHouse         | Boolean  | Include house shifts? These are shifts which were never assigned to someone on a schedule, or were once assigned but removed from an employee when their status, job, etc. changed.
isScheduled     | Boolean  | Include scheduled shifts? These are shifts which are on a schedule that has been saved in HotSchedules, but might not have been posted
isPosted        | Boolean  | These are shifts that are in schedules that have been set to the 'posted' status within HotSchedules.
jobCodes        | IntArray | Integer array of job codes to be included in this method's return. if this parameter is null or empty, all jobs will be included.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getShiftsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&is_house=true&is_scheduled=true&is_posted=true"`


> **Sample JSON response:**

```
  [
    {
    empHSId: -1,
    empPosId: -1,
    jobHsId: 786323133,
    jobPosId: 11,
    inDate: {
    day: 5,
    month: 5,
    year: 2016
    },
    outDate: {
    day: 5,
    month: 5,
    year: 2016
    },
    inTime: {
    hours: 9,
    militaryTime: true,
    minutes: 0,
    seconds: 0
    },
    outTime: {
    hours: 16,
    militaryTime: true,
    minutes: 0,
    seconds: 0
    },
    weekStart: {
    day: 2,
    month: 5,
    year: 2016
    },
    weekEnd: {
    day: 8,
    month: 5,
    year: 2016
    },
    locationId: 787124196,
    scheduleId: 781691586,
    payRate: 0,
    ovtRate: 0,
    ovtMinutes: 0,
    regMinutes: 420,
    specialPay: 0
    }
  ]
```  
  
Key        | Type   | Description 
-----------|--------|-------------
empHsId    | Number | HotSchedules internal employee account ID
empPosId   | Number | POS numeric Employee ID
jobHsId    | Number | HotSchedules internal job code ID
jobPosId   | Number | POS job code ID
inDate     | Object | Scheduled in date
outDate    | Object | Schedules out date
inTime     | Object | Scheduled in time
outTime    | Object | Scheduled out time
weekStart  | Object | Start date of the work week
weekEnd    | Object | End date of the work week
locationId | Number | Location ID
scheduleId | Number | Schedule ID
payRate    | Number | Regular hourly pay rate for employee
ovtRate    | Number | overtime pay rate
ovtMinutes | Number | Total overtime minutes for employee
regMinutes | Number | total regular minutes for employee
specialPay | Number | Special Pay amounts



#### getStoreEmployees
This method takes in a **concept ID**, **store ID**, a flag to determine if only active employees are returned, and returns an **array of WSEmployee objects**.

Query parameter | Type    | Description
----------------|---------|------------
concept         | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number  | Numeric (integer) identifier for the store. Must be unique within the concept.
active_only     | Boolean | Boolean that defines whether or not to include terminated employees in response.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getStoreEmployees?active_only=true"`


> **Sample JSON response:**

```
[
    {
      "zipCode": 12345,
      "hireDate": "2016-11-03T10:16:38.533-05:00",
      "address": "111 Addy Way",
      "clientId": 87654321,
      "LName": "Lockman",
      "address2": "Unit 3",
      "city": "Austin",
      "mobile": "(222) 222-2222",
      "NName": "Jay",
      "altId": -1,
      "FName": "Harrison",
      "empNum": -1,
      "phone": "(333) 333-3333",
      "hsId": 987654321,
      "dob": "1981-09-16T00:00:00-05:00",
      "state": "TX",
      "storeNum": 3,
      "email": "harrison.lockman@email.com",
      "status": 1
    }
]
```  

Key      | Type   | Description 
---------|--------|-------------
zipCode  | Number | Zip Code 
hireDate | String | Employee Hire Date
address  | String | Employee Address line 1
clientId | Number | Unique identifier for client provided via HotSchedules
LName    | String | Employee Last Name
address2 | String | Employee Address line 2
city     | String | City field for Address
mobile   | String | Employees Mobile Phone
NName    | String | Employee Nickname
altId    | Number | Employee HR ID. This must be a unique value across the company. It is used for HotSchedules Shared Employees.
FName    | String | Employee First Name
empNum   | Number | Employee POS ID
phone    | String | Phone Number
hsId     | Number | HS unique ID of an employee that is assigned at the time the employee is created in HS. This number is not configurable but automatically assigned. This number can be obtained through the get method and is an option to include in the set. However this is not necessary
dob      | String | Date of birth
state    | String | State 
storeNum | Number | Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.
email    | String | Employee’s email address
status   | Number | Active = 1, Inactive = 0, Terminated = -1



#### getStoreJobs
This method takes in a **concept ID** and a **store ID**, and returns an array of all jobs currently defined in HotSchedules for the given concept/store.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getStoreJobs"`


> **Sample JSON response:**

```
  [
    {
      "jobName": "Manager",
      "posId": 11,
      "clientId": 14935376,
      "hsId": 786323133,
      "defRate": 0,
      "storeNum": 3
    }
  ]
```

Key      | Type   | Description 
---------|--------|-------------
jobName  | String | Name for Job Code
posId    | Number | Numeric POS ID for Job Code
clientId | Number | Unique identifier for client provided via HotSchedules
hsId     | Number | HS unique ID of an employee that is assigned at the time the employee is created in HS. This number is not configurable but automatically assigned. This number can be obtained through the get method and is an option to include in the set. However this is not necessary
defRate  | Number | Default Pay Rate for a Job Code



#### getStoresV2
Returns information about the stores within a group.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
group_id        | Number | Group in which the store is assigned



  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/getStoresV2?group_id=0"`

> **Sample JSON response:**

```
  [
    {
      "groupName": "HS Grill",
      "active": true,
      "groupExtId": 1,
      "storeName": "Sales Demo - Bug Test",
      "storeNum": -1,
      "city": "Fremont",
      "postalCode": "94555",
      "stateProvince": "CA",
      "streetAddress1": "1 st. address",
      "streetAddress2": "Unit 3",
      "timeZone": "US/Central"
    }
  ]
```
  
Key            | Type    | Description 
---------------|---------|-------------
groupName      | String  | Name of the group
active         | Boolean | Indicates if the store is active
groupExtId     | Number  | The external ID for the store
storeName      | String  | The name of the store
storeNum       | Number  | Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.
city           | String  | City
postalCode     | Number  | Zip code / postal code
stateProvince  | String  | State province
streetAddress1 | String  | Main street adress
streetAddress2 | String  | Apartment number, Suite, Unit, etc..
timeZone       | String  | Store timezone



#### getTimeCards
This method takes in a **concept ID**, **store ID**, **start** and **end dates**. It returns an **array of wsTimeCard3 objects**, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in and clock out times. If this store is using HotSchedules' web-based timeclock for employee clock-in, any open punches in the date range are also included in the response.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`
  
> **Sample JSON response**

```
[
    {
      "jobName": "Bartender",
      "ovtTtl": 0,
      "ovtHrs": 0,
      "clockOut": "2016-05-01T23:48:00-05:00",
      "regWage": 0,
      "clockIn": "2016-05-01T16:36:00-05:00",
      "ovtWage": 7.5,
      "breakMinutes": 0,
      "jobExtId": 18,
      "jobId": -1,
      "businessDate": {
        "month": 5,
        "year": 2016,
        "day": 1
      },
      "regHrs": 7.2,
      "spcTtl": 7.25,
      "hsId": 929931332168,
      "spcHrs": 0,
      "ovtMins": 0,
      "extId": -2005922,
      "storeNum": 3,
      "empPosId": 2068,
      "regTtl": 0
    }
]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
jobName      | String | POS job code name
ovtTtl       | Number | Optional-Overtime total pay amount
ovtHrs       | Number | Optional-Overtime hours in shift
clockOut     | String | Clock out timestamp for the shift
regWage      | Number | Regular hourly pay rate
clockIn      | String | Clock in timestamp for the shift
ovtWage      | Number | Optional-Overtime hourly pay rate
breakMinutes | Number | Number of non-paid break minutes in shift
JobId        | Number | POS numeric identifier for the job
jobExtId     | Number | POS numeric Job Code ID
businessDate | Array  | Business Date information, Day, Months and Year
regHrs       | Number | Regular hours represented in shift
spcTtl       | Number | Optional-Special Pay total pay amount
hsId         | Number | Optional-Internal HotSchedules employee Account ID. Not required, will be set by the service.
spcHrs       | Number | Optional-Special Pay Hours
ovtMins      | Number | Optional-Overtime minutes in shift
storeNum     | Number | Unique numeric store identifier. Generally set up to mirror the client internal store ID.  
empPosId     | Number | POS numeric Employee ID
regTtl       | Number | Regular total pay amount
extId        | Number | Optional-Unique transaction ID for the time card record



#### getTimeCardsDeclaredTips
This method takes in a **concept ID**, **store ID**, **start** and **end dates**. It returns an **array of wsTimeCard3 objects**, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in, clock out times and declared tips. If this store is using HotSchedules' web-based timeclock for employee clock-in, any open punches in the date range are also included in the response.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy


  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`
  
> **Sample JSON object**

```
  [
    {
      "breakMinutes": 0,
      "empPosId": 4067,
      "extId": -2031248,
      "hsId": 929931332583,
      "jobExtId": 18,
      "jobId": -1,
      "jobName": "Bartender",
      "ovtHrs": 0,
      "ovtMins": 0,
      "ovtTtl": 0,
      "ovtWage": 6.75,
      "regHrs": 5.1,
      "regTtl": 22.95,
      "regWage": 4.5,
      "spcHrs": 0,
      "spcTtl": 0,
      "storeNum": 2,
      "businessDate": {
      "day": 30,
      "month": 4,
      "year": 2016
      },
      "clockIn": "2016-04-30T09:29:00-05:00",
      "clockOut": "2016-04-30T14:35:00-05:00",
      "declaredTips": 0
    }
  ]
```
  
Key          | Type   | Description 
-------------|--------|-------------
jobName      | String | POS job code name
ovtTtl       | Number | Optional-Overtime total pay amount
ovtHrs       | Number | Optional-Overtime hours in shift
clockOut     | String | Clock out timestamp for the shift
regWage      | Number | Regular hourly pay rate
clockIn      | String | Clock in timestamp for the shift
ovtWage      | Number | Optional-Overtime hourly pay rate
breakMinutes | Number | Number of non-paid break minutes in shift
JobId        | Number | POS numeric identifier for the job
jobExtId     | Number | POS numeric Job Code ID
businessDate | Array  | Business Date information, Day, Months and Year
regHrs       | Number | Regular hours represented in shift
spcTtl       | Number | Optional-Special Pay total pay amount
hsId         | Number | Optional-Internal HotSchedules employee Account ID. Not required, will be set by the service.
spcHrs       | Number | Optional-Special Pay Hours
ovtMins      | Number | Optional-Overtime minutes in shift
storeNum     | Number | Unique numeric store identifier.  Generally set up to mirror the client internal store ID.  
empPosId     | Number | POS numeric Employee ID
regTtl       | Number | Regular total pay amount
extId        | Number | Optional-Unique transaction ID for the time card record
declaredTips | Number | Tip amount




#### getVolumeCounts
This method will take a **concept ID**, **store number**, **start** and **end dates** and a **volume type** and return a list of volume counts for the date range requested.
Supported Volume Types are:  “TABLES”, “ENTRÉE”, “GUESTS”, “DELIVERIES”, “PRODUCTS”, and “TRANSACTIONS”.

Query parameter | Type         | Description
----------------|--------------|------------
concept         | Number       | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number       | Numeric (integer) identifier for the store. Must be unique within the concept.
volumeType      | volumeType   | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”.
start           | hsSimpleDate | Start date for the range of data requested
end             | hsSimpleDate | End date for the range of data requested


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE"`


> **Sample JSON response:**

```
  [
    {
      "dateTime": "2016-05-03T23:30:00-05:00",
      "volumeAmount": 5,
      "businessDate": "2016-05-03T00:00:00-05:00",
      "volumeType": "Guests",
      "rvcExtId": 0
    }
  ]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
dateTime     | String | Date of business
volumeAmount | Number | Value of the volume count for the transaction
businessDate | String | Business Date information, Day, Months and Year
volumeType   | String | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”.
rvcExtId     | Number | Represents the numeric revenue center ID associated with the volume count 



<aside class="notice"> <strong>WRITING DATA METHODS</strong> </aside>



#### setTimeCardsV3
Extends dataTimeCard (includes business date and clock in and clockout date/times).

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{ \"jobName\": \"Cook\", \"ovtTtl\": 0, \"ovtHrs\": 0, \"clockOut\": \"2016-07-31T22:05:00-05:00\", \"regWage\": 9, \"clockIn\": \"2016-07-30T15:56:00-05:00\", \"ovtWage\": 13.5, \"breakMinutes\": 0, \"jobId\": 16921407, \"businessDate\": { \"month\": 7, \"year\": 2016, \"day\": 31 }, \"regHrs\": 6.15, \"spcTtl\": 0, \"hsId\": 929931334634, \"spcHrs\": 0, \"ovtMins\": 0, \"storeNum\": 1, \"empPosId\": 1052, \"regTtl\": 55.35 }]"`
  
> **Sample JSON object**

```
  [
    {
      "jobName": "Cook",
      "ovtTtl": 0,
      "ovtHrs": 0,
      "clockOut": "2016-07-31T22:05:00-05:00",
      "regWage": 9,
      "clockIn": "2016-07-30T15:56:00-05:00",
      "ovtWage": 13.5,
      "breakMinutes": 0,
      "JobId": 16921407,
      "businessDate": {
        "month": 7,
        "year": 2016,
        "day": 31,
      },
      "regHrs": 6.15,
      "spcTtl": 0,
      "hsId": 929931334634,
      "spcHrs": 0,
      "ovtMins": 0,
      "storeNum": 1,
      "empPosId": 1052,
      "regTtl": 55.35
    }
  ]
```

Key          | Type   | Description 
-------------|--------|-------------
jobName      | String | POS job code name
ovtTtl       | Number | Optional-Overtime total pay amount
ovtHrs       | Number | Optional-Overtime hours in shift
clockOut     | String | Clock out timestamp for the shift
regWage      | Number | Regular hourly pay rate
clockIn      | String | Clock in timestamp for the shift
ovtWage      | Number | Optional-Overtime hourly pay rate
breakMinutes | Number | Number of non-paid break minutes in shift
JobId        | Number | POS numeric identifier for the job
jobExtId     | Number | POS numeric Job Code ID
businessDate | Array  | Business Date information, Day, Months and Year
regHrs       | Number | Regular hours represented in shift
spcTtl       | Number | Optional-Special Pay total pay amount
hsId         | Number | Optional-Internal HotSchedules employee Account ID. Not required, will be set by the service.
spcHrs       | Number | Optional-Special Pay Hours
ovtMins      | Number | Optional-Overtime minutes in shift
storeNum     | Number | Unique numeric store identifier. Generally set up to mirror the client internal store ID.  
empPosId     | Number | POS numeric Employee ID
regTtl       | Number | Regular total pay amount
extId        | Number | Optional-Unique transaction ID for the time card record



#### setEmpJobs
This method takes in a **concept ID**, **store ID**, and an **array of WSEmpJob** objects to assign jobs to individual employees. This method returns a WSReturn object.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setEmpJobs?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "hsJobId": 11878523,
      "clientId": 14935376,
      "regWage": 1,
      "posEmpId": 2069,
      "hsEmpId": 4177214,
      "storeNum": 3,
      "ovtWage": 1.5,
      "posJobId": 18,
      "primary": true
    }
  ]
```  

Key      | Type    | Description 
---------|---------|-------------
hsJobId  | Number  | HotSchedules internal job code ID
clientId | Number  | Unique identifier for client provided via HotSchedules
regWage  | Number  | Regular hourly wage rate for employee
posEmpId | Number  | POS numeric ID for employee
hsEmpId  | Number  | HotSchedules internal employee account ID
storeNum | Number  | Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.
ovtWage  | Number  | Overtime hourly wage rate for employee
posJobId | Number  | POS numeric ID for the job code
primary  | Boolean | Boolean flag to designate if the job code is the primary job for the employee



#### setEmps
This method takes in a **concept ID**, **store ID** and an **array of WSEmployee objects**. Using the authentication from the username token and the conecpt and store IDs, the server will resolve which HotSchedules client this sync is for. The array of employees will be parsed on the server side to employees who need to be inserted or updated in the HS database. This method returns a WSReturn object.

Query parameter | Type            | Description
----------------|-----------------|------------
concept         | Number          | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number          | Numeric (integer) identifier for the store. Must be unique within the concept.
emps            | wsEmployeeArray | Array of WSEmployee objects. Each object represents an employee at this store.
Day             | Number          | Day formatted dd
Month           | Number          | Month formatted mm
Year            | Number          | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setEmps?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "zipCode": 12345,
      "hireDate": "2016-11-03T10:16:38.533-05:00",
      "address": "111 Addy Way",
      "clientId": 87654321,
      "LName": "Lockman",
      "address2": "Unit 3",
      "city": "Austin",
      "mobile": "(222) 222-2222",
      "NName": "Jay",
      "altId": -1,
      "FName": "Harrison",
      "empNum": -1,
      "phone": "(333) 333-3333",
      "hsId": 987654321,
      "dob": "1981-09-16T00:00:00-05:00",
      "state": "TX",
      "storeNum": 3,
      "email": "harrison.lockman@email.com",
      "status": 1
    }
  ]
```  

Key      | Type   | Description 
---------|--------|-------------
zipCode  | Number | Zip Code 
hireDate | String | Employee Hire Date
address  | String | Employee Address line 1
clientId | Number | Unique identifier for client provided via HotSchedules
LName    | String | Employee Last Name
address2 | String | Employee Address line 2
city     | String | City field for Address
mobile   | String | Employees Mobile Phone
NName    | String | Employee Nickname
altId    | Number | Employee HR ID. This must be a unique value across the company. It is used for HotSchedules Shared Employees.
FName    | String | Employee First Name
empNum   | Number | Employee POS ID
phone    | String | Phone Number
hsId     | Number | HS unique ID of an employee that is assigned at the time the employee is created in HS. This number is not configurable but automatically assigned. This number can be obtained through the get method and is an option to include in the set. However this is not necessary
dob      | String | Date of birth
state    | String | State 
storeNum | Number | Unique numeric store ID within HotSchedules. Generally set up to mirror the client internal store IDs.
email    | String | Employee’s email address
status   | Number | Active = 1, Inactive = 0, Terminated = -1



#### setForecastDriversV2

This method takes in a **concept ID**, **store ID**, **workweek**, **startdate**, **enddate**, **starttime**, **endtime**, **volume amount**, **volume type**, and a **revenue center** for the purpose of submitting forecasted volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The server side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setForecastDriversV2?start_day=30&start_month=4&start_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "concept": 1,
      "storeNum": 1,
      "workweekStartDate": {
        "day": 11,
        "month": 10,
        "year": 2016
      },
      "driverAmount": 10,
      "intervalStartDate" : {
        "day": 1,
        "month": 5,
        "year": 2016
      },
      "intervalEndDate": {
        "day": 11,
        "month": 10,
        "year": 2016
      },
      "intervalStartTime": {
        "amPm": "am",
        "hours": 0,
        "seconds": 0,
        "militaryTime": true,
        "minutes": 0
      },
      "intervalEndTime": {
        "amPm": "am",
        "hours": 0,
        "seconds": 0,
        "militaryTime": true,
        "minutes": 15
      },
      "rvcId": 1,
      "volumeType": "Guests"
    }
  ]
```

Key               | Type   | Description 
------------------|--------|-------------
concept           | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum          | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
workweekStartDate | Object | Start date of the work week
driverAmount      | Number | Quantity of driver for interval expressed in the record
intervalStartTime | Object | The hour, minutes, and seconds corresponding to the start of the interval expressed in the record. Interval times are local to the store’s time zone. 
intervalEndTime   | Object | The hour, minutes, and seconds corresponding to the end of the interval expressed in the record. Interval times are local to the store’s time zone. 
intervalStartDate | Object | The date corresponding to the start of the interval expressed in the record
intervalEndDate   | Object | The date corresponding to the end of the interval expressed in the record
rvcId             | Number | Numeric ID for the revenue center associated with the location within the restaurant
volumeType        | String | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”.



#### setGuestCounts
This method takes in a **concept ID**, **store ID**, **business date**, **date time**, **guest count** and a **revenue center** for the purpose of submitting actual guest count drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains guest counts for a range of dates, corresponding to the start and end dates. The server-side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setGuestCounts?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "dateTime": "2016-05-03T23:30:00-05:00",
      "businessDate": "2016-05-03T00:00:00-05:00",
      "guestCount": 113,
      "rvcExtID": 123
    }
  ]
```  

Key               | Type   | Description 
------------------|--------|-------------
businessDate      | String | Business date of transaction
dateTime          | String | Date Time of the transaction
guestCount        | Number | Number of guests for the transaction
rvcExtID          | Number | Numeric ID for the revenue center associated with the transaction



#### setRVC
This method takes in a **concept ID** and a **store ID** and returns an **array of revenue centers** for that store.

Query parameter | Type    | Description
----------------|---------|------------
concept         | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number  | Numeric (integer) identifier for the store. Must be unique within the concept
group           | Number  | Numeric ID group in which the store is assigned
rvcId           | Number  | Numeric ID for the revenue center associated with the location within the restaurant
rvcName         | String  | Name for the revenue center associated with the location within the restaurant. <br> i.e. Bar, Togo etc...
isGroupLevel    | Boolean | Indicates if the revenue center is assigned at the group level. <br> i.e. Bar used across all locations

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setRVC?group=1&rvcId=1&rvcName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object** 

```
[
    {
      "concept": 1,
      "group": 1,
      "isGroupLevel": true,
      "store": 13,
      "rvcId": 11,
      "rvcName": "Bar"
    }
]
```  

Key               | Type    | Description 
------------------|---------|-------------
concept           | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum          | Number  | Numeric (integer) identifier for the store. Must be unique within the concept.
group             | Number  | Numeric ID group in which the store is assigned
rvcId             | Number  | Numeric ID for the revenue center associated with the location within the restaurant
rvcName           | String  | Name for the revenue center associated with the location within the restaurant. <br> i.e. Bar, Togo etc...
isGroupLevel      | Boolean | Indicates if the revenue center is assigned at the group level. <br> i.e. Bar used across all locations


#### setSalesCat

This method allows you to add the sales category associated with menu items. Sales categories will typically establish what kind of item was sold: Food, Beverage, Alcohol, Merchandise. Sales categories can be local to a particular store.


Query parameter | Type    | Description
----------------|---------|------------
concept         | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number  | Numeric (integer) identifier for the store. Must be unique within the concept.
group           | Number  | Numeric ID group in which the store is assigned
salesCatId      | Number  | Numeric ID for the sales category associated with the location within the restaurant
salesCatName    | String  | Name for the sales category associated with the item sold within the restaurant. <br> i.e. Liquor, Beer, etc..
isGroupLevel    | Boolean | Indicates if the sales category is assigned at the group level. <br> i.e. Liquor ID 2 used across all locations

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setSalesCat?group=1&salesCatId=1&salesCatName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object** 

```
[
  {
    "concept": 1,
    "group": 1,
    "isGroupLevel": true,
    "store": 13,
    "salesCatId": 9,
    "salesCatName": "Liquor"
  }
]

```  

Key               | Type    | Description 
------------------|---------|-------------
concept           | Number  | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum          | Number  | Numeric (integer) identifier for the store. Must be unique within the concept.
group             | Number  | Numeric ID group in which the store is assigned
salesCatId        | Number  | Numeric ID for the sales category associated with the location within the restaurant
salesCatName      | String  | Name for the sales category associated with the item sold within the restaurant. <br> i.e. Liquor, Beer, etc..
isGroupLevel      | Boolean | Indicates if the sales category is assigned at the group level. <br> i.e. Liquor ID 2 used across all locations


#### setSalesItemsV4

This method takes in a **concept ID**, **store ID**, a **start** and **end date** and an **array of WSSalesItem objects**. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains sales items for a range of dates, corresponding to the start and end dates. The server-side logic can handle overlapping data (i.e. if you sync 7 days worth of sales, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the sales items are already in the HS database and do not need to be updated, then nothing will change. The method returns a WSReturn object.
This method uses hsSimpleDate objects for dates.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setSalesItemsV4?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**
```
  [
    "concept": 1,
    "storeNum": 1,
    "sales": {
      "catName": "Beer",
      "clientId": 3,
      "empId": 123,
        "extId": 333,
        "rvc": "Revenue",
        "rvcName": "Bar",
        "salesCat": "Beer",
        "storeNum": 3,
        "ttl": 0,
        "businessDate": {
          "day": 1,
          "month": 7,
          "year": 2016
        },
        "transDate": {
          "day": 1,
          "month": 7,
          "year": 2015
        },
        "transTime": {
          "amPm": "am",
          "hours": 1,
          "militaryTime": true,
          "minutes": 15,
          "seconds": 0
        }
    },
      "start": {
        "day": 1,
        "month": 7,
        "year": 2016
      },
      "end": {
        "day": 1,
        "month": 8,
        "year": 2016
      }
  ]
```

Key          | Type   | Description 
-------------|--------|-------------
concept      | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum     | Number | Numeric (integer) identifier for the store. Must be unique within the concept
catName      | String | Category name
clientId     | Number | Unique identifier for client provided via HotSchedules
empId        | Number | Employee ID
extId        | Number | External ID
rvc          | String | Revenue Center
rvcName      | String | Name for the revenue center associated with the location within the restaurant
salesCat     | String | Sales category
ttl          | String | Total sales for the sales category
businessDate | Object | Business Date information, Day, Months and Year
transDate    | Object | Transaction date
transTime    | Object | Transaction time
start        | Object | Start date for the range of data requested
end          | Object | End date for the range of data requested


#### setTimeCardsDeclaredTips
This method takes in a **concept ID**, **store ID**, a **start** and **end date** and an **array of WSTimeCardsDeclaredTips** objects. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains time cards for a range of dates, corresponding to the start and end dates. The server-side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the time cards are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "breakMinutes": 0,
      "empPosId": 4067,
      "extId": -2031248,
      "hsId": 929931332583,
      "jobExtId": 18,
      "jobId": -1,
      "jobName": "Bartender",
      "ovtHrs": 0,
      "ovtMins": 0,
      "ovtTtl": 0,
      "ovtWage": 6.75,
      "regHrs": 5.1,
      "regTtl": 22.95,
      "regWage": 4.5,
      "spcHrs": 0,
      "spcTtl": 0,
      "storeNum": 2,
      "businessDate": {
      "day": 30,
      "month": 4,
      "year": 2016
      },
      "clockIn": "2016-04-30T09:29:00-05:00",
      "clockOut": "2016-04-30T14:35:00-05:00",
      "declaredTips": 0
    }
  ]
``` 
  
Key          | Type   | Description 
-------------|--------|-------------
jobName      | String | POS job code name
ovtTtl       | Number | Optional-Overtime total pay amount
ovtHrs       | Number | Optional-Overtime hours in shift
clockOut     | String | Clock out timestamp for the shift
regWage      | Number | Regular hourly pay rate
clockIn      | String | Clock in timestamp for the shift
ovtWage      | Number | Optional-Overtime hourly pay rate
breakMinutes | Number | Number of non-paid break minutes in shift
JobId        | Number | POS numeric identifier for the job
jobExtId     | Number | POS numeric Job Code ID
businessDate | Array  | Business Date information, Day, Months and Year
regHrs       | Number | Regular hours represented in shift
spcTtl       | Number | Optional-Special Pay total pay amount
hsId         | Number | Optional-Internal HotSchedules employee Account ID. Not required, will be set by the service.
spcHrs       | Number | Optional-Special Pay Hours
ovtMins      | Number | Optional-Overtime minutes in shift
storeNum     | Number | Unique numeric store identifier.  Generally set up to mirror the client internal store ID.  
empPosId     | Number | POS numeric Employee ID
regTtl       | Number | Regular total pay amount
extId        | Number | Optional-Unique transaction ID for the time card record
declaredTips | Number | Tip amount



#### setVolumeCountsV2

This method takes in a **concept ID**, **store ID**, **business date**, **date time**, **volume amount**, **volume type**, and a **revenue center** for the purpose of submitting actual volume drivers to HotSchedules from a third party system or point of sale. Using the authentication from the username token and the concept and store IDs, the server will resolve which HotSchedules client this sync is for. The array contains volume driver counts for a range of dates, corresponding to the start and end dates. The server-side logic can handle overlapping data (i.e. if you sync 7 days worth of time cards, every day, 6 days of it will be "overlapping" data) and will insert and update data as needed. If the guest are already in the HS database and do not need to be updated, then nothing will change. This method returns a WSReturn object.


Query parameter | Type   | Description
----------------|------- |------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.bodhi.space/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setVolumeCountsV2" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
  [
    {
      "businessDate": "2014-10-05T00:00:00",
      "dateTime": "2014-10-05T06:41:00-05:00",
      "rvcExtId": 4,
      "volumeAmount": 1,
      "volumeType": "GUESTS"
    }
  ]
```  

Key          | Type   | Description 
-------------|--------|-------------
businessDate | String | Business date of transaction
dateTime     | String | Date time of transaction
rvcExtId     | Number | Represents the numeric revenue center ID associated with the guest 
volumeAmount | Number | Value of the volume count for the transaction
volumeType   | String | Classification of driver requested. Allowed types would be all of the classifications supported from API, HSC, or FTP integration.  “Guests”, “Tables”, “Entrees”, “Deliveries”, "Transactions" and “Products”.
