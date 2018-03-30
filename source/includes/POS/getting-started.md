#POS Canonical Service
## Introduction

This section will be used to define what canonical is and what the different POS canonical data types are. 

A canonical data module (also known as CDM) in general terms is something used to take the language of one application and translate it into the language of another. So for us, canonical is how we take the million different ways that a point of sale might define something like an employee’s status and translate it into a single language that can be used by our products.  

Canonical has two types of files that it can generate depending on the circumstance.

  * **StoreInfo** - Only updated when new data is available. For example, a StoreInfo file will include employee data that only sends when it is updated.

  * **StoreBusinessDay** - These files are generated on a schedule and will be for things like sales and labor summaries. 

Using our RESTful service, a call can be made to endpoints to **GET** data. The minimum base call is the url to the endpoint and a page limit.

HTTP Status Codes provide a description of the sucess or failure of a call: [https://httpstatuses.com] (https://httpstatuses.com)


[Base Call] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1) <br> ```https://api.hotschedules.io/NAMESPACE/resources/PosCheck?paging=limit:25,page:1```

Using a field in the  **where**  or **fields** clause will narrow the focus to specific data.

[Where:] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1) <br>```https://api.hotschedules.io/NAMESAPCE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&paging=limit:25,page:1```

[Fields:] (https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1) <br> ```https://api.hotschedules.io/NAMESPACE/resources/PosCheck?where={"guest_count": { "$eq": "1" }}&fields=table_id,check_id,shift_id&paging=limit:25,page:1```

COMING SOON: Using the [FILEUPLOAD ENDPOINT] Process to post files (StoreInfo and StoreBusinessDay) to be consumed by Clarifi Applications

Below you will find descriptions for each canonical type that we use and the available fields. 

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

##Posjob
**A list of job codes from the customer’s point of sale system.**<br>

*  **Instore_name** - The name of the job code.<br>
*  **Instore_id** - The point of sale ID given to the job code.<br>
*  **regular _rate** - The pay rate attached to the job code.<br>
*  **Overtime_rate** - The overtime rate attached to the job.<br>
*  **Doubletime_rate** - The doubletime rate assigned to the job.

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

##PosRevenueCenter
**The revenue centers listed in the point of sale.**<br>

*  **Instore_id** - The point of sale ID given to the revenue center. <br>
*  **Name** - The name of the revenue center. <br>

##PosMenu
**Different menu types. Examples can include things like a brunch or dinner menu.**<br>

*  **Name** - The name of the menu <br>
*  **Category** - The category assigned to a menu.<br>
*  **Items** - The items that make up a menu. <br>
*  **Modifiers** - The modifiers that can be used by items in the menu. <br>

##PosMenuItems
**The items that can be used in all of the different menus.**<br>

*  **Id** - The point of sale ID given to a menu item. <br>
*  **Name** - The name of the item in the point of sale. <br>
*  **Category** - The category that an item is assigned to. <br>
*  **Description** - an extension of the name that can provide further information about the item. <br>
*  **Unit_price** - The default menu price of the item. <br>
*  **Prices** - If that item has a different price associated with it outside of the default. For example a cocktail might have a happy hour price outside of the menu price. <br>

##PosMenumodifiers
**Things like ketchup that can be used in tandem with a menu item.**<br>

*  **Id** - The given point of sale ID for the menu modifier.<br>
*  **Name** - The name of the menu modifier. <br>
*  **Description** - A longer version of the name that can provide further insight into the name. <br>
*  **Unit_price** - The default menu price for a particular modifier. <br>
*  **Prices** - Any other prices outside of the menu price that is associated with the modifier. <br>

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