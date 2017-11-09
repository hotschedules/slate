#Working with HotSchedules data

####Making a call
**Note:** If your **namespace** has been created under the new IDM model, you will not have the ability to make calls using **api.hotschedules.io**. Please refer to the section on using Postman to make a call. You will need to have retrieved your JWT Token before you can use this method.

<br>
The HotSchedules REST API supports all the standard REST verbs.

**GET**  
**POST**  
**PUT**  
**PATCH**  
**DELETE**  

You can access these verbs for each of the types in the HotSchedules system. When an organization is created in the HotSchedules Platform, the organization automatically gets 32 'types' that will store standard information and data about your organization. Those 'types' can be viewed and reviewed at [https://api.hotschedules.io/apidocs/index.html](https://api.hotschedules.io/apidocs/index.html)

####GET
As an example, let's do a **GET** on a store via CURL
`curl -ik --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" -X GET https://api.hotschedules.io/bodhi-social/resources/Store`

This call will return the information about a store that's been created for the bodhi-social organization
    
`[{"sys_version":1,"image_url":"https://upload.wikimedia.org/wikipedia/commons/5/54/Golden_Gate_Bridge_0002.jpg","sys_type_version":12,"address":{"street_address":"555 Mission","extended_address":"","locality":"San Francisco","region":"CA","postal_code":"94111","country":"US"},"store_hours":[{"days":[7,1],"start":"0500","end":"0000"},{"days":[1,2],"start":"1200","end":"0200"},{"days":[2,3],"start":"1200","end":"0200"},{"days":[3,4],"start":"1200","end":"0200"},{"days":[4,5],"start":"1200","end":"0200"},{"days":[5,6],"start":"1200","end":"0200"},{"days":[6,7],"start":"0500","end":"0000"}],"sys_created_by":"admin__bodhi-social","sys_created_at":"2016-05-21T15:37:15.560Z","name":"platformstore","store_number":"1","display_name":"Platform Store","sys_id":"574080abb9a19e2dadee775b"}]`

You can also get the JSON payload by navigating directly to this URL `https://api.hotschedules.io/bodhi-social/resources/Store`  

You can create your own store for your organization either by executing a **POST** command (see below) to `https://api.hotschedules.io/<organization_name>/resources/Store` or using our free store manager tool at `https://hotschedules.io/store-manager` . Either way, a store is a critical anchor for information in the Platform.

Next let's look up a sale for our store in bodhi-social

`curl -ik --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" -X GET https://api.hotschedules.io/bodhi-social/resources/SalesTransaction`

RESULT:

`[{"order_number":10184,"item_count":1,"store_id":"574080abb9a19e2dadee775b","employee":{"id":"5151","name":"Ted Morrison"},"business_day":"2016-05-20","revenue_center":{"id":"2","name":"Restaraunt"},"type":{"id":"4","name":"1"},"timestamp":"2016-05-21T03:34:00.000Z","transaction_id":"557605fc4c32e071180a46042016-05-2010184","net_total":{"value":325,"code":"USD","scale":2},"discount_total":{"value":0,"code":"USD","scale":2},"tax_total":{"value":23,"code":"USD","scale":2},"gross_total":{"value":348,"code":"USD","scale":2},"tender_total":{"value":348,"code":"USD","scale":2},"order_opened_at":"2016-05-21T03:33:00.000Z","order_closed_at":"2016-05-21T03:34:00.000Z","guest_count":1,"sys_version":1,"sys_created_at":"2016-05-21T16:02:30.800Z","sys_created_by":"admin__bodhi-social","sys_type_version":12,"sys_id":"574086965eacd06aa3db036b"}]`

We can also look up our Store using query parameters in our URL

`curl --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" 'https://api.hotschedules.io.io/bodhi-social/resources/SalesTransaction?where=%7Bbusiness_day:"2016-05-20"%7D&fields=business_day'`

OR alternatively:

`curl -g --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=platform" 'https://api.hotschedules.io/bodhi-social/resources/SalesTransaction?where={business_day:"2016-05-20"}&fields=business_day'`

RESULT:    
`[{"order_number":10184,"item_count":1,"store_id":"574080abb9a19e2dadee775b","employee":{"id":"5151","name":"Ted Morrison"},"business_day":"2016-05-20","revenue_center":{"id":"2","name":"Restaraunt"},"type":{"id":"4","name":"1"},"timestamp":"2016-05-21T03:34:00.000Z","transaction_id":"557605fc4c32e071180a46042016-05-2010184","net_total":{"value":325,"code":"USD","scale":2},"discount_total":{"value":0,"code":"USD","scale":2},"tax_total":{"value":23,"code":"USD","scale":2},"gross_total":{"value":348,"code":"USD","scale":2},"tender_total":{"value":348,"code":"USD","scale":2},"order_opened_at":"2016-05-21T03:33:00.000Z","order_closed_at":"2016-05-21T03:34:00.000Z","guest_count":1,"sys_version":1,"sys_created_at":"2016-05-21T16:02:30.800Z","sys_created_by":"admin__bodhi-social","sys_type_version":12,"sys_id":"574086965eacd06aa3db036b"}]`

So `https://api.hotschedules.io/bodhi-social/resources/SalesTransaction?where={%27business_day%27:%272016-05-20%27}` would return all SalesTransaction's for the business day of 2016-05-20.
The URL `https://api.hotschedules.io/bodhi-social/resources/SalesTransaction?where={%27store_id%27:%27574080abb9a19e2dadee775b%27}` would return all SalesTransaction's for the store 574080abb9a19e2dadee775b (our Platform test store).

All Types can be queried by any parameter within the type using a ?where={} clause. It's **EXTREMELY** important for efficiency and performance to query using indexes on your types. You can review the Types for your organization as well as the Indexes and Parameters by using our free Type Tool located at `https://tools.hotschedules.io/types` or by inspecting `https://api.hotschedules.io/<organization_name>/resources/BodhiType`

####POST
To **POST** to a type you need to add the the header: 'Content-Type: application/json' to your cURL Command

`curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X POST -d '{
  "store_id": "l8zeL",
  "business_day": "2016-05-13",
  "timestamp": "2016-05-12T05:58:31.296Z",
  "transaction_id": "FGHG012",
     "tender_total": {
      "code": "USD",
      "scale": 2,
      "value": 620
    }
}' https://api.hotschedules.io/<organization_name>/resources/SalesTransaction`

That command will post the json object to the SalesTransaction type. You can now GET on this type either using cURL or the free query tools available at https://tools.hotschedules.io/query

####Bulk Post
All bulk operations are accessible through https://api.hotschedules.io  
The size limitation for the body is 17MB  

###Syntax: 
**POST** `/<organization_name>/bulk` with json body  
```{
  "config": {
    "op": "insert" or "update" or "upsert" or "invite",  * see below
     "report": true,        <- optional, need a report? (default false) 
     "target": "target_name”    <- the name of the type (not for invite)
  },
  "payload": [{
    "the_field": "my first thing to insert or upsert or invite",
    "other_field": "the_other_field"
  }, {
    "the_field": "my second thing to insert or upsert",
    "other_field": "the_other_field2"
  }]
}```  

The payload varies depending on the type of operation and Returns 202 with header `bulk_id:<the bulk id>`

The result of a report, if requested, is accessible as soon as the processing is done on:

**GET** `/<organization_name>/bulk/<bulk_id>`

**RESPONSE:**  
returns **200** with a json array body where the order of the cells matches the order of the payload. The report can be accessed only once.  
returns **204** if the report is not ready yet  
returns **404** if no report was found with that id  

  * update/upsert is only available for types not encapsulated 
  * insert on system types only BodhiUser, BodhiType and BodhiEnumeration and any not encapsulated type

###Example:
```{
  "config": {
    "op": "insert",
    "report": true,
    "target":  "BulkTest"
  },
  "payload": [{
    "name": "leo",
    "other_field": "mauris non"
  }, {
    "name": "orci",
    "other_field": "sit amet justo"
  }, {
    "name": "nulla",
    "other_field": "pulvinar sed nisl nunc rhoncus"
  }, {
    "name": "nulla",
    "other_field": "diam cras"
  }, {
    "name": "est",
    "other_field": "dui nec nisi volutpat"
  }, {
    "name": "lorem",
    "other_field": "cursus id"
  }, {
    "name": "molestie",
    "other_field": "potenti nullam porttitor lacus at"
  }, {
    "name": "sapien",
    "other_field": "ultrices aliquet maecenas leo"
  }, {
    "name": "nibh",
    "other_field": "consectetuer eget rutrum at"
  }, {
    "name": "luctus",
    "other_field": "nisl nunc"
  }]
}```

####PUT
The HTTP verb PUT can be used on any type as long as there's a unique index on the field or fields. You can always PUT on sys_id

As an example, in the above SalesTransaction example, the sys_id is 574086965eacd06aa3db036b, a PUT to the SalesTransaction based on sys_id would be as follows:

`
curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X PUT -d '{ "store_id": "l8zeL", "business_day": "2016-05-13", "timestamp": "2016-05-12T05:58:31.296Z", "transaction_id": "FGHG012", "tender_total": { "code": "USD", "scale": 2, "value": 620 } }' https://api.hotschedules.io/tutorial/resources/SalesTransaction/574086965eacd06aa3db036b
` 

####PUT Upsert
Upsert is a safe way to replace an existing record, or POST a record if the entry does not currently exist.

You can upsert by appending your URL with ?upsert=true

As an example, the above PUT example can be changed to a replace by appending the ?upsert=true to the cURL command:

`
curl -ik -H 'Content-Type: application/json' --cookie "RUSK=8a6f98bb1033055fc04d644c0006789335f96c2b-username=foo" -X PUT -d '{ "store_id": "l8zeL", "business_day": "2016-05-13", "timestamp": "2016-05-12T05:58:31.296Z", "transaction_id": "FGHG012", "tender_total": { "code": "USD", "scale": 2, "value": 620 } }' https://api.hotschedules.io/tutorial/resources/SalesTransaction/574086965eacd06aa3db036b?upsert=true
`


####PATCH
the HTTP verb PATCH will allow you to alter single parameters or fields within a record in your type. Patch commands follow the following sytax:
[ { "op": "replace", "path": "/baz", "value": "boo" }, { "op": "add", "path": "/hello", "value": ["world"] }, { "op": "remove", "path": "/foo"} ]

The HTTP verb PATCH can be used on any type as long as there's a unique index on the field or fields. You can always PATCH on sys_id

####DELETE
the HTTP verb DELETE will allow you to remove a record in your type. DELETE commands follow the following sytax:

To delete multiple records, include a ?where={} in your URL to narrow or expand then number of records removed.

####File Upload
The Platform BodhiFileUpload endpoints are special types that allow a user to upload and download any file (like a dbf file from your store's POS).

Metadata of your file is posted to type BodhiFileUpload on successful upload  

**BodhiFileUpload example record:**  
`{ "namespace": "bodhi", "original_name": "profile_pic5.jpg", "sys_version": 1, "location": "bodhi/profile_pic5.jpg", "uploaded_at": "2015-09-10T19:42:48+0000", "sys_created_by": "admin__bodhi", "sys_created_at": "2015-09-10T19:42:49+0000", "name": "profile_pic5.jpg", "media_type": "image/jpeg", "sys_id": "55f1dd39b9b5904f64c8212f" }`

**Examples:**  
The following are curl examples of how to specify file location in your upload/download/delete commands.  Everything after “upload/” or “download/” in the url is used as the destination.  Note that filename is always specified in the url.  

`curl -X POST -u <username>:<password> https://api.hotschedules.io/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt -F "upload1=@THE_FILE"`  

`curl -X PUT -u <username>:<password> https://api.hotschedules.io/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt -F "upload1=@THE_FILE"`

**Download by path:**  
`curl -X GET -u <username>:<password> https://api.hotschedules.io/<organization_name>/controllers/vertx/download/recipes/food/BurritoRecipe.txt`

**Download by sys_id:**  
`curl -X GET -u <username>:<password> https://api.hotschedules.io/<organization_name>/controllers/vertx/download/56f9c2b4fa92ec27934a76ae`  

**Delete a file:**  
`curl -X DELETE -u <username>:<password> https://api.hotschedules.io/<organization_name>/controllers/vertx/upload/recipes/food/BurritoRecipe.txt`

#Using Postman To Make a Call

Postman makes API development faster, easier, and better. Postman is the most complete toolchain for API development. The most-used REST client worldwide. Designed from the ground up to support the API developer. Intuitive user interface to send requests, save responses, add tests, and create workflows Read the docs.

You can make calls using both Basic Authentication using your HotSchedules IoT Platform account credentials (username and password) and the JWT Token method.


**Basic Authentication Example:** Let's do a Basic Authentication call to getEmpInfo. This method takes in a concept ID and a store ID and returns an array of wsEmpInfo objects. It is meant to get a list of all employees for that store.

<br>

**1.** Create a new Request in Postman and name it 'Get Employee Info'.

![alt text](/images/pms1.png?raw=false "Step 1")

**2.** Set the request type to 'GET' and enter the following URL.
__https://api.hotschedules.io/YOURNAMESPACE/controllers/vertx/hotschedules/YOURCONCEPTID/YOURSTORENUMBER/getEmpInfo?active_only=true__
  
  - Replace the **'YOURNAMESPACE'**, **'YOURCONCEPTID'** and **'YOURSTORENUMBER'** with your values.

![alt text](/images/pms2.png?raw=false "Step 2")

**3.** Select **'Basic Auth'** in the Authorization section and enter your username and password.

![alt text](/images/pms3.png?raw=false "Step 3")
![alt text](/images/pms3a.png?raw=false "Step 3")


**4.** Push the **'Send'** button to make the call and review the response in the **'Body'** section.

![alt text](/images/pms4.png?raw=false "Step 4")

**5.** Save the request so you can refer back and make repetitive calls to update the response.

<br><br>

**Note: Completing the step of [retrieving your JWT Token](#idm-how-to-programatically-retrieve-jwt-tokens) is required before you can utilize the following example to make a call to the API with your JWT Token.**

**JWT Token Example:** To perform a call using this method, follow the same steps as the Basic Authentication method with the exception of Step 3. Select **'Bearer Token'** as the Authorization type and enter the bearer token you received when you performed the 'Retrieve JWT Token' call.


![alt text](/images/pms5.png?raw=false "Bearer Token")

#Available REST API Methods

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

`curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/getConcepts"`


> **Sample JSON response:**


```
[
    {
        "extId": 3714,
        "name": "HotSchedules"
    }
]
```


Key   | Type   | Description 
------|--------|-------------
extId | Number | Concept external ID
name  | String | Concept Name


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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getDriversByInterval?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&volume_type=TABLE&data_type=ACTUAL"`
  
> **Sample JSON response:**


```
[
    {
        "companyExtRef": 264319,
        "conceptExtRef": 3714,
        "driverAmount": 0,
        "driverClass": "TABLE",
        "driverType": "ACTUAL",
        "intervalEndDate": {
            "day": 1,
            "month": 10,
            "year": 2017
        },
        "intervalEndTime": {
            "hours": 0,
            "militaryTime": true,
            "minutes": 30,
            "seconds": 0
        },
        "intervalStartDate": {
            "day": 1,
            "month": 10,
            "year": 2017
        },
        "intervalStartTime": {
            "hours": 0,
            "militaryTime": true,
            "minutes": 0,
            "seconds": 0
        },
        "storeExtRef": 98
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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpAvailability?active_only=true"`


> **Sample JSON response:**

```
[
    {
        "availabilities": [
            {
                "dayName": "Sunday",
                "dayNum": 1,
                "parHoursMax": -1,
                "parHoursMin": -1,
                "parShiftsMax": -1,
                "parShiftsMin": -1,
                "partialBeforeAfter": null,
                "partialTime": null,
                "shiftId": 1582006201,
                "shiftName": "AM",
                "statusName": "Not Available",
                "statusNum": 3
            },
            {
                "dayName": "Sunday",
                "dayNum": 1,
                "parHoursMax": -1,
                "parHoursMin": -1,
                "parShiftsMax": -1,
                "parShiftsMin": -1,
                "partialBeforeAfter": null,
                "partialTime": null,
                "shiftId": 1582006202,
                "shiftName": "PM",
                "statusName": "Not Available",
                "statusNum": 3
            }
        ],
        "empHrId": -1,
        "empNum": 9801
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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpInfo?active_only=true"`
  
  
> **Sample JSON response:**

```  
[
    {
        "accountCreated": "2017-05-04T10:18:46.957-05:00",
        "empHrId": -1,
        "empNum": -1,
        "lastUpdated": "2017-05-04T10:18:47.040-05:00",
        "permissionSetName": "Default HotSchedules Employee"
    },
    {
        "accountCreated": "2017-07-07T10:05:48.820-05:00",
        "assignedSchedules": {
            "extId": -1,
            "hsId": 1050941698,
            "name": "FOH"
        },
        "empHrId": -1,
        "empNum": 9898,
        "lastUpdated": "2017-10-13T13:59:36.523-05:00",
        "permissionSetName": "Employee"
    },
    {
        "accountCreated": "2017-05-04T10:18:46.817-05:00",
        "empHrId": -1,
        "empNum": -1,
        "lastUpdated": "2017-07-07T10:00:20.487-05:00",
        "permissionSetName": "Default HS Support User"
    },
    {
        "accountCreated": "2017-10-13T12:48:57.903-05:00",
        "assignedSchedules": {
            "extId": -1,
            "hsId": 1050941698,
            "name": "FOH"
        },
        "empHrId": -1,
        "empNum": 9801,
        "lastUpdated": "2017-10-13T12:50:58.597-05:00",
        "permissionSetName": "Employee"
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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getEmpJobs?active_only=true"`
  
> **Sample JSON response:**

``` 
[
    {
        "clientId": 25124840,
        "hsEmpId": 587378309,
        "hsJobId": 27134060,
        "ovtWage": 22.5,
        "posEmpId": 9898,
        "posJobId": 1099,
        "primary": true,
        "regWage": 15,
        "storeNum": 98
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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/getGroups"`

> **Sample JSON response:**

```
[
    {
        "conceptExtId": 3714,
        "extId": 0,
        "name": "My Group Name"
    }
]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
conceptExtId | Number | Concept external ID
extId        | Number | Group external ID
name         | String | Group name



#### getGuestCounts
This method will take a **concept ID**, **store number**, **start** and **end dates** and return a list of guest counts for the date range requested.

Query parameter | Type     | Description
----------------|----------|------------
concept         | Number   | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number   | Numeric (integer) identifier for the store. Must be unique within the concept.
start           | dateTime | Start date for the range of data requested.  This is a basic dateTime object.
end             | dateTime | End date for the range of data requested.  This is a basic dateTime object.


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getGuestCounts?start_date=2016-04-30T00:00:00&end_date=2016-05-03T00:00:00"`

> **Sample JSON response:**

```
[
    {
        "businessDate": "2017-02-05T00:00:00-06:00",
        "dateTime": "2017-02-05T05:41:00-06:00",
        "guestCount": 8,
        "rvcExtId": 1
    },
    {
        "businessDate": "2017-03-05T00:00:00-06:00",
        "dateTime": "2017-03-05T05:41:00-06:00",
        "guestCount": 18,
        "rvcExtId": 1
    }
]
```  
  
Key          | Type   | Description 
-------------|--------|-------------
businessDate | String | Business date of transaction
dateTime     | String | Date time of the transaction
guestCount   | Number | Number of guests for the transaction
rvcExtId     | Number | Represents the numeric revenue center ID associated with the guest 



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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getLaborByBusDay?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"`


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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getLaborByJobAndInterval?start_day=30&start_month=1&start_year=2016&end_day=5&end_month=5&end_year=2016&labor_type=optimal"`

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


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getSalesItemsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


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
extId        | Number | Optional-Unique transaction ID for the sales item
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


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getProjectedSalesV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getRCVs"`

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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getSalesCats"`

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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getScheduleV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`


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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getShiftsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016&is_house=true&is_scheduled=true&is_posted=true"`


> **Sample JSON response:**

```
  [
    {
      "empHSId": -1,
      "empPosId": -1,
      "jobHsId": 786323133,
      "jobPosId": 11,
      "inDate": {
        "day": 5,
        "month": 5,
        "year": 2016
      },
      "outDate": {
        "day": 5,
        "month": 5,
        "year": 2016
      },
      "inTime": {
        "hours": 9,
        "militaryTime": true,
        "minutes": 0,
        "seconds": 0
      },
      "outTime": {
        "hours": 16,
        "militaryTime": true,
        "minutes": 0,
        "seconds": 0
      },
      "weekStart": {
        "day": 2,
        "month": 5,
        "year": 2016
      },
      "weekEnd": {
        "day": 8,
        "month": 5,
        "year": 2016
      },
      "locationId": 787124196,
      "scheduleId": 781691586,
      "payRate": 0,
      "ovtRate": 0,
      "ovtMinutes": 0,
      "regMinutes": 420,
      "specialPay": 0
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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getStoreEmployees?active_only=true"`


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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getStoreJobs"`


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



  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/getStoresV2?group_id=0"`

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

  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getTimeCards?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`
  
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
jobId        | Number | POS numeric identifier for the job
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


#### getTimeCardsV2
Same as getTimeCards but additionally provides double time info for each timecard.


#### getTimeCardsDeclaredTips
This method takes in a **concept ID**, **store ID**, **start** and **end dates**. It returns an **array of wsTimeCard3 objects**, which represent one employee time card each. Each time card has information for one employee punch record, including business date, regular and OT minutes and wages, clock in, clock out times and declared tips. If this store is using HotSchedules' web-based timeclock for employee clock-in, any open punches in the date range are also included in the response.

Query parameter | Type   | Description
----------------|--------|------------
concept         | Number | The identifier for the location's concept. Must be unique within the company, contact HotSchedules if you're not sure about this value.
storeNum        | Number | Numeric (integer) identifier for the store. Must be unique within the concept.
Day             | Number | Day formatted dd
Month           | Number | Month formatted mm
Year            | Number | Year formated yyyy


  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016"`
  
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
jobId        | Number | POS numeric identifier for the job
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


  `curl -X GET -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/getVolumeCounts?start_date=2015-04-30T00:00:00&end_date=2016-05-03T00:00:00&volume_type=TABLE"`


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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/1/1/setTimeCardsV3?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{ \"jobName\": \"Cook\", \"ovtTtl\": 0, \"ovtHrs\": 0, \"clockOut\": \"2016-07-31T22:05:00-05:00\", \"regWage\": 9, \"clockIn\": \"2016-07-30T15:56:00-05:00\", \"ovtWage\": 13.5, \"breakMinutes\": 0, \"jobId\": 16921407, \"businessDate\": { \"month\": 7, \"year\": 2016, \"day\": 31 }, \"regHrs\": 6.15, \"spcTtl\": 0, \"hsId\": 929931334634, \"spcHrs\": 0, \"ovtMins\": 0, \"storeNum\": 1, \"empPosId\": 1052, \"regTtl\": 55.35 }]"`
  
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
      "jobId": 16921407,
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
jobId        | Number | POS numeric identifier for the job
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setEmpJobs?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setEmps?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
> **Sample JSON object**

```
[
    {
      "zipCode": 78681,
      "hireDate": "2017-08-03T10:16:38.533-05:00",
      "termDate": "2017-11-05T10:16:38.533-05:00",
      "address": "111 Addy Way",
      "clientId": 25124840,
      "LName": "Lockman",
      "address2": "Unit 3",
      "city": "Austin",
      "mobile": "(222) 222-2222",
      "NName": "Jay",
      "altId": -1,
      "FName": "Harrison",
      "empNum": -1,
      "phone": "(333) 333-3333",
      "hsId": 587378309,
      "dob": "1981-09-16T00:00:00-05:00",
      "state": "TX",
      "storeNum": 98,
      "email": "harrison.lockman@email.com",
      "status": 1
    }
  ]
```  

Key      | Type   | Description 
---------|--------|-------------
zipCode  | Number | Zip Code 
hireDate | String | Employee Hire Date
termDate | String | Employee Termination Date
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setForecastDriversV2?start_day=30&start_month=4&start_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setGuestCounts?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setRVC?group=1&rvcId=1&rvcName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setSalesCat?group=1&salesCatId=1&salesCatName=1&isGroupLevel=true" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setSalesItemsV4?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setTimeCardsDeclaredTips?start_day=30&start_month=4&start_year=2016&end_day=5&end_month=5&end_year=2016" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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
jobId        | Number | POS numeric identifier for the job
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

  `curl -X PUT -H "Content-Type:application/json" -u <username>:<password> "https://api.hotschedules.io/<namespace>/controllers/vertx/hotschedules/<concept>/<storeNum>/setVolumeCountsV2" -d "[{json_object_1}, {json_object_2}, {json_object_3}...]"`
  
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
