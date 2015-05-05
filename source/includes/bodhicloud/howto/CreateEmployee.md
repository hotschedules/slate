#### How Do I Create An Employee using the Bodhi API Documentation 

##### Overview 
The Bodhi Cloud API provide an employee as part of it's base types which should be used or extended to store all your stores for your namespace.  This tutorial will walk through a sample set of data to create an employee within your namespace.    


##### Getting Started
The goal of this tutorial is to show how to create an employee for your namespace and show you how to represent the attributes and properties that the Bodhi API and Base type system.   

###### Prerequisites
In order to be able to complete this tutorial, you will need to be an admin user of your namespace or have write privileges to the employee base type in your namespace.  Your credentials and privileges can be provided by your Hot Schedules representative or the admin of your namespace.  Please login to each of the tools prior to starting the section.


##### How To Create a Store using Bodhi API Documentation
The Bodhi API Documentation is a full featured interactive set of documentation that also allows the user to Create, Update, and Delete using the REST APIs for each type.  This tutorial is intended to both allow the user to get familiar with how the Bodhi API Documentation as well as the minimum requirements to create an employe and view the employee you created through the Bodhi API Documentation.  

1.Go to [https://api.bodhi.space/apidocs/index.html](https://api.bodhi.space/apidocs/index.html)

2.Login using the credentials provided to you from your Hot Schedules Representative and click Explore.  

*NOTE:* See [How Do I login to the Bodhi Cloud API Documentation](http://docs.bodhi.space/#bodhi-cloud-api-tutorials) for more details on logging in.

3.Onced logged in, scroll down through the types and click on Employee. 

*Note:* The Bodhi Cloud Types are shown in alphabetical order.: 

![CloudAPI_ClickEmployee](/images/CloudAPI_ClickEmployee.png?raw=true "")

_Creating An Employee, Click Employee_

4.Click POST /resources/Employee:

![CloudAPI_ClickPOSTEmployee](/images/CloudAPI_ClickPOSTEmployee.png?raw=true "") 

_Creating An Employee, Click POST /resources/Employee_

5.Click the Value box an add the following JSON to the Value box:

![CloudAPI_ClickValueboxEmployee](/images/CloudAPI_ClickValueBoxEmployee.png?raw=true "")

_Creating An Employee, Click Value box_

```
{
"name":
{ "family_name": "Nitzsche", "given_name": "Jamir", "middle_name": "Matteo", "formatted_name": "Dr. Jamir Matteo Nitzsche I", "honorific_prefix": "Dr.", "honorific_suffix": "I" }
,
"emails": [
"cordell.ratke@example.com"
],
"phone_numbers": [
"776.481.4925"
],
"birthdate": "1990-08-25T14:17:12-07:00",
"addresses": [
{ "type": "home", "street_address": "60834 Stella Road", "extended_address": "Suite 317", "region": "Wyoming", "locality": "New Malinda", "postal_code": "13443-9712", "country": null }
],
"status": "Active",
"external_ids": [
{ "key": "human_resource_id", "value": "18d683ec-3a6a-4873-b548-70a4d56da3a9" }
,
{ "key": "another_external_id", "value": "b550d805-6268-4e4c-b8ba-1e050861251c" }
]
}
```
*NOTE:*  If you plan to change any of the data to this store, please know that there is a Query Tutorial that depends on this data and you will need to adjust the Query Tutorial as per your data changes.

*NOTE:* The store data is intentionally created for each attribute to show a sample of how to create data for each of the attributes/properties of the Store Type.

6.Click Try it out!

![CloudAPI_ClickTryitoutEmployee](/images/CloudAPI_ClickTryitoutEmployee.png?raw=true "")

_Create An Employee, Click Try it out!_

7.Check that the Employee got created.

Once you click Try it out! you should immediately see that you have a response code of 201:
![CloudAPI_CreateEmployee201](/images/CloudAPI_CreateEmployee201.png?raw=true "")

_Create An Employee, Check that Response Code is 201_

8.Verify the employee got created.

In order to verify the store got created just click GET and Try it out!

![CloudAPI_ClickEmployeeGet](/images/CloudAPI_ClickGetEmployee.png?raw=true "")

_Create An Employee, Check GET from the Employee type_


![CloudAPI_GETCLICKTryitoutEmployeeGet](/images/CloudAPI_GETCLICKTryitoutEmployeeGet.png?raw=true "")

_Create An Employee, Click Employee GET, Try it out!_

You should see the employee you just created above in the response body:

```
[
  {
    "external_ids": [
      {
        "key": "human_resource_id",
        "value": "18d683ec-3a6a-4873-b548-70a4d56da3a9"
      },
      {
        "key": "another_external_id",
        "value": "b550d805-6268-4e4c-b8ba-1e050861251c"
      }
    ],
    "addresses": [
      {
        "type": "home",
        "street_address": "60834 Stella Road",
        "extended_address": "Suite 317",
        "region": "Wyoming",
        "locality": "New Malinda",
        "postal_code": "13443-9712",
        "country": null
      }
    ],
    "phone_numbers": [
      "776.481.4925"
    ],
    "emails": [
      "cordell.ratke@example.com"
    ],
    "name": {
      "family_name": "Nitzsche",
      "given_name": "Jamir",
      "middle_name": "Matteo",
      "formatted_name": "Dr. Jamir Matteo Nitzsche I",
      "honorific_prefix": "Dr.",
      "honorific_suffix": "I"
    },
    "birthdate": "1990-08-25T14:17:12-07:00",
    "status": "Active",
    "sys_namespace": "tutest",
    "sys_version": 1,
    "sys_created_at": "2015-05-05T19:24:54+0000",
    "sys_created_by": "tut1",
    "sys_id": "97b2c6a7-f570-41d6-94eb-fc22fd023717"
  }
]          "extended_address": "Suite 177",
          "region": "Washington",
          "locality": "Skilesville",
          "postal_code": "97280-5066",
          "country": null
        },
        "mailto": null,
        "telephone": "100-074-0150"
      }
    ],
    "address": {
      "type": "home",
      "street_address": "59049 Scottie Path",
      "extended_address": "Suite 667",
      "region": "South Carolina",
      "locality": "Lake Mabelleton",
      "postal_code": "93062",
      "country": null
    },
    "external_ids": [
      {
        "key": "cross-platform_id",
        "value": "939b95a6-a6e9-4d78-a2dd-3cbaa3d2dee3"
      },
      {
        "key": "back-end_id",
        "value": "4b4d8330-b711-4162-82c7-926debaa019b"
      }
    ],
    "timezone": "Asia/Irkutsk",
    "agent_ids": [
      "63863728-25c2-4e47-9d08-e2ff40ff9882"
    ],
    "name": "fantastic-mongolian-bbq-587",
    "organization_id": "41be6add-d7ae-4208-80a3-bc8451b2c166",
    "organization_name": "King LLC",
    "status": "Awesome",
    "telephone": "(400) 076-6535",
    "store_number": "1",
    "business_contacts": [
      {
        "title": "Senior Mobility Assistant",
        "full_name": "Loyce Smith Sr.",
        "display_name": "Loyce Smith Sr.",
        "roles": "bluetooth",
        "postal_address": {
          "type": "home",
          "street_address": "7235 Kraig Centers",
          "extended_address": "Suite 239",
          "region": "Ohio",
          "locality": "Port Stephaniaburgh",
          "postal_code": "14121-6541",
          "country": null
        },
        "mailto": null,
        "telephone": "(329) 870-4298"
      },
      {
        "title": "Forward Directives Liason",
        "full_name": "Nichole Dooley",
        "display_name": "Nichole Dooley",
        "roles": "wireless",
        "postal_address": {
          "type": "home",
          "street_address": "564 Powlowski Freeway",
          "extended_address": "Suite 529",
          "region": "North Carolina",
          "locality": "South Amyport",
          "postal_code": "67876-9982",
          "country": null
        },
        "mailto": null,
        "telephone": "(137) 018-2393 x279"
      }
    ],
    "tags": [
      "cross-platform",
      "primary"
    ],
    "display_name": "Fantastic Mongolian BBQ",
    "language": "EN",
    "sys_namespace": "tutest",
    "sys_version": 1,
    "sys_created_at": "2015-04-06T21:29:06+0000",
    "sys_created_by": "tammie",
    "sys_id": "215c3fe9-d23d-4e81-8240-fa4056eb9ac1"
  }
]
```

*NOTE:* If you have other data in your namespace, you will see the other data in the response body.
