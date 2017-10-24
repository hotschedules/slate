##Working with Labor data

Storing and accessing labor data is a critical function of the HotSchedule IoT Platform. To access your labor data, you will use the following types:  

* Store  
* StoreJob  
* Employee  
* EmployeePosition  
* Timecard  


###Steps to create new data:
1. Create a Store  
2. Create a StoreJob  
3. Create a Employee  
4. Create EmployeePosition using the Employee, Store, and StoreJob data  
  * Patch Store.employee_ids with the new employee's sys_id  
  * Patch Employee.positions with the new EmployeePosition  
5. Create Timecard using EmployeePosition data  

####How does the data map together?
EmployeePosition is a reference table for looking up stores, employees, jobs, and pay rates.  Ideally, this should be the first place you look for information when querying labor data.

A Store has many employees (Array of sys_ids)
-- Store.employee_ids maps to each Employee.sys_id

-- Example Query: Return all stores that the specified employee is associated with  
`https://api.hotschedules.io/<organization_name>/Store?where={'employee_ids':'<EMPLOYEE_ID>'}`

A Store has **many** jobs
--  Store.sys_id maps to StoreJob.store_id

-- Example Query: Return all jobs at a specified store  
`https://api.hotschedules.io/<organization_name>/StoreJob?where={'store_id':'<STORE_ID>'}`  

An Employee has many positions (Array of EmployeePosition)
  
* Employee.sys_id maps to EmployeePosition.employee_id  
* Employee.name.family_name maps to EmployeePosition.employee_reference.name  
* Employee.external_ids maps to EmployeePosition.employee_reference.id  
* Store.sys_id maps to EmployeePosition.store_id  
* Store.store_number maps to EmployeePosition.store_reference.id  
* Store.name maps to EmployeePosition.store_reference.name  
* StoreJob.sys_id maps to EmployeePosition.job_id  
* StoreJob.instore_id maps to EmployeePosition.job_reference.id  
* StoreJob.instore_name maps to EmployeePosition.job_reference.name  

**Example Queries:**  

Return all positions for a specified employee across all stores  
`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'employee_id':'<EMPLOYEE_ID>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'employee_reference.name':'<EMPLOYEE_NAME>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'employee_reference.id':'<EMPLOYEE_EXTERNAL_ID>'}`  

Return all positions at a specified store across all employees and jobs.  
**(NOTE: May include duplicates if employees have multiple positions at the same store)**  
`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'store_id':'<STORE_ID>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'store_reference.name':'<STORE_NAME>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'store_reference.id':'<STORE_NUMBER>'}`  

Return all employees with a specified job across all stores
`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'job_id':'<JOB_ID>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'job_reference.name':'<JOB_NAME>'}`  

`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'job_reference.id':'<JOB_EXTERNAL_ID>'}`  

An Employee has many Stores through EmployeePosition

* Employee.sys_id maps to EmployeePosition.employee_id
* EmployeePosition.store_id maps to Store.sys_id
* Therefore: Employee.sys_id maps to Store.sys_id

-- Example Query: Return an array of Store.sys_id that the employee works at
`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'employee_id':'<EMPLOYEE_ID>'}&fields=store_id`

An Employee has many StoreJobs through EmployeePosition

* Employee.sys_id maps to EmployeePosition.employee_id
* EmployeePosition.job_id maps to StoreJob.sys_id
* Therefore: Employee.sys_id maps to StoreJob.sys_id

-- Example Query: Return an array of StoreJob.sys_id for the specified employee  
`https://api.hotschedules.io/<organization_name>/EmployeePosition?where={'employee_id':'<EMPLOYEE_ID>'}&fields=job_id`

(Same as the two previous examples)  

* A Store has many StoreJobs through EmployeePosition
* A Store has many Employees through EmployeePosition
* A StoreJob has many Employees through EmployeePosition

An Employee has many Timecards
* Employee.sys_id maps to Timecard.employee_id
* Employee.external_ids maps to Timecard.employee_reference.id
* Employee.name.family_name maps to Timecard.employee_reference.name

-- Example Query: Return all timecards for a specified employee  
`https://api.hotschedules.io/<organization_name>/Timecard?where={'employee_id': '<EMPLOYEE_ID>'}`

A Store has many Timecards

* Store.sys_id maps to Timecard.store_id
* Store.store_number maps to Timecard.store_reference.id
* Store.name maps to Timecard.store_reference.name

-- Example Query:Return all timecards for all employees at a specified store  
`https://api.hotschedules.io/<organization_name>/Timecard?where={'store_id': '<STORE_ID>'}`


A StoreJob has many Timecards

* StoreJob.sys_id maps to Timecard.job_id
* StoreJob.instore_id maps to Timecard.job_reference.id
* StoreJob.instore_name maps to Timecard.job_reference.name

-- Example Query:Return all timecards for all employees with the specified job across all stores  
`https://api.hotschedules.io/<organization_name>/Timecard?where={'job_id': '<JOB_ID>'}`  

-- Example Query:Return all timecards for all employees with the specified job at a specified store  
`https://api.hotschedules.io/<organization_name>/Timecard?where={'job_id': '<JOB_ID>', 'store_id': '<STORE_ID>'}`  


Employee payment rates:
Base payment rates for a position are defined in the StoreJob type.  When an EmployeePosition is created, the regular, overtime, and double time rates are copied from the StoreJob and adjusted for that employee.  This allows for multiple employees to have the same job, but different payment rates.


