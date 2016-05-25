##Working with Sales data

Storing and accessing Sales data is a critical function of the HotSchedule IoT Platform. To access your sales data, you will use the following types:  

* Store  
* SalesTransaction  
* SalesItem  
* SalesCategory  
* RevenueCenter

###Steps to create new data:
1. Create a Store  
2. Create a SalesTransaction  
3. Create a SalesItem  

####How does the data map together?
SalesTransaction is a reference table for looking up items sold and the meta data about those items as they refer to a specific order on a specific business day.  Ideally, this should be the first place you look for information when querying Sales data.

A Store has many SalesTransactions  
--  SalesTransaction.store_id maps to Store.sys_id

-- Example Query: Return all SalesTransactions for a store  
`https://api.bodhi.space/<organization_name>/SalesTransaction?where={'store_id':'<store.sys_id>'}`

A Store has many SalesItem  
--  SalesItem.store_id maps to Store.sys_id

-- Example Query: Return all SalesItem for a store  
`https://api.bodhi.space/<organization_name>/SalesItem?where={'store_id':'<store.sys_id>'}`

A Store has many entries in SalesCategory  
--  SalesCategory.store_id maps to Store.sys_id

-- Example Query: Return all SalesCategories for a store  
`https://api.bodhi.space/<organization_name>/SalesCategory?where={'store_id':'<store.sys_id>'}`

A Store has many RevenueCenters  
--  RevenueCenter.store_id maps to Store.sys_id

-- Example Query: Return all RevenueCenters for a store  
`https://api.bodhi.space/<organization_name>/RevenueCenter?where={'store_id':'<store.sys_id>'}`

A SalesTransaction has many SalesItems  
--  SalesTransaction.transaction_id maps to SalesItem.transaction_id

-- Example Query: Return all SalesItems for a SalesTransaction  
`https://api.bodhi.space/<organization_name>/SalesTransaction?where={'transaction_id':'<SalesTransaction.transaction_id>'}`

A SalesTransaction has a RevenueCenter  
--  SalesTransaction.revenue_center.id maps to RevenueCenter.instore_id  
--  SalesTransaction.revenue_center.name maps to RevenueCenter.display_name  

-- Example Query: Return all SalesTransactions for a RevenueCenter
`https://api.bodhi.space/<organization_name>/SalesTransaction?where={'revenue_center.id':'<RevenueCenter.instore_id>'}`

A SalesTransaction has an Employee  
--  SalesTransaction.employee.id maps to Employee.external_ids.key  
--  SalesTransaction.employee.name maps to Employee.name.formatted_name  

-- Example Query: Return all SalesTransaction for an Employee
`https://api.bodhi.space/<organization_name>/SalesItems?where={'employee.id':'<Employee.external_ids.key>'}`

A SalesTransaction AND SalesItem have a day of business  
-- Example Query: Return all SalesTransactions for business day 05/21/2016
`https://api.bodhi.space/<organization_name>/SalesTransaction?where={'business_day':'2016-05-21'}`

-- Example Query: Return all SalesItems for business day 05/21/2016
`https://api.bodhi.space/<organization_name>/SalesItems?where={'business_day':'2016-05-21'}`

A SalesItem has a SalesCategory  
--  SalesItem.sales_category.id maps to SalesCategory.instore_id  
--  SalesItem.sales_category.name maps to SalesCategory.display_name  

-- Example Query: Return all SalesItems for a SalesCategory
`https://api.bodhi.space/<organization_name>/SalesItems?where={'sales_category.id':'<SalesCategory.instore_id>'}`

