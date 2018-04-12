#Clarifi API Service
##Introduction

This section defines what canonical is and what the different POS canonical data types are for getting data from Clarifi. 

A canonical data module (also known as CDM) in general terms is something used to take the language of one application and translate it into the language of another. So for us, canonical is how we take the million different ways that a point of sale might define something like an employee’s status and translate it into a single language that can be used by our products.  

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


**Base Call:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1)

Using a field in the  **where**  or **fields** clause will narrow the focus to specific data.

**Where:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1)

**Fields:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1)

Below you will find descriptions for each canonical type that we use and the available fields.

<aside class="notice"> <strong>QUERY StoreInfo</strong> </aside> 

PosEmployee, PosJob, PosEmployeePosition, PosRevenueCenter, PosMenu, PosMenuItems and PosMenumodifiers are only types that are queryable via StoreInfo.

**Example:** To get a list of employees for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1)

**Note:** store_id is the sys_id of the store you are running the call for. To retrieve the list of sys_id's for all stores, use the following call.

[https://api.hotschedules.io/NAMESPACE/resources/Store?fields=name,sys_id&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/Store?fields=name,sys_id&paging=limit:25,page:1)

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


##PosEmployee
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

##Posjob
**A list of job codes from the customer’s point of sale system.**<br>

<a href="/images/PosJob.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Instore_name** - The name of the job code.<br>
*  **Instore_id** - The point of sale ID given to the job code.<br>
*  **regular _rate** - The pay rate attached to the job code.<br>
*  **Overtime_rate** - The overtime rate attached to the job.<br>
*  **Doubletime_rate** - The doubletime rate assigned to the job.

**Example:** To get a list of jobs for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_jobs,name&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=store_jobs,name&paging=limit:25,page:1)

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

##PosEmployeePosition
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

[https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=employee_positions,name&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=employee_positions,name&paging=limit:25,page:1)

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

##PosRevenueCenter
**The revenue centers listed in the point of sale.**<br>
<a href="/images/PosRevenueCenter.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

*  **Instore_id** - The point of sale ID given to the revenue center. <br>
*  **Name** - The name of the revenue center. <br>

**Example:** To get a list of revenue centers for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=revenue_centers,name&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "sys_id" }}&fields=revenue_centers,name&paging=limit:25,page:1)

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

##PosMenu
**Different menu types. Examples can include things like a brunch or dinner menu.**<br>
**Note:** PosMenu is nested within StoreInfo <br>

*  **Name** - The name of the menu <br>
*  **Category** - The category assigned to a menu.<br>
*  **Items** - The items that make up a menu. <br>
*  **Modifiers** - The modifiers that can be used by items in the menu. <br>

<a href="/images/PosMenu.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>


##PosMenuItems
**The items that can be used in all of the different menus.**<br>
**Note:** PosMenuItems are nested within StoreInfo <br>

*  **Id** - The point of sale ID given to a menu item. <br>
*  **Name** - The name of the item in the point of sale. <br>
*  **Category** - The category that an item is assigned to. <br>
*  **Description** - an extension of the name that can provide further information about the item. <br>
*  **Unit_price** - The default menu price of the item. <br>
*  **Prices** - If that item has a different price associated with it outside of the default. For example a cocktail might have a happy hour price outside of the menu price. <br>

<a href="/images/PosMenuItems.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

##PosMenumodifiers
**Things like ketchup that can be used in tandem with a menu item.**<br>
**Note:** PosMenumodifiers are nested within StoreInfo <br>

*  **Id** - The given point of sale ID for the menu modifier.<br>
*  **Name** - The name of the menu modifier. <br>
*  **Description** - A longer version of the name that can provide further insight into the name. <br>
*  **Unit_price** - The default menu price for a particular modifier. <br>
*  **Prices** - Any other prices outside of the menu price that is associated with the modifier. <br>

<a href="/images/PosMenumodifiers.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download File Spec</a>

**Example Call to retrieve PosMenu, PosMenuItems and PosMenumodifiers:** [https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=store_menus&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=store_menus&paging=limit:25,page:1)


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

##PosPunch
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

**Example:** get punch records [https://api.hotschedules.io/NAMESPACE/resources/PosPunch?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=employee_reference&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosPunch?where={"store_id": { "$eq": "5a1653d772bd660b0e9270bc" }}&fields=employee_reference&paging=limit:25,page:1)

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

##PosCheck
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

##PosCheckItem
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

[https://api.hotschedules.io/NAMESPACE/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}] ] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}])

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

[https://api.hotschedules.io/NAMESPACE/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1,business_day:1}},{$match:{items.item_code:"55136"}},{$group:{_id:{items:"$items.item_code",business_day:"$business_day"},count:{"$sum":1}}}] ] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1,business_day:1}},{$match:{items.item_code:"55136"}},{$group:{_id:{items:"$items.item_code",business_day:"$business_day"},count:{"$sum":1}}}])

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

##POSTing Data to Clarifi
<aside class="notice"> <strong>How To POST data to Clarifi</strong> </aside>

The BodhiFileUpload endpoint is special type that allows a user to upload files (StoreInfo and StoreBusinessDay) to be consumed by Clarifi Applications.

**FileUpload EndPoint URL:** https://files.hotschedules.io/files/raw/store_id/filename

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

To **POST** data into Clarifi, you will need to create 2 files and upload those to BodhiFileUpload endpoint. When the files are received, Airwaves listens for those files, consumes them and transforms them into Canonical data for consumption by Clarifi applications.

**Note:** You will create a separate zip file for each file as you will POST each file separately when you submit your call to upload data into Clarifi. Attached are the file spec for each file type and further in this example, completed example files are provided for download.

<a href="http://docs.hotschedules.io/images/StoreInfo.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download StoreInfo.json File Spec</a>

<a href="http://docs.hotschedules.io/images/StoreBusinessDay.json" download><img border="0" src="/images/jsonicon.png" alt="Download File Spec" width="32" height="32">Download StoreBusinessDay.json File Spec</a>

We have created a Postman collection to enable you to test posting data to the POS Canonical Service. The Collection includes examples for validating the JSON data in your StoreInfo and StoreBusinessDay files and POSTing to the File Upload Endpoint. The examples are titled "Validate StoreInfo", "Validate StoreBusinessDay", "StoreInfo" and "StoreBusinessDay".

Select the "Run In Postman" button below to open the collection in Postman to start testing.

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

**Configure Postman**

To validate your JSON data for StoreInfo or StoreBusinessDay, you'll **POST** the data to the "validate" endpoint and receive a JSON repsonse upon success or failure.

Validate Endpoint URL: https://api.hotschedules.io/NAMESPACE/validate/**StoreInfo** or **StoreBusinessDay**

**Please see the example in the Postman Collection for configuration settings** 

The following is an example of a **Success** message.


{
    "valid": true,
    "sys_type_version": "1"
}

The example provided below has been created using Postman. Configure Postman using the following example to POST your file to the API.

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
