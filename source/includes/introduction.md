#HotSchedules IoT Platform

The HotSchedules Bodhi Platform is a set of REST APIs that power the Clarifi suite of applications - gathering data from a variety of sources and allowing a restaurant manager to gain both just-in-time as well as forward-looking insights into how they can improve their business.

This document is meant to be a resource for software developers who want to interact with our data set.  We will be taking a particular eye towards interacting with existing point-of-sale and existing labor schedule data, as well as how to pass in point-of-sale data in our canonical data model, so that applications can consume it.    _

##**Building Blocks**

The Bodhi Platform is built as a series of **namespaces**.  A **namespace** represents the data store for 1 company, and has a collection of **stores** under it.  A store represents a single venue, and some of the elements of a store are what you would expect from a venue: address, business hours, etc.

**Users** can be created within a namespace and assigned to a set of stores within a hierarchy, and assigned **profiles** that are sets of permissions to control what they can or cannot do within various applications.

An **admin** profile represents the top level of permissions within a namespace, and is needed in order to GET and POST data to our REST APIs.

For our purposes within this document, we are going to refer to users as people or machines who have access to a username and password that has the admin profile within their namespace, and can thus authenticate to the API.

To move forward, make sure you have acquired the following:

* A namespace
* A username and password with the admin profile

We will be using Postman as our tool to test and validate many of the elements discussed within this doc, so we highly recommend taking a moment to download it and familiarize yourself with its functionality.  Our Platform also includes a Query tool and additional interactive docs that you can use to interact with our dataset (keep reading!).

##**URLs**

