#HS POS Canonical Service

This section will be used to define what canonical is and what the different POS canonical data types are. 

A canonical data module (also known as CDM) in general terms is something used to take the language of one application and translate it into the language of another. So for us, canonical is how we take the million different ways that a point of sale might define something like an employee’s status and translate it into a single language that can be used by our products.  

Canonical has two types of files that it can generate depending on the circumstance.

  * StoreInfo - Only updated when new data is available. For example, a StoreInfo file will include employee data that only sends when it is updated.

  * StoreBusinessDay - These files are generated on a schedule and will be for things like sales and labor summaries. 

Below you will find descriptions for each canonical type that we use. 

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

*  **DEmployee_reference** - The employee’s POS ID.<br>
*  **DJob_reference** - The job code’s POS ID. <br>
*  **DRegular_rate** - The job code rate given to the employee. <br>
*  **DOvertime_rate** - The overtime rate given to the employee.<br>
*  **DDoubletime_rate** - The doubletime rate give to the employee. <br>
*  **DPosSalesCategory** - The sales categories listed in the point of sale. <br>
*  **DInstore_id** - The point of sale ID given to the sales category. <br>
*  **DName** - The name of the assigned sales category.

##PosRevenueCenter
**The revenue centers listed in the point of sale.**<br>

*  **DInstore_id** - The point of sale ID given to the revenue center. <br>
*  **DName** - The name of the revenue center. <br>

##PosMenu
**Different menu types. Examples can include things like a brunch or dinner menu.**<br>

*  **DName** - The name of the menu <br>
*  **DCategory** - The category assigned to a menu.<br>
*  **DItems** - The items that make up a menu. <br>
*  **DModifiers** - The modifiers that can be used by items in the menu. <br>

##PosMenuItems
**The items that can be used in all of the different menus.**<br>

*  **DId** - The point of sale ID given to a menu item. <br>
*  **DName** - The name of the item in the point of sale. <br>
*  **DCategory** - The category that an item is assigned to. <br>
*  **DDescription** - an extension of the name that can provide further information about the item. <br>
*  **DUnit_price** - The default menu price of the item. <br>
*  **DPrices** - If that item has a different price associated with it outside of the default. For example a cocktail might have a happy hour price outside of the menu price. <br>

##PosMenumodifiers
**Things like ketchup that can be used in tandem with a menu item.**<br>

*  **Id** - The given point of sale ID for the menu modifier.<br>
*  **Name** - The name of the menu modifier. <br>
*  **Description** - A longer version of the name that can provide further insight into the name. <br>
*  **Unit_price** - The default menu price for a particular modifier. <br>
*  **Prices** - Any other prices outside of the menu price that is associated with the modifier. <br>

##PosPunch
**The punch records that are present in the point of sale system.**<br>

*  **DEmployee_reference** - the employee’s given point of sale ID. <br>
*  **DJob_reference** - The given point of sale ID for the job code that is assigned to the employee. <br>
*  **DBusiness_day** - The business day that the employee has worked. <br>
*  **DStarted_at** - The time that the employee started working at. <br>
*  **DEnded_at** - The time that the employee stopped working at.<br>
*  **DTotal_minutes_worked** - The total amount of time that the employee worked. <br>
*  **DBreaks** - The number of breaks that the employee took. <br>
*  **DRegular_rate** - The regular rate that the employee is working at<br>
*  **DOvertime_rate** - The overtime rate that the employee is working at<br>
*  **DDoubletime_rate** - The doubletime rate that the employee is working at. <br>
*  **DDeclared_tips** - The declared tips that the employee has. <br>
*  **DCash_tips** - The cash tips that the employee has. <br>
*  **DCredit_tips** - The credit tips that the employee has. <br>

##PosCheck
**The different transactions at a restaurant.**<br>

*  **DCheck_id** - The point of sale ID given to the transaction. <br>
*  **DVoided** - Whether or not the transaction was voided. <br>
*  **DCanceled** - Whether or not the check was cancelled. <br>
*  **DEmployee_reference** - The point of sale ID given to the employee who handled the transaction. <br>
*  **DTable_id** - The point of sale ID given to the table. <br>
*  **DRegister_id** - The point of sale ID given to the register.<br>
*  **DShift_id** - The given point of sale ID for the shift. <br>
*  **DOpened_at** - When the transaction was opened. <br>
*  **DClosed_at** - When the transaction was closed. <br>
*  **DGuest_count** - The total number of guests that were present for the transaction. <br>
*  **DItem_count** - The total number of items on the transaction. <br>
*  **DNet_total** - The total without taxes or coupons applied to it. <br>
*  **DGross_total** - The total including taxes and coupons. <br>
*  **DDiscount_total** - The total after any discounts have been applied to it. <br>
*  **DTax_total** - The total with the tax applied to it. <br>
*  **DTender_total** - The total amount of dollars paid. <br>
*  **DChange_total** - The total amount of change paid. <br>
*  **DGratuity_total** - Any gratuity that was given to the transaction.<br>
*  **DVoid_total** - if the check was voided how much was it for. <br>
*  **DItems** - The items that are on the transaction. <br>

##PosCheckItem
**The items that make up a transaction. Items listed here roll into PosCheck.**<br>

*  **DItem_code** - The given POS ID for the item.<br>
*  **DUnit_price** - The menu price of the check item. <br>
*  **DQuantity** - The amount of the item on the transaction. <br>
*  **DSales_category** - The sales category assigned to the item. <br>
*  **DNet_total** - The total dollar amount of the item on the check without taxes or coupons applied to it. <br>
*  **DGross_total** - The total dollar amount of the item on the check with taxes and coupons applied to it. <br>
*  **DTax_total** - The total amount of taxes. <br>
*  **DDiscount_total** - The total amount of discounts that have been applied to the check. <br>
*  **DVoid_total** - If the check was voided this is its total. <br>
*  **DVoided** - Whether or not the check was voided. <br>
*  **DDiscounted** - whether or not the check was discounted. <br>
*  **DPosVolumeItem** - A dynamic driver that can represent things like guest counts, entree counts, and table counts. <br>
*  **DDatetime** - The date that the amount being presented was captured. <br>
*  **DAmount** - The total amount being presented by the driver. <br>
*  **DVolume_type** - The type of volume that is being displayed. <br>
*  **DRevenue_center** - The revenue center that data is being pulled from. <br>
*  **DEmployee_reference** - The point of sale ID given to the employee whose data you are viewing (?) 