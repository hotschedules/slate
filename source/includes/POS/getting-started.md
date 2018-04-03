#POS Canonical Service
## Introduction

This section will be used to define what canonical is and what the different POS canonical data types are. 

A canonical data module (also known as CDM) in general terms is something used to take the language of one application and translate it into the language of another. So for us, canonical is how we take the million different ways that a point of sale might define something like an employee’s status and translate it into a single language that can be used by our products.  

Canonical has two types of files that it can generate depending on the circumstance.

  * **StoreInfo** - Only updated when new data is available. For example, a StoreInfo file will include employee data that only sends when it is updated.

  * **StoreBusinessDay** - These files are generated on a schedule and will be for things like sales and labor summaries. 

Using our RESTful service, a call can be made to endpoints to **GET** data. The minimum base call is the url to the endpoint and a page limit.

HTTP Status Codes provide a description of the sucess or failure of a call: [https://httpstatuses.com] (https://httpstatuses.com)


**Base Call:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1)

Using a field in the  **where**  or **fields** clause will narrow the focus to specific data.

**Where:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1)

**Fields:** [https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1)

COMING SOON: Using the [FILEUPLOAD ENDPOINT] Process to post files (StoreInfo and StoreBusinessDay) to be consumed by Clarifi Applications

Below you will find descriptions for each canonical type that we use and the available fields.

<aside class="notice"> <strong>QUERY StoreInfo</strong> </aside> 

PosEmployee, PosJob, PosEmployeePosition, PosRevenueCenter, PosMenu, PosMenuItems and PosMenumodifiers are only types that are queryable via StoreInfo.

**Example:** To get a list of employees for a specific store and associated values, this would be the query string used

[https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_number": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESPACE/resources/StoreInfo?where={"store_number": { "$eq": "sys_id" }}&fields=store_employees,name&paging=limit:25,page:1)

**Note:** store_number is the sys_id of the store you are running the call for. To retrieve the list of sys_id's for all stores, use the following call.

[https://api.hotschedules.io/NAMESPACE/resources/Store?fields=name,sys_id&paging=limit:25,page:1] (https://api.hotschedules.io/NAMESAPCE/resources/Store?fields=name,sys_id&paging=limit:25,page:1)

> **EXAMPLE JSON RESPONSE:**

```
{
name: "store_test_07",
sys_id: "5a1653d772bd660b0e9270bc"
},
{
name: "store_test_05",
sys_id: "5a1653d79534035f755308cf"
}
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
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

##Posjob
**A list of job codes from the customer’s point of sale system.**<br>

*  **Instore_name** - The name of the job code.<br>
*  **Instore_id** - The point of sale ID given to the job code.<br>
*  **regular _rate** - The pay rate attached to the job code.<br>
*  **Overtime_rate** - The overtime rate attached to the job.<br>
*  **Doubletime_rate** - The doubletime rate assigned to the job.

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
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

##PosEmployeePosition
**The job code assigned to the employee in the point of sale.**<br>

*  **Employee_reference** - The employee’s POS ID.<br>
*  **Job_reference** - The job code’s POS ID. <br>
*  **Regular_rate** - The job code rate given to the employee. <br>
*  **Overtime_rate** - The overtime rate given to the employee.<br>
*  **Doubletime_rate** - The doubletime rate give to the employee. <br>
*  **PosSalesCategory** - The sales categories listed in the point of sale. <br>
*  **Instore_id** - The point of sale ID given to the sales category. <br>
*  **Name** - The name of the assigned sales category.

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
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      }
]
```

##PosRevenueCenter
**The revenue centers listed in the point of sale.**<br>

*  **Instore_id** - The point of sale ID given to the revenue center. <br>
*  **Name** - The name of the revenue center. <br>

> **EXAMPLE JSON RESPONSE:**

```
[
  {
    "revenue_centers": [
      {
        "name": "Dining",
        "instore_id": "1",
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
        "store_reference": {
          "id": "7"
        }
      },
      {
        "name": "Bar Downstairs",
        "instore_id": "2",
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
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

##PosMenuItems
**The items that can be used in all of the different menus.**<br>
**Note:** PosMenuItems are nested within StoreInfo <br>

*  **Id** - The point of sale ID given to a menu item. <br>
*  **Name** - The name of the item in the point of sale. <br>
*  **Category** - The category that an item is assigned to. <br>
*  **Description** - an extension of the name that can provide further information about the item. <br>
*  **Unit_price** - The default menu price of the item. <br>
*  **Prices** - If that item has a different price associated with it outside of the default. For example a cocktail might have a happy hour price outside of the menu price. <br>

##PosMenumodifiers
**Things like ketchup that can be used in tandem with a menu item.**<br>
**Note:** PosMenumodifiers are nested within StoreInfo <br>

*  **Id** - The given point of sale ID for the menu modifier.<br>
*  **Name** - The name of the menu modifier. <br>
*  **Description** - A longer version of the name that can provide further insight into the name. <br>
*  **Unit_price** - The default menu price for a particular modifier. <br>
*  **Prices** - Any other prices outside of the menu price that is associated with the modifier. <br>


> **EXAMPLE JSON RESPONSE:**

```
  {
    "store_menus": [
      {
        "store_id": "5a1653d772bd660b0e9270bc",
        "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180403/StoreInfo",
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
    "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180331/StoreBusinessDay",
    "store_reference": {
      "id": "7"
    },
    "store_id": "5a1653d772bd660b0e9270bc",
    "key": "79e5a5c698d0c09fd66fb927d97b3dae",
    "sys_version": 4,
    "sys_created_at": "2018-03-28T13:13:20.165Z",
    "sys_created_by": "admin__itccsb",
    "sys_type_version": 6,
    "sys_modified_at": "2018-03-31T17:00:24.001Z",
    "sys_modified_by": "admin__itccsb",
    "sys_id": "5abb94f03d0408724e91e8db"
  }
```

##PosCheck
**The different transactions at a restaurant.**<br>

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
    "content_url": "itccsb/5a1653d772bd660b0e9270bc/20180326/StoreBusinessDay",
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
    "sys_created_by": "admin__itccsb",
    "sys_type_version": 3,
    "sys_modified_at": "2018-03-27T12:24:00.269Z",
    "sys_modified_by": "admin__itccsb",
    "sys_id": "5ab97b8f9534036231f8b72a"
  }
```

<aside class="notice"> <strong>QUERY PosCheck</strong> </aside>

PosCheckItem are only queryable via PosCheck.

##PosCheckItem
**The items that make up a transaction. Items listed here roll into PosCheck.**<br>

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

[https://api.hotschedules.io/itccsb/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}] ] (https://api.hotschedules.io/itccsb/resources/PosCheck/aggregate?pipeline=[{$match:{store_id:"sys_id"}},{"$unwind":"$items"},{$project:{items:1}},{$match:{items.item_code:"55136"}},{$group:{_id:"$items.item_code",count:{"$sum":1}}}])

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