The Bodhi Platform is built around a central URL:  [https://api.hotschedules.io] (https://api.hotschedules.io).  We also have components and applications available at other tiers such as,

[https://tools.hotschedules.io] (https://tools.hotschedules.io)

[https://apps.hotschedules.io] (https://apps.hotschedules.io)

The syntax of your URL will include your namespace name within it.  For example, a call to return data about all of the Stores in your namespace would look like this:

[https://api.hotschedules.io/namespace/resources/Store] (https://api.hotschedules.io/namespace/resources/Store)

You’ll be seeing this a lot.  Our API uses Mongo DB for storage, so to learn more about this foundation, see this link: [http://docs.mongodb.org/manual/reference/operator] (http://docs.mongodb.org/manual/reference/operator)

You may be unfamiliar with the REST query syntax.  If you’re familiar with SQL, you should note the same types of SQL query operations are possible using the REST API.  

To learn more about the semantic differences, see this document: [http://docs.mongodb.org/manual/reference/sql-comparison] (http://docs.mongodb.org/manual/reference/sql-comparison).  No need to do it right now - you can come back to it later!


##**Tokens**

Authenticating to the REST API requires generating a JWT, or Java Web Token.  For more information around JWTs, see this link: https://jwt.io/introduction/

Internally, we refer to capturing and refreshing JWTs as “IDM” or “Identity Management” -- so if you see or hear reference to IDM, they are talking about authenticating a user via a JWT (as opposed to a simple username/password combo).

For more details on IDM, please click [HERE](https://help.hotschedules.com/hc/en-us/articles/115001464671-IDM-Creating-Your-Global-Profile).

Before you can retrieve your token, follow these simple setup steps before proceeding.

**Step 1:** [Create your global profile] (https://help.hotschedules.com/hc/en-us/articles/115001464671-IDM-Creating-Your-Global-Profile).<br>
**Step 2:** Obtain your API credentials from HotSchedules if you have not already done so.<br>
**Step 3:** Login into the [Account Manager](https://tools.hotschedules.io/account/#/)<br>
**Step 4:** In the upper right corner, select the wrench icon, then keychain, then your namespace.<br>
**Step 5:** Enter your API credentials as provided by hotSchedules and click save.<br>
**Step 6:** Continue with the example below to retrieve your token.

Your application will need to not only pass a JWT as part of requests it makes to the REST API, but also refresh that token programmatically when it expires.

To generate a JWT, you’ll need to POST your request to the following URL:
https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token

With the following information:

**Header** 

* content-type: application/x-www-form-urlencoded

**Params**

* **grant_type** 
    * Value must be "password" 

* **client_id**
    * Value must be "urn:mace:oidc:hotschedules.com"

* **username** (this is your global profile username)
    * Value should reflect the username of account you’re requesting tokens for

* **password** (this is your global profile password)
    * Value should reflect the password of the account you’re requesting tokens for

You should return 3 items:

* Access token
* Refresh_token
* Id_token

**The Id_token is your JWT -- save that!**

Here’s an example response (with the JWT bolded)

![alt text](/images/tokenimg.png?raw=true "ID_token")

The tokens generally are active for 8 hours, and thus would need to be refreshed on that schedule.  Refreshing the token is very similar, just hit this URL:

[https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token] (https://login.hotschedules.io/auth/realms/hotschedules/protocol/openid-connect/token)


**Header** 

* content-type: application/x-www-form-urlencoded

**Params**

* **grant_type** 
    * Value must be "refresh_token" 

* **client_id**
    * Value must be "urn:mace:oidc:hotschedules.com"

* **refresh_token**
    * Value should reflect the token you are attempting to refresh

As a human interacting with this data, generating a new token each time is handy to do, but your application should eventually automate the process of refreshing its token.


**Now that you know how to authenticate to the REST API, let’s create a Store!**

##Creating A Store

We have a namespace, but we have no stores to post any data to!  Let’s fix that right now.

As mentioned before, the Store endpoint is:
[https://api.hotschedules.io/namespace/resources/Store] (https://api.hotschedules.io/namespace/resources/Store
)

The Store endpoint allows you to post and receive a great deal of information about the configuration of your store - addresses, contact information, business hours, an identifying image, etc.  


The minimum amount of data to pass in to create a Store in your namespace, and the expected types, are:

{
	"name": "String",
	"display_name": "String",
	"store_number": "String",
	"organization_id": "String",
	"concept": "String",
	"status": "String",
	"website_url": "String",
	"telephone": "String",
	"timezone": "String",
	"organization_name": "String"
}

If you replace the “Strings” in the above example with actual data corresponding with your restaurant, POST that to the URL above with your JWT as the bearer token, you should receive a Status: 201 response with the text: “Created”.  
Success!  Nicely done, you’ve created your first store.

If you get an error message, the Store endpoint will give you some additional information about an object that may be misattributed, or an error in the syntax.

**What are all these IDs?**

You’ll be interacting with several different types of IDs throughout this process, and it’s important to keep these straight.
Many of these IDs are meant as an “external reference” value, to match an ID that may be in place within a different application, either within the Clarifi ecosystem or external, as opposed to a “sys_id” which is meant to identify a particular object within the Mongodb database the REST API is calling.

A “concept ID” is a value meant to indicate a grouping of stores, so each store will need its own “store_number” and multiple stores can roll up to a single “concept” ID.

##Introducing the Bodhi Query Tool

Before we move away from interacting with Stores and start interacting with individual components, it’s time to familiarize yourself with the Query tool - a handy way to interact with the API within our product itself!

The Query tool can be found at this URL:
[https://tools.hotschedules.io/query] (https://tools.hotschedules.io/query)

The Query tool will save you a lot of time, in that it has a UI that will allow you to input the parameters you are attempting to search, auto-fill in with available options, and provide you with the output as well as the final URL you can use to access your data.

In the top nav bar, enter Store and click Send.  As long as the drop down on the left is set to GET, you will be performing a GET on the Store type and the API should return all the data about Stores in your namespace.

![alt text](/images/qu1.JPG?raw=true "ID_token")

If, in the previous step, you went hog wild and created several stores, you may want to search just for one particular store, maybe the first one you created.  So let’s look at how the UI allows you to narrow your search.  In this case let’s grab the sys_id of one particular store, and then do a GET to get *just* the data related to that Store object.


In the Fields box, click to open the drop down of available fields, and choose display_name and sys_id.  Click Send!

![alt text](/images/qu2.JPG?raw=true "ID_token")

In my namespace, this returns just the display_name and sys_id of all my stores:

![alt text](/images/qu3.JPG?raw=true "ID_token")


If I want to just see the data for my store “Airwaves Cafe”, I can then plug the sys_id in the “where” clause of the tool:

![alt text](/images/qu4.JPG?raw=true "ID_token")

As you gain more experience with the Bodhi REST API, it is likely that the Query tool will become a very good friend of yours.

Now that we’re able to authenticate to the API,  create and get objects, and use the Query tool, let’s talk about POS data.

#Clarifi API Service
##Introduction
We have built multiple POS integrations that source raw data in a variety of ways - SQL queries, DBF files, APIs - and transform that data into a generalized format that we refer to as “canonical”.  Since different POS’s have different object names, types, and other architectures, transforming that data into a canonical format helps provide a standard dataset that the different Clarifi applications to call to and consume in order to provide value to their users.

Thus, if you are tasked with building a POS integration of your own to enable your customers to use Clarifi, then you will need to pass in some canonical data.  So let’s take a look at what it is!

**StoreInfo** and **StoreBusinessDay**

There are two main components to the Clarifi POS canonical data model.  We collect **definitions** of elements at a store - the employees, their job codes and pay rates, menu items and their pricing, sales categories, revenue centers, and more!  These elements collectively we refer to as StoreInfo.  Secondly, we collect events that occur at the store - the transactions that were generated, the items that were sold, sales totals, timecards that are generated, and more.  These items were collectively refer to as StoreBusinessDay.

* StoreInfo = definition of elements

* StoreBusinessDay = events involving those elements

For example, a StoreBusinessDay timecard may indicate that Employee #12 clocked in as Job 26 at 3:00pm - a Clarifi application would take this data from StoreBusinessDay and be able to lookup to StoreInfo that Employee #12 is named David and Job 26 is Bartender, and give information to an end user about Jason clocking in as a Bartender.

Let’s take a look at the Types of data that make up StoreInfo and StoreBusinessDay, and then we’ll take a look at how exactly to pass that information into our REST API.

**StoreInfo types**

**_PosEmployee:_** PosEmployee’s represent a list of data about the employee profiles that are housed in the POS.

Here’s a breakdown:

*  Name - The first and last name of the employee
*  Nickname - The employee’s nickname or assumed moniker.
*  Birthdate - the employee’s date of birth
*  Addresses - The street, city, state, zipcode, and country assigned to the employee
*  Emails - the employee’s email address
*  Status - whether or not the employee is terminated
*  Employment Period - the span of time between the employee’s hire date and last day.
*  Instore_id - A ID meant to identify the employee at the store level
*  HR ID - An ID meant to identify the employee at a company level (i.e. across multiple stores)
*  Phone Numbers - the employee’s phone numbers

**Additional StoreInfo types:**

**_PosJob:_** A comprehensive list of jobs or roles available for employees to clock in as.<br>
**_pmPosEmployeePosition:_** An employee position indicates which PosEmployees are assigned which PosJobs, along with their designated payrate.<br>
**_PosRevenueCenter:_** A list of revenue centers within a venue, such as “Bar” “Patio” “Dining Room”, etc.<br>
**_PosSalesCategory:_** A list of types of items being sold at this venue, such as “Food”, “Liquor” ,“Beer”, “NA Bev”, “Retail”, etc.<br>
**_PosMenu:_** A list of menus available within the POS, such as “Dinner”, “Happy Hour”, etc<br>
**_PosMenuItems:_** A list of menu items and pricing available for sale at the venue.<br>
**_PosMenuModifiers:_** A list of menu items that would be classified as modifiers, i.e. attachments to menu items.

**StoreBusinessDay Types**

**_PosPunch:_** The punch records that are present in the point of sale system.
<br>
**_PosCheck:_** The different transactions at a restaurant.
<br>
**_PosCheckItem:_** The items that make up a transaction. Items listed here roll into PosCheck.


A full breakdown of each type can be found in the **Getting Data From Clarifi** section below.

##Do I have to send you _all_ this stuff?

Not at all!  As we get deeper into building and validating the data itself, you’ll find that some fields are required and some are not.  If a field is required but is irrelevant to your business, you can leave it with a null value.

For instance, you may only have a single menu at your venue.  In that case, you would populate a single PosMenu, and your PosMenuItems would roll up to that PosMenu. Similarly, if you haven’t collected your employee email addresses, your PosEmployee’s do not need to have that field filled out.

We have some validation tools we’ll discuss later on to hone in on what is and is not required.

##Getting Data From Clarifi

<aside class="notice"> <strong>Getting Data From Clarifi</strong> </aside>

HotSchedules provides a tool called "Bodhi Query" which can be used to interact with the Clarifi API. Using the query tool will allow you to get store data such as the "sys_id". The query tool also alllows the user to to use RESTful verbs to get, set and update data within Clarifi.

To familiarize yourself with the query tool, start by logging into to your namespace.

**Login to your namespace:** [https://tools.hotschedules.io] (https://tools.hotschedules.io)

Once you have authenticated to your namespace, you will be on the tools page where you will select "Bodhi Query"

![Bodhi Tools Page](/images/bqt1.png?raw=true)

The Bodhi Query tool will allow you to use the **GET** verb to access dta relevant to your store. Let's use the Query tool to get the sys_id of a store.

In the primary window, there are 2 select boxes. Box 1 is where you will select the verb type and box 2 provides the service from which to access.

In this example, we are using the **GET** verb and the **API** service to get the store data. In the "Type Name" field, enter "Store" and click the send button. A list of store for your namespace will be returned.Within the body of the JSON response, locate the sys_id.

![Bodhi Tools Page](/images/bqt2.png?raw=true)

![Bodhi Tools Page](/images/bqt3.png?raw=true)


Now that we have the sys_id of a store, we will use "Package" to query the StoreInfo of a specific store. Selec the **GET** verb as the method and the **Package** as the service type. In the "Type Name" field enter "StoreIno". To narrow to a specific store, we will use the **Where** clause. Enter "store_id" in the first field and the "sys_id" in the 2nd field and then select the send button. The results of your call will be displayed in the main body of the query tool.

![Bodhi Tools Page](/images/bqt4.png?raw=true)


The Query Tool can be used to get or set data to any of the POSTypes listed below. As noted in this documentation, you can try different calls using the **Where** and **Fields** paramaters to narrow data to more specific details. 

![Bodhi Tools Page](/images/bqt5.png?raw=true)


Using our RESTful service, a call can be made to **GET** data from the API. Examples of the various calls are listed below with sample JSON Outputs. The file spec is available for download providing the data points and the expected data type for each field.

HTTP Status Codes provide a description of the sucess or failure of a call: [https://httpstatuses.com] (https://httpstatuses.com)


**Base Call:** [https://api.hotschedules.io/namespace/resources/PosCheck?paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/PosCheck?paging=limit:25,page:1)

Using a field in the  **where**  or **fields** clause will narrow the focus to specific data.

**Where:** [https://api.hotschedules.io/namespace/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1)

**Fields:** [https://api.hotschedules.io/namespace/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1)

Below you will find descriptions for each canonical type that we use and the available fields.

<aside class="notice"> <strong>QUERY StoreInfo</strong> </aside> 

PosEmployee, PosJob, PosEmployeePosition, PosRevenueCenter, PosMenu, PosMenuItems and PosMenumodifiers are only types that are queryable via StoreInfo.

**Example:** To get a list of employees for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1)

**Note:** store_id is the sys_id of the store you are running the call for. To retrieve the list of sys_id's for all stores, use the following call.

[https://api.hotschedules.io/namespace/resources/Store?fields=name,sys_id&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/Store?fields=name,sys_id&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
[
{
name: "store_test_07",
sys_id: "5a1653d772bd660b0e9270bc"
},
{
name: "store_test_05",
sys_id: "5a1653d79534035f755308cf"
}
]
```


####PosEmployee
**A list of employees pulled from the point of sale.**<br>

*  **Name** - The first and last name of the employee.<br>
*  **Nickname** - The employee’s nickname or assumed moniker.<br>
*  **Birthdate** - The employee’s date of birth.<br>
*  **Addresses** - The street, city, state, zipcode, and country assigned to an employee.<br>
*  **Emails** - The employee’s email address.<br> 
*  **Status** - Whether or not the employee is terminated.<br>
*  **Employment_period** - The span of time between the employee’s hire date and last day.<br> 
*  **Instore_id** - The point of sale id given to the employee.<br>
*  **Hr_id** - The ID given to the employee by the company.<br> 
*  **Phone_numbers** - The employee’s phone number.

<a href="/images/PosEmployee.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

> **EXAMPLE JSON RESPONSE:**

```
[
  {
    "store_employees": [
      {
        "name": {
          "family_name": "DO NOT REMOVE",
          "given_name": "ATO TRAINING 5"
        },
        "nickname": "ATO TRAINING 5",
        "birthdate": null,
        "addresses": [
          {
            "street_address": null,
            "extended_address": null,
            "locality": null,
            "region": null,
            "postal_code": null,
            "country": null
          }
        ],
        "status": "Active",
        "employment_period": {
          "from": "2018-04-03T00:00:00.000Z"
        },
        "instore_id": "905",
        "hr_id": "",
        "phone_numbers": [],
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

####Posjob
**A list of job codes from the customer’s point of sale system.**<br>

<a href="/images/PosJob.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Instore_name** - The name of the job code.<br>
*  **Instore_id** - The point of sale ID given to the job code.<br>
*  **regular _rate** - The pay rate attached to the job code.<br>
*  **Overtime_rate** - The overtime rate attached to the job.<br>
*  **Doubletime_rate** - The doubletime rate assigned to the job.

**Example:** To get a list of jobs for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_jobs,name&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_jobs,name&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
[
  {
    "store_jobs": [
      {
        "instore_name": "Server",
        "instore_id": "1",
        "regular_rate": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "overtime_rate": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

####PosEmployeePosition
**The job code assigned to the employee in the point of sale.**<br>

<a href="/images/PosEmployeePosition.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Employee_reference** - The employee’s POS ID.<br>
*  **Job_reference** - The job code’s POS ID. <br>
*  **Regular_rate** - The job code rate given to the employee. <br>
*  **Overtime_rate** - The overtime rate given to the employee.<br>
*  **Doubletime_rate** - The doubletime rate give to the employee. <br>
*  **PosSalesCategory** - The sales categories listed in the point of sale. <br>
*  **Instore_id** - The point of sale ID given to the sales category. <br>
*  **Name** - The name of the assigned sales category.

**Example:** To get a list of positions for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=employee_positions,name&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=employee_positions,name&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
[
  {
    "employee_positions": [
      {
        "employee_reference": {
          "id": "905",
          "name": "ATO TRAINING 5 DO NOT REMOVE"
        },
        "job_reference": {
          "id": "12"
        },
        "regular_rate": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "overtime_rate": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "doubletime_rate": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

####PosRevenueCenter
**The revenue centers listed in the point of sale.**<br>
<a href="/images/PosRevenueCenter.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Instore_id** - The point of sale ID given to the revenue center. <br>
*  **Name** - The name of the revenue center. <br>

**Example:** To get a list of revenue centers for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=revenue_centers,name&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=revenue_centers,name&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
[
  {
    "revenue_centers": [
      {
        "name": "Dining",
        "instore_id": "1",
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      },
      {
        "name": "Bar Downstairs",
        "instore_id": "2",
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

####PosMenu
**Different menu types. Examples can include things like a brunch or dinner menu.**<br>
**Note:** PosMenu is nested within StoreInfo <br>

*  **Name** - The name of the menu <br>
*  **Category** - The category assigned to a menu.<br>
*  **Items** - The items that make up a menu. <br>
*  **Modifiers** - The modifiers that can be used by items in the menu. <br>

<a href="/images/PosMenu.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>


####PosMenuItems
**The items that can be used in all of the different menus.**<br>
**Note:** PosMenuItems are nested within StoreInfo <br>

*  **Id** - The point of sale ID given to a menu item. <br>
*  **Name** - The name of the item in the point of sale. <br>
*  **Category** - The category that an item is assigned to. <br>
*  **Description** - an extension of the name that can provide further information about the item. <br>
*  **Unit_price** - The default menu price of the item. <br>
*  **Prices** - If that item has a different price associated with it outside of the default. For example a cocktail might have a happy hour price outside of the menu price. <br>

<a href="/images/PosMenuItems.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

####PosMenumodifiers
**Things like ketchup that can be used in tandem with a menu item.**<br>
**Note:** PosMenumodifiers are nested within StoreInfo <br>

*  **Id** - The given point of sale ID for the menu modifier.<br>
*  **Name** - The name of the menu modifier. <br>
*  **Description** - A longer version of the name that can provide further insight into the name. <br>
*  **Unit_price** - The default menu price for a particular modifier. <br>
*  **Prices** - Any other prices outside of the menu price that is associated with the modifier. <br>

<a href="/images/PosMenumodifiers.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

**Example Call to retrieve PosMenu, PosMenuItems and PosMenumodifiers:** [https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=store_menus&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/StoreInfo?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=store_menus&paging=limit:25,page:1)


> **EXAMPLE JSON RESPONSE:**

```
  {
    "store_menus": [
      {
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "namespace/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        },
        "name": "Test Printers",
        "items": [
          {
            "id": "400520",
            "name": "Expo Test",
            "description": "Expo Test",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          },
          {
            "id": "400521",
            "name": "Fry Test",
            "description": "Fry Test",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          },
          {
            "id": "400522",
            "name": "Grill Test",
            "description": "Grill Test",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          },
          {
            "id": "400523",
            "name": "Saute Test",
            "description": "Saute Test",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          },
          {
            "id": "400524",
            "name": "SVR UP",
            "description": "SVR UP",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          },
          {
            "id": "400525",
            "name": "SVR BAR",
            "description": "SVR BAR",
            "unit_price": {
              "value": 0,
              "scale": 2,
              "code": "USD"
            }
          }
        ],
        "modifiers": []
      }
```

####PosPunch
**The punch records that are present in the point of sale system.**<br>

<a href="/images/PosPunch.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Employee_reference** - the employee’s given point of sale ID. <br>
*  **Job_reference** - The given point of sale ID for the job code that is assigned to the employee. <br>
*  **Business_day** - The business day that the employee has worked. <br>
*  **Started_at** - The time that the employee started working at. <br>
*  **Ended_at** - The time that the employee stopped working at.<br>
*  **Total_minutes_worked** - The total amount of time that the employee worked. <br>
*  **Breaks** - The number of breaks that the employee took. <br>
*  **Regular_rate** - The regular rate that the employee is working at<br>
*  **Overtime_rate** - The overtime rate that the employee is working at<br>
*  **Doubletime_rate** - The doubletime rate that the employee is working at. <br>
*  **Declared_tips** - The declared tips that the employee has. <br>
*  **Cash_tips** - The cash tips that the employee has. <br>
*  **Credit_tips** - The credit tips that the employee has. <br>

**Example:** get punch records [https://api.hotschedules.io/namespace/resources/PosPunch?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=employee_reference&paging=limit:25,page:1] (https://api.hotschedules.io/namespace/resources/PosPunch?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=employee_reference&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
  {
    "employee_reference": {
      "id": "395"
    },
    "job_reference": {
      "id": "10"
    },
    "business_day": "2008-01-10",
    "started_at": "2008-01-10T12:32:00.000Z",
    "ended_at": "2008-01-11T04:00:00.000Z",
    "total_minutes_worked": 928,
    "overtime_minutes_worked": 0,
    "breaks": [],
    "regular_rate": {
      "value": 0,
      "scale": 2,
      "code": "USD"
    },
    "overtime_rate": {
      "value": 0,
      "scale": 2,
      "code": "USD"
    },
    "tips": {
      "declared_tips": {
        "value": 0,
        "scale": 2,
        "code": "USD"
      }
    },
    "content_url": "namespace/5a1653d772bd660b0e9270bc/20180331/StoreBusinessDay",
    "store_reference": {
      "id": "7"
    },
    "store_id": "5a1653d772bd660b0e9270bc",
    "key": "79e5a5c698d0c09fd66fb927d97b3dae",
    "sys_version": 4,
    "sys_created_at": "2018-03-28T13:13:20.165Z",
    "sys_created_by": "admin",
    "sys_type_version": 6,
    "sys_modified_at": "2018-03-31T17:00:24.001Z",
    "sys_modified_by": "admin",
    "sys_id": "5abb94f03d0408724e91e8db"
  }
```

####PosCheck
**The different transactions at a restaurant.**<br>

<a href="/images/PosCheck.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Check_id** - The point of sale ID given to the transaction. <br>
*  **Voided** - Whether or not the transaction was voided. <br>
*  **Canceled** - Whether or not the check was cancelled. <br>
*  **Employee_reference** - The point of sale ID given to the employee who handled the transaction. <br>
*  **Table_id** - The point of sale ID given to the table. <br>
*  **Register_id** - The point of sale ID given to the register.<br>
*  **Shift_id** - The given point of sale ID for the shift. <br>
*  **Opened_at** - When the transaction was opened. <br>
*  **Closed_at** - When the transaction was closed. <br>
*  **Guest_count** - The total number of guests that were present for the transaction. <br>
*  **Item_count** - The total number of items on the transaction. <br>
*  **Net_total** - The total without taxes or coupons applied to it. <br>
*  **Gross_total** - The total including taxes and coupons. <br>
*  **Discount_total** - The total after any discounts have been applied to it. <br>
*  **Tax_total** - The total with the tax applied to it. <br>
*  **Tender_total** - The total amount of dollars paid. <br>
*  **Change_total** - The total amount of change paid. <br>
*  **Gratuity_total** - Any gratuity that was given to the transaction.<br>
*  **Void_total** - if the check was voided how much was it for. <br>
*  **Items** - The items that are on the transaction. <br>


> **EXAMPLE JSON RESPONSE:**

```
  {
    "business_day": "2018-03-26",
    "check_id": "60025",
    "employee_reference": {
      "id": "922"
    },
    "net_total": {
      "value": 500,
      "scale": 2,
      "code": "USD"
    },
    "gross_total": {
      "value": 58198,
      "scale": 2,
      "code": "USD"
    },
    "discount_total": {
      "value": 0,
      "scale": 2,
      "code": "USD"
    },
    "tender_total": {
      "value": 70198,
      "scale": 2,
      "code": "USD"
    },
    "shift_id": "1",
    "revenue_center": {
      "id": "1"
    },
    "opened_at": "2018-03-26T18:00:00.000Z",
    "closed_at": "2018-03-26T19:19:00.000Z",
    "canceled": false,
    "item_count": "4",
    "content_url": "namespace/5a1653d772bd660b0e9270bc/20180326/StoreBusinessDay",
    "store_reference": {
      "id": "7"
    },
    "store_id": "5a1653d772bd660b0e9270bc",
    "items": [
      {
        "item_code": "55032",
        "quantity": "1",
        "sales_category": {
          "id": "4"
        },
        "gross_total": {
          "value": 500,
          "scale": 2,
          "code": "USD"
        },
        "net_total": {
          "value": 500,
          "scale": 2,
          "code": "USD"
        },
        "tax_total": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "unit_price": {
          "value": 500,
          "scale": 2,
          "code": "USD"
        },
        "discount_total": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "void_total": {
          "value": 0,
          "scale": 2,
          "code": "USD"
        },
        "discounted": false
      }
    ],
    "guest_count": "42",
    "voided": false,
    "sys_version": 4,
    "sys_created_at": "2018-03-26T23:00:30.351Z",
    "sys_created_by": "admin",
    "sys_type_version": 3,
    "sys_modified_at": "2018-03-27T12:24:00.269Z",
    "sys_modified_by": "admin",
    "sys_id": "5ab97b8f9534036231f8b72a"
  }
```

<aside class="notice"> <strong>QUERY PosCheck</strong> </aside>

PosCheckItem are only queryable via PosCheck.

####PosCheckItem
**The items that make up a transaction. Items listed here roll into PosCheck.**<br>

<a href="/images/PosCheckItem.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Item_code** - The given POS ID for the item.<br>
*  **Unit_price** - The menu price of the check item. <br>
*  **Quantity** - The amount of the item on the transaction. <br>
*  **Sales_category** - The sales category assigned to the item. <br>
*  **Net_total** - The total dollar amount of the item on the check without taxes or coupons applied to it. <br>
*  **Gross_total** - The total dollar amount of the item on the check with taxes and coupons applied to it. <br>
*  **Tax_total** - The total amount of taxes. <br>
*  **Discount_total** - The total amount of discounts that have been applied to the check. <br>
*  **Void_total** - If the check was voided this is its total. <br>
*  **Voided** - Whether or not the check was voided. <br>
*  **Discounted** - whether or not the check was discounted. <br>
*  **PosVolumeItem** - A dynamic driver that can represent things like guest counts, entree counts, and table counts. <br>
*  **Datetime** - The date that the amount being presented was captured. <br>
*  **Amount** - The total amount being presented by the driver. <br>
*  **Volume_type** - The type of volume that is being displayed. <br>
*  **Revenue_center** - The revenue center that data is being pulled from. <br>
*  **Employee_reference** - The point of sale ID given to the employee whose data you are viewing.

**Example:** To get a count of a number of items

[https://api.hotschedules.io/namespace/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}] ] (https://api.hotschedules.io/namespace/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}])

> **EXAMPLE JSON RESPONSE:**

```
[
{
_id: "55136",
count: 630
}
]
```

**Example:** How many items sold over a time period

[https://api.hotschedules.io/namespace/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1,business_day:1}},{$match:{items.item_code:"55136"}},{$group:{_id:{items:"$items.item_code",business_day:"$business_day"},count:{"$sum":1}}}] ] (https://api.hotschedules.io/namespace/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1,business_day:1}},{$match:{items.item_code:"55136"}},{$group:{_id:{items:"$items.item_code",business_day:"$business_day"},count:{"$sum":1}}}])

> **EXAMPLE JSON RESPONSE:**

```
[
{
_id: {
items: "55136",
business_day: "2018-04-01"
},
count: 26
},
{
_id: {
items: "55136",
business_day: "2018-04-02"
},
count: 17
}
]
```


##Sending Canonical Data Over the REST API

In order to send data into the Clarifi ecosystem, your application will need to construct StoreInfo and StoreBusinessDay files and pass them over a RESTful endpoint to a particular location within your namespace, at which point those files will be parsed out and made available via the API.

##Files?  I Just Want to GET and SET!

In order to understand how to upload data into the REST API, we have to introduce a new term.  A job is a webservice within your namespace assigned to a particular store that can perform a particular function, either on an event-based schedule or on a user-configured timer.  Jobs can perform many functions within your namespace, such as calling to a variety of endpoints and packaging up the results, populating a UI for an end user to interact with, or flushing data that is no longer needed.

Clarifi applications are powered by jobs that run on the backend and move data throughout the ecosystem.  As mentioned, jobs can either run on a schedule, or based on events.  The Bodhi REST API utilizes SQS, a tool that allows applications to generate messages that other applications can listen for in order to know when to activate.  For more information, check out this link: [https://aws.amazon.com/sqs/] (https://aws.amazon.com/sqs/).

![alt text](/images/qu5.JPG?raw=true "ID_token")


Here’s how our POS integrations work: Our Agent application generates raw data from the machine and sends it up into the namespace in a “raw” bucket.  The act of a new file landing in the raw bucket generates an SNS message.  A “transform” job is listening for that SNS message, and so upon receiving it, it activates, running its service to transform the raw data into Canonical data and make it available via our API server.  Upon completion of the job, the files are now placed in a “processed” bucket, generating a new SNS message.  Other applications listening for that SNS message now know to activate.

That means that you *can* just GET and SET data over our API, however you’d be doing it here:

![alt text](/images/qu6.JPG?raw=true "ID_token")


Only applications that run on timers would be able to access this data.  A job that calls to the PosPunch endpoints every 30 minutes for example, would work just fine.  However, a job that is listening for the SNS message (for example, to alert that the availability of a particular menu item has dropped below an acceptable threshold) would have no way of knowing your data is there.

Therefore, you need to introduce your data into the ecosystem earlier in the chain:

![alt text](/images/qu7.JPG?raw=true "ID_token")

By doing this, you can be assured that Clarifi applications will be empowered to consume your data properly and thus provide value to your customers!

##What’s Airwaves?

Airwaves is a job that you will need to install on your namespace that will listen for raw StoreInfo and StoreBusinessDay files that you POST into your namespace, parsing the data within, moving it through the API server, and generating an SNS message for downstream applications.

To install Airwaves, you’ll need to go to the Bodhi Shop.  The Bodhi Shop is a place within your namespace where you can install and configure a variety of jobs and applications.  Here’s a link:
https://tools.hotschedules.io/shop/#/all?appType=job
Find Airwaves from the list of available jobs and install.

<aside class="notice"> <strong>How To POST data to Clarifi</strong> </aside>

The File Upload endpoint is special type that allows a user to upload files (StoreInfo and StoreBusinessDay) to be consumed by Clarifi Applications.

**File Upload EndPoint URL:** https://files.hotschedules.io/files/raw/store_id/filename

**What you'll need:**

* A namespace running the Airwaves job
* Your files (StoreInfo and StoreBusinessDay)
* Method to pass data to the API (HS Bodhi Query Tool or Postman for example)

At a minimum, your file needs to include a full business day of data. For example, if you are posting sales at 10:00am and then again at 11:00am, your 11:00am file needs include all the data you posted at 10:00am as well as the data from 10:00am to 11:00am.


<aside class="notice"> <strong>Let's Get Started</strong> </aside>


**Login to your namespace:** [https://tools.hotschedules.io] (https://tools.hotschedules.io)


**Install the Airwaves app:** Login to your namespace and use the Bodhi Shop to install the Airwaves App. This app is required to consume the files you will POST later in this example and enable Clarifi to consume the data for the apps within Clarifi.


![Install Airwaves](/images/airwaves.png?raw=true)

Once installed, Airwaves will be available in the Job Manager.

![Configuration](/images/airwavesjob.png?raw=true)


**You're ready to start posting data to Clarifi.**

To **POST** data into Clarifi, you will need to create 2 files and upload those to File Upload endpoint. When the files are received, Airwaves listens for those files, consumes them and transforms them into Canonical data for consumption by Clarifi applications.

**Note:** You will create a separate zip file for each file as you will POST each file separately when you submit your call to upload data into Clarifi. Attached are the file spec for each file type and further in this example, completed example files are provided for download.

<a href="http://docs.hotschedules.io/images/StoreInfo.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download StoreInfo.json File Spec</a>

<a href="http://docs.hotschedules.io/images/StoreBusinessDay.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download StoreBusinessDay.json File Spec</a>

We have created a Postman collection to enable you to test posting data to the POS Canonical Service. The Collection includes examples for validating the JSON data in your StoreInfo and StoreBusinessDay files and POSTing to the File Upload Endpoint. The examples are titled "Validate StoreInfo", "Validate StoreBusinessDay", "StoreInfo" and "StoreBusinessDay".

Select the **"Run In Postman"** button below to open the collection in Postman to start testing.

<div id="btn" style="padding-left: 30px;">
<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="caea705a1c30e38ea420"></div></div>


<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>

<br>

To **validate** your JSON data to ensure it's well formed before you create your files, you can **POST** the data to the "validate" endpoint and receive a JSON repsonse upon success or failure.

Validate Endpoint URL: https://api.hotschedules.io/namespace/validate/**StoreInfo** or **StoreBusinessDay**

The following is an example of a **Success** message.


{
    "valid": true,
    "sys_type_version": "1"
}

The example provided below has been created using Postman. Configure Postman using the following example to **POST** your file to the API.

**Configure Header**

![Configuration](/images/postmanheader.png?raw=true)

**Configure Body**

![Configuration](/images/postmanbody.png?raw=true)

The configuration will enable you to pass in your bearer token and namespace, and do a **PUT** to
[https://files.hotschedules.io/files/raw/store_id/filename] (https://files.hotschedules.io/files/raw/store_id/filename)

You'll be passing in a .zip file that contains your data, and attach the zip as part of the body. Postman will show a success message.

> **EXAMPLE JSON RESPONSE:**

```
[
    {
        "namespace": "theposthatrefreshes",
        "name": "StoreInfo6.zip",
        "original_name": "StoreInfo6.zip",
        "location": "theposthatrefreshes/5a997e4a490d05496aae228b/StoreInfo6.zip",
        "media_type": "application/zip",
        "uploaded_at": "2018-04-03T22:11:27.725Z",
        "bucket": "raw",
        "BodhiAsyncStatus": "/theposthatrefreshes/resources/BodhiAsyncStatus/5ac3fc0ff4a7c05f0ead361b"
    }
]
```

Your files will be visible in your File Manager.

![Configuration](/images/filemanager.png?raw=true)

Once the file arrives in the namespace, the Airwaves job will activate and Airwaves will put the file through the API server, basically unpacking all the data within the file and making it available for other applications to consume.

The following example files (StoreInfoMMDDYR.json and StoreBusinessDayMMDDYR.json) are provided for download.

**Best Practice:** Name your json file and your zip file using a simliar naming convention.

i.e. StoreInfo040418.json and StoreInfo040418.zip

<a href="http://docs.hotschedules.io/images/StoreInfoMMDDYR.json" download><img border="0" src="/images/jsonicon.png" alt="Download File StoreInfoMMDDYR.json" width="32" height="32">StoreInfoMMDDYR.json</a>

<a href="http://docs.hotschedules.io/images/StoreBusinessDayMMDDYR.json" download><img border="0" src="/images/jsonicon.png" alt="Download File StoreBusinessDayMMDDYR.json" width="32" height="32">StoreBusinessDayMMDDYR.json</a>

## Working with HotSchedules Labor and Schedule Data

So far we have been focusing on interacting with POS data.  However, perhaps you want to interact with labor or schedule data that has been generated within HS Labor.  HS Labor offers a SOAP API that returns a variety of data, and the Bodhi REST API offers a proxy of those endpoints.  This basically means that instead of having to change your calls to use (for example):
https://soap.hotschedules.com/ws/getStoreEmployees (not a real URL)

You can use the REST API’s URL and auth mechanism:

[https://api.hotschedules.io/namespace/services/hotschedules/concept_id/store_id/getStoreEmployees] (https://api.hotschedules.io/namespace/services/hotschedules/concept_id/store_id/getStoreEmployees) (not a real URL)

In order to utilize the HS SOAP proxy, you will need to acquire HS SOAP credentials and put them in a tool called the BodhiUserKeychain.  Luckily, these credentials do not expire, so doing this once will set you up for life.

Follow these simple setup steps before proceeding.

**Step 1:** Obtain your API credentials from HotSchedules if you have not already done so.<br>
**Step 2:** Login into the [Account Manager](https://tools.hotschedules.io/account/#/)<br>
**Step 3:** In the upper right corner, select the wrench icon, then keychain, then your namespace.<br>
**Step 4:** Enter your API credentials as provided by hotSchedules and click save.<br>
**Step 5:** Continue with the example below to retrieve your token.

####Making a call

**Please Note:** Through our standard service offering, HotSchedules will support up to 100 calls per hour, per store with bursts not to exceed 20 calls per minute per store. At this service level, the API will have a rate limit and status code 429 will return for calls beyond those limits.

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

You can create your own store for your organization either by executing a **POST** command (see below) to `https://api.hotschedules.io/<organization_name>/resources/Store` or using our store manager tool at `https://hotschedules.io/store-manager` . Either way, a store is a critical anchor for information in the Platform.

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
the HTTP verb DELETE will allow you to remove a record in your type. To delete multiple records, include a ?where={} in your URL to narrow or expand then number of records removed.

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

We have created a Postman collection to enable you with making calls to the REST API.

<div id="btn" style="padding-left: 30px;">
<div class="postman-run-button"
data-postman-action="collection/import"
data-postman-var-1="caea705a1c30e38ea420"></div></div>


<script type="text/javascript">
  (function (p,o,s,t,m,a,n) {
    !p[s] && (p[s] = function () { (p[t] || (p[t] = [])).push(arguments); });
    !o.getElementById(s+t) && o.getElementsByTagName("head")[0].appendChild((
      (n = o.createElement("script")),
      (n.id = s+t), (n.async = 1), (n.src = m), n
    ));
  }(window, document, "_pm", "PostmanRunObject", "https://run.pstmn.io/button.js"));
</script>